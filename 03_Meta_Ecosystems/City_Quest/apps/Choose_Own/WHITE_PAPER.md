---
id: "3003a"
title: "Choose&Own"
layer: "03_Meta_Ecosystems"
doctype: "App"
status: active
priority: high
tags: [city-quest, civic, app]
related: ["3003", "4001", "3003f"]
is_1149: true
created: 2025-01-01
updated: 2026-03-16
author: Founder
---

# Choose&Own — White Paper

> *Civic ownership made real: every civic action earns you a stake in your community.*

---

## The Mechanism

Every deliberate civic action — voting on a local issue, attending a meeting, completing a neighborhood task — earns the participant a measurable **stake** that determines governance weight.

### Core Loop
```
Citizen performs civic action
  → Action verified (peer witness or oracle)
  → Stake minted proportional to action weight
  → Recorded in Trustnet: "civic/{community-id}"
  → Governance weight updated
  → Stakes decay at 2%/month if inactive
```

### Action Weights

| Action | Weight | Verification |
|--------|--------|-|
| Vote on issue | 1.0 | On-chain |
| Attend meeting | 1.5 | MeetMap check-in |
| Complete task | 2.0–5.0 | 3 peer confirmations |
| Propose initiative | 3.0 | Submission + acceptance |

### Solidarity: Fair BEAT Split
- 85% → winning proposal
- 10% → Community Treasury
- 5% → participation reward pool (all voters earn, even losing side)

### Anti-Absenteeism
```
stake_today = stake_yesterday × (1 - 0.02/30)
```
Stakes decay ~2%/month. Prevents early contributors permanently dominating governance.

---

## Solidarity Mechanism

Participation itself is economically rewarded. Even voting on the losing side earns tokens.

---

## Related

| Idea | Relationship |
|------|-------------|
| [City Quest](../../WHITE_PAPER.md) | Parent ecosystem |
| [Trustnet](../../../../04_Technical_Nodes/Trustnet/WHITE_PAPER.md) | Identity and reputation |
| [Fair BEAT](../Fair_BEAT/WHITE_PAPER.md) | Redistribution engine |

---

*App White Paper · City Quest · Reality Refactor Lab · 1149*

