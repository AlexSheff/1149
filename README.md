# 1149 // Idea Repository

> *"Who am I in the context of the universe?"*
> Every idea here is an attempt to answer.

**Founder:** Alexandr Tokarev (Founder Alex)
**Base:** Dumaguete, Philippines
**Number:** 1149 — personal mythological symbol elevated to a system-level principle

---

## What this is

This repository is an **Idea Repository + Knowledge Archive** — not a task tracker, not a product backlog.
It captures every project, concept, white paper, and technical specification I've explored,
regardless of current status. Ideas here range from raw seeds to fully specified systems.

Each idea has one or both of:
- `WHITE_PAPER.md` — the *why*: philosophy, vision, use case, social architecture
- `TECH_SPEC.md` — the *how*: architecture, stack, mechanisms, data structures

---

## Registry

| # | Idea | Category | Status | Has WP | Has TS | Updated |
|---|------|----------|--------|--------|--------|---------|
| 001 | [Neuromicon](ideas/platforms/neuromicon/) | Platform | 🟢 Active | ✅ | ✅ | 2025-03 |
| 002 | [City Quest](ideas/platforms/city-quest/) | Ecosystem | 🟢 Active | ✅ | ✅ | 2025-03 |
| 003 | [Choose&Own](ideas/apps/choose-and-own/) | App | 🟢 Active | ✅ | ✅ | 2025-03 |
| 004 | [JobAround](ideas/apps/jobaround/) | App | 🟢 Active | ✅ | — | 2025-02 |
| 005 | [Guardians](ideas/apps/guardians/) | App | 🟢 Active | ✅ | — | 2025-02 |
| 006 | [Press Club](ideas/apps/press-club/) | App | 🟢 Active | ✅ | — | 2025-02 |
| 007 | [Art Maze](ideas/apps/art-maze/) | App | 🟢 Active | ✅ | — | 2025-02 |
| 008 | [Fair BEAT](ideas/apps/fair-beat/) | App | 🟢 Active | ✅ | ✅ | 2025-03 |
| 009 | [Recycle Economy](ideas/apps/recycle-economy/) | App | 🟢 Active | ✅ | — | 2025-02 |
| 010 | [Trustnet](ideas/protocols/trustnet/) | Protocol | 🔵 Research | ✅ | ✅ | 2025-03 |
| 011 | [UUCP Film Festival](ideas/events/uucp-film-festival/) | Event | 🟢 Active | ✅ | — | 2025-03 |
| 012 | [BTC Puzzle #66](ideas/research/btc-puzzle-66/) | Research | 🔵 Research | — | ✅ | 2025-03 |
| 013 | [ECC Cryptography](ideas/research/ecc-cryptography/) | Research | 🔵 Research | — | ✅ | 2025-02 |
| 014 | [AI Music Pipeline](ideas/creative/ai-music-pipeline/) | Creative | 🟢 Active | ✅ | ✅ | 2025-03 |
| 015 | [AI Cinema Lab](ideas/creative/ai-cinema-lab/) | Creative | 🟡 Concept | ✅ | — | 2025-03 |
| 016 | [Good Project Corp](organizations/good-project-corp/) | Org | 🟢 Active | ✅ | — | 2025-03 |
| 017 | [4Boon](organizations/4boon/) | Org | 🟢 Active | ✅ | — | 2025-02 |
| 018 | [UMKA Gasifier](ideas/research/umka-gasifier/) | Hardware | ⚪ Paused | ✅ | ✅ | 2024-12 |

**Status legend:** 🟢 Active · 🔵 Research · 🟡 Concept / Seed · ⚪ Paused · 🔴 Archived

---

## Structure

```
/
├── README.md                        ← You are here. Master index.
├── IDEAS_REGISTRY.md                ← Searchable flat list with metadata
├── CONNECTIONS.md                   ← How ideas link to each other
│
├── _templates/
│   ├── WHITE_PAPER_TEMPLATE.md      ← Use for new idea white papers
│   └── TECH_SPEC_TEMPLATE.md        ← Use for new technical specs
│
├── ideas/
│   ├── platforms/                   ← Core conceptual platforms
│   ├── apps/                        ← Product apps (City Quest family + others)
│   ├── protocols/                   ← Technical protocols and standards
│   ├── events/                      ← Recurring or one-time events
│   ├── research/                    ← Ongoing research threads
│   └── creative/                    ← Music, film, AI creative work
│
├── organizations/                   ← Legal/operational entities
│
└── .github/
    └── ISSUE_TEMPLATE/
        ├── new-idea.md              ← GitHub issue template: new idea
        └── new-whitepaper.md        ← GitHub issue template: add white paper
```

---

## How to add a new idea

### Option A — GitHub Issue (quickest capture)
Click **New Issue** → select **"New Idea"** template → fill in the seed fields.
This captures the idea immediately without writing full docs.

### Option B — Create the folder
```bash
# 1. Pick the right category
mkdir ideas/apps/my-new-idea

# 2. Copy the relevant template
cp _templates/WHITE_PAPER_TEMPLATE.md ideas/apps/my-new-idea/WHITE_PAPER.md
cp _templates/TECH_SPEC_TEMPLATE.md   ideas/apps/my-new-idea/TECH_SPEC.md

# 3. Fill in the fields
# 4. Add to the Registry table in README.md
# 5. Add connections in CONNECTIONS.md
```

### Option C — One-liner seed (for raw ideas)
Add a single row to `IDEAS_REGISTRY.md` with status `🟡 Concept` and just a title + one sentence description. Write the full doc later.

---

## Core principles embedded in this repository

1. **Solidarity is structural** — not rhetorical. Every product spec must describe *the mechanism*, not the intention.
2. **1149** — this number is a reference point, not a counter. When an idea connects to the 1149 mythological thread, note it in the front matter.
3. **Timeless map** — this repo is a mental map, not a sprint backlog. Ideas do not expire. They wait.
4. **Local anchor** —  Global vision, local mechanics.

---

*Last updated: March 2026*
