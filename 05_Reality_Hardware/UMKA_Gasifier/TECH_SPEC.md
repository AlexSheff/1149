---
id: "5002"
title: "UMKA Gasifier — Technical Specification"
layer: "05_Reality_Hardware"
status: paused
version: 0.3
stack: [biomass-gasification, syngas, internal-combustion-generator]
created: 2024-01-01
updated: 2026-03-16
author: Founder Alex
---

# UMKA Gasifier — Technical Specification

---

## 1. Gasification Process Flow

```
Biomass feedstock (coconut husks / rice straw / wood chips)
  │
  ▼ DRYING ZONE (100–200°C)
  │   Moisture removed, feedstock prepared
  │
  ▼ PYROLYSIS ZONE (200–500°C)
  │   Volatile compounds released, char formed
  │
  ▼ OXIDATION ZONE (700–1200°C)
  │   Partial combustion, heat generation
  │
  ▼ REDUCTION ZONE (800–1000°C)
  │   CO₂ + H₂O + C → CO + H₂ (syngas reactions)
  │
  ▼ SYNGAS OUTPUT
      Composition: CO (18–22%) + H₂ (15–20%) + CH₄ (2–4%) + N₂ + CO₂
      Lower heating value: ~4–5 MJ/m³
  │
  ▼ GAS CLEANING
      Cyclone separator → tar scrubber → filter
  │
  ▼ ENGINE / GENERATOR
      Syngas-fueled internal combustion engine
      Electrical output: 5–20 kW
```

---

## 2. Key Design Parameters

| Zone | Temperature | Residence Time |
|------|------------|----------------|
| Drying | 100–200°C | 10–20 min |
| Pyrolysis | 200–500°C | 5–10 min |
| Oxidation | 700–1200°C | 1–2 sec |
| Reduction | 800–1000°C | 2–5 sec |

---

## 3. Feedstock Preparation

```
Raw biomass → Size reduction (< 50mm pieces)
  → Moisture reduction (< 15% moisture content)
  → Hopper feed (continuous or batch)
```

Coconut husks have natural moisture ~30–50%. Sun-drying to <15% required before gasification.

---

## 4. Output Quality Targets

| Parameter | Target |
|-----------|--------|
| Tar content | < 50 mg/m³ |
| Particulate | < 50 mg/m³ |
| H₂S | < 200 ppm |
| Cold gas efficiency | > 70% |

---

## 5. Resumption Conditions

- [ ] Physical space secured (minimum 50m² covered area)
- [ ] Initial materials budget (~$3,000–5,000 USD)
- [ ] Local fabrication partner identified
- [ ] Philippine DOE permit pathway clarified
- [ ] Biomass supply agreement with Recycle Economy

---

*Tech Spec · Reality Refactor Lab · 1149*
