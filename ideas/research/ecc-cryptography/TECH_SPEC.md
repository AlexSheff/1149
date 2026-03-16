---
id: 018
title: "ECC Cryptography — Reference Notes"
category: research
status: research
priority: medium
related_1149: false
created: 2025-01-01
updated: 2026-03-14
author: Founder Alex
tags: [ECC, elliptic-curves, secp256k1, cryptography, mathematics, trustnet, bitcoin]
---

# ECC Cryptography — Reference Notes

> *Working reference for elliptic curve cryptography as used in Bitcoin, Trustnet, and City Quest identity systems.*

---

## 1. Core Concepts

### Elliptic Curve over Finite Field

```
Curve equation: y² ≡ x³ + ax + b  (mod p)

For secp256k1 (used by Bitcoin, Ethereum):
  a = 0
  b = 7
  y² ≡ x³ + 7  (mod p)

p = 2^256 - 2^32 - 977
  = 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFEFFFFFC2F
```

### Group Operations

```python
def point_add(P, Q, p):
    """Add two points on secp256k1."""
    if P is None: return Q
    if Q is None: return P
    if P[0] == Q[0] and P[1] != Q[1]: return None  # point at infinity

    if P == Q:
        # Point doubling
        lam = (3 * P[0]**2) * pow(2 * P[1], -1, p) % p
    else:
        # Point addition
        lam = (Q[1] - P[1]) * pow(Q[0] - P[0], -1, p) % p

    x = (lam**2 - P[0] - Q[0]) % p
    y = (lam * (P[0] - x) - P[1]) % p
    return (x, y)

def scalar_mult(k, P, p):
    """Multiply point P by scalar k using double-and-add."""
    result = None
    addend = P
    while k:
        if k & 1:
            result = point_add(result, addend, p)
        addend = point_add(addend, addend, p)
        k >>= 1
    return result
```

---

## 2. Key Generation

```python
import secrets

def generate_keypair():
    """Generate secp256k1 keypair."""
    n = 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFEBAAEDCE6AF48A03BBFD25E8CD0364141
    Gx = 0x79BE667EF9DCBBAC55A06295CE870B07029BFCDB2DCE28D959F2815B16F81798
    Gy = 0x483ADA7726A3C4655DA4FBFC0E1108A8FD17B448A68554199C47D08FFB10D4B8
    p  = 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFEFFFFFC2F

    G = (Gx, Gy)
    private_key = secrets.randbelow(n - 1) + 1   # k ∈ [1, n-1]
    public_key = scalar_mult(private_key, G, p)

    return private_key, public_key

def compress_public_key(pub: tuple) -> bytes:
    """Compress public key to 33 bytes."""
    prefix = b'\x02' if pub[1] % 2 == 0 else b'\x03'
    return prefix + pub[0].to_bytes(32, 'big')
```

---

## 3. Schnorr Signatures (Taproot)

```python
import hashlib

def schnorr_sign(message: bytes, private_key: int) -> bytes:
    """Simplified Schnorr signature (BIP-340 style)."""
    n = secp256k1_order
    G = secp256k1_generator

    # Deterministic nonce
    k = int.from_bytes(hashlib.sha256(
        private_key.to_bytes(32, 'big') + message
    ).digest(), 'big') % n

    R = scalar_mult(k, G)
    e = int.from_bytes(hashlib.sha256(
        R[0].to_bytes(32, 'big') + compress_public_key(scalar_mult(private_key, G)) + message
    ).digest(), 'big') % n

    s = (k + e * private_key) % n
    return R[0].to_bytes(32, 'big') + s.to_bytes(32, 'big')
```

---

## 4. Applications in This Repository

| Project | ECC Use |
|---------|---------|
| Trustnet | Trust score commitments signed with secp256k1 |
| City Quest identity | Wallet-based identity derived from HD keys |
| BTC Puzzle #66 | Discrete log problem on secp256k1 |
| Fair BEAT | Payment authorization signatures |

---

## 5. Recommended Libraries

| Language | Library | Notes |
|----------|---------|-------|
| JavaScript | `@noble/secp256k1` | Audited, no native deps, fastest pure-JS |
| Python | `coincurve` | libsecp256k1 bindings |
| Rust | `k256` | RustCrypto, constant-time |
| Solidity | Built-in `ecrecover` | Limited to ECDSA recovery |

---
*Document type: Technical Reference · Repository: 1149 // Idea Repository*
