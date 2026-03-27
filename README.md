# 🛡️ OWASP Juice Shop: Web Application Security Assessment

![Security Assessment](https://img.shields.io/badge/Assessment-Web%20Application-3776AB?style=for-the-badge)
![Methodology](https://img.shields.io/badge/Methodology-OWASP%20WSTG-FF6633?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active%20Engagement-success?style=for-the-badge)

## 📌 Executive Summary
This repository serves as the official documentation for a comprehensive, gray-box penetration test conducted against the OWASP Juice Shop web application. The objective of this assessment is to identify, exploit, and provide remediation strategies for critical vulnerabilities affecting the confidentiality, integrity, and availability of the application.

## 🎯 Scope of Work & Rules of Engagement
* **Target Environment:** Local Docker Container (Isolated Infrastructure)
* **Application Version:** OWASP Juice Shop v14.5.1
* **Testing Methodology:** OWASP Web Security Testing Guide (WSTG) & PTES
* **Authorized Activity:** Vulnerability discovery, automated/manual exploitation, and data exfiltration within the isolated lab environment.
* **Out of Scope:** Denial of Service (DoS) attacks against the host machine.

## 🗂️ Engagement Directory
1. `/01-Reconnaissance`: Infrastructure mapping, endpoint discovery, and traffic analysis.
2. `/02-Vulnerability-Analysis`: Identification of attack vectors (SQLi, XSS, etc.).
3. `/03-Exploitation-PoC`: Weaponized payloads, custom Python tooling, and proof-of-concept exfiltration.
4. `/04-Reporting-and-Remediation`: CVSS v3.1 scoring, business impact analysis, and secure coding guidelines.

---
*Disclaimer: All activities documented in this repository were conducted in a legally authorized, locally hosted lab environment for educational and professional development purposes. Do not utilize these tools or methodologies against targets without explicit, written mutual consent.*
