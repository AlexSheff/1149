---
id: "4001"
title: "Trustnet"
layer: "04_Technical_Nodes"
doctype: "Protocol"
status: research
priority: high
tags: [ECC, blockchain, trust, secp256k1, protocol, decentralized, social-coordination]
related: ["3003", "3003f", "4003"]
is_1149: true
created: 2025-06-01
updated: 2026-03-16
author: Founder
---

# Trustnet — White Paper

> *A trust-based decentralized social coordination protocol built on elliptic curve cryptography.*

---

## 1. The Problem

Every existing decentralized social network solves for identity or ownership — but not trust. They can prove *who* you are and *what* you own, but they cannot prove *how trustworthy* you are, *how reliable* your word is, or *how embedded* you are in a community of practice.

Trust in human systems is relational, contextual, accumulated over time, and impossible to fake at scale. The social mechanics of the modern web — follower counts, likes, reputation scores — are gameable proxies, not real measures of trust.

---

## 2. The Vision

Trustnet makes trust **cryptographically computable** and **socially meaningful**.

It allows:
- Any two people to establish a trust relationship with a signed cryptographic commitment
- Communities to build trust graphs with provable, auditable histories
- Applications (like City Quest) to gate access and distribute resources based on verified trust scores
- Trust to be **earned, delegated, lost, and recovered** — not purchased or gamed

---

## 3. Trust Score Formula

```
Trust Score = f(
  commitments_made,    // what you said you'd do
  commitments_kept,    // what you actually did
  voucher_weight,      // who vouches for you (weighted by their score)
  community_tenure,    // how long you've been active
  context_tags         // which community context
)
```

---

## 4. Vouching (ECC Commitment)

Any participant can vouch for another using a signed ECC commitment:

```
vouch = sign(
  voucher_private_key,
  { target: address, context: tag,
    weight: 0.0–1.0, expires: timestamp }
)
```

Vouches can be withdrawn. Withdrawn vouches reduce the target's score proportionally.

---

## 5. Trust Levels

| Level | Name | Threshold |
|-------|------|-----------|
| 1 | Acquaintance | score > 0.1 |
| 2 | Collaborator | score > 0.3 |
| 3 | Trusted Partner | score > 0.6 |
| 4 | Core Circle | score > 0.85 |

---

## 6. City Quest Integration

Trustnet is the identity and reputation backbone for all 14 City Quest apps. Access to governance, resource allocation, and Fair BEAT distributions are gated by trust scores in context.

---

## 7. Solidarity Mechanics

Trust scores feed directly into Fair BEAT distribution weights. Consistent contributors receive proportionally more from the community pool — structural reward for structural contribution.

---

*White Paper · Reality Refactor Lab · 1149*

