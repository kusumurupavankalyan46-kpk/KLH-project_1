# SentinelX AI-SOC
## Enterprise-Grade AI-Powered Security Operations Platform

[![Python](https://img.shields.io/badge/Python-3.12-blue.svg)](https://python.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.110+-green.svg)](https://fastapi.tiangolo.com)
[![React](https://img.shields.io/badge/React-19+-61DAFB.svg)](https://react.dev)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0+-blue.svg)](https://www.typescriptlang.org)
[![Tests](https://img.shields.io/badge/Tests-8%20Passed%20(100%25)-success.svg)](backend/tests)

---

## 1. Project Overview & Mission

**SentinelX AI-SOC** is a professional, modular Security Operations Center platform that merges eight defensive security specializations into a unified analyst command center. Every security module shares one canonical event schema, one correlation engine, one incident database, and one evidence-handling workflow.

### The Eight Security Modules
1. **Module 1 — SOC Monitoring & SIEM**: High-volume log ingestion from Wazuh and Linux systems, normalized event schema, real-time WebSocket alert delivery, and raw log payload inspection.
2. **Module 2 — Brute-Force & Credential Attack Detection**: Sliding-window authentication failure clustering, password-spray identification, and post-failure logon progression tracking.
3. **Module 3 — Network Intrusion Detection (Suricata IDS)**: Checkpointed Suricata EVE JSON parser, signature classification, C2 beacon correlation, and raw PCAP reference tracking.
4. **Module 4 — Threat Intelligence & IOC Enrichment**: Multi-provider enrichment (VirusTotal, AbuseIPDB, AlienVault OTX) with confidence scoring, freshness indicators, and local caching.
5. **Module 5 — Digital Forensics & Incident Response (DFIR)**: SHA-256 intake cryptographic hashing, automated tamper detection, unbroken chain-of-custody tracking, and chronological forensic timeline synthesis.
6. **Module 6 — Endpoint Threat Hunting**: Sysmon process telemetry querying, Sigma-compatible rule logic, MITRE ATT&CK technique mapping, and 1-click finding promotion to SOC alerts.
7. **Module 7 — Phishing Email Analysis Lab**: Safe MIME parsing of `.eml` files, SPF/DKIM/DMARC verification, sender vs reply-to mismatch detection, safe URL defanging, and attachment cryptographic hashing.
8. **Module 8 — SOAR & Playbook Automation**: Predefined response catalog, dual-control senior approval gating for high-impact containment, safe lab simulation mode, and immutable audit logs.

---

## 2. Technology Stack

- **Backend**: Python 3.12, FastAPI, Pydantic v2, SQLAlchemy 2.0, SQLite (local default) / PostgreSQL, PyJWT, Native Bcrypt, WebSockets.
- **Frontend**: React 19, TypeScript, Vite, Vanilla Cyber SOC CSS Design System, Lucide Icons, Recharts.
- **Integrations**: Wazuh EDR/SIEM, Suricata IDS, Sysmon, VirusTotal, AbuseIPDB, AlienVault OTX.
- **Testing**: Pytest, Pytest-Asyncio, HTTPX TestClient.

---

## 3. Quick Start (Local Deployment)

### Prerequisites
- Python 3.11+
- Node.js 18+ (tested on Node.js 26)
- Git

### 1. Clone & Set Up Backend
```powershell
# Navigate to project
cd "c:\Users\scs64\OneDrive\Documents\SENTINELX AI-SOC"

# Activate Python virtual environment
.\.venv\Scripts\Activate.ps1

# Install backend dependencies
pip install -r backend/requirements.txt

# Run the backend server
python backend/run.py
```
*Backend runs on http://127.0.0.1:8000 with interactive docs at http://127.0.0.1:8000/docs.*

### 2. Set Up Frontend
```powershell
# In a new terminal
cd frontend

# Install frontend dependencies
npm install

# Start Vite development server
npm run dev
```
*Frontend runs on http://localhost:5173/.*

---

## 4. Default Credentials & Personas

SentinelX implements server-side Role-Based Access Control (RBAC). You can switch between personas directly using the persona dropdown in the top header:

| Persona | Email | Role | Privileges |
|---|---|---|---|
| **Super Administrator** | `admin@sentinelx.io` | `admin` | Full system control, rule editing, containment approval |
| **Sarah Chen** | `senior.analyst@sentinelx.io` | `senior_analyst` | Triage alerts, approve SOAR playbooks, promote hunts |
| **Alex Mercer** | `analyst@sentinelx.io` | `soc_analyst` | Alert triage, simulate playbooks, investigation notes |
| **Maya Lin** | `hunter@sentinelx.io` | `threat_hunter` | Telemetry queries, Sigma hunts, IOC discovery |
| **David Ross** | `auditor@sentinelx.io` | `auditor` | Read-only compliance audit logging & evidence inspection |
| **Guest Observer** | `viewer@sentinelx.io` | `viewer` | Read-only dashboard metric observation |

*Default password for all demo accounts:* `SentinelX@2026`

---

## 5. Automated Verification Results

All automated backend and frontend build checks have been executed:

```
============================= test session starts =============================
platform win32 -- Python 3.12.10, pytest-9.1.1, pluggy-1.7.0
rootdir: C:\Users\scs64\OneDrive\Documents\SENTINELX AI-SOC
configfile: pytest.ini
collected 8 items

backend/tests/test_backend.py::test_auth_login_and_me PASSED             [ 12%]
backend/tests/test_backend.py::test_dashboard_stats PASSED               [ 25%]
backend/tests/test_backend.py::test_brute_force_detection_logic PASSED   [ 37%]
backend/tests/test_backend.py::test_evidence_integrity_and_tampering PASSED [ 50%]
backend/tests/test_backend.py::test_phishing_email_parsing PASSED        [ 62%]
backend/tests/test_backend.py::test_soar_playbook_approval_workflow PASSED [ 75%]
backend/tests/test_backend.py::test_threat_intel_enrichment PASSED       [ 87%]
backend/tests/test_backend.py::test_risk_score_calculation PASSED        [100%]

======================== 8 passed, 1 warning in 6.58s =========================
```

Frontend production bundle verification:
```
✓ 1959 modules transformed.
dist/index.html                   0.96 kB │ gzip:   0.61 kB
dist/assets/index-MBXuSzJA.css    6.78 kB │ gzip:   2.05 kB
dist/assets/index-4l9El05S.js   411.14 kB │ gzip: 112.57 kB
✓ built in 3.90s
```

---

## 6. End-to-End Walkthrough Scenario

To demonstrate the full incident response lifecycle:
1. **Visit Landing Page** (`http://localhost:5173/`): Review the architectural blueprint, 8 modules, and 11-stage pipeline.
2. **Open SOC Console** (`http://localhost:5173/dashboard`): Observe real-time KPIs, active triage queue, and connector statuses.
3. **Simulate Live Attack**: Click the **Inject Attack Demo** button in the header. Five rapid SSH failed login events are ingested, processed through sliding window rule `AUTH-001`, and broadcast across WebSockets without refreshing the page.
4. **Investigate Multi-Stage Compromise**: Navigate to **Incident Cases** (`/incidents`) and select `INC-2026-0001`. Examine how phishing (`PHISH-2026-0001`), endpoint process execution (`PROC-001`), and network C2 beaconing (`NET-001`) correlate into a single high-risk case.
5. **Verify Evidence Integrity**: Navigate to **Module 5: Digital Forensics** (`/modules/forensics`). Click **Verify** to confirm the SHA-256 baseline, then click **Simulate Tamper** to watch the cryptographic tamper violation trigger in real-time.
6. **Generate Forensic Report**: Return to Incident `INC-2026-0001` and click **Generate Forensic Report (.md)** to view or export a Markdown investigation report complete with hashes and chain of custody.

---

## 7. Safety Principles & Limitations

- **Simulation Mode**: Version 1 containment actions (endpoint isolation, firewall blocking) execute in safe simulation mode to prevent unintended production disruption.
- **AI Copilot Guardrails**: The AI assistant strictly observes verified database evidence IDs, operates read-only, and cannot execute shell commands or autonomous containment actions.
- **External Feeds**: If third-party API keys are not supplied in `.env`, SentinelX returns clearly labeled curated benchmark indicators rather than fabricating responses.
