---
id: 008
title: "Fair BEAT"
category: app
status: active
priority: high
related_1149: true
created: 2025-03-01
updated: 2026-03-14
author: Founder Alex
tags: [redistribution, solidarity, economy, City-Quest, mechanics, smart-contract]
---

# Fair BEAT — White Paper

> *Structural redistribution mechanics embedded in every transaction — solidarity by design, not by donation.*

---

## 1. The Problem

Every economic system in the City Quest ecosystem — and most solidarity-oriented projects in general — faces the same structural contradiction: the people who articulate the need for redistribution are rarely the ones who implement it in code. The result is systems that *say* they redistribute but *actually* accumulate at the top.

The problem is not intent. The problem is architecture. If redistribution requires a deliberate action (donation, vote, manual transfer), it will not happen at scale. Human coordination fails under friction.

---

## 2. The Vision

Fair BEAT is a **redistribution protocol** that makes every economic transaction in a City Quest app automatically allocate a configurable percentage to a community pool, distributed according to trust scores and participation metrics.

There is no opt-in. There is no donation button. There is no charity. **Redistribution happens in the transaction itself**, at the smart contract level, before anyone can withhold it.

---

## 3. Core Philosophy

- **Structural, not rhetorical** — the mechanism enforces redistribution; human virtue is not required
- **Configurable, not fixed** — each community sets its own parameters; Fair BEAT is the engine, not the policy
- **Transparent by default** — every distribution is on-chain and auditable by any participant
- **Trust-weighted** — distribution is proportional to Trustnet scores in context, rewarding consistent contributors

---

## 4. The Mechanism

### 4.1 Transaction Flow

```
User initiates transaction (e.g. JobAround payment: 1000 PHP)
  → Smart contract intercepts
  → Base amount: 930 PHP → recipient
  → BEAT split: 70 PHP (7%) → Community Pool
    → 40% distributed immediately to top trust-score contributors
    → 30% held in Community Treasury (governance-controlled)
    → 20% to Fair BEAT Protocol development fund
    → 10% burned / removed from circulation (deflationary pressure)
```

*All percentages are community-configurable. The 7% example is a default.*

### 4.2 Distribution Logic

Recipients of the immediate 40% pool receive shares proportional to:

```
share_i = trust_score_i / sum(trust_scores_all_active_members)
```

"Active" is defined per community — e.g., participated in last 30 days.

### 4.3 Solidarity Mechanics

The Community Treasury (30% allocation) is governed by trust-weighted voting. Proposals can direct funds to:
- Local community projects
- Onboarding new members
- Infrastructure maintenance
- Emergency support for members

---

## 5. Related Ideas

| Idea | Relationship |
|------|-------------|
| [Trustnet](../../protocols/trustnet/) | Provides trust scores for distribution weighting |
| [City Quest](../../../platforms/city-quest/) | Parent ecosystem — Fair BEAT is embedded in all 14 apps |
| [Good Project Corp](../../../../organizations/good-project-corp/) | Organizational layer that governs Treasury in physical deployment |

---

*Document type: White Paper · Repository: 1149 // Idea Repository*
