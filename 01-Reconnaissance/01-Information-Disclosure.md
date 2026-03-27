# 01 - Reconnaissance & Information Disclosure

## 1. Objective
To systematically map the application's attack surface, identify hidden endpoints, and discover sensitive information exposed through misconfigurations.

## 2. Methodology: Directory Brute-Forcing
Aggressive directory enumeration was conducted using `gobuster`. To bypass the application's Single Page Application (SPA) wildcard routing (which returned false 200 OK responses for non-existent pages), the scan was filtered to exclude the default Angular response length (`--exclude-length 75002`).

**Execution:**
`gobuster dir -u http://localhost:3000 -w /usr/share/wordlists/dirb/common.txt --exclude-length 75002`

## 3. Critical Findings

### Finding A: Security Through Obscurity (`/robots.txt`)
* **Endpoint:** `http://localhost:3000/robots.txt`
* **Description:** The application utilizes `robots.txt` to instruct web crawlers to ignore a specific directory (`Disallow: /ftp`). This inadvertently reveals the location of a hidden, sensitive endpoint to attackers.

### Finding B: Unauthenticated Directory Listing (`/ftp`)
* **Endpoint:** `http://localhost:3000/ftp`
* **Description:** The `/ftp` directory lacks authentication and access controls. Furthermore, the web server is misconfigured to allow open directory listing, exposing highly sensitive internal files to the public internet.

**High-Value Assets Discovered:**
1. `incident-support.kdbx`: An exposed KeePass password database.
2. `package.json.bak`: Infrastructure configuration and dependency backups.
3. `encrypt.pyc`: Compiled Python logic, indicating potential cryptographic operations.

## 4. Remediation Recommendation
* **Disable Directory Listing:** Ensure the web server (e.g., Express, Nginx) is explicitly configured to deny directory indexing.
* **Implement Access Controls:** Enforce strict authentication and authorization checks on the `/ftp` route.
* **Remove Sensitive Assets:** Never store password vaults (`.kdbx`), backup files (`.bak`), or source code in web-accessible directories.
