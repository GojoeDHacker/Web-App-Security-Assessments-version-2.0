# 🛡️ OWASP Juice Shop: Advanced Security Assessment (V2.0)

![Security Assessment](https://img.shields.io/badge/Assessment-Web%20Application-3776AB?style=for-the-badge)
![Methodology](https://img.shields.io/badge/Methodology-OWASP%20WSTG-FF6633?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)

## 📌 Executive Summary
This repository contains the official documentation, proof-of-concept exploits, and custom tooling developed during a comprehensive, gray-box penetration test of the OWASP Juice Shop web application. 

**Version 2.0** of this assessment represents an advanced evolution in methodology, moving away from basic manual testing to focus on automated data exfiltration, protocol-level WAF evasion, OSINT-driven cryptography breaks, and custom exploit development.

## ⚔️ Key Attack Vectors & Findings

### 1. Reconnaissance & Information Disclosure (Phase 1)
* **Action:** Aggressive directory enumeration using `gobuster` while filtering out SPA routing noise (`--exclude-length`).
* **Result:** Discovered an unauthenticated, publicly exposed `/ftp` directory hidden via `robots.txt` ("Security Through Obscurity").
* **Impact:** Exfiltrated a highly sensitive KeePass password database (`incident-support.kdbx`).

### 2. Cryptographic Break & Account Takeover (Phase 2A)
* **Action:** Extracted the KeePass database hash (`keepass2john`). When standard dictionaries (`rockyou.txt`) failed, a targeted OSINT dictionary was dynamically generated using Bash brace expansion based on corporate password patterns.
* **Result:** Instantly cracked the AES-256 encryption (`Support2022!`).
* **Impact:** Achieved complete Account Takeover (ATO) of the IT Support Team's internal credentials for DEV, INT, and PROD environments.

### 3. Advanced SQL Injection & Data Exfiltration (Phase 2B)
* **Action:** Bypassed backend API logic gates using custom injection boundaries (`')) -- `). Defeated `500 Internal Server Error` crashes by forcing the database to encode output into hexadecimal (`--hex`) and dropping strict type-casting (`--no-cast`).
* **Result:** Successfully exfiltrated the entire `Users` table, including Administrator hashes.
* **Impact:** Gained the ability to manipulate the database and execute an Authentication Bypass (`admin@juice-sh.op'-- `) to achieve Master Administrator privileges.

### 4. Stored XSS & WAF Evasion (Phase 2C)
* **Action:** Engineered HTML polyglots (e.g., broken image handlers `<img src="x" onerror="...">`) to bypass frontend input sanitization and simulated Web Application Firewalls.
* **Result:** Permanently stored malicious JavaScript within the Customer Feedback database.
* **Impact:** Triggered a reliable, zero-click execution of the payload within the trusted session of the Administrator's dashboard, allowing for session hijacking.

## 🛠️ Custom Tooling
To streamline the evasion process, a custom Python tool was developed to automatically wrap raw JavaScript payloads into various WAF-evading HTML polyglots.
* **Script:** `polyglot_generator.py` (Located in `/03-Exploitation-PoC/scripts/`)
* **Capabilities:** Generates Image, SVG, Iframe, Body, and Link-based evasion vectors dynamically.

## 🔐 Remediation Strategies
Detailed remediation guidelines for developers, including the implementation of Parameterized Queries (for SQLi) and Context-Aware Output Encoding (for XSS), can be found in the respective vulnerability reports within this repository.

---
*Disclaimer: All activities documented in this repository were conducted in a legally authorized, locally hosted lab environment. Do not utilize these tools or methodologies against targets without explicit, written mutual consent.*
