# Cryptographic Design

## Overview

This document explains the cryptographic design of VaultLink.

The system uses a **hybrid approach**:

* Symmetric encryption for data
* Password-based key derivation
* (Planned) Post-Quantum Cryptography for key exchange

---

## Design Goals

* Protect sensitive data at rest
* Avoid storing plaintext secrets
* Resist brute-force attacks
* Enable future PQC integration

---

## 1. Symmetric Encryption

### Algorithm

* AES-256-GCM

### Reason

* Strong industry standard
* Provides confidentiality + integrity (AEAD)
* Efficient for local storage

---

## 2. Key Derivation

### Algorithm

* PBKDF2 (Rfc2898DeriveBytes)

### Inputs

* Master password
* Random salt

### Reason

* Slows down brute-force attacks
* Widely supported in .NET

---

## 3. Vault Key Structure

```text
Master Password
      ↓
PBKDF2
      ↓
Vault Encryption Key
      ↓
AES Encryption
      ↓
Encrypted Vault Data
```

---

## 4. Randomness

* Secure random generator used
* Salt and IV are randomly generated

---

## 5. Initialization Vector (IV)

* Unique IV per encryption
* Stored alongside ciphertext

---

## 6. Integrity Protection

* AES-GCM provides built-in authentication
* (Planned) additional validation layer if needed

---

## 7. Post-Quantum Cryptography (Planned)

### Algorithm

* ML-KEM (Kyber)

### Usage

* Key encapsulation
* Secure key exchange (Windows ↔ Android)
* Secure vault key export

### Reason

* Future-proof security
* Demonstrates modern cryptography understanding

---

## 8. Why Not Use PQC for Everything?

* PQC is not optimized for bulk data encryption
* AES is faster and more practical
* Hybrid approach is industry standard

---

## Security Considerations

* Master password is never stored
* Keys are derived, not stored directly
* All sensitive data is encrypted before storage

---

## Summary

VaultLink uses:

* AES-256-GCM → data encryption
* PBKDF2 → key derivation
* PQC (planned) → key exchange

This ensures a balance between:

* Security
* Performance
* Practical implementation
