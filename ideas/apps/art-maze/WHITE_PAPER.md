---
id: 007
title: "Art Maze"
category: app
status: active
priority: medium
related_1149: true
created: 2025-01-01
updated: 2026-03-14
author: Founder Alex
tags: [city-quest, art, creative-economy, collaboration, artists, culture, AI]
---

# Art Maze — White Paper

> *A creative economy platform where artists collaborate, earn, and own their work — without galleries, without intermediaries, without extraction.*

## 1. The Problem

The economics of visual art, music, and creative work are structurally broken for independent artists. Platforms (Instagram, Spotify, OpenSea) capture most of the value. Galleries extract 50%. Algorithms reward engagement over quality. AI-generated art creates attribution chaos.

Artists in cities like Dumaguete are doubly disadvantaged: they work in markets that undervalue local culture while being too far from global markets to access them effectively.

## 2. The Vision

Art Maze is the creative economy layer of City Quest:
- Artists publish, sell, and license work directly, with smart contract-enforced royalties
- AI-generated art includes mandatory attribution chains (human creative direction is tracked)
- Collaborative works automatically split revenue according to contribution weights
- Local art economy is visible, measurable, and fundable by the community treasury

## 3. Core Philosophy

- **Attribution is infrastructure** — every creative contribution is recorded; remix cultures thrive when credit flows correctly
- **AI augmentation, not replacement** — AI tools are collaborative instruments; the human creative direction is the copyrightable element
- **Fair BEAT embedded** — every sale contributes to the community creative fund
- **No curation monopoly** — Trustnet-weighted community curation, not gallery gatekeepers

## 4. The Mechanism

### Publication Flow
```
Artist creates work (solo or collaborative)
  → Attribution declared: contributors + AI tools used
  → Work published on Art Maze (IPFS storage)
  → Smart contract minted with royalty splits
  → Appears in community feed (Trustnet-ranked)
  → Buyer purchases / licenses
  → Fair BEAT: 85% artist(s) / 8% community fund / 7% Art Maze protocol
  → Secondary sales: 10% royalty to original creator(s) forever
```

### AI Art Attribution Standard

```
work_metadata = {
  human_creators: [address1, address2],
  ai_tools: ["Midjourney v6", "Stable Diffusion XL"],
  human_direction: "text prompt / sketch / reference — stored on IPFS",
  copyright_holder: address1,  // the human who directed the AI
}
```

## 5. Related Ideas

| Idea | Relationship |
|------|-------------|
| [City Quest](../../platforms/city-quest/) | Parent ecosystem |
| [AI Cinema Lab](../../creative/ai-cinema-lab/) | Art Maze is the distribution channel for AI film |
| [AI Music Pipeline](../../creative/ai-music-pipeline/) | Art Maze houses the visual art layer of music releases |
| [UUCP Film Festival](../../events/uucp-film-festival/) | Festival submissions feed Art Maze catalogue |
| [Fair BEAT](../fair-beat/) | Revenue redistribution |
| [Trustnet](../../protocols/trustnet/) | Artist credibility and curation weighting |

## 6. Open Questions

- [ ] How to handle copyright disputes over AI-generated elements?
- [ ] Physical art: can real-world pieces be tokenized in Art Maze?
- [ ] Community curation: how to prevent popularity bias over quality?

---
*Document type: White Paper · Repository: 1149 // Idea Repository*
