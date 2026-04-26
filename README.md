# vault-link

> Local-first password manager with Windows (C#) and Android (Java) integration, featuring post-quantum cryptography concepts

---

## Overview

`vault-link` is a **secure password manager** designed with a **local-first architecture**.

The project consists of:

* A **Windows desktop application** (C# .NET Framework)
* A **planned Android companion app** (Java)

It focuses on implementing **practical security mechanisms**, including:

* Strong encryption
* Secure key management
* Device-based authentication (planned)
* Post-quantum cryptography (PQC) concepts

---

## Goals

* Build a secure and usable password manager
* Apply real-world cryptographic design patterns
* Implement secure local storage architecture
* Extend to **Windows ↔ Android secure authentication**
* Explore **Post-Quantum Cryptography (PQC)** in a practical system

---

## Tech Stack

### Windows Application

* C#
* .NET Framework
* WPF or WinForms
* Local storage (JSON / SQLite)
* BouncyCastle (cryptography)

### Android Application (Planned)

* Java
* Android SDK
* BouncyCastle
* Biometric / PIN authentication
* QR-based pairing

---

## Features (MVP - Windows)

* Master password setup & authentication
* Encrypted local vault storage
* Credential management (CRUD)
* Secure password generator
* Clipboard auto-clear
* Auto-lock after inactivity
* Basic audit logging

---

## Cryptography Design

### 1. Data Encryption

* AES-256-GCM for vault encryption
* All sensitive data is encrypted before disk storage

### 2. Key Derivation

* PBKDF2 (Rfc2898DeriveBytes)
* Random salt + high iteration count
* Master password is never stored directly

### 3. Post-Quantum Cryptography (PQC)

Planned usage:

* ML-KEM (Kyber) for key encapsulation
* PQC-based key exchange (Windows ↔ Android)
* PQC-based key protection for backup/export

PQC is used for **key exchange and protection**,
not for bulk data encryption.

---

## Architecture

```text id="7m4j3s"
vault-link/
├── windows/
│   └── VaultLink/
│       ├── UI/
│       ├── Models/
│       ├── Services/
│       │   ├── Crypto/
│       │   ├── Vault/
│       │   └── Storage/
│       ├── Utils/
│       └── Program.cs
│
├── android/
│   └── VaultLinkApp/   (Planned)
│
├── docs/
│   ├── architecture.md
│   ├── threat-model.md
│   └── crypto-design.md
│
└── README.md
```

---

## Project Structure Details

### Windows App

* **UI/** → 화면 구성 (로그인, Vault, 설정)
* **Models/** → 데이터 모델 (Credential, Vault, User 등)
* **Services/**

  * Crypto → 암호화/복호화
  * Vault → 비즈니스 로직
  * Storage → 파일/DB 저장 처리
* **Utils/** → 공통 유틸

### Android App (Planned)

* QR 기반 디바이스 페어링
* 사용자 인증 (PIN / 생체 인증)
* Windows 로그인 승인 (2FA)
* PQC 기반 키 교환

---

## Security Features

### MVP

* Encrypted local vault
* Master password authentication
* Secure password generation
* Clipboard auto-clear
* Auto-lock
* Basic audit logging

### Planned

* Android companion authentication
* QR pairing
* Device-based approval
* PQC key exchange
* Vault integrity verification
* Secure export/import
* Tamper detection

---

## Threat Model

### Considered

* Local vault file theft
* Brute-force attack on master password
* Clipboard leakage
* Unauthorized access after inactivity
* Data tampering

### Out of Scope (MVP)

* Malware / keylogger attacks
* Kernel-level attacks
* Memory dumping
* Cloud sync security

---

## Roadmap

### Phase 1 - Windows MVP

* [ ] Project setup
* [ ] Master password system
* [ ] PBKDF2 key derivation
* [ ] AES-256 encryption
* [ ] Credential CRUD
* [ ] Password generator
* [ ] Clipboard auto-clear
* [ ] Auto-lock

### Phase 2 - Security Hardening

* [ ] Vault integrity validation
* [ ] Failed login delay
* [ ] Secure export/import
* [ ] Audit log viewer

### Phase 3 - Android Integration

* [ ] Android app (Java)
* [ ] QR pairing
* [ ] Device authentication
* [ ] Login approval system

### Phase 4 - PQC Integration

* [ ] ML-KEM/Kyber module
* [ ] PQC key exchange
* [ ] PQC-based key protection
* [ ] Hybrid crypto design documentation

---

## Development Environment

* OS: Windows 11
* Windows App: C# (.NET Framework)
* Android App: Java
* IDE:

  * Visual Studio
  * Android Studio

---

## Motivation

This project is based on experience in:

* Android application development
* Smart factory systems
* Set-top box / AVN environments
* Secure key handling (DRM, key provisioning)
* Windows desktop application development

The goal is to build a **practical security-focused application**
that demonstrates both **development capability and security understanding**.

---

## License

MIT License
