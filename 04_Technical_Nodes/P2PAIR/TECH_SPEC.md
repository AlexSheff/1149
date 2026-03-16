---
id: "4002"
title: "P2PAIR — Technical Specification"
layer: "04_Technical_Nodes"
status: concept
version: 0.1
stack: [secp256k1, AES-GCM-256, WebRTC, HKDF-SHA256]
created: 2026-02-01
updated: 2026-03-16
author: Founder
---

# P2PAIR — Technical Specification

---

## 1. Key Exchange Implementation

```javascript
import { secp256k1 } from '@noble/secp256k1';
import { hkdf } from '@noble/hashes/hkdf';
import { sha256 } from '@noble/hashes/sha256';

async function establishSession(theirPublicKey) {
  const myPrivKey = secp256k1.utils.randomPrivateKey();
  const myPubKey  = secp256k1.getPublicKey(myPrivKey);

  // ECDH shared secret
  const sharedPoint  = secp256k1.getSharedSecret(myPrivKey, theirPublicKey);
  const sharedSecret = sharedPoint.slice(1, 33);  // x-coordinate only

  // Derive AES-GCM key via HKDF
  const aesKey = hkdf(sha256, sharedSecret, undefined, 'P2PAIR-v1', 32);

  return { aesKey, myPubKey };
}
```

---

## 2. Encryption / Decryption

```javascript
async function encrypt(plaintext, aesKey) {
  const nonce = crypto.getRandomValues(new Uint8Array(12));
  const key   = await crypto.subtle.importKey(
    'raw', aesKey, { name: 'AES-GCM' }, false, ['encrypt']);
  const ct    = await crypto.subtle.encrypt(
    { name: 'AES-GCM', iv: nonce }, key,
    new TextEncoder().encode(plaintext));
  // Prepend nonce to ciphertext
  const result = new Uint8Array(nonce.length + ct.byteLength);
  result.set(nonce, 0);
  result.set(new Uint8Array(ct), nonce.length);
  return result;
}

async function decrypt(data, aesKey) {
  const nonce = data.slice(0, 12);
  const ct    = data.slice(12);
  const key   = await crypto.subtle.importKey(
    'raw', aesKey, { name: 'AES-GCM' }, false, ['decrypt']);
  const pt    = await crypto.subtle.decrypt(
    { name: 'AES-GCM', iv: nonce }, key, ct);
  return new TextDecoder().decode(pt);
}
```

---

## 3. WebRTC Transport

```javascript
// Both peers use a signaling server only for initial handshake
// After ICE negotiation, communication is truly peer-to-peer
const pc = new RTCPeerConnection({ iceServers: [{ urls: 'stun:stun.l.google.com:19302' }] });
const dc = pc.createDataChannel('p2pair');

dc.onopen = () => {
  // Session established — signaling server no longer needed
  // Exchange public keys, derive shared AES key
};

dc.onmessage = async (e) => {
  const decrypted = await decrypt(e.data, sharedAesKey);
  handleMessage(decrypted);
};
```

---

## 4. Security Properties

| Property | Value |
|----------|-------|
| Key exchange | ECDH on secp256k1 |
| Key derivation | HKDF-SHA256 |
| Encryption | AES-GCM 256 |
| Authentication | GCM authentication tag |
| Forward secrecy | Yes — ephemeral keys per session |
| Metadata | Minimal — only ICE candidates during setup |
| Post-compromise | Sessions are isolated — key rotation ends compromise |

---

*Tech Spec · Reality Refactor Lab · 1149*

