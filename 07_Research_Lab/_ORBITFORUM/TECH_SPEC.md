---
id: "8006"
title: "🛰️ ORBITFORUM — Technical Specification"
layer: "07_Research_Lab"
status: concept
version: 0.1
updated: 2026-03-17
author: Founder Alex
---

# 🛰️ ORBITFORUM — Technical Specification

2. Technical Architecture
2.1 Space Segment (The Satellite)
Form Factor: 1.5U to 3U CubeSat (compact and cost-effective).
Onboard Computer (OBC): STM32H7 (for real-time protocol handling) + Raspberry Pi Compute Module (for forum database management).
Radio System:
UHF/VHF Transceiver (435–438 MHz Amateur Band).
Antenna: Tape-spring dipole for reliable omnidirectional transmission.


Storage: 128–512 MB Flash memory (stores forum threads, user public keys, and the "Orbit Voice" header).
Power: Body-mounted solar panels + 30–40 Wh battery (ensuring operation during orbital eclipse).
2.2 Communication Protocols
OrbitForum utilizes custom extensions over the CubeSat Space Protocol (CSP).
A. Downlink (Public Read Access)
Mode: Continuous Broadcast (Beacon).
Protocol: AX.25 with Forward Error Correction (FEC).
Data Format: MessagePack or CBOR + Gzip compression.
Packet Structure:
Priority Header: The Philippine Flag render + The "Orbit Voice" Winner (Phrase of the Day).
Static Content: The Manifesto.
Dynamic Content: Recent forum threads/posts.


Speed: 1.2–9.6 kbps (optimized for low-bandwidth receivers).
B. Uplink (Restricted Write Access)
Access Control: Whitelisted Public Keys (Ed25519).
Security: Challenge-Response authentication to prevent replay attacks.
Rate Limiting: Hardware-enforced limit (e.g., 1 message per user per 3 orbital passes).
Encryption: AES-256 or XTEA for uplink privacy.
2.3 Ground Segment
Client Application: A cross-platform app (Flutter/Electron) that tracks satellite passes, caches downloaded content (offline-first), and manages the user's wallet for voting.
Ground Stations: A decentralized network of automated stations (based on SatNOGS) that upload the winning "Orbit Voice" messages and new user keys to the satellite.

---

*Tech Spec · Reality Refactor Lab · 1149*
