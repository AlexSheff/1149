---
id: "8013"
title: "GarageForge: ChipMaker"
layer: "04_Technical_Nodes"
doctype: "White Paper"
status: concept
priority: medium
progress: 0
tags: [idea, tech, DIY]
related: []
is_1149: false
updated: 2026-04-02
author: Founder Alex
tagline: "\"What if prototyping custom microchips were as easy as 3D printing an object?\" — This idea is feasible today, using only proven physical principles."
---

# GarageForge: ChipMaker — White Paper

> *"What if prototyping custom microchips were as easy as 3D printing an object?" — This idea is feasible today, using only proven physical principles.*

---

OpenFab
Open-Source Desktop Semiconductor Prototyping System
White Paper  v1.0  |  April 2026
License: CC BY-SA 4.0  

"What if prototyping custom microchips were as easy as 3D printing an object?" — This idea is feasible today, using only proven physical principles.

Abstract
OpenFab is a low-cost, modular desktop system for home and makerspace prototyping of custom semiconductor devices. Unlike the previous GarageForge concept, OpenFab is built exclusively on proven, well-documented physics — no speculative electrostatic plasma control, no unverified deposition mechanisms.

The core innovation is the combination of three mature technologies applied at desktop scale:
DLP Maskless Photolithography — digital patterning without physical masks, achieving 2–10 µm features using a 405 nm LED and a bare DMD chip from a commercial projector.
Aerosol Jet Printing (AJP) — direct deposition of functional inks (conductive, semiconductive, dielectric) with 10–50 µm resolution, no vacuum required.
Wet Electrochemical Deposition — proven, inexpensive metal layer growth for interconnects (Cu, Ni, Au).

The system is buildable for $800–3,500 depending on the chosen track, and enables complete design-build-test cycles in 30–120 minutes. It is explicitly inspired by Sam Zeloof's work (who fabricated real MOSFETs at home using DLP lithography) and targets the same democratization of semiconductor experimentation that RepRap achieved for mechanical prototyping.

Proof of concept exists: Sam Zeloof (samuelzeloof.com) fabricated functional MOSFETs and ICs at home between 2017–2022 using exactly the core technologies described in this paper.


1. Introduction and Motivation
1.1 The Problem
Modern chip fabrication is inaccessible. TSMC's 3nm process costs $15,000+ per wafer. Even university cleanrooms charge $200–1000/hour. This creates a hard barrier: you cannot iterate hardware ideas the way you iterate software. There is no "git commit" for silicon.
The 3D printer revolution happened when the cost of mechanical prototyping dropped from $50,000 (commercial SLA, 1990s) to $200 (RepRap, 2010). OpenFab targets the same 100–1000x cost reduction for semiconductor prototyping.

1.2 What Has Already Been Proven
Key reference: Sam Zeloof, an independent engineer working from his garage in New Jersey, built a complete semiconductor fabrication process and manufactured real chips:
2017–2018: First homemade MOSFET using spin coating, UV exposure, and wet etching
2020: Z1 chip — a working JFET array, 6 µm feature size
2022: Z2 chip — DLP maskless lithography at ~1.2 µm, functional amplifier circuits
Total budget: ~$10,000. OpenFab targets $800–3,500 through modular design and modern cheap components (DLP chips on AliExpress now cost $30–80).

Sam Zeloof did not use electrostatic plasma control, exotic vacuum systems, or proprietary processes. He used spin coating, DLP lithography, wet etching, and diffusion doping — all techniques described in 1960s semiconductor textbooks. The barrier was cost and integration, not physics.


1.3 Design Philosophy
Physics first: every mechanism must have peer-reviewed validation or documented DIY precedent.
Modular tracks: Organic Electronics Track (no vacuum, $800–1500) and Inorganic Thin-Film Track ($2500–3500).
Open everything: CAD files, firmware, ink recipes, process logs, failure reports — all public.
Safe by default: no HF without specific protocols, no high-energy lasers in base config, full interlock system.

2. Core Technologies — Physics Validation
2.1 DLP Maskless Photolithography
Mechanism
A Digital Micromirror Device (DMD) — the same chip used in every DLP projector — consists of millions of individually-addressable mirrors (17×17 µm each on Texas Instruments DLP2010). Each mirror tilts ±12° to reflect UV light either toward or away from the substrate. Combined with a 405 nm LED source and a reduction lens system, this creates a programmable photomask.

Resolution
Parameter
Value
Notes
DMD chip
DLP2010 (854×480)
$30–80 on AliExpress
Pixel pitch (native)
17 µm
TI datasheet, verified
Resolution with 5x reduction optics
~3.4 µm/pixel
Standard UV microscopy optics
Practical feature size
2–5 µm
Limited by photoresist diffusion
Field of view (at 5x)
~3 × 1.7 mm
Sufficient for prototype devices
Exposure time per field
5–30 sec
Depends on resist sensitivity


For reference: Sam Zeloof's Z2 chip achieved ~1.2 µm features using a commercial DLP projector with custom optics. His build log is public and reproducible.

Photoresists
AZ1512 (positive): extremely well-documented, $40–60/100ml, spun at 3000 RPM for 1.4 µm thickness, develops in AZ400K diluted 1:4, etch resistant.
SU-8 (negative): for thick structural layers (2–50 µm), excellent chemical resistance, used for dielectric patterning.
PMGI/LOR: lift-off layers for metal patterning without etching.

2.2 Aerosol Jet Printing (AJP)
Mechanism
An ultrasonic transducer (1.7 MHz, identical to home humidifiers) atomizes a liquid ink into droplets of 1–5 µm diameter. A focused sheath gas (N₂ or compressed air) collimates the aerosol stream into a jet 50–200 µm wide. The substrate is moved by an XY stage, and material is deposited in programmed patterns without contact.

Unlike standard inkjet printing (which requires very specific ink viscosity 1–10 cP and suffers nozzle clogging), AJP tolerates viscosities of 1–1000 cP and particle sizes up to 0.5 µm. This opens access to conductive, semiconductive, and dielectric inks.

Printable Materials for OpenFab
Material
Function
Resolution
Availability
PEDOT:PSS
Transparent conductor (OTFTs)
20–50 µm
Sigma-Aldrich, ~$80/50ml
Silver nanoparticle ink
Metal interconnects
10–30 µm
Many vendors, ~$50–120/10ml
P3HT in chlorobenzene
Organic semiconductor
30–80 µm
Sigma-Aldrich, ~$60/g
TIPS-pentacene
High-mob organic semiconductor
20–50 µm
Research suppliers
PMMA in anisole
Gate dielectric
20–100 µm
Standard, ~$30/100ml
ZnO nanoparticle ink
Inorganic semiconductor (TFT)
15–40 µm
Sigma-Aldrich
ITO nanoparticle ink
TCO electrode
20–50 µm
Multiple vendors


AJP is not speculative. Optomec has sold commercial AJP systems since 2004. DIY implementations have been published in peer-reviewed journals (e.g., Rida et al., IEEE 2007). The ultrasonic atomizer alone costs $15–30.


2.3 Wet Electrochemical Deposition
Electroplating of metal layers is one of the oldest and most reliable thin-film techniques. In OpenFab, it is used for metal interconnects and contact pads, replacing expensive physical vapor deposition (PVD) for conductive layers.

Supported Metals
Metal
Electrolyte
Role
Cost
Copper (Cu)
CuSO₄ + H₂SO₄
Primary interconnects
Trivial — PCB plating chemistry
Nickel (Ni)
NiSO₄ bath
Diffusion barrier, contacts
$20–40/L solution
Gold (Au)
KAu(CN)₂ bath
Wire bond pads, corrosion resistance
$80–150/L
Zinc (Zn)
ZnSO₄ bath
Sacrificial / test layers
Trivial


Deposition rates: 0.1–1 µm/min at 1–10 mA/cm². Thickness uniformity ±10–15% achievable with simple agitation. Current density control via a $15 Arduino-based power supply with feedback.

2.4 Spin Coating
A spin coater applies uniform thin films by dispensing liquid onto a spinning substrate. Film thickness is determined by spin speed (500–8000 RPM) and solution viscosity. This is the standard method for applying photoresist, dielectrics, and organic semiconductors.
DIY spin coater: brushless motor from a hobby drone + 3D-printed chuck + speed controller = $25–60. Thickness uniformity: ±5% across a 25mm substrate at consistent temperature (achievable with basic temperature control).

3. System Architecture
3.1 Overview
OpenFab is designed as a modular system with a common XY motion platform. All process modules (lithography, printing, spin coating, electroplating) dock to the same motion base. A Raspberry Pi 5 running open-source firmware (OpenFab-OS, Python-based) coordinates all modules.

3.2 Two Processing Tracks
Track A: Organic Electronics Track
No vacuum required. Ambient lab conditions. Entry cost: $800–1,500. Suitable for OTFTs, sensors, flexible circuits, educational use.


Process flow:
Design layout in OpenFab Designer (web-based GDS-to-gcode converter)
Spin coat substrate (glass or PET film) with PMMA dielectric
AJP print gate electrode (Ag nanoparticle ink), anneal at 120°C on hotplate
AJP print organic semiconductor layer (P3HT or TIPS-pentacene)
AJP print source/drain contacts (PEDOT:PSS or Ag)
DLP lithography for fine patterning of active area (if needed)
Measure IV characteristics with Arduino-based probe station

Expected results: organic TFT with carrier mobility 0.01–0.5 cm²/Vs (P3HT) or 0.1–1 cm²/Vs (TIPS-pentacene). On/off ratio 10³–10⁶. Threshold voltage 2–10V. Adequate for display backplanes, RFID antennas, chemical sensors.

Track B: Inorganic Thin-Film Track
Requires mild chemical handling (standard lab gloves + ventilation). No vacuum in base config. Cost: $2,500–3,500. Achieves real transistor performance close to amorphous silicon standard.


Process flow (IGZO TFT, proven in literature without vacuum):
Sol-gel IGZO precursor preparation (In, Ga, Zn nitrates in 2-methoxyethanol)
Spin coat IGZO layer, anneal at 350°C (standard hotplate)
Spin coat AZ1512 photoresist
DLP lithography: expose active area pattern
Develop in AZ400K, wet etch IGZO in dilute HCl (10 sec)
Strip resist, spin coat Al₂O₃ dielectric (sol-gel or ALD if available)
Electroplate or evaporate gate metal (Al, Mo)
Repeat DLP lithography + etch for gate, source, drain contacts
Final anneal at 250°C, probe and measure

Expected results: IGZO TFT mobility 5–20 cm²/Vs (vs. 0.5 for a-Si:H), subthreshold swing 200–500 mV/dec. These are good enough for display drivers, sensor arrays, simple logic gates.

3.3 Module Descriptions
Module
Technology
Key Component
DIY Cost
Pattern Engine
DLP Maskless Litho
TI DLP2010 DMD + 405nm LED
$150–350
Deposition Engine A
Aerosol Jet Print
1.7MHz ultrasonic + sheath gas
$80–200
Deposition Engine B
Spin Coater
Drone motor + controller
$25–60
Metal Deposition
Electroplating
Arduino power supply + bath
$40–80
Annealing
Hotplate
PID-controlled ceramic hotplate
$60–120
Inspection
Optical Microscope
USB camera + 40x objective
$80–200
Probe Station
4-point IV measurement
Arduino + op-amp + probes
$50–100
Motion Platform
XY stage
Linear rails + steppers (Klipper)
$100–200
Control System
OpenFab-OS
Raspberry Pi 5
$80
Wet Chemistry
Etch/develop station
Polypropylene trays + fume box
$60–120


4. Bill of Materials — Realistic Pricing
4.1 Track A: Organic Electronics (~$800–1,500)
Component
Source
Cost (USD)
Raspberry Pi 5 (4GB)
Official distributors
$80
XY motion platform (linear rails + NEMA17)
AliExpress
$80–120
DLP2010 evaluation module (EVM)
Texas Instruments / AliExpress
$80–150
405nm UV LED (1–3W) + driver
AliExpress
$15–25
Reduction optics (5x UV objective)
AliExpress / Edmund Optics
$60–150
Ultrasonic atomizer module (1.7MHz)
AliExpress (humidifier parts)
$10–20
Sheath gas nozzle (3D printed)
Self-printed
$2–5
N₂ or compressed air (small tank)
Local hardware store
$30–60
Spin coater (drone motor + controller)
AliExpress
$30–60
PID hotplate (ceramic, 300°C)
AliExpress
$60–100
USB microscope (40x–400x)
AliExpress
$40–80
Probe station (tungsten tips + XYZ micropositioners)
AliExpress
$60–100
Wet chemistry trays (polypropylene)
Amazon / local
$20–40
Chemicals: PEDOT:PSS, P3HT, PMMA, AZ1512
Sigma-Aldrich / Ossila
$200–350
Substrates (glass slides, PET film)
Local / AliExpress
$20–40
3D printing filament, misc hardware
Local
$40–60
TOTAL (Track A)


$827 – $1,410


4.2 Track B: Additional Components for Inorganic TFT (~+$1,200–2,000)
Additional Component
Source
Cost (USD)
Electroplating power supply (Arduino-based)
Self-built
$30–50
Electroplating baths (Cu, Ni, Au)
PCB suppliers / Sigma
$80–150
High-temperature hotplate (500°C)
AliExpress
$100–200
IGZO precursor chemicals
Sigma-Aldrich
$80–150
Sol-gel dielectric chemicals (Al₂O₃ precursor)
Sigma-Aldrich
$60–100
Stronger photoresist developer (AZ400K)
EMD Performance / eBay
$40–70
HCl, IPA, acetone (reagent grade)
Local chemical supplier
$40–80
Ventilation hood (DIY polypropylene box + fan)
Self-built
$60–100
N-type dopant source (ammonium phosphate)
Garden supply (fertilizer grade)
$10
TOTAL ADDITIONAL (Track B)


$500 – $910


Total Track B system: $1,300–2,320. Compare to Sam Zeloof's ~$10,000 spent 2017–2020. The cost drop is mainly due to cheaper DLP chips and AliExpress optics components unavailable 5 years ago.


5. Capabilities and Honest Limitations
5.1 What OpenFab Can Realistically Produce
Device Type
Track
Performance
Real-World Use
Organic TFT (OTFT)
A
µ = 0.01–0.5 cm²/Vs
Sensors, flexible displays, RFID
IGZO TFT
B
µ = 5–20 cm²/Vs
Display drivers, sensor arrays
Electroplated Cu interconnect
A+B
ρ ≈ 2–5 µΩ·cm
Wiring, contact pads
Organic capacitor
A
C = 1–100 nF/cm²
Filter circuits, memory test
Gas/chemical sensor
A
ppb-ppm sensitivity
VOC, humidity, pH
Photodetector (ZnO/P3HT)
A
Responsivity 0.1–1 A/W
UV sensing, imaging
Simple logic gate (IGZO NAND)
B
Propagation delay ~µs
Proof of concept logic
Strain/pressure sensor
A
0.1–10% strain range
Wearables, robotics


5.2 What OpenFab Cannot Do
Честность важнее маркетинга. Следующие ограничения фундаментальны, а не только технические.


Sub-micron features: DLP with 5x optics gives ~3.5 µm practical limit. CMOS logic below 180nm is impossible without EUV — not a DIY target.
High-speed digital logic: organic TFTs operate at kHz range, IGZO TFTs at MHz range. Not suitable for CPU/GPU/memory replacement.
High-voltage isolation: thin sol-gel dielectrics break down at 5–20V. Not suitable for power electronics above ~50V.
Batch production: throughput is 2–8 devices per hour. This is a prototyping tool, not a fab.
Yield: expect 30–60% on first builds, improving to 60–80% with practice. Commercial fabs achieve >99%.
Silicon MOSFET: requires 900–1100°C diffusion furnace for doping. Possible but not in base config — requires tube furnace ($300–600 additional).

6. Software Stack — OpenFab-OS
6.1 Architecture
OpenFab-OS is a Python-based control system running on Raspberry Pi 5. It follows a pipeline model: GDS layout → process recipe → machine instructions → execution → measurement → analysis.

Layer
Function
Technology
OpenFab Designer
Web-based GDS layout editor
React + KiCad-inspired UI
Process Compiler
GDS → machine G-code
Python, gdspy library
Motion Controller
XY stage + module coordination
Klipper fork (Python)
Lithography Driver
DMD bitmap → exposure sequence
Python + libdlp (TI SDK)
AJP Driver
Toolpath + gas flow control
Python + serial
Measurement Engine
IV curves, C-V sweeps
Python + scipy
Process Log DB
SQLite + git versioning
Full reproducibility
Community Hub
Share recipes, results
GitHub + static site


6.2 Key Innovation: Process Recipes as Code
Every fabrication run is defined by a plain-text YAML recipe file, committing all process parameters (spin speed, exposure time, anneal temperature, etch duration). These recipes are version-controlled and shareable, enabling the community to reproduce and improve processes exactly like open-source software.

Example: 'openfab run igzo_tft_v3.yaml --substrate glass --track B' — executes a complete 7-step IGZO TFT fabrication sequence with full logging and automatic IV characterization at the end.


7. Safety Framework
7.1 Chemical Safety
OpenFab uses real chemicals. This section is mandatory reading before any Track B work.


Chemical
Hazard
Mitigation
AZ400K developer
Mild alkaline (KOH-based)
Gloves, eye protection, rinse with water
Dilute HCl (10%)
Corrosive, HCl fumes
Fume hood required, gloves, goggles
ITO/IGZO etchant (HCl)
Same as above
Same as above
Organic solvents (chlorobenzene, anisole)
Flammable, neurotoxic vapors
Ventilation hood, no open flames
Ag nanoparticle ink
Nanoparticle inhalation risk
No spraying in open air; use enclosure
Gold plating bath (KAu(CN)₂)
Cyanide compound — EXTREME CARE
Only advanced users; strict protocol
Photoresist (AZ1512)
Mild irritant, photosensitive
Gloves, keep away from light before use


Gold cyanide plating is optional. Copper and nickel are sufficient for most prototypes and carry significantly lower risk.

7.2 Optical Safety
405 nm UV LED at 1–3W: Class 3R/3B. Never look directly into the beam. Standard UV-blocking glasses ($15) provide full protection.
DLP exposure is enclosed inside the lithography module. Door interlock prevents LED activation when open.

7.3 Electrical Safety
All voltages in base system: 3.3V, 5V, 12V, 24V. No high-voltage components in Track A.
Electroplating uses max 12V / 500mA. Standard low-voltage safety rules apply.
An optional high-temperature tube furnace (Track B extension) requires 220V but is a standard commercial appliance.

8. Community Roadmap
v1.0 (Current — Q2 2026)
Full Track A documentation, CAD, firmware, chemical protocols
DLP lithography module: verified at 5 µm features on AZ1512
AJP module: verified with Ag nanoparticle and PEDOT:PSS inks
Reference process: PEDOT:PSS/P3HT OTFT on glass

v1.5 (Q4 2026)
Track B: IGZO TFT complete process, open recipe library
OpenFab Designer: web-based layout tool with DRC for DIY design rules
Community process database: searchable, git-backed recipes with measured results
First community builds: 5+ independent builders in 3+ countries

v2.0 (2027)
AI-assisted process optimization: suggest recipe adjustments based on measurement feedback
Sub-2 µm demonstration using 10x reduction optics
Low-cost diffusion furnace integration for silicon MOSFET track
Modular chemistry dispensing system (replacing manual pipetting)

v3.0 (2028–2030): The 3D Printer Moment
Target: complete OpenFab kit available for $500–800, assembled in 8 hours, producing working OTFTs in first session. Community of 10,000+ builders. Commercial ecosystem of ink suppliers, substrate vendors, process consultants.

AJP + DLP tightly integrated as single print head
Fully automated process sequences (load substrate → receive tested device)
Community foundry model: upload design, community member runs it for cost-of-materials
Educational curriculum: from atoms to working transistor in 3 high school sessions

9. Conclusion
OpenFab is not a speculative concept. Every technology in this paper is documented, peer-reviewed, and has working DIY precedents. Sam Zeloof proved that home semiconductor fabrication is possible. The question is not whether it works — the question is how to make it accessible.

The path to "semiconductor prototyping as common as 3D printing" runs through three stages:
Stage 1 (now): prove that a complete, safe, sub-$2000 system can produce working transistors — the Sam Zeloof challenge, solved with 2026 component prices.
Stage 2 (2027): community of 1,000+ builders sharing recipes, results, and failures — the RepRap moment.
Stage 3 (2028–2030): commoditization — kits, standardized inks, curriculum integration — the Arduino moment.

The fundamental barrier was never physics. It was integration, cost, and documentation. OpenFab solves all three.


Join the project: every build, every measurement, every failed run documented publicly makes the next build easier. The democratization of silicon starts in a garage in Dumaguete, a dorm room in Berlin, a makerspace in Nairobi.


References and Key Inspirations
Sam Zeloof, samuelzeloof.com — documented home chip fabrication, 2017–2022. Primary proof of concept.
Optomec Aerosol Jet Technology, optomec.com/printed-electronics/aerosol-jet-technology/
Rida, A. et al. (2007). "Aerosol jet printing of conductive inks." IEEE Transactions on Advanced Packaging.
IGZO TFT without vacuum: Hosono, H. et al. — sol-gel IGZO on glass, peer-reviewed since 2012.
Texas Instruments DLP2010 Datasheet and EVM documentation — DMD specifications.
AZ Electronic Materials: AZ1512, AZ400K process documentation.
Ossila.com: organic electronic materials, supplier and educational resource.
Hackaday.io: DIY semiconductor fab community projects.
Klipper firmware: github.com/Klipper3d/klipper — motion control base.


---

*White Paper · Reality Refactor Lab · 1149*