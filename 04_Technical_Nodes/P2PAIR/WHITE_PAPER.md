---
id: "4002"
title: "P2PAIR"
layer: "04_Technical_Nodes"
doctype: "Protocol"
status: concept
priority: high
tags: [privacy, P2P, AES-GCM, encryption, communication, sovereignty]
related: ["4003"]
is_1149: false
created: 2026-02-01
updated: 2026-03-16
author: Founder Alex
---

# P2PAIR — White Paper

> *Ultra-private peer-to-peer communication protocol using AES-GCM 256 — no servers, no logs, no intermediaries.*

---

## 1. The Problem

Every communication platform — Signal, Telegram, WhatsApp — is controlled by a company that can be compelled, hacked, or voluntarily compliant with state surveillance. Even end-to-end encryption still leaks metadata: who talked to whom, when, how often.

P2PAIR eliminates the server entirely.

---

## 2. Design Principles

1. **No central server** — peers connect directly or via relays they control
2. **No persistent identity** — each session uses ephemeral key pairs
3. **No metadata leakage** — connection patterns are obfuscated
4. **No logs** — messages exist only in the moment of transmission
5. **AES-GCM 256** — authenticated encryption for all payload

---

## 3. Protocol Flow

```
Alice generates: ephemeral keypair (secp256k1)
Bob generates:   ephemeral keypair (secp256k1)

Key exchange: Diffie-Hellman on secp256k1
Shared secret → HKDF-SHA256 → AES-GCM 256 key

Message:
  [nonce 12B] + AES-GCM-256(plaintext, key, nonce)
  → sent over WebRTC DataChannel (peer-to-peer, no server)

Session ends → both keys discarded → no recovery possible
```

---

## 4. Use Cases

- Trustnet sensitive coordination between verified community members
- City Quest Guardian emergency communications
- Secure whistleblower and journalist channels
- Any communication requiring both privacy and non-repudiation

---

## 5. Solidarity Mechanics

Privacy is a precondition for solidarity. People cannot organize freely without secure communication. P2PAIR treats privacy as infrastructure, not a premium feature.

---

*White Paper · Reality Refactor Lab · 1149*
