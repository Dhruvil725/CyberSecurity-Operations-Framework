# Playbook: Ransomware – L3 Forensics and Advanced Analysis

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Ransomware (L3 Forensics) |
| Document ID | IR-PB-RAN-004 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | IR Team Lead / L3 Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 ransomware incident |

---

## 2. Purpose

This document defines the L3 procedure for forensic acquisition and
advanced analysis during ransomware incidents. It supports:

- forensic readiness and defensible evidence collection
- root cause analysis (initial access vector and attack chain)
- validation of persistence mechanisms and re-entry pathways
- ransomware family/variant identification
- detection and scoping of exfiltration (double extortion)
- production of high-quality technical findings for IR Team, management,
  legal, and regulatory needs
- detection engineering improvements (IOCs and TTP-based rules)

L3 focuses on accuracy, defensibility, and completeness of technical
analysis.

---

## 3. Scope

Applies to:
- P1 and major P2 ransomware incidents
- ransomware precursor incidents with confirmed attacker presence
- enterprise and MSSP client environments (client evidence segregation required)

Includes:
- memory forensics
- disk triage imaging and artifact analysis
- network forensics (where available)
- identity and log correlation for attack chain reconstruction
- validation of eradication readiness (persistence removed)

---

## 4. Forensic Principles and Legal Considerations

### 4.1 Evidence Integrity
- preserve original evidence where possible
- record hashes of acquired files/images
- store evidence in approved secure location
- maintain chain-of-custody documentation for transfers

### 4.2 Minimal Impact and Safety
- do not crash production systems during acquisition without approval
- memory acquisition is preferred before shutdown/reboot
- coordinate with IT Ops for timing and operational constraints

### 4.3 Confidentiality and Access Control
- restrict evidence access to authorized responders
- for MSSP: strict client segregation and client-approved transfer methods

Reference:
- `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`
- `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Evidence-Chain-of-Custody.md`

---

## 5. L3 Objectives and Required Outputs

### 5.1 Objectives
1. Confirm ransomware family and operational profile (as possible)
2. Identify initial access vector and earliest compromise timestamp
3. Identify all persistence mechanisms (host, identity, cloud, application)
4. Confirm credential compromise and privilege escalation path
5. Reconstruct lateral movement path across environment
6. Validate exfiltration activity and likely datasets involved
7. Provide technical guidance for eradication and recovery decisions
8. Produce high-quality technical findings for final report and audit evidence

### 5.2 Required Outputs
- technical timeline (authoritative) with evidence references
- patient zero confirmation and initial access determination
- persistence inventory and remediation guidance
- list of compromised accounts and recommended credential resets
- IOC package (hashes, domains, IPs, file paths, registry, tasks, services)
- TTP/MITRE mapping and hypothesis of attacker tradecraft
- exfiltration assessment (confirmed/likely/possible) with evidence
- recommended detection improvements (rules/hunts)
- forensic acquisition log + chain-of-custody completion status

---

## 6. Forensic Acquisition Plan (What to Collect and When)

### 6.1 Acquisition Priority Guidance
Prioritize evidence collection from:
1. Patient Zero host (initial compromise point)
2. Pivot hosts (jump boxes, admin endpoints)
3. High-value servers (file servers, DCs, backup servers, hypervisors)
4. Hosts showing encryption behavior
5. Hosts with suspicious outbound traffic or staging artifacts

### 6.2 Minimum Evidence Set (P1 Ransomware)
| Evidence | Priority | Notes |
|---------|----------|------|
| Memory capture (selected systems) | Critical | before reboot/shutdown |
| Disk triage image (selected systems) | High | full image preferred for patient zero |
| EDR telemetry export | Critical | process trees, file events, network connections |
| SIEM log exports | Critical | 48+ hours prior to first activity |
| Identity logs | Critical | sign-ins, group changes, MFA events |
| Network logs / NetFlow | High | C2/exfil indicators |
| Ransom note samples | Medium | preserve copies; do not execute on infected host |
| Encrypted file samples | Medium | preserve for strain identification |
| Backup platform logs | High | verify tampering attempts |

Reference:
- `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/`
- `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/`

### 6.3 Chain-of-Custody Requirements
For each evidence item:
- unique evidence ID
- collector name, date/time, method
- hashes (if applicable)
- storage location and access controls
- transfer log (if moved/shared)

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/`

---

## 7. Advanced Analysis Workflow (L3)

### Step 1: Ransomware Variant and Behavior Identification
Actions:
- review ransom note text patterns, filenames, extensions
- compare indicators with threat intel sources (internal TI and vendor intel)
- review EDR classification and behavioral indicators
- identify encryption mechanism patterns (where visible)

Outputs:
- variant hypothesis (if possible)
- known decryptor availability (if applicable)
- known TTP profile for targeted group (without claiming attribution unless approved)

---

### Step 2: Build the Authoritative Timeline
Actions:
- collect earliest timestamps:
  - first suspicious sign-in
  - first suspicious process execution
  - first lateral movement event
  - first staging/exfil event
  - first encryption event
- create a structured timeline table:
  - time, system, user, action, evidence reference
- maintain version control of timeline in ticket/evidence package

Outputs:
- authoritative timeline used for final report and PIR

---

### Step 3: Determine Initial Access Vector (Root Cause)
Common vectors to validate:
- phishing and user execution
- VPN or remote access compromise
- exploitation of public-facing application
- vendor access / RMM tool abuse
- exposed credentials or leaked keys
- supply chain updates

Evidence sources to correlate:
- email gateway logs
- VPN logs
- WAF/web logs
- identity logs
- EDR process history
- patch status and vulnerability scanning history

Outputs:
- initial access determination with confidence level and supporting evidence
- vulnerability or control failure linkage (for RCA)

---

### Step 4: Persistence Identification and Verification
Persistence areas to check:

Host persistence examples:
- scheduled tasks
- new services
- autoruns/run keys
- startup folder entries
- new local users
- WMI event subscriptions

Identity persistence examples:
- new accounts
- new privileged group memberships
- MFA method changes
- OAuth consents / app registrations
- mailbox forwarding rules

Network persistence examples:
- firewall rule changes
- VPN configuration changes
- remote access allow lists

Outputs:
- persistence inventory
- removal guidance and verification steps

---

### Step 5: Credential Compromise and Privilege Escalation Assessment
Validate:
- credential dumping tools and indicators
- LSASS access and memory scraping
- use of alternative authentication materials
- Kerberos abuse patterns (ticket anomalies)
- abnormal admin activity from non-admin endpoints

Outputs:
- list of compromised accounts (confirmed/suspected)
- reset/disable recommendations and sequencing
- privileged access lockdown recommendations

---

### Step 6: Lateral Movement Mapping
Identify:
- source host(s)
- destination host(s)
- tools/protocols used (RDP/SMB/WMI/PsExec/WinRM/SSH)
- account used for each hop
- timeline of lateral movement

Outputs:
- lateral movement map (table format)
- containment and segmentation recommendations
- additional hunt recommendations for similar movement patterns

---

### Step 7: Exfiltration Analysis (Double Extortion)
Exfiltration evidence categories:
- staging directories and archive creation
- outbound transfers to suspicious destinations
- cloud storage uploads
- email forwarding or mailbox exports
- unusual API access to storage/data services

Validation steps:
- correlate network logs with host artifacts:
  - archive creation timestamp vs outbound traffic windows
- validate destination reputation and ownership
- estimate data volume and likely data type (with data owners)

Outputs:
- exfiltration status and confidence
- suspected destinations and time windows
- recommended regulatory/legal engagement triggers

---

### Step 8: Malware and Post-Exploitation Tooling Analysis
Identify and document:
- droppers, loaders, scripts, binaries
- post-exploitation frameworks (beacons, remote shells)
- living-off-the-land techniques used
- evidence of security tool tampering
- evidence of automated deployment mechanisms (GPO, scripts, RMM)

Outputs:
- tooling inventory
- IOC package
- detection improvement recommendations

---

## 8. Analysis Deliverables (Standard Tables)

### 8.1 Authoritative Timeline Table Template
| Time (UTC) | System | User/Account | Event | Evidence Source | Evidence Reference |
|-----------|--------|--------------|-------|-----------------|-------------------|
| | | | | | |

### 8.2 Persistence Inventory Template
| System | Persistence Type | Artifact | Created Time | Evidence | Removal Action | Verified Removed (Y/N) |
|--------|------------------|----------|--------------|----------|----------------|------------------------|
| | | | | | | |

### 8.3 Compromised Account Table Template
| Account | Type (User/Service/Admin) | Indicators | First Seen | Actions Taken | Recommended Next Actions |
|--------|----------------------------|-----------|------------|---------------|--------------------------|
| | | | | | |

### 8.4 IOC Package Template
| IOC Type | Value | First Seen | Confidence | Source | Action Recommended |
|---------|-------|-----------|-----------|--------|-------------------|
| Hash | | | | | block in EDR |
| Domain | | | | | block in DNS/Proxy |
| IP | | | | | block in firewall |
| File Path | | | | | hunt + remove |
| Registry/Task/Service | | | | | remove |

---

## 9. Verification and “Clean State” Criteria (L3 Support)

L3 must support IR Team in validating eradication readiness.

Minimum conditions:
- no active encryption
- no C2 beaconing observed
- persistence mechanisms removed and verified
- compromised accounts reset and sessions revoked
- critical vulnerabilities mitigated (patch/workaround)
- monitoring increased for re-entry indicators

Reference:
`02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Eradication.md`

---

## 10. Communication and Reporting Support (L3)

L3 provides:
- technical deep dive content for final incident report
- executive-appropriate summaries of technical findings (via SOC Lead/IR Lead)
- risk assessment statements (data exposure likelihood, persistence removed confidence)
- detection improvement recommendations and action items

Reference:
`07_REPORTING/07.1_Incident-Reports/Technical-Deep-Dive-Template.md`

---

## 11. MSSP Evidence Segregation and Client Handling

For MSSP incidents:
- evidence must be stored per-client with client case identifiers
- do not include cross-client comparisons in client evidence packages
- any shared intelligence output must be anonymized and approved by SDM
- client evidence transfers must be encrypted and documented with transfer CoC

Reference:
- `01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/Multi-Client-Triage-MSSP.md`
- `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md`

---

## 12. Common L3 Pitfalls to Avoid

| Pitfall | Impact | Prevention |
|--------|--------|------------|
| collecting evidence too late | artifacts lost | prioritize patient zero and volatile data early |
| removing persistence before preservation | weak forensics | preserve first; remove second |
| focusing only on ransomware payload | miss attacker operations | map the full intrusion chain |
| ignoring identity persistence | re-entry | validate tokens, rules, app consents, group changes |
| not documenting evidence references | audit gaps | maintain tables with clear references and hashes |
| unclear confidence statements | decision confusion | use confirmed/likely/possible statements consistently |

---

## 13. Related Documents

| Document | Path |
|---------|------|
| Ransomware Master | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Master.md` |
| L1 Triage | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-L1-Triage.md` |
| L2 Investigation | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-L2-Investigation.md` |
| Containment | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Containment.md` |
| Eradication | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Eradication.md` |
| Recovery | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Recovery.md` |
| Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| Chain-of-Custody | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/` |
| RCA Templates | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/` |

---

## 14. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | IR Team Lead / L3 Lead | Initial version |

---

## 15. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

End of Document