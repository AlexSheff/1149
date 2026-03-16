---
id: "3003i"
title: "MeetMap"
layer: "03_Meta_Ecosystems"
doctype: "App"
status: active
priority: high
tags: [city-quest, civic, app]
related: ["3003", "4001", "3003f"]
is_1149: true
created: 2025-01-01
updated: 2026-03-16
author: Founder Alex
---

# MeetMap — White Paper

> *The geospatial coordination layer — making community activity spatially visible in real time.*

---

## What MeetMap Shows

Every City Quest activity that involves a physical location pins to MeetMap:
- Community meetings (Choose&Own, Guardians)
- Job locations (JobAround)
- Recycling collection points (Recycle Economy)
- Guardian response zones
- Civic quest locations (ImInGame)
- Cultural events (UUCP Film Festival, Art Maze)

### Check-in Protocol
```
Citizen arrives → App detects GPS proximity (50m)
  → Soft check-in: GPS confirmation
  → Hard check-in: peer confirmation (another citizen confirms)
  → Trustnet event logged: "attended:{event_id}:{location}"
```
Hard check-in carries higher trust weight than GPS-only.

---

## Solidarity Mechanism

Physical attendance verification creates unfakeable proof of civic participation.

---

## Related

| Idea | Relationship |
|------|-------------|
| [City Quest](../../WHITE_PAPER.md) | Parent ecosystem |
| [Trustnet](../../../../04_Technical_Nodes/Trustnet/WHITE_PAPER.md) | Identity and reputation |
| [Fair BEAT](../Fair_BEAT/WHITE_PAPER.md) | Redistribution engine |

---

*App White Paper · City Quest · Reality Refactor Lab · 1149*
