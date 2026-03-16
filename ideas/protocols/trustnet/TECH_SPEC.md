---
id: 010
title: "Trustnet — Technical Specification"
category: protocol
status: research
version: 0.2
created: 2025-06-01
updated: 2026-03-14
author: Founder Alex
stack: [secp256k1, Ethereum L2, Node.js, Supabase, IPFS]
---

# Trustnet — Technical Specification

> *ECC-based trust scoring protocol. Cryptographically verifiable, socially meaningful.*

---

## 1. System Overview

```
[User Wallet]
      │ sign commitment
      ▼
[Trustnet Contract] ──→ [Trust Score Engine] ──→ [Score Registry]
      │                          │                       │
      │                    [Context Tags]          [City Quest]
      │                                             [Fair BEAT]
      ▼
[Vouch Graph] (IPFS-stored, on-chain hashed)
```

---

## 2. Tech Stack

| Layer | Technology | Reason |
|-------|-----------|--------|
| Curve | secp256k1 | BTC/ETH ecosystem consistency |
| Blockchain | Ethereum L2 (Arbitrum / Base) | Low gas, EVM compatible |
| Off-chain storage | IPFS + Supabase | Vouch graph too large for on-chain |
| Backend | Node.js (TypeScript) | n8n integration, City Quest stack alignment |
| Key library | `@noble/secp256k1` | Audited, modern, no native deps |
| Indexer | The Graph | Query trust graphs efficiently |
| API layer | Supabase Edge Functions | Serverless, low cost |

---

## 3. Data Models

### 3.1 Trust Identity

```typescript
interface TrustIdentity {
  address: string           // EVM wallet address — primary key
  contexts: string[]        // ['city-quest', 'uucp', 'blockchain-ph']
  public_key: string        // secp256k1 compressed public key
  created_at: number        // Unix timestamp
  metadata_ipfs: string     // IPFS CID → off-chain profile data
}
```

### 3.2 Commitment

```typescript
interface Commitment {
  id: string                // keccak256 hash
  maker: string             // address
  description: string       // plain text, stored on IPFS
  context: string           // tag — which community this applies to
  deadline: number          // Unix timestamp
  status: 'pending' | 'kept' | 'broken' | 'disputed'
  witnesses: string[]       // addresses that observed the outcome
  signature: string         // ECC signature of commitment hash
}
```

### 3.3 Vouch

```typescript
interface Vouch {
  id: string
  voucher: string           // address of voucher
  target: string            // address being vouched for
  context: string           // community context tag
  weight: number            // 0.01 – 1.0
  expires: number           // Unix timestamp, 0 = permanent
  signature: string         // secp256k1 signed: hash(voucher+target+context+weight+expires)
  revoked: boolean
  revoked_at?: number
}
```

### 3.4 Trust Score (computed, not stored)

```typescript
interface TrustScore {
  address: string
  context: string
  score: number             // 0.0 – 1.0 normalized
  components: {
    commitment_ratio: number    // kept / (kept + broken)
    vouch_weight: number        // sum of active vouch weights, normalized
    tenure: number              // log(days_active) normalized
    community_activity: number  // context-specific events, normalized
  }
  computed_at: number
}
```

---

## 4. Trust Score Algorithm

```typescript
function computeTrustScore(address: string, context: string): number {
  const commitments = getCommitments(address, context)
  const vouches = getActiveVouches(address, context)
  const tenure = getTenureDays(address, context)

  // Commitment ratio — 0.0 to 1.0
  const kept = commitments.filter(c => c.status === 'kept').length
  const broken = commitments.filter(c => c.status === 'broken').length
  const commitment_ratio = kept + broken > 0 ? kept / (kept + broken) : 0.5

  // Vouch weight — sum of voucher trust * vouch weight, normalized by max possible
  const vouch_weight = vouches.reduce((sum, v) => {
    const voucher_score = computeTrustScore(v.voucher, context) // recursive, cached
    return sum + voucher_score * v.weight
  }, 0)
  const normalized_vouch = Math.min(vouch_weight / 5.0, 1.0) // cap at 5 full vouches

  // Tenure — logarithmic growth, 1 year ≈ 0.7
  const tenure_score = Math.min(Math.log(tenure + 1) / Math.log(365), 1.0)

  // Weighted combination (community-configurable weights)
  const W = { commitment: 0.40, vouch: 0.35, tenure: 0.25 }

  return (
    W.commitment * commitment_ratio +
    W.vouch * normalized_vouch +
    W.tenure * tenure_score
  )
}
```

---

## 5. Smart Contract Skeleton

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract TrustnetRegistry {

    struct CommitmentRecord {
        bytes32 id;
        address maker;
        string ipfs_cid;        // full commitment data on IPFS
        string context;
        uint256 deadline;
        uint8 status;           // 0=pending 1=kept 2=broken 3=disputed
        uint256 created_at;
    }

    struct VouchRecord {
        bytes32 id;
        address voucher;
        address target;
        string context;
        uint16 weight_bps;      // basis points: 100 = 1.0
        uint256 expires;
        bool revoked;
    }

    mapping(bytes32 => CommitmentRecord) public commitments;
    mapping(bytes32 => VouchRecord) public vouches;
    mapping(address => bytes32[]) public commitmentsByAddress;
    mapping(address => bytes32[]) public vouchesByTarget;

    event CommitmentCreated(bytes32 indexed id, address indexed maker, string context);
    event CommitmentResolved(bytes32 indexed id, uint8 status);
    event VouchCreated(bytes32 indexed id, address indexed voucher, address indexed target);
    event VouchRevoked(bytes32 indexed id);

    function createCommitment(
        string calldata ipfs_cid,
        string calldata context,
        uint256 deadline,
        bytes calldata signature
    ) external returns (bytes32 id) {
        // verify signature, store commitment
    }

    function resolveCommitment(bytes32 id, uint8 status) external {
        // witnesses or auto-oracle resolves
    }

    function createVouch(
        address target,
        string calldata context,
        uint16 weight_bps,
        uint256 expires,
        bytes calldata signature
    ) external returns (bytes32 id) {
        // verify signature, store vouch
    }

    function revokeVouch(bytes32 id) external {
        // only voucher can revoke
    }
}
```

---

## 6. API Endpoints

```
GET    /api/trust/:address                      Get overall trust profile
GET    /api/trust/:address/:context             Get context-specific score
GET    /api/trust/:address/vouches              Get received vouches
GET    /api/trust/:address/commitments          Get commitment history
POST   /api/vouch                               Create vouch (signed payload)
POST   /api/commitment                          Create commitment
PUT    /api/commitment/:id/resolve              Resolve commitment outcome
GET    /api/graph/:context                      Get full trust graph for context
```

---

## 7. City Quest Integration

Trustnet acts as the identity and reputation backbone for all 14 City Quest apps:

```typescript
// City Quest app checks trust before action
async function canPerformAction(user: string, action: string, context: string): Promise<boolean> {
  const score = await trustnet.getScore(user, context)
  const threshold = ACTION_THRESHOLDS[action]   // e.g. { 'vote': 0.3, 'propose': 0.5 }
  return score >= threshold
}
```

---

## 8. Open Technical Questions

- [ ] Sybil resistance: how to prevent wallet farming for trust scores?
- [ ] Oracle design: who resolves disputed commitments?
- [ ] Privacy: can trust scores be queried privately (ZK proofs)?
- [ ] Cross-context trust transfer: should 0.8 in film community count in civic community?
- [ ] Gas optimization: batch vouch updates to minimize L2 transaction costs

---

## 9. Version History

| Version | Date | Notes |
|---------|------|-------|
| 0.1 | 2025-06 | Initial architecture sketch |
| 0.2 | 2026-03 | Added City Quest integration, refined scoring algorithm |

---

*Document type: Technical Specification · Repository: 1149 // Idea Repository*
