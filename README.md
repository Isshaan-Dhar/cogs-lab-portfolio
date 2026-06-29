# COGS Tech Support Lab Portfolio
**Engineer:** Ishaan Dhar

## 📖 Overview
This repository contains the practical implementations, configurations, and documentation for the InstaSafe Technologies COGS Cloud Lab Guide. It serves as a comprehensive record of 12 hands-on infrastructure, identity, and observability experiments across 5 modules, culminating in a functional mini-Zero Trust Network Access (ZTNA) architecture.

## 🛠️ Technology Stack
* **Cloud Infrastructure:** OCI Always Free, AWS Free Tier, DigitalOcean
* **Networking & Web:** Nginx, WireGuard, curl, OpenSSL, TCPDump
* **Identity & Authentication:** OpenLDAP, Keycloak, Python TOTP (pyotp)
* **Monitoring & APM:** Uptime Kuma, Prometheus, Grafana
* **Operations & Version Control:** Git, GitHub Issues, Markdown

---

## 🚀 Engineering Milestones

### Module 1: Cloud & Networking Fundamentals
Deployed and secured core networking infrastructure to understand point-to-point connections and traffic encryption.
* **Lab 1.1 - Cloud Server & Toolkit:** Provisioned cloud VMs and utilized core diagnostic tools (traceroute, dnsutils, nmap, openssl) to troubleshoot connectivity and DNS resolution.
* **Lab 1.2 - Web Server & TLS:** Configured Nginx with self-signed TLS certificates, managing UFW firewall rules and analyzing HTTPS handshakes.
* **Lab 1.3 - WireGuard VPN:** Built an encrypted point-to-point VPN tunnel between two cloud VMs, verified via packet capture (tcpdump).

### Module 2: Identity & Authentication
Configured open-source Identity Providers (IdP) and authentication protocols used in enterprise SSO and MFA environments.
* **Lab 2.1 - OpenLDAP Directory:** Deployed OpenLDAP, created LDIF records, and executed bind tests to simulate Active Directory sync behaviors.
* **Lab 2.2 - Keycloak SSO (SAML):** Deployed Keycloak via Docker, established a realm, and configured a SAML client with attribute mappers to trace full SAML login flows.
* **Lab 2.3 - TOTP MFA:** Engineered a Python-based Time-based One-Time Password (TOTP) generator and verification script, confirming RFC 6238 standardization via Google Authenticator.

### Module 3: Monitoring & Observability
Instrumented application performance monitoring (APM) and alerting systems to visualize infrastructure health.
* **Lab 3.1 - Uptime Kuma:** Configured active monitoring (HTTP, TCP, Ping) and simulated service failures to trigger and track incident alerts.
* **Lab 3.2 - Prometheus & Grafana:** Deployed a monitoring stack via Docker Compose, utilizing PromQL to query CPU/Memory/Network metrics and visualize them in a Grafana dashboard.

### Module 4: Support Operations
Standardized incident documentation and ticket lifecycle management.
* **Lab 4.1 - Ticket Lifecycle:** Managed P1-P4 incidents through a GitHub Project board, executing escalation and resolution workflows.
* **Lab 4.2 - PACE & PIR:** Authored PACE shift handovers and detailed Post-Incident Reports (PIR) in Markdown, using Git commits for immutable timestamping.

### Module 5: Incident Response & Change Management
Simulated live-environment pressure tests and controlled configuration deployments.
* **Lab 5.1 - P1 Simulation:** Executed a full P1 response drill (detection, acknowledgement, investigation, resolution, PIR) within a strict 45-minute window following an induced Nginx crash.
* **Lab 5.2 - Change Management:** Authored and executed a Normal Change plan to upgrade Nginx from TLS 1.2 to TLS 1.3, successfully demonstrating a planned rollback procedure.

### 💎 Capstone: Mini-ZTNA Architecture
Integrated all prior modules into a unified, simplified Zero Trust architecture.
* **Architecture:** Routed a client laptop through a WireGuard tunnel into an Nginx reverse proxy, serving an application strictly gated by Keycloak SAML authentication, with the entire stack monitored by Uptime Kuma and Prometheus.

---

## 📂 Repository Structure

```text
cogs-lab-portfolio/
├── README.md
├── module-1-networking/
│   ├── lab1-1-findings.md
│   ├── lab1-2-findings.md
│   └── lab1-3-findings.md
├── module-2-identity/
│   ├── lab2-1-findings.md
│   ├── lab2-2-findings.md
│   └── lab2-3-findings.md
├── module-3-monitoring/
│   ├── lab3-1-findings.md
│   └── lab3-2-findings.md
├── module-4-operations/
│   ├── handovers/
│   │   └── handover-2026-04-08-1800.md
│   └── pirs/
│       └── PIR-2026-04-08-MFA-Bulk-Failure.md
├── module-5-incident/
│   ├── lab5-1-findings.md
│   ├── lab5-2-findings.md
│   ├── changes/
│   │   └── CHANGE-001-TLS-Upgrade.md
│   └── pirs/
│       └── PIR-2026-06-01-Nginx-Crash.md
├── capstone/
│   └── lab-capstone-architecture.md
└── screenshots/
