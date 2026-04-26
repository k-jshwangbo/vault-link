# Threat Model

## Overview

This document defines the security threats considered in VaultLink and how the system mitigates them.

---

## Assets to Protect

* User credentials (ID / Password)
* Vault encryption key
* Master password
* Encrypted vault file

---

## Threat Actors

* Local attacker (file access)
* Insider with system access
* Offline attacker (stolen storage)
* Curious user / misuse

---

## Threats and Mitigations

### 1. Vault File Theft

**Threat**
Attacker obtains the vault file from disk.

**Mitigation**

* AES-256 encryption
* Strong key derived via PBKDF2
* No plaintext storage

---

### 2. Brute-force Attack

**Threat**
Attacker attempts to guess master password.

**Mitigation**

* PBKDF2 with high iteration count
* Salt usage
* (Planned) login delay

---

### 3. Clipboard Leakage

**Threat**
Password copied to clipboard is exposed.

**Mitigation**

* Clipboard auto-clear after timeout

---

### 4. Unauthorized Access (Idle Session)

**Threat**
User leaves vault open.

**Mitigation**

* Auto-lock after inactivity

---

### 5. Data Tampering

**Threat**
Vault file modified by attacker.

**Mitigation**

* (Planned) integrity verification (HMAC or AEAD)

---

### 6. Device Impersonation (Future)

**Threat**
Fake Android device attempts authentication.

**Mitigation**

* Device pairing
* Public/private key validation
* PQC-based key exchange (planned)

---

## Out of Scope

* Malware / keylogger attacks
* Memory dumping attacks
* Kernel-level attacks
* Physical attacks on hardware

---

## Assumptions

* OS provides basic isolation
* User environment is not fully compromised
* Cryptographic libraries are trusted

---

## Summary

VaultLink focuses on protecting:

* Data at rest
* Authentication integrity
* Basic operational security

Advanced threats (e.g., malware) are out of scope for MVP.
