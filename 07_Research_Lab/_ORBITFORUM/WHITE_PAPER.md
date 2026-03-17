---
id: "8006"
title: "🛰️ ORBITFORUM"
layer: "07_Research_Lab"
doctype: "Concept"
status: concept
priority: medium
progress: 0
tags: [space, orbit, satellite]
related: []
is_1149: false
solidarity: "1. The Crisis: The \"Dead Internet\" and Data Theft
The current internet is failing. It is saturated with bot-generated content (\"AI Slop\"), algorithmic manipulation, and synthetic noise.
Furthermor"
updated: 2026-03-17
author: Founder Alex
tagline: "The Celestial Intranet — Censorship-Resistant Communication"
---

# 🛰️ ORBITFORUM — White Paper

> *The Celestial Intranet — Censorship-Resistant Communication*

---

OrbitForum: A Decentralized Satellite-Based Forum for Global Freedom
Whitepaper Version 1.0
Date: January 2026
Authors: The OrbitForum DAO Community
https://sites.google.com/view/orbitforum/home

Abstract
OrbitForum is a groundbreaking initiative to launch a CubeSat satellite hosting an isolated, decentralized forum. The platform creates a "celestial intranet," enabling global citizens to access a read-only broadcast of discussions independent of terrestrial internet infrastructure. While read access is universal, write access is secured via cryptographic subscription.
A core innovation of OrbitForum is the "Orbit Voice" mechanism—a Web3-based social consensus system where the community collectively votes (using ETH or governance tokens) to select the "Phrase of the Day." This winning message is broadcasted via the satellite’s beacon, serving as a global, uncensorable status update. Symbolizing freedom with the Philippine flag and a Manifesto for World Citizens, OrbitForum leverages space technology to ensure the continuity of free speech.

1. Introduction
In an era of increasing digital surveillance, internet blackouts, and centralized algorithmic control, OrbitForum emerges as a beacon of resilience. Launched under Philippine jurisdiction, this CubeSat-based platform represents the spirit of independence.
1.1 The Problem
Fragile Infrastructure: Terrestrial internet is vulnerable to government-mandated shutdowns and physical cable severing.
Centralized Control: Social media giants control visibility through opaque algorithms.
Lack of Global Consensus: There is no neutral, borderless medium where humanity can collectively highlight a single, unified message.
1.2 The Solution: OrbitForum
We are building a standalone server in Low Earth Orbit (LEO).
Uncensorable: The satellite broadcasts to anyone within its footprint (approx. 5,000 km radius moving globally).
Symbolic: The broadcast header features the Philippine Flag and the Manifesto for World Citizens.
Democratic: The content of the main broadcast loop is determined by blockchain voting, not by a corporate admin.
1.3 Manifesto for World Citizens
"We, the citizens of the world, united in our pursuit of knowledge and expression, declare this satellite a symbol of unyielding freedom. Under the banner of the Philippine flag—a testament to resilience and sovereignty—we build a forum beyond borders. Here, ideas flow freely, guarded by technology and community, immune to earthly constraints. Let this be our shared space for dialogue, innovation, and unity."

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

3. Economic Model & "Orbit Voice"
OrbitForum introduces a Social Consensus Economy. Instead of a traditional ad auction, we use a "Token Curated Registry" approach to determine what the world sees.
3.1 The "Orbit Voice" Mechanism
The most prominent space on the satellite's broadcast (The Header) is reserved for one message chosen by the community.
Proposal Phase:
Any user can submit a phrase (max 140 chars) via a Web3 DApp.
A small anti-spam fee (collateral) is required.


Voting Window (24 Hours):
The community votes on proposals using ETH or the Orbit Governance Token.
Weighted Voting: The winner is not necessarily the user with the most money, but the message with the highest cumulative support from the community. (e.g., 100 people voting $1 beats one person bidding $90).


Execution (The Oracle):
The smart contract finalizes the winner at 00:00 UTC.
The Ground Station "Oracle" fetches the text, signs it with the Admin Key, and uploads it to the satellite.


Broadcast:
The satellite updates its header. For the next 24 hours, every signal packet begins with this phrase.


3.2 Tokenomics & Revenue Allocation
Funds generated from "Orbit Voice" voting and Write-Key sales are distributed via Smart Contract:
60% — DAO Treasury: Funds satellite maintenance, ground station costs, and future launches (OrbitForum V2).
30% — Community Rewards: Distributed back to the author of the winning phrase (Proof-of-Quality) or active voters.
10% — Operational Gas: Covers blockchain transaction fees and server costs.
3.3 Monetization of Standard Access
Write Access Keys: Sold as NFTs or License Keys (
        20–20–20–
     
 100 lifetime access).
Allows posting in standard forum threads (tech, philosophy, general chat) stored in the satellite's database, separate from the high-priority "Orbit Voice" header.

4. Governance (DAO)
To ensure longevity and legal safety, OrbitForum is community-owned.
Legal Structure: Initially registered as a Cooperative in the Philippines (compliance with PhilSA), transitioning into a fully autonomous DAO.
Decision Making: Token holders vote on:
Protocol upgrades (e.g., changing bandwidth allocation).
Content Moderation Policy (defining "illegal content" to protect the license).
Treasury Management.


Moderation: Automated filters block hash-verified illegal content. Disputes are resolved via a decentralized community court (Kleros-style).

---

*White Paper · Reality Refactor Lab · 1149*
