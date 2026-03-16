---
id: 008
title: "Fair BEAT — Technical Specification"
category: app
status: active
version: 0.3
created: 2025-03-01
updated: 2026-03-14
author: Founder Alex
stack: [Solidity, Ethereum L2, Node.js, Supabase, secp256k1]
---

# Fair BEAT — Technical Specification

> *Redistribution engine: every transaction automatically splits to community pool, distributed by trust scores.*

---

## 1. System Overview

```
Any City Quest Transaction (e.g. JobAround payment)
        │
        ▼
[FairBEAT Router Contract]
        │
        ├──► 93% → Recipient (worker/artist/provider)
        │
        └──► 7%  → Community Pool Contract
                      │
                      ├──► 40% → Immediate Distribution
                      │          (trust-weighted, current period contributors)
                      │
                      ├──► 30% → Community Treasury
                      │          (governance-controlled, Choose&Own vote)
                      │
                      ├──► 20% → Protocol Development Fund
                      │          (multisig, Foundation-controlled)
                      │
                      └──► 10% → Burn / Deflation sink
```

---

## 2. Tech Stack

| Layer | Technology | Notes |
|-------|-----------|-------|
| Blockchain | Arbitrum One (Ethereum L2) | Low gas, EVM compatible |
| Smart contracts | Solidity 0.8.20 | OpenZeppelin base |
| Trust oracle | Trustnet API | Off-chain score → on-chain commitment |
| Backend | Node.js / TypeScript | Distribution calculation |
| Database | Supabase | Participant registry, period tracking |
| Currency | USDC or local stablecoin | Avoids crypto volatility for workers |

---

## 3. Data Models

```typescript
interface DistributionPeriod {
  id: string               // UUID
  community_id: string     // which City Quest community
  start: number            // Unix timestamp
  end: number              // Unix timestamp
  pool_amount: number      // total USDC collected this period
  status: "open" | "calculating" | "distributed" | "closed"
}

interface PeriodContributor {
  period_id: string
  address: string
  trust_score: number      // snapshot at period end
  actions_count: number    // number of qualifying actions
  share_bps: number        // basis points of immediate pool
  amount_earned: number    // USDC amount distributed
}

interface Transaction {
  id: string
  app: string              // "jobaround" | "artmaze" | "recycle" | ...
  payer: string            // address
  recipient: string        // address
  gross_amount: number     // total
  beat_amount: number      // 7% of gross
  recipient_amount: number // 93% of gross
  community_id: string
  timestamp: number
  tx_hash: string          // on-chain confirmation
}
```

---

## 4. Smart Contracts

### 4.1 FairBEAT Router

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC20/IERC20.sol";
import "@openzeppelin/contracts/security/ReentrancyGuard.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract FairBEATRouter is ReentrancyGuard, Ownable {

    IERC20 public immutable stablecoin;
    ICommunityPool public immutable communityPool;

    uint256 public constant BEAT_RATE_BPS = 700;     // 7% in basis points
    uint256 public constant TOTAL_BPS = 10000;

    event Payment(
        address indexed payer,
        address indexed recipient,
        uint256 gross,
        uint256 beat_contribution,
        string community_id,
        string app_id
    );

    constructor(address _stablecoin, address _pool) Ownable(msg.sender) {
        stablecoin = IERC20(_stablecoin);
        communityPool = ICommunityPool(_pool);
    }

    function pay(
        address recipient,
        uint256 amount,
        string calldata community_id,
        string calldata app_id
    ) external nonReentrant {
        require(amount > 0, "zero amount");

        uint256 beat = (amount * BEAT_RATE_BPS) / TOTAL_BPS;
        uint256 net  = amount - beat;

        stablecoin.transferFrom(msg.sender, recipient, net);
        stablecoin.transferFrom(msg.sender, address(communityPool), beat);
        communityPool.recordContribution(beat, community_id);

        emit Payment(msg.sender, recipient, amount, beat, community_id, app_id);
    }
}
```

### 4.2 Community Pool

```solidity
contract CommunityPool is ReentrancyGuard, Ownable {

    IERC20 public immutable stablecoin;
    ITrustnetOracle public immutable trustnet;

    // Split configuration (in BPS, must sum to 10000)
    uint256 public immediate_bps  = 4000;   // 40%
    uint256 public treasury_bps   = 3000;   // 30%
    uint256 public protocol_bps   = 2000;   // 20%
    uint256 public burn_bps       = 1000;   // 10%

    mapping(string => uint256) public period_pool;       // community_id => accumulated USDC
    mapping(string => address[]) public period_contributors;

    event Distributed(string community_id, uint256 total, uint256 immediate, uint256 treasury);

    function recordContribution(uint256 amount, string calldata community_id) external {
        // called by Router only
        period_pool[community_id] += amount;
    }

    function distributeperiod(
        string calldata community_id,
        address[] calldata contributors,
        uint256[] calldata trust_scores   // from Trustnet oracle, scaled 1e18
    ) external onlyOwner {
        uint256 total = period_pool[community_id];
        require(total > 0, "empty pool");

        uint256 immediate = (total * immediate_bps) / 10000;
        uint256 treasury  = (total * treasury_bps) / 10000;
        uint256 protocol  = (total * protocol_bps) / 10000;
        // burn amount is simply left in contract or sent to 0x000...dead

        // Trust-weighted distribution of immediate pool
        uint256 total_score = 0;
        for (uint i = 0; i < trust_scores.length; i++) total_score += trust_scores[i];

        for (uint i = 0; i < contributors.length; i++) {
            uint256 share = (immediate * trust_scores[i]) / total_score;
            if (share > 0) stablecoin.transfer(contributors[i], share);
        }

        stablecoin.transfer(treasury_address, treasury);
        stablecoin.transfer(protocol_address, protocol);

        period_pool[community_id] = 0;
        emit Distributed(community_id, total, immediate, treasury);
    }
}
```

---

## 5. Distribution Calculation (Off-chain)

```typescript
async function calculateDistribution(
  community_id: string,
  period_end: Date
): Promise<PeriodContributor[]> {

  // 1. Get all active contributors in this period
  const contributors = await supabase
    .from("civic_actions")
    .select("address, count(*)")
    .eq("community_id", community_id)
    .gte("timestamp", period_start.getTime())
    .lte("timestamp", period_end.getTime())

  // 2. Fetch Trustnet scores for each contributor
  const scores = await Promise.all(
    contributors.map(c =>
      trustnet.getScore(c.address, `cityquest/${community_id}`)
    )
  )

  // 3. Calculate shares
  const total_score = scores.reduce((s, x) => s + x, 0)
  return contributors.map((c, i) => ({
    address: c.address,
    trust_score: scores[i],
    share_bps: Math.round((scores[i] / total_score) * 10000),
    amount_earned: (immediate_pool * scores[i]) / total_score
  }))
}
```

---

## 6. Integration Pattern (for each City Quest app)

```typescript
// Any app that processes payments just calls the Router
import { FairBEATClient } from "@cityquest/fair-beat"

const fairbeat = new FairBEATClient({
  rpc: process.env.ARBITRUM_RPC,
  contract: process.env.FAIRBEAT_ROUTER_ADDRESS,
  community_id: "dumaguete-district-4"
})

// In JobAround payment handler:
await fairbeat.pay({
  recipient: worker.wallet_address,
  amount: job.agreed_amount_usdc,
  app_id: "jobaround",
  payer: employer.wallet_address
})
// That's it. Fair BEAT handles the split automatically.
```

---

## 7. Open Technical Questions

- [ ] Sybil resistance: how to prevent one person creating many wallets for higher share?
- [ ] Period frequency: weekly vs monthly distribution — what is best for worker cash flow?
- [ ] Fiat on/off ramp: how do workers in Philippines cash out USDC without crypto friction?
- [ ] Gas subsidization: who pays L2 gas for workers making small transactions?

---

## 8. Version History

| Version | Date | Notes |
|---------|------|-------|
| 0.1 | 2025-03 | Initial architecture |
| 0.2 | 2025-09 | Added treasury split, burn sink |
| 0.3 | 2026-03 | Trustnet integration, distribution algorithm |

---
*Document type: Technical Specification · Repository: 1149 // Idea Repository*
