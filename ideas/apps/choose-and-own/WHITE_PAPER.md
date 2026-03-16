---
id: 003
title: "Choose&Own"
category: app
status: active
priority: high
related_1149: true
created: 2025-01-01
updated: 2026-03-14
author: Founder Alex
tags: [city-quest, civic, ownership, democracy, participation, voting, solidarity]
---

# Choose&Own — White Paper

> *Civic ownership made real: every choice you make in your community earns you a stake in it.*

## 1. The Problem

Democratic participation in modern cities is broken at the micro level. Voting happens once every few years, on issues most citizens barely understand, through interfaces designed for compliance rather than engagement. There is no feedback loop between **civic action** and **civic stake**.

## 2. The Vision

Choose&Own makes the feedback loop explicit and material. Every deliberate civic action — voting on a local issue, attending a community meeting, completing a neighborhood task — earns the participant a measurable **stake** in that resource or decision. Stakes are tracked on-chain via Trustnet, visualized in the app, and used to weight future participation.

## 3. Core Philosophy

- **Participation is ownership** — contributing earns stake, stake earns voice
- **No passive ownership** — stakes decay slowly without continued participation (anti-absentee landlord)
- **Solidarity over plutocracy** — stake earned through action only, never purchased
- **Transparent ledger** — every stake, vote, and action is auditable

## 4. The Mechanism

### Core Loop
```
Citizen performs civic action
  → Action verified (peer witness or oracle)
  → Stake minted proportional to action weight
  → Stake recorded in Trustnet context: "civic/{community-id}"
  → Governance weight updated
  → Stakes decay at 2%/month if inactive
```

### Action Weights

| Action | Stake Weight | Verification |
|--------|-------------|--------------|
| Vote on community issue | 1.0 | On-chain |
| Attend community meeting | 1.5 | MeetMap check-in |
| Complete neighborhood task | 2.0–5.0 | 3 peer confirmations |
| Propose an initiative | 3.0 | Submission + acceptance |
| Fulfill a commitment | +50% bonus | Trustnet resolution |
| Miss a commitment | −30% penalty | Trustnet failure |

### Solidarity Mechanics (Fair BEAT split)
- 85% → direct allocation to winning proposal
- 10% → Community Treasury
- 5% → participation reward pool (all voters, proportional to stake)

### Stake Decay
```
stake_today = stake_yesterday × (1 - 0.02/30)
```
~2% decay per month. Prevents early contributors permanently dominating governance.

## 5. Related Ideas

| Idea | Relationship |
|------|-------------|
| [City Quest](../../platforms/city-quest/) | Parent ecosystem |
| [Trustnet](../../protocols/trustnet/) | Identity + stake recording |
| [Fair BEAT](../fair-beat/) | Redistribution engine |
| [MeetMap](../meetmap/) | Meeting attendance verification |
| [ImInGame](../imin-game/) | Gamification and civic quests |

## 6. Open Questions

- [ ] Stake transferability for minors?
- [ ] Multi-district participation: how are stakes separated?
- [ ] Integration with existing Philippine barangay governance structures?

## 7. Status Notes

**[2026-03-14]** — Solidarity mechanics specification in progress. UX assigned to Petra Novak.

---
*Document type: White Paper · Repository: 1149 // Idea Repository*
