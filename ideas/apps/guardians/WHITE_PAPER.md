---
id: 005
title: "Guardians"
category: app
status: active
priority: high
related_1149: true
created: 2025-01-01
updated: 2026-03-14
author: Founder Alex
tags: [city-quest, civic-protection, ethics, community-safety, new-guardians, mutual-aid]
---

# Guardians — White Paper

> *A civic protection network where community safety is a shared, transparent, mutual responsibility — not a monopoly of force.*

## 1. The Problem

Public safety in most cities is either privatized (expensive, exclusionary) or monopolized (opaque, unaccountable). Neither model produces genuine community safety. Both models create communities where people feel managed rather than protected.

Mutual aid safety networks — neighbors looking out for each other — have always existed informally. But they are uncoordinated, invisible, and not scalable. There is no layer that turns diffuse civic care into organized civic protection.

## 2. The Vision

Guardians is the civic protection layer of City Quest. It coordinates people who choose to act as protectors of their community — not as police, but as witnesses, helpers, de-escalators, and advocates.

A Guardian is:
- Someone who has completed a community-verified ethics training
- Someone with a Trustnet score above a minimum threshold in the `guardians` context
- Someone who opts in to receiving alerts in their area and committing to response protocols

## 3. Core Philosophy

- **Transparency over secrecy** — all Guardian activity is logged and auditable
- **De-escalation first** — the protocol never incentivizes confrontation
- **Community accountability** — Guardians are accountable to the community, not to a hierarchy
- **Ethics as prerequisite** — you cannot be a Guardian without completing the ethical framework (New Guardians module)

## 4. The Mechanism

### Guardian Lifecycle
```
Citizen applies → Ethics training completion verified
  → Trustnet score check (minimum 0.4 in civic context)
  → Guardian status granted (on-chain badge)
  → Guardian receives area alerts
  → Guardian responds (or delegates)
  → Response logged: outcome, time, peers present
  → Trust score updated based on community feedback
```

### Alert Types

| Type | Description | Response Protocol |
|------|-------------|-------------------|
| Wellness check | Someone may need help | 1 Guardian minimum |
| Mediation request | Conflict needing neutral party | 2 Guardians |
| Documentation | Record a civic incident | 1 Guardian + camera |
| Emergency escalation | Beyond community scope | Hand off to authorities + document |

### Solidarity Mechanics

Guardians earn civic stake in Choose&Own for every logged response. The more you protect, the more governance weight you accumulate in your community.

## 5. Related Ideas

| Idea | Relationship |
|------|-------------|
| [City Quest](../../platforms/city-quest/) | Parent ecosystem |
| [Trustnet](../../protocols/trustnet/) | Guardian trust verification |
| [New Guardians](../../research/new-guardians/) | Ethical framework prerequisite |
| [Choose&Own](../choose-and-own/) | Civic stake earned through Guardian activity |
| [MeetMap](../meetmap/) | Location coordination for responses |

## 6. Open Questions

- [ ] How to handle Guardian misconduct? Community or external review?
- [ ] What is the minimum community size for a functional Guardian network?
- [ ] Integration with barangay tanod (Philippines community watch)?

---
*Document type: White Paper · Repository: 1149 // Idea Repository*
