---
id: 013b
title: "MeetMap"
category: app
status: active
priority: medium
related_1149: false
created: 2025-01-01
updated: 2026-03-14
author: Founder Alex
tags: [city-quest, maps, location, events, geospatial, coordination, community]
---

# MeetMap — White Paper

> *The location layer of City Quest — making community activity spatially visible.*

## 1. The Vision

MeetMap is the geospatial coordination layer for all City Quest activities. It answers: **where is civic life happening right now?**

Every app in City Quest that involves a physical location pins to MeetMap:
- Community meetings (Choose&Own, Guardians)
- Job locations (JobAround)
- Recycling drop-off points (Recycle Economy)
- Guardian response zones
- ImInGame civic quest locations
- Cultural events (UUCP Film Festival, Art Maze)

## 2. The Mechanism

### Live City Map

A real-time map showing all active City Quest activity in a geographic area. Filtered by:
- Category (civic / work / culture / ecology / safety)
- Trust level required (open / verified / guardian-only)
- Time (now / today / this week)

### Check-in Protocol

Physical attendance verification for civic actions:
```
Citizen arrives at location
  → App detects GPS proximity (50m radius)
  → Soft check-in: confirms presence
  → Optional: photo with location tag
  → Hard check-in: peer confirmation (another citizen at location confirms)
  → Trustnet event logged: "attended:{event_id}:{location_id}"
```

Hard check-in (peer-confirmed) carries higher trust weight than GPS-only check-in.

### Community Points of Interest

Any citizen can register a Point of Interest (POI):
- Recycling drop-off points
- Community resource locations
- Guardian safe zones
- Public art (Art Maze integration)

POIs require 3 community confirmations to become official. They decay if not re-confirmed every 6 months.

## 3. Related Ideas

| Idea | Relationship |
|------|-------------|
| [City Quest](../../platforms/city-quest/) | Parent ecosystem |
| [Recycle Economy](../recycle-economy/) | Drop-off point mapping |
| [Guardians](../guardians/) | Response zone coordination |
| [ImInGame](../imin-game/) | Quest location layer |
| [Choose&Own](../choose-and-own/) | Meeting attendance verification |

---
*Document type: White Paper · Repository: 1149 // Idea Repository*
