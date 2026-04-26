# Architecture Design

## Overview

VaultLink is a **local-first password manager** designed with a modular architecture.

The system is composed of:

* Windows Desktop Application (MVP)
* Android Companion App (Planned)

---

## High-Level Architecture

```text
User
  │
  ▼
[ UI Layer ]
  │
  ▼
[ Application Layer ]
  │
  ▼
[ Security Layer (Crypto) ]
  │
  ▼
[ Storage Layer ]
```

---

## Layer Description

### 1. UI Layer

Responsible for user interaction.

* Login screen (Master password)
* Vault dashboard
* Credential management UI
* Settings

---

### 2. Application Layer

Handles business logic.

* Credential CRUD
* Vault state management
* Auto-lock logic
* Clipboard handling
* Password generation

---

### 3. Security Layer (Crypto)

Handles all cryptographic operations.

* Key derivation (PBKDF2)
* Encryption / Decryption (AES-256-GCM)
* Secure random generation
* (Planned) PQC key encapsulation

---

### 4. Storage Layer

Responsible for data persistence.

* Encrypted vault storage
* Local file (JSON / SQLite)
* Future: secure export/import

---

## Data Flow

### Login Flow

```text
User Input Password
        ↓
PBKDF2 Key Derivation
        ↓
Attempt Decrypt Vault
        ↓
Success → Unlock Vault
Fail → Reject Access
```

---

### Save Credential Flow

```text
User Input Data
        ↓
Serialize Data
        ↓
Encrypt (AES)
        ↓
Write to Storage
```

---

## Future Architecture (Android Integration)

```text
Windows App
   │
   │ (Local Network / Secure Channel)
   ▼
Android App
   │
   ▼
User Approval (2FA)
```

* QR-based pairing
* Device authentication
* PQC-based key exchange

---

## Design Principles

* Separation of concerns
* Security-first design
* Local-first architecture
* Extensibility for mobile integration
* Minimal trust assumptions

---

## Summary

The architecture is designed to ensure:

* Clear separation between UI, logic, security, and storage
* Strong cryptographic boundaries
* Easy extension for Android and PQC integration
