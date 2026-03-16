---
id: 006
title: "Press Club"
category: app
status: active
priority: medium
related_1149: true
created: 2025-01-01
updated: 2026-03-14
author: Founder Alex
tags: [city-quest, media, journalism, decentralized, community, press, independence]
---

# Press Club — White Paper

> *Independent community journalism as a civic commons — structurally protected from capture by money or power.*

## 1. The Problem

Local journalism is dying. Community media is captured by advertisers, politicians, or media conglomerates — or simply disappears for lack of funding. In its absence, misinformation fills the gap. Communities lose their mirror.

What survives is either institutional (and captured) or individual (and unsustainable). There is no structural middle ground that is simultaneously independent, sustainable, and community-owned.

## 2. The Vision

Press Club is a decentralized community media platform where:
- Journalists are funded directly by the community through Fair BEAT pools
- Editorial independence is protected by Trustnet (no funder can have a trust-weighted editorial vote)
- Every community member is both a potential contributor and a verified source
- Stories are archived on IPFS — uncensorable, permanent

## 3. Core Philosophy

- **Editorial independence is structural** — no advertiser, no patron, no entity with >5% of funding can influence editorial decisions (enforced by governance rule, not by ethics)
- **Community ownership** — the publication belongs to its readers/contributors, tracked via Choose&Own stake
- **Quality through trust scores** — journalists with higher Trustnet scores in `press/{community}` context get visibility, not those who are loudest
- **Permanent record** — every published article is IPFS-pinned at publication

## 4. The Mechanism

### Funding Loop
```
Community treasury (from Fair BEAT) allocates monthly press budget
  → Choose&Own vote determines allocation (investigative / local news / culture / etc.)
  → Journalists submit pitches
  → Trust-weighted community vote selects pitches for commissioning
  → Journalist completes article
  → Published → IPFS pinned → journalist paid
  → Reader feedback updates journalist trust score
```

### Source Verification

Any community member can register as a source for a specific topic area. Sources earn Trustnet score in the `press/source` context for accurate, verified contributions. Inaccurate sources lose score.

## 5. Related Ideas

| Idea | Relationship |
|------|-------------|
| [City Quest](../../platforms/city-quest/) | Parent ecosystem |
| [Trustnet](../../protocols/trustnet/) | Journalist/source credibility |
| [Fair BEAT](../fair-beat/) | Journalist compensation mechanism |
| [Choose&Own](../choose-and-own/) | Editorial governance |
| [UUCP Film Festival](../../events/uucp-film-festival/) | Cultural media overlap |
| [AI Cinema Lab](../../creative/ai-cinema-lab/) | Future: AI-assisted journalism tools |

## 6. Open Questions

- [ ] Content moderation: who decides what crosses from journalism to defamation?
- [ ] How to handle breaking news that can't wait for community voting?
- [ ] Multi-language publishing: EN + Cebuano simultaneously?

---
*Document type: White Paper · Repository: 1149 // Idea Repository*
