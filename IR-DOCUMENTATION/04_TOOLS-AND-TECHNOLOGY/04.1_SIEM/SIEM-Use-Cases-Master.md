# REGISTER: SIEM Use Cases Master

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | REGISTER – SIEM Use Cases Master |
| Document ID | TOOL-SIEM-005 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / Detection Engineering Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This document is the authoritative master register of the organization’s SIEM detection and correlation **use cases**. It defines:

- The standardized structure for SIEM use cases
- Required metadata for each use case (owner, severity mapping, data sources, dependencies)
- Operational lifecycle controls (build, test, deploy, tune, review, retire)
- Coverage visibility across threat categories and MITRE ATT&CK tactics
- MSSP considerations (tenant scope, segregation, and client-specific enablement)
- Audit-ready evidence that detections exist, are governed, and are periodically reviewed

This master register supports:

- SOC operations (L1/L2/L3)
- Incident Response and escalation decisions
- Threat Hunting planning
- Detection engineering and tuning governance
- Compliance readiness (ISO 27001/NIST/RBI expectations for monitoring and incident handling)

---

# 3. Scope

Applies to:

- All SIEM correlation rules and analytics detections
- All tenants/workspaces for MSSP operations (where applicable)
- All data sources integrated into the SIEM (identity, endpoint, network, cloud, email, applications)

Out of scope:

- EDR-only detections not forwarded to SIEM (tracked in EDR detection register)
- Preventive controls (firewall rules, IAM policy) unless used as detection sources

---

# 4. Use Case Lifecycle Governance

---

## 4.1 Use Case Lifecycle Stages

| Stage | Description | Entry Criteria | Exit Criteria |
|---|---|---|---|
| Proposed | Use case requested | Request + business rationale | Approved for design |
| Designed | Logic and dependencies defined | Data sources available | Design review complete |
| Built | Rule implemented | Parsing/fields validated | Unit test passed |
| Tested | Validated via replay/simulation | Test plan executed | Accepted for production |
| Deployed | Enabled in production | Change record approved | Live monitoring started |
| Tuned | Reduced FP, improved fidelity | First 2 weeks of metrics | Stable FP/TP ratio |
| Reviewed | Quarterly effectiveness review | KPI review | Retain / improve / retire |
| Retired | Disabled & archived | Replacement or obsolete | Documentation updated |

---

## 4.2 Change Control Requirements

| Change Type | Examples | Approval |
|---|---|---|
| Low-risk tuning | threshold change, suppression window | SOC Lead |
| Medium-risk tuning | whitelist addition, field logic changes | SOC Manager |
| High-risk change | rule disablement, cross-tenant changes | Detection Engineering Lead + SOC Manager |
| Critical change | changes affecting regulatory monitoring or P1 detection | CISO |

All changes must be logged in the tuning change log:
`04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md`

---

# 5. Standard Use Case Metadata (Required Fields)

Each use case must include the following fields:

| Field | Description |
|---|---|
| Use Case ID | Unique ID (UC-<DOMAIN>-###) |
| Name | Detection name |
| Objective | What it detects |
| Threat Category | Credential / Malware / Exfiltration / Cloud / Web / etc. |
| MITRE ATT&CK | Tactic/Technique mapping |
| Default Severity | P1/P2/P3/P4 recommendation |
| Escalation Target | L2 / L3 / IR Team |
| Data Sources | Logs required |
| Dependencies | Normalized fields / TI lookups / asset criticality |
| Rule Type | Threshold / Correlation / Behavioral / IOC match |
| Investigation Notes | What L1/L2 should validate |
| False Positive Notes | Common benign triggers |
| Tuning Controls | Suppression/whitelist/threshold tuning guidance |
| Test Method | Replay / simulation / red team validation |
| Owner | Detection engineering owner |
| Last Reviewed | Date |
| Status | Proposed/Active/Retired |
| MSSP Scope | Global / Client-specific / Optional |

---

# 6. Severity Mapping Standard (SOC)

Use case default severity must align to the incident severity matrix.

| Severity | Meaning | Typical Action |
|---|---|---|
| P1 | Active major compromise / high business impact | Bridge call + IR activation likely |
| P2 | Confirmed compromise likely / privileged risk | L2+ investigation, possible IR |
| P3 | Suspicious behavior / needs investigation | L2 standard investigation |
| P4 | Informational / low risk | Document and monitor |

Reference:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

---

# 7. Data Source Dependency Standards

A use case must not be marked **Production/Active** unless dependencies are met.

---

## 7.1 Minimum Required Dependencies

| Dependency | Requirement |
|---|---|
| Time sync | NTP and UTC normalization |
| Source identity | hostname, asset_id, or device_id present |
| User identity | user/UPN mapped where applicable |
| IP normalization | src_ip/dest_ip extracted |
| Asset criticality | asset tier mapping available (preferred) |
| Threat intel enrichment | IOC feeds where relevant |
| Tenant tagging (MSSP) | client_id/tenant enforced |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Integration-Map.md`

---

# 8. Use Case Catalog (Master Register)

**Legend**
- Domain: ID=Identity, EP=Endpoint, NW=Network, CLD=Cloud, EML=Email, WEB=Web/App, DB=Database, OPS=Operations
- Status: Active/Proposed/Retired

---

## 8.1 Master Use Case Table

| Use Case ID | Domain | Name | Threat Category | Default Severity | Escalation Target | Primary Data Sources | MITRE (High Level) | Status | MSSP Scope | Owner | Last Reviewed |
|:--|---|---|---|---|---|---|---|---|---|---|---|
| UC-ID-001 | ID | Password Spray Detection | Credential Attack | P2 | L2 | Entra/AD/VPN | Credential Access | Active | Global | Detection Eng | 2026-05-22 |
| UC-ID-002 | ID | Brute Force Against Single User | Credential Attack | P3 | L2 | Entra/AD/VPN | Credential Access | Active | Global | Detection Eng | 2026-05-22 |
| UC-ID-003 | ID | Impossible Travel / Geo-Anomaly | Account Takeover | P2 | L2 | Entra/SSO | Initial Access | Active | Global | Detection Eng | 2026-05-22 |
| UC-ID-004 | ID | MFA Fatigue / Push Bombing | Account Takeover | P2 | L2 | MFA/Entra | Credential Access | Active | Global | Detection Eng | 2026-05-22 |
| UC-ID-005 | ID | New Admin Account Creation | Privilege Abuse | P1 | IR Team | AD/Entra Audit | Privilege Escalation | Active | Global | Detection Eng | 2026-05-22 |
| UC-ID-006 | ID | Privileged Group Membership Change | Privilege Abuse | P1 | IR Team | AD/Entra Audit | Privilege Escalation | Active | Global | Detection Eng | 2026-05-22 |
| UC-EP-001 | EP | Encoded PowerShell Execution | Malware/LOLBins | P2 | L2/L3 | EDR/Sysmon | Execution | Active | Global | Detection Eng | 2026-05-22 |
| UC-EP-002 | EP | LOLBin Abuse (rundll32/mshta/certutil) | Malware/LOLBins | P2 | L2 | EDR/Sysmon | Execution | Active | Global | Detection Eng | 2026-05-22 |
| UC-EP-003 | EP | Credential Dumping Indicators (LSASS) | Credential Attack | P1 | IR Team | EDR/Sysmon | Credential Access | Active | Global | Detection Eng | 2026-05-22 |
| UC-EP-004 | EP | New Service Install (Persistence) | Persistence | P2 | L2/L3 | Windows System | Persistence | Active | Global | Detection Eng | 2026-05-22 |
| UC-EP-005 | EP | Scheduled Task Creation (Persistence) | Persistence | P2 | L2/L3 | Windows Security | Persistence | Active | Global | Detection Eng | 2026-05-22 |
| UC-EP-006 | EP | Ransomware Precursor: Shadow Copy Deletion | Ransomware | P1 | IR Team | EDR/Sysmon | Impact | Active | Global | Detection Eng | 2026-05-22 |
| UC-EP-007 | EP | Mass File Modification (Encryption Heuristic) | Ransomware | P1 | IR Team | EDR File Events | Impact | Proposed | Global | Detection Eng | 2026-05-22 |
| UC-NW-001 | NW | Beaconing / Repeated Outbound Connections | C2 | P2 | L2 | Firewall/Proxy/NetFlow | Command & Control | Active | Global | Detection Eng | 2026-05-22 |
| UC-NW-002 | NW | Large Outbound Transfer | Exfiltration | P1 | IR Team | Firewall/Proxy/NetFlow | Exfiltration | Active | Global | Detection Eng | 2026-05-22 |
| UC-NW-003 | NW | DNS Tunneling Heuristic | Exfiltration/C2 | P1 | IR Team | DNS Logs | Exfiltration | Proposed | Global | Detection Eng | 2026-05-22 |
| UC-NW-004 | NW | Lateral Movement via RDP/SMB (High Fan-out) | Intrusion | P2 | L2/IR | NetFlow/Firewall/Windows | Lateral Movement | Active | Global | Detection Eng | 2026-05-22 |
| UC-CLD-001 | CLD | AWS Root Account Usage | Cloud Compromise | P1 | IR Team | CloudTrail | Privilege Escalation | Active | Client-Specific | Detection Eng | 2026-05-22 |
| UC-CLD-002 | CLD | Cloud API Key Creation/Rotation (Anomalous) | Cloud Compromise | P2 | L2/IR | CloudTrail/Azure Audit | Credential Access | Active | Global | Detection Eng | 2026-05-22 |
| UC-CLD-003 | CLD | Azure Privileged Role Assignment | Cloud Compromise | P1 | IR Team | Azure AuditLogs | Privilege Escalation | Active | Global | Detection Eng | 2026-05-22 |
| UC-CLD-004 | CLD | M365 Mailbox Rule Creation (Forwarding/Hide) | BEC | P2 | L2 | M365 Audit | Persistence | Active | Global | Detection Eng | 2026-05-22 |
| UC-EML-001 | EML | Phishing Campaign Detection (Sender/Domain Burst) | Phishing | P2 | L2 | Email Gateway/M365 | Initial Access | Active | Global | Detection Eng | 2026-05-22 |
| UC-EML-002 | EML | Suspicious URL Click (If Telemetry Available) | Phishing | P2 | L2 | Proxy/SWG | Initial Access | Proposed | Client-Specific | Detection Eng | 2026-05-22 |
| UC-WEB-001 | WEB | WAF SQLi / High Severity Signatures | Web Attack | P2 | L2/IR | WAF Logs | Initial Access | Active | Global | Detection Eng | 2026-05-22 |
| UC-WEB-002 | WEB | Webshell Indicators (Suspicious POST + New File) | Web Attack | P1 | IR Team | WAF/Web Server/EDR | Persistence | Proposed | Client-Specific | Detection Eng | 2026-05-22 |
| UC-OPS-001 | OPS | Critical Log Source Silence (EDR/AD/Firewall) | Monitoring Gap | P1 | SOC Lead | SIEM Health/Indexes | Detect | Active | Global | SIEM Eng | 2026-05-22 |
| UC-OPS-002 | OPS | Parsing Error Spike | Monitoring Quality | P2 | SIEM Eng | SIEM Internal Logs | Detect | Active | Global | SIEM Eng | 2026-05-22 |

---

# 9. Use Case Details (Critical & High Priority)

The following use cases are designated **Tier-1** due to high impact and/or regulatory relevance. These must be tested, tuned, and reviewed quarterly at minimum.

---

## UC-EP-003 — Credential Dumping Indicators (LSASS)

| Field | Value |
|---|---|
| Objective | Detect credential dumping activity (LSASS access/dumps/tool patterns) |
| Default Severity | P1 |
| Escalation Target | IR Team (Immediate) |
| Data Sources | EDR process telemetry, Sysmon (preferred), Windows Security |
| Dependencies | Process command line visibility; privileged account tagging |
| MITRE | Credential Access (e.g., OS Credential Dumping) |
| Investigation Notes | Confirm process ancestry, user context, server/DC involvement, concurrent auth anomalies |
| Common False Positives | Approved security tools, sanctioned admin dumps (rare), IR tools |
| Tuning Controls | Whitelist only with approval + expiration; require server/DC boost |
| Test Method | Controlled red-team simulation in lab; replay historical |
| Related Playbooks | `02_PLAYBOOKS/02.7_Credential-Attack/` and `02_PLAYBOOKS/02.11_Network-Intrusion/` |

---

## UC-EP-006 — Ransomware Precursor: Shadow Copy Deletion / Backup Tampering

| Field | Value |
|---|---|
| Objective | Detect commands associated with backup destruction and shadow copy deletion |
| Default Severity | P1 |
| Escalation Target | IR Team (Immediate) |
| Data Sources | EDR telemetry, Sysmon |
| Dependencies | Command-line logging; endpoint coverage |
| MITRE | Impact (Inhibit System Recovery) |
| Investigation Notes | Validate actor identity; correlate with file modification spikes and lateral movement |
| Common False Positives | Rare; some backup/IT scripts (validate change tickets) |
| Tuning Controls | Minimal tuning; only whitelist with executive approval |
| Test Method | Lab execution of safe test commands; red-team validation |
| Related Playbooks | `02_PLAYBOOKS/02.1_Ransomware/` |

---

## UC-NW-002 — Large Outbound Transfer (Potential Exfiltration)

| Field | Value |
|---|---|
| Objective | Detect unusually large outbound transfers from hosts/users, including to rare destinations |
| Default Severity | P1 |
| Escalation Target | IR Team + Legal/Compliance if sensitive data suspected |
| Data Sources | Firewall, Proxy, NetFlow, Cloud storage logs (preferred) |
| Dependencies | Byte counters and directionality; asset criticality mapping |
| MITRE | Exfiltration |
| Investigation Notes | Confirm business justification (backup/CDN); correlate with new destinations, unusual hours, credential abuse |
| Common False Positives | Backup jobs, sanctioned large data exports, patch distribution |
| Tuning Controls | Baseline per subnet/application; exclude known backup endpoints; add rare-destination condition |
| Test Method | Replay known transfers; validate via change tickets |
| Related Playbooks | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/` |

---

## UC-ID-005 — New Admin Account Creation

| Field | Value |
|---|---|
| Objective | Detect new privileged account creation or admin-level user provisioning |
| Default Severity | P1 |
| Escalation Target | IR Team (Immediate) |
| Data Sources | AD Security, Entra AuditLogs, PAM |
| Dependencies | Reliable identity audit logs; privileged group mapping |
| MITRE | Privilege Escalation / Persistence |
| Investigation Notes | Validate change approval; identify creator account; correlate with suspicious sign-in source IP |
| Common False Positives | Approved provisioning (must correlate with change ticket) |
| Tuning Controls | Use approved admin provisioning list; require change-ticket field/tag where possible |
| Test Method | Controlled creation in lab/QA tenant |
| Related Playbooks | `02_PLAYBOOKS/02.11_Network-Intrusion/` and `02_PLAYBOOKS/02.7_Credential-Attack/` |

---

## UC-CLD-003 — Azure Privileged Role Assignment

| Field | Value |
|---|---|
| Objective | Detect privileged role assignment, especially outside change windows or by unusual actors |
| Default Severity | P1 |
| Escalation Target | IR Team (Immediate) |
| Data Sources | Azure AuditLogs, Entra logs |
| Dependencies | Cloud audit retention; actor/target extraction |
| MITRE | Privilege Escalation |
| Investigation Notes | Validate initiator, target role, IP/geo, MFA status; check if role is PIM eligible/active |
| Common False Positives | Scheduled access reviews, approved role grants |
| Tuning Controls | Restrict to high-value roles; enforce change window checks |
| Test Method | PIM role assignment testing in staging tenant |
| Related Playbooks | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/` |

---

## UC-OPS-001 — Critical Log Source Silence

| Field | Value |
|---|---|
| Objective | Detect when critical log sources stop sending telemetry to SIEM |
| Default Severity | P1 |
| Escalation Target | SOC Lead + SIEM Engineering |
| Data Sources | SIEM internal logs/heartbeats, index monitoring |
| Dependencies | Source inventory; last_event_time field; integration mapping |
| MITRE | Detect (Monitoring) |
| Investigation Notes | Identify impacted sources/tenants; assess detection gaps; initiate troubleshooting |
| Common False Positives | Planned maintenance (must be pre-notified/approved) |
| Tuning Controls | Per-source thresholds; maintenance window suppression |
| Test Method | Controlled collector stop/start in lab |
| Related SOPs | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Troubleshooting-SOP.md` |

---

# 10. Testing Standards (Minimum)

All Active use cases must meet one of the following testing standards:

| Test Type | Description | When Required |
|---|---|---|
| Historical Replay | Query/rule validated against known events | Minimum for all |
| Simulation | Controlled benign simulation triggers rule | For P1/P2 |
| Purple Team | Adversary simulation validates detection end-to-end | Quarterly for top Tier-1 |
| Production Canary | Controlled “safe signal” event | For integration-dependent rules |

---

# 11. Review & Effectiveness Metrics

Each quarterly review must evaluate:

| Metric | Objective |
|---|---|
| Alert volume | Operational load |
| False positive rate | Detection quality |
| True positive rate | Detection utility |
| Time-to-triage | SOC efficiency |
| Coverage gaps | Visibility improvement |
| Tuning actions | Continuous improvement |

Maintain improvements in:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

---

# 12. MSSP Considerations

For MSSP environments, each use case must specify scope:

| MSSP Scope | Meaning |
|---|---|
| Global | Enabled for all tenants by default (tenant-safe) |
| Client-Specific | Enabled only for select clients due to data availability or contract |
| Optional | Available but requires client approval |

Mandatory MSSP controls:

- Tenant segregation enforced
- No cross-client correlation unless approved and legally permitted
- Client-specific baselines where required (e.g., exfil thresholds)
- Client notification workflows aligned to SLAs

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 13. Related Documents

| Document | Path |
|---|---|
| SIEM Integration Map | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Integration-Map.md` |
| SIEM Query Library | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Query-Library.md` |
| SIEM Alert Tuning Guide | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md` |
| SIEM Troubleshooting SOP | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Troubleshooting-SOP.md` |
| L2 SIEM Deep Investigation SOP | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-SIEM-Deep-Investigation.md` |
| Incident Severity Guide | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md` |

---

# 14. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | Detection Engineering Lead | Initial version |

---

# 15. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**