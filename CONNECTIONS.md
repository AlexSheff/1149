# Connections Map

*How ideas in this repository relate to each other.*
*Read this before creating a new idea — it may already exist, or connect to something you haven't considered.*

---

## Core Dependency Graph

```
                        1149 (axiom)
                            │
                       NEUROMICON (001)
                      ╱    │    │    ╲
                     ╱     │    │     ╲
              TRUSTNET   CITY   AI     SOCIAL
               (010)    QUEST  MEDIA   ARCH
                         (002)  PIPE   LAYER
                         ╱╲      │       │
                        ╱  ╲     │       │
                   14 APPS  │  AI CINEMA  GOOD PROJECT
                     ...    │    LAB     CORP (016)
                            │   (015)     │
                         FAIR             4BOON
                          BEAT           (017)
                          (008)
```

---

## Dependency Table

| Idea | Depends on | Enables | Feeds data to |
|------|-----------|---------|---------------|
| Neuromicon (001) | — | Everything | Everything |
| City Quest (002) | Neuromicon | 14 apps | Fair BEAT, Trustnet |
| Trustnet (010) | Neuromicon, ECC Research | City Quest identity, Fair BEAT weights | All City Quest apps |
| Fair BEAT (008) | Trustnet, City Quest | All economic apps | Good Project Corp treasury |
| Choose&Own (003) | City Quest, Trustnet | — | Fair BEAT |
| JobAround (004) | City Quest, Trustnet | — | Fair BEAT |
| Guardians (005) | City Quest, Trustnet | New Guardians framework | — |
| Press Club (006) | City Quest | AI Music Pipeline (distribution layer) | — |
| Art Maze (007) | City Quest | AI Cinema Lab (distribution) | — |
| ImInGame (008) | City Quest, Trustnet | — | Trust scores |
| MeetMap (009) | City Quest | — | Recycle Economy (locations) |
| Recycle Economy (011) | City Quest, MeetMap | — | Fair BEAT |
| Duma inWork (012) | City Quest | — | — |
| UUCP Film Festival (013) | — | AI Cinema Lab, Press Club | Neuromicon (narrative) |
| Good Project Corp (016) | Fair BEAT | 4Boon | Treasury governance |
| 4Boon (017) | Good Project Corp | — | — |
| AI Music Pipeline (014) | — | AI Cinema Lab | Press Club (content) |
| AI Cinema Lab (015) | UUCP, Art Maze, AI Music | — | Neuromicon (media) |
| Trustnet (010) | ECC Research (013) | City Quest, Fair BEAT | — |
| BTC Puzzle #66 (012) | ECC Research | — | — |
| ECC Cryptography (013) | — | Trustnet, BTC Puzzle | — |
| New Guardians (017) | Guardians app | — | Neuromicon (philosophy) |
| UMKA Gasifier (018) | — | — | — (paused) |

---

## Cluster Summary

### Cluster 1 — Foundation
`Neuromicon` → `1149 axiom` → *everything else*

### Cluster 2 — City Quest Ecosystem
`City Quest` → `Choose&Own` `JobAround` `Guardians` `Press Club` `Art Maze`
`ImInGame` `MeetMap` `Fair BEAT` `Recycle Economy` `Duma inWork`
All share: Trustnet identity + Fair BEAT redistribution + solidarity mechanics

### Cluster 3 — Trust & Cryptography
`ECC Research` → `Trustnet` → City Quest identity layer → `Fair BEAT` weights

### Cluster 4 — Creative Pipeline
`AI Music Pipeline` → `AI Cinema Lab` → `UUCP Film Festival` → `Art Maze` `Press Club`

### Cluster 5 — Civic Infrastructure
`Good Project Corp` ↔ `4Boon` → `Fair BEAT` governance → Dumaguete pilot

---

## Quick Reference: What enables what

If you want to build **X**, you need **Y** first:

| Want to build | Needs first |
|--------------|-------------|
| Any City Quest app with payments | Fair BEAT |
| Fair BEAT | Trustnet |
| Trustnet | ECC Research |
| Trust-gated governance | Trustnet |
| AI Cinema Lab | AI Music Pipeline (tools), UUCP (venue) |
| City Quest Dumaguete pilot | Choose&Own + MeetMap + Recycle Economy MVP |

---

*Last updated: March 2026*
