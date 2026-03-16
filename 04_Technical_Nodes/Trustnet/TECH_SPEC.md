---
id: "4001"
title: "Trustnet — Technical Specification"
layer: "04_Technical_Nodes"
doctype: "Tech Spec"
status: research
version: 0.2
stack: [secp256k1, Ethereum-L2, Node.js, Supabase, IPFS, The-Graph]
created: 2025-06-01
updated: 2026-03-16
author: Founder
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
| Backend | Node.js (TypeScript) | n8n integration, City Quest stack |
| Key library | @noble/secp256k1 | Audited, no native deps |
| Indexer | The Graph | Efficient trust graph queries |

---

## 3. Data Models

```typescript
interface TrustIdentity {
  address: string           // EVM wallet address
  contexts: string[]        // ['city-quest', 'uucp', 'blockchain-ph']
  public_key: string        // secp256k1 compressed public key
  created_at: number        // Unix timestamp
}

interface Commitment {
  id: string                // keccak256 hash
  maker: string             // address
  description: string       // plain text, stored on IPFS
  context: string           // community tag
  deadline: number          // Unix timestamp
  status: 'pending' | 'kept' | 'broken' | 'disputed'
  signature: string         // ECC signature
}

interface Vouch {
  id: string
  voucher: string           // address of voucher
  target: string            // address being vouched for
  context: string           // community context tag
  weight: number            // 0.01–1.0
  expires: number           // 0 = permanent
  signature: string         // secp256k1 signed
  revoked: boolean
}
```

---

## 4. Trust Score Algorithm

```typescript
function computeTrustScore(address: string, context: string): number {
  const commitments = getCommitments(address, context);
  const vouches = getActiveVouches(address, context);
  const tenureDays = getTenureDays(address, context);

  const kept   = commitments.filter(c => c.status === 'kept').length;
  const broken = commitments.filter(c => c.status === 'broken').length;
  const commitmentRatio = kept + broken > 0 ? kept / (kept + broken) : 0.5;

  // Trust-weighted vouches (recursive, cached)
  const vouchWeight = vouches.reduce((sum, v) => {
    const voucherScore = computeTrustScore(v.voucher, context);
    return sum + voucherScore * v.weight;
  }, 0);
  const normalizedVouch = Math.min(vouchWeight / 5.0, 1.0);

  const tenure = Math.min(Math.log(tenureDays + 1) / Math.log(365), 1.0);

  const W = { commitment: 0.40, vouch: 0.35, tenure: 0.25 };
  return W.commitment * commitmentRatio
       + W.vouch * normalizedVouch
       + W.tenure * tenure;
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
    string ipfs_cid;
    string context;
    uint256 deadline;
    uint8 status;       // 0=pending 1=kept 2=broken 3=disputed
    uint256 created_at;
  }

  struct VouchRecord {
    bytes32 id;
    address voucher;
    address target;
    string context;
    uint16 weight_bps;  // basis points: 10000 = 1.0
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
}
```

---

## 6. Open Technical Questions

- [ ] Sybil resistance: how to prevent wallet farming for trust scores?
- [ ] Oracle design: who resolves disputed commitments?
- [ ] ZK proofs: can trust scores be queried privately?
- [ ] Cross-context trust transfer: should score in film community count in civic community?

---

*Tech Spec · Reality Refactor Lab · 1149*

