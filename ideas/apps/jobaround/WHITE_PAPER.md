---
id: 004
title: "JobAround"
category: app
status: active
priority: high
related_1149: true
created: 2025-01-01
updated: 2026-03-14
author: Founder Alex
tags: [city-quest, work, hyperlocal, marketplace, fair-economy, labor, redistribution]
---

# JobAround — White Paper

> *A hyperlocal work marketplace where fair pay and community solidarity are enforced by the protocol, not by goodwill.*

## 1. The Problem

Gig economy platforms (Fiverr, Upwork, local Facebook groups) extract 20–30% of every transaction, impose opaque rating systems that disadvantage newcomers, and create race-to-the-bottom pricing dynamics that harm local workers. The platform captures value the workers create.

In cities like Dumaguete, where informal labor is the economic backbone, there is no trusted infrastructure for local work: no verification of skills, no fair pricing signals, no history of completed work that travels with you.

## 2. The Vision

JobAround is a hyperlocal work marketplace where:
- The platform fee is 0% (replaced by the Fair BEAT 7% community contribution)
- Ratings are trust-score based (Trustnet) — not gameable, not biased
- Pricing floors are set by community governance via Choose&Own
- Workers accumulate portable, on-chain work history that increases their trust score
- Every transaction contributes to the local community treasury

## 3. Core Philosophy

- **Zero extraction** — the platform does not profit from transactions; the community does
- **Trust-portable history** — a worker's reputation belongs to them, not to the platform
- **Fair pricing signals** — community-set floors prevent race-to-the-bottom
- **Solidarity built in** — Fair BEAT triggers on every payment automatically

## 4. The Mechanism

### Posting Flow
```
Employer posts job (location-tagged via MeetMap)
  → Job appears in radius feed for workers
  → Workers apply with Trustnet score visible
  → Employer selects; escrow created on-chain
  → Work completed; peer verification (optional)
  → Payment released from escrow
  → Fair BEAT splits: 93% worker / 7% community
  → Both parties' Trustnet scores updated
```

### Trust-Based Discovery

Workers with higher Trustnet scores in the `work/{category}` context appear higher in search. No paid promotion. No boosted listings. Merit and history determine visibility.

### Pricing Floors

Communities using Choose&Own can vote to set minimum rates for specific job categories in their area. The smart contract enforces the floor — it is impossible to post a job below the community-set minimum.

## 5. Related Ideas

| Idea | Relationship |
|------|-------------|
| [City Quest](../../platforms/city-quest/) | Parent ecosystem |
| [Trustnet](../../protocols/trustnet/) | Worker/employer reputation |
| [Fair BEAT](../fair-beat/) | Payment redistribution |
| [MeetMap](../meetmap/) | Job location tagging |
| [Choose&Own](../choose-and-own/) | Pricing floor governance |

## 6. Open Questions

- [ ] How to handle dispute resolution between worker and employer?
- [ ] Cross-city job postings: how does trust score transfer across cities?
- [ ] Handling cash-preferred workers who can't use on-chain escrow?

## 7. Status Notes

**[2026-03-14]** — MVP feature list and UX spec in queue.

---
*Document type: White Paper · Repository: 1149 // Idea Repository*
