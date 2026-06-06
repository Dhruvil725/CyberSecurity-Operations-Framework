# Playbook: Ransomware (Master)

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Ransomware (Master) |
| Document ID | IR-PB-RAN-001 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | IR Team Lead / SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 ransomware incident |

---

## 2. Purpose

This playbook provides the authoritative, end-to-end procedure for handling ransomware incidents across Enterprise and MSSP environments.

It standardizes:
- detection and triage
- escalation and communications
- containment, eradication, and recovery
- evidence preservation and chain-of-custody
- decision points and approvals
- post-incident reporting and improvement actions

This master playbook is supported by role-specific procedures:
- L1 triage
- L2 investigation
- L3 forensics
- containment
- eradication
- recovery
- MITRE mapping and threat intel integration

---

## 3. Scope

Applies to:
- endpoints, servers, and virtual machines
- on-prem, hybrid, and cloud-hosted workloads
- corporate and MSSP-managed client environments
- ransomware and ransomware-precursor activity (pre-encryption stage)

Out of scope unless explicitly contracted or approved:
- ransom payment negotiation
- insurance claim management
- law enforcement engagement (owned by Legal/Management)
- public communications (owned by Legal/PR)

---

## 4. Definitions

| Term | Definition |
|------|------------|
| Ransomware | Malware that encrypts data or disrupts access, demanding payment for restoration |
| Double extortion | Ransomware operation where data is exfiltrated before encryption |
| P1 | Critical severity incident (see severity matrix) |
| Patient Zero | The first identified infected system in the incident timeline |
| Initial Access Vector | The first confirmed entry point (phishing, VPN compromise, exploit, etc.) |
| Containment | Actions to stop spread and ongoing harm |
| Eradication | Removal of malware and attacker persistence |
| Recovery | Restore systems and services from known-good state |

---

## 5. Severity Guidance (Ransomware)

Default classification:
- Active encryption, ransom note, or backup destruction behavior: P1
- Ransomware precursor toolchain detected (post-exploitation frameworks, staging behavior): P2, with strong bias to upgrade if scope expands

Reference:
- `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P1-Critical-Definition.md`
- `01_INCIDENT-CLASSIFICATION/01.2_Incident-Categories/CAT-01-Ransomware.md`

---

## 6. Activation Criteria (When to Trigger This Playbook)

Trigger this playbook when any of the following are detected:

### 6.1 Confirmed Ransomware Indicators
- encrypted file extensions appearing at scale
- ransom note present on endpoint/server/file share
- EDR detection confirming ransomware behavior (mass file encryption)
- mass file rename / high-entropy write behavior

### 6.2 Strong Precursor Indicators (Treat as “Pre-Ransomware”)
- credential dumping behavior targeting privileged identities
- suspicious remote admin activity across multiple hosts (lateral movement)
- deletion or tampering with backups or shadow copies
- staging of large archives prior to transfer
- evidence of data exfiltration and subsequent destructive activity

### 6.3 High-Risk Systems Affected
- domain controller, identity systems, backup servers, virtualization hosts
- file servers, ERP/finance systems, production applications
- SOC tooling or logging infrastructure

---

## 7. Roles and Responsibilities (Incident Command)

### 7.1 Incident Command Structure
| Role | Responsibilities |
|------|------------------|
| Incident Commander (IC) | Owns incident execution, decision flow, task assignment, and status reporting |
| SOC Lead | Coordinates SOC workstreams, ensures SLA/communications, maintains ticket hygiene |
| L1 Analyst | Initial validation, ticket creation, initial evidence capture, escalation |
| L2 Analyst | Investigation, scoping, correlation, recommends containment |
| L3 Analyst | Advanced analysis, TTP mapping, threat hunting, forensic guidance |
| IR Team | Containment/eradication/recovery leadership, evidence governance |
| IT Operations | Executes technical actions (isolation, restore, rebuild, patching) |
| Network Team | Network segmentation, blocking, routing, captures |
| IAM/AD Team | Account actions (disable/reset/revoke), privileged control |
| GRC/Compliance | Regulatory decision support and reporting coordination |
| Legal | Legal advice, law enforcement coordination, litigation hold |
| MSSP SDM (if MSSP) | Client communications governance, contractual SLA alignment |

Reference:
- `00_GOVERNANCE/00.3_Roles-and-Responsibilities/RACI-Matrix-IR.xlsx`
- `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

## 8. Tools and Data Sources (Minimum Expectations)

| Area | Primary Sources |
|------|------------------|
| Endpoint | EDR telemetry, quarantine logs, process trees, file activity |
| Identity | AD logs, SSO logs, MFA logs, privileged group changes |
| Network | Firewall logs, proxy logs, DNS logs, NetFlow, IDS/IPS |
| Email | Secure email gateway logs, mailbox audit logs |
| Servers | OS event logs, application logs, file share audit logs |
| Backup | Backup job logs, backup integrity status, restore history |
| Cloud | Cloud audit logs, storage access logs, IAM role changes |
| Threat Intel | IOC reputation, campaign reporting, YARA/signature support |

---

## 9. Constraints and Safety Rules (Critical)

### 9.1 Evidence Preservation
Do not destroy evidence during containment. For high-severity ransomware, preserve:
- logs, EDR data, memory (where feasible), disk triage artifacts
- copies of ransom notes and encrypted file samples (for identification)

### 9.2 Avoid Uncontrolled Changes
Avoid untracked remediation actions that:
- overwrite artifacts (aggressive cleaning without capture)
- break investigation continuity
- contaminate evidence

### 9.3 Business Impact Controls
Containment actions affecting critical systems require:
- approval per Containment Authority Matrix
- documented business impact assessment (where time allows)

---

## 10. Workflow Overview (End-to-End)

This playbook follows a structured lifecycle. Each phase has required outputs and decision points.

### Phase A: Identification and Declaration
1. Validate ransomware indicators
2. Open incident ticket and assign severity
3. Notify SOC Lead and trigger P1 bridge call (if P1)
4. Activate IR Team (P1 mandatory; P2 as required)

Outputs:
- incident declared (P1/P2)
- initial scope estimate
- first status notification issued

### Phase B: Containment (Stop Spread and Harm)
1. Isolate affected endpoints/servers (network containment)
2. Block known attacker destinations and IOCs
3. Disable compromised accounts and revoke sessions
4. Segment network where needed
5. Protect backups and critical infrastructure

Outputs:
- containment plan documented
- containment actions executed with timestamps
- “encryption stopped” confirmation (or ongoing status)

### Phase C: Investigation and Scoping
1. Identify Patient Zero and attack entry point
2. Identify lateral movement and privileged compromise
3. Determine whether exfiltration occurred
4. Build authoritative timeline

Outputs:
- scope list (affected hosts/users/data)
- initial access vector hypothesis and evidence
- IOC/TTP list
- timeline maintained

### Phase D: Eradication (Remove Threat and Persistence)
1. Remove malware artifacts and persistence mechanisms
2. Patch exploited vulnerabilities and close exposed services
3. Rotate credentials/keys/secrets
4. Validate systems are clean (EDR scans/hunts/log review)

Outputs:
- eradication actions documented
- persistence removed verification
- re-entry prevention actions applied

### Phase E: Recovery (Restore Services Safely)
1. Restore from known-good backups or rebuild systems
2. Validate integrity and business functionality
3. Reconnect systems gradually under monitoring
4. Implement enhanced monitoring window

Outputs:
- recovery plan and sign-off
- return-to-service approval recorded
- post-recovery monitoring plan

### Phase F: Post-Incident Review and Improvement
1. PIR and RCA completed
2. Final incident report delivered
3. Improvement actions tracked to closure
4. Detection tuning and control updates implemented

Outputs:
- final report and executive summary
- action tracker updated
- playbooks updated

---

## 11. Phase A – Identification and Declaration (Detailed)

### 11.1 L1 Responsibilities (Minimum)
- confirm alert source and evidence
- gather initial affected asset list (at least top 5 impacted)
- create incident ticket with:
  - time detected and time observed
  - affected host(s), user(s), and location
  - evidence snapshots and log extracts
  - initial severity recommendation
- escalate to SOC Lead immediately for suspected ransomware

Reference:
- `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-L1-Triage.md`

### 11.2 SOC Lead Actions (P1/P2)
- declare severity and start SLA timers
- initiate bridge call (P1 mandatory)
- engage IR Team and required support teams
- set status update cadence (P1: 30 minutes; P2: 60 minutes)

Reference:
- `03_SOC-TIER-PROCEDURES/03.4_SOC-Lead-Procedures/SOCLead-P1-P2-Bridge-Call-SOP.md`

---

## 12. Phase B – Containment (Detailed)

### 12.1 Containment Priorities (Order of Operations)
1. Stop encryption (isolate actively encrypting hosts)
2. Protect identity systems and privileged accounts
3. Stop lateral movement (segment, block admin channels where needed)
4. Protect backups (isolate backup networks; restrict credentials)
5. Stop exfiltration (block destinations; monitor data flows)

### 12.2 Containment Checklist (P1 Default)
- isolate confirmed infected endpoints via EDR containment
- isolate infected servers using network segmentation when EDR containment is not possible
- disable compromised user accounts and revoke sessions
- lock down privileged accounts:
  - remove suspicious admin group changes
  - rotate privileged credentials (with approvals)
- block known IOCs at:
  - DNS/proxy (domains/URLs)
  - firewall (IPs/ports)
  - EDR (hashes/IOCs)
- verify backup repositories are not reachable from infected zones
- prevent reinfection:
  - restrict RDP/SMB/admin tools if actively abused (change control where required)

Reference:
- `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Containment.md`

---

## 13. Phase C – Investigation and Scoping (Detailed)

### 13.1 Key Investigation Objectives
- confirm Patient Zero and earliest activity timestamp
- determine initial access vector:
  - phishing, remote access compromise, exploit, vendor access, etc.
- confirm credential compromise:
  - privileged accounts, service accounts, admin sessions
- confirm lateral movement path:
  - which protocols, which hosts, which accounts
- confirm data breach risk:
  - exfiltration indicators, staging directories, large outbound transfers
- determine ransomware family/variant:
  - based on EDR detection, ransom note characteristics, file extensions, known IOCs

Reference:
- `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-L2-Investigation.md`
- `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-L3-Forensics.md`

---

## 14. Phase D – Eradication (Detailed)

### 14.1 Eradication Principles
- do not restore systems until persistence and access paths are removed
- rotate secrets/credentials after verifying identity compromise scope
- rebuild preferred for high-risk systems when integrity cannot be trusted

Eradication actions may include:
- removing malicious services/tasks/autoruns
- patching exploited vulnerabilities
- removing unauthorized accounts and reversing policy changes
- hardening remote access and disabling exposed management interfaces
- updating detection content (IOCs and TTP-based rules)

Reference:
- `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Eradication.md`

---

## 15. Phase E – Recovery (Detailed)

### 15.1 Recovery Readiness Gates (Must Pass)
Before restore or reconnect:
- containment confirmed (no active encryption)
- compromised accounts remediated and monitored
- persistence mechanisms removed
- backups verified clean and not encrypted/tampered
- reinfection risk reduced (blocks in place, vulnerabilities mitigated)

### 15.2 Return-to-Service Approval
For P1 incidents, return-to-service must be approved by:
- IT Service Owner (Accountable)
- IR Team Lead (Security approval)
- SOC Lead (operational readiness)
- Management/CISO (if business critical)

Reference:
- `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Recovery.md`
- `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Closure-Criteria.md`

---

## 16. Communications (P1/P2 Requirements)

### 16.1 Internal
- P1: management notified within 15 minutes of declaration
- P2: management notified within 30 minutes of declaration
- updates per cadence

### 16.2 MSSP Clients (If Applicable)
- notify client within SLA timelines
- do not share cross-client evidence
- document approvals and client actions clearly

Reference:
- `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/`
- `00_GOVERNANCE/00.4_SLA-and-SLO/MSSP-Client-SLA-Template.md`

---

## 17. Evidence Handling (Minimum Standard)

### 17.1 Minimum Evidence Set (P1/P2)
- incident timeline notes (authoritative)
- EDR exports: process trees, detections, containment actions
- key logs: identity, firewall/proxy/DNS, server event logs
- ransom note copies and file extension evidence (if present)
- list of affected assets and users (versioned)
- chain-of-custody initiated when evidence may be legal/regulatory

Reference:
- `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 18. Post-Incident Requirements (Mandatory for P1/P2)

Deliverables:
- final incident report (executive + technical)
- RCA identifying initial access vector and control failures
- lessons learned and corrective action plan
- detection improvements and tuning updates
- verification that actions are tracked to closure

Reference:
- `08_POST-INCIDENT/`
- `07_REPORTING/07.1_Incident-Reports/Final-Incident-Report-Template.md`

---

## 19. Playbook Links (Ransomware Set)

| Document | Path |
|---------|------|
| L1 Triage | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-L1-Triage.md` |
| L2 Investigation | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-L2-Investigation.md` |
| L3 Forensics | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-L3-Forensics.md` |
| Containment | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Containment.md` |
| Eradication | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Eradication.md` |
| Recovery | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Recovery.md` |
| MITRE Mapping | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-MITRE-Mapping.md` |

---

## 20. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | IR Team Lead / SOC Manager | Initial version |

---

## 21. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

End of Document