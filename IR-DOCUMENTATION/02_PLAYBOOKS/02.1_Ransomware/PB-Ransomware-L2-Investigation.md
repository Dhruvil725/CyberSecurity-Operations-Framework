# Playbook: Ransomware – L2 Investigation

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Ransomware (L2 Investigation) |
| Document ID | IR-PB-RAN-003 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | SOC Manager / IR Team Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 ransomware incident |

---

## 2. Purpose

This document defines the L2 SOC Analyst procedure for investigating
suspected or confirmed ransomware activity. It focuses on:

- confirmation of ransomware activity (true incident validation)
- scoping and impact assessment (affected hosts, users, services)
- identification of initial access vector and attack chain
- detection of lateral movement and privilege escalation
- exfiltration assessment (double extortion)
- producing actionable containment recommendations
- preparing investigation outputs for IR Team and management reporting

L2’s goal is to convert L1 triage into a verified, scoped incident with
a clear response direction.

---

## 3. Scope

Applies to P1/P2 ransomware incidents and ransomware precursor incidents
likely to escalate. Covers:

- endpoints and servers impacted or suspected
- identity systems and privileged accounts
- network and cloud telemetry relevant to ransomware operations
- coordination with IT/Network/IAM for containment actions
- MSSP client environments with client-specific constraints and SLAs

---

## 4. Investigation Objectives and Outputs

### 4.1 Primary Objectives
1. Confirm ransomware execution or precursor stage activity
2. Determine if encryption is active and where
3. Identify Patient Zero and initial access vector
4. Determine scope: hosts, users, shares, business services affected
5. Detect and stop lateral movement
6. Determine if data exfiltration occurred or is likely
7. Identify compromised credentials and privileged compromise
8. Produce a validated timeline and evidence package
9. Recommend containment strategy immediately

### 4.2 Required Outputs (Minimum)
- updated severity recommendation with justification
- scope table (affected and suspected assets)
- compromised identity list (confirmed/suspected)
- ransomware family/variant hypothesis (if possible)
- list of IOCs and observed TTPs (for blocking and hunting)
- initial access vector hypothesis and evidence
- lateral movement map (hosts and protocols)
- exfiltration assessment and confidence level
- investigation notes and evidence attachments suitable for audit

---

## 5. L2 SLA Targets (Ransomware)

| Metric | P1 Target | P2 Target |
|-------|-----------|-----------|
| Acknowledge escalation | 5 minutes | 10 minutes |
| Begin investigation | immediately | within 15 minutes |
| Initial scoping update to SOC Lead/IC | within 30 minutes | within 60 minutes |
| Containment recommendation | within 60 minutes | within 120 minutes |
| Update cadence to SOC Lead | every 30 minutes | every 60 minutes |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

## 6. Data Sources (L2 Minimum Coverage)

L2 investigation must use multiple sources to avoid single-tool bias.

### 6.1 Endpoint and Host Telemetry
- EDR detections, process tree, file activity, quarantine
- host event logs (Windows Security/System/Application)
- file server audit logs where available

### 6.2 Identity and Access Telemetry
- AD logon events, group membership changes
- SSO/MFA sign-in logs (cloud identity)
- privileged access management logs (if available)

### 6.3 Network Telemetry
- firewall logs, proxy logs, DNS logs
- NetFlow/sFlow (if available)
- IDS/IPS alerts

### 6.4 Email Telemetry (if phishing suspected)
- email gateway delivery and click logs
- mailbox audit logs (for account takeover scenarios)

### 6.5 Backup and Infrastructure Telemetry
- backup job and repository logs
- virtualization platform logs (hypervisors)
- monitoring system alerts (service outages)

### 6.6 Threat Intelligence
- IOC reputation (domain/IP/hash)
- known ransomware group indicators
- public decryptor availability indicators

---

## 7. Investigation Workflow (Step-by-Step)

### Step 1: Confirm Incident Status (Ransomware vs Precursor)

Confirm one of the following states and record in the ticket:

| State | Definition |
|------|------------|
| Confirmed ransomware | encryption behavior or ransom note confirmed |
| Likely ransomware | strong indicators, encryption not fully confirmed yet |
| Precursor stage | post-exploitation behavior strongly associated with ransomware operations |
| Not ransomware | activity belongs to a different incident category |

Minimum confirmation evidence examples:
- EDR behavioral encryption alert
- mass file rename/high-entropy write evidence
- ransom note artifact
- confirmed shadow copy deletion behavior tied to suspicious process chain

If uncertain, treat as “Likely ransomware” and proceed with P2 response minimum.

---

### Step 2: Identify Patient Zero (First Infected System)

Goal: determine where the ransomware operation began.

Actions:
- find earliest detection timestamp across all alerts
- search SIEM for earliest related event (same user, same hash, same domain)
- review EDR for first host with:
  - suspicious process chain
  - initial payload execution
  - first outbound C2 contact
- correlate with identity logs:
  - first suspicious login tied to the account or host

Output:
- patient zero candidate
- earliest timestamp (start of incident timeline)
- evidence references

---

### Step 3: Determine Encryption Status and Impact

Confirm:
- active encryption ongoing (yes/no)
- impacted asset types:
  - endpoints
  - servers
  - file shares
  - virtualization hosts
  - backup repositories
- whether business-critical services are disrupted

Actions:
- use EDR file activity view to confirm rate and scope
- check file server logs for mass changes
- confirm presence of ransom note on shares
- check backup platform for tampering signals

Output:
- impacted systems list (confirmed)
- suspected systems list (needs validation)
- business service impact summary (if known)

---

### Step 4: Identify Lateral Movement and Privilege Escalation

Ransomware operators commonly escalate privileges and pivot.

Actions:
- check for remote execution tools:
  - PsExec, WMI, WinRM, RDP, SMB admin shares
- check for credential dumping indicators:
  - LSASS access, suspicious dump tools
- check for suspicious admin group changes:
  - Domain Admins, Enterprise Admins, local admin changes
- check for creation of new accounts or service accounts
- check for GPO changes or mass deployment scripts

Output:
- lateral movement map (source host, destination host, protocol/tool)
- list of compromised or abused accounts (confirmed/suspected)
- list of privileged escalation indicators

Escalate to P1 immediately if:
- domain controller involvement is confirmed
- multiple servers are pivoted
- privileged accounts are compromised

---

### Step 5: Exfiltration Assessment (Double Extortion)

Ransomware groups often steal data before encryption.

Assess exfiltration via:
- proxy logs (large POST uploads, new cloud storage destinations)
- firewall/NetFlow (large sustained outbound connections)
- DNS logs (tunneling patterns)
- cloud logs (storage downloads, sharing changes)
- endpoint artifacts:
  - staging directories
  - large archives (zip/rar/7z)
  - file transfer tools

Assign confidence level and record in ticket:

| Level | Meaning |
|------|---------|
| Confirmed | evidence of transfer to external destination with volume indicators |
| Likely | strong staging + outbound connections consistent with transfer |
| Possible | weak indicators requiring more data |
| Not observed | no evidence with current telemetry (not definitive) |

Output:
- exfiltration assessment with evidence
- suspected destinations (domains/IPs/services)
- estimated data type at risk (if known)

If confirmed or likely with sensitive data: treat as P1 and engage Legal/GRC.

---

### Step 6: IOC and TTP Extraction (Operational Outputs)

Create an IOC list for immediate blocking and hunting:

IOC categories:
- file hashes (payloads, droppers, scripts)
- domains/URLs (C2, exfil destinations)
- IP addresses (C2, scanning sources, VPN sources)
- file paths (ransom notes, payload locations)
- registry keys / scheduled tasks / service names
- mutex names (if available)
- command-line patterns (shadow deletion, backup tampering)

Also document observed TTPs:
- initial access technique
- persistence method
- lateral movement method
- credential access method

Output:
- IOC list attached to ticket
- IOC distribution request to Network/SIEM/EDR owners
- hunting queries recommended to L3 (if needed)

---

### Step 7: Containment Recommendation to SOC Lead / IC

Provide a prioritized containment plan based on observed scope:

Containment priorities:
1. isolate actively encrypting hosts
2. isolate patient zero and pivot hosts
3. disable or reset compromised accounts (especially privileged)
4. block C2/exfil destinations
5. protect backups and administrative planes
6. segment network if lateral movement continues

Containment must follow authority matrix and client approvals (MSSP).

Output:
- containment recommendations documented with reasoning and urgency
- approvals requested and tracked

Reference:
`02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Containment.md`

---

## 8. Investigation Checklists (Detailed)

### 8.1 Host-Level Checklist (for each confirmed host)
- hostname, IP, OS, criticality
- user logged in at time of infection
- initial suspicious process and parent process
- suspicious command lines (encoded, LOLBins)
- persistence artifacts (tasks, services, registry run keys)
- outbound connections (domains, IPs, ports)
- file paths modified and extension changes
- ransomware note presence
- EDR containment status

### 8.2 Account-Level Checklist (for each suspected compromised account)
- account type: user/service/admin
- MFA enabled status and sign-in patterns
- last logon time and source IP/device
- privileged group membership changes
- suspicious mailbox rules (if email account)
- password reset status and session revocation status

### 8.3 Network-Level Checklist
- top outbound destinations from patient zero and pivot hosts
- evidence of SMB/RDP spread
- internal scanning evidence
- proxy uploads and data transfer indicators
- blocklist changes implemented and timestamps

### 8.4 Backup and Recovery Checklist (Investigation View)
- backup repository access attempts
- deletion events or job tampering
- last known good backup timestamps
- backup system isolation status
- backup admin account access anomalies

---

## 9. Severity and Escalation Rules (L2)

### 9.1 Upgrade to P1 Immediately If Any Condition Is True
- encryption confirmed on servers or file shares
- domain controller or privileged identity compromise confirmed
- lateral movement across multiple segments confirmed
- exfiltration confirmed or likely with sensitive data at risk
- backup destruction or tampering confirmed
- security tool tampering confirmed
- business-critical outage linked to ransomware

### 9.2 Downgrade Only With Evidence and SOC Lead Approval
Downgrades (P1 to P2) require:
- containment verified
- limited scope confirmed
- no exfil evidence (or ruled out by evidence)
- management approval as required

All reclassification must be documented in ticket with rationale.

Reference:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Escalation-Criteria.md`

---

## 10. Communication Requirements (L2 Responsibilities)

L2 must provide SOC Lead/IC with structured updates:

Minimum content:
- current status: active encryption yes/no
- scope: confirmed affected count + suspected count
- identity risk: suspected compromised accounts
- exfil assessment: confirmed/likely/possible/not observed
- key risks: DC involvement, backup risk, continued spread
- recommended next actions and approvals needed

Update cadence:
- P1: every 30 minutes (or more frequently if major changes)
- P2: every 60 minutes

---

## 11. Evidence Handling (L2 Requirements)

L2 must ensure:
- evidence is exported and attached in ticket or referenced in approved evidence store
- all evidence exports are time-stamped
- chain-of-custody is initiated if forensic images will be collected or evidence may be used legally

Minimum evidence set for ransomware investigations:
- EDR process trees and file activity evidence
- SIEM queries and raw logs
- identity logs for compromised users
- proxy/firewall logs for C2/exfil indicators
- ransomware note samples and extension evidence (if present)

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 12. Common L2 Investigation Mistakes to Avoid

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| focusing on one host only | misses spread | always scope across environment |
| ignoring identity compromise | attacker re-enters | assess credential compromise early |
| delaying exfil assessment | missed breach decision | evaluate exfil indicators in first hour |
| recommending restore too early | reinfection | eradicate persistence before recovery |
| assuming “no exfil” without evidence | wrong reporting | record confidence level and sources checked |
| not protecting backups | permanent data loss | isolate backup infrastructure quickly |

---

## 13. MSSP Notes (Client Handling)

For MSSP incidents:
- validate correct tenant attribution for each log source
- follow client severity and notification requirements
- document client approvals for containment actions
- ensure evidence shared is client-scoped only
- if multiple clients are affected, handle incidents separately and use anonymized TI outputs for cross-client advisories

Reference:
`01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/Multi-Client-Triage-MSSP.md`

---

## 14. Related Documents

| Document | Path |
|---------|------|
| Ransomware Master | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Master.md` |
| L1 Triage | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-L1-Triage.md` |
| L3 Forensics | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-L3-Forensics.md` |
| Containment | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Containment.md` |
| Eradication | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Eradication.md` |
| Recovery | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Recovery.md` |
| Severity Guide | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md` |
| Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |

---

## 15. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | SOC Manager / IR Team Lead | Initial version |

---

## 16. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

End of Document