# L2 to L3 Escalation

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – L2 to L3 Escalation |
| Document ID | ESC-PATH-006 |
| Version | 1.0 |
| Effective Date | 28-May-2026 |
| Owner | SOC Lead / SOC Operations Lead |
| Approved By | SOC Manager |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines the standard process for escalating investigations from **Level 2 (L2)** to **Level 3 (L3)** for advanced analysis and forensics.

L2→L3 escalation is critical because:

- L3 investigations require a complete evidence package to preserve time and maintain SLA compliance
- Advanced forensics, malware analysis, and complex scope validation require specialized skills and tooling
- Incomplete handoff increases time-to-containment and increases business risk
- Audit readiness requires documented rationale and traceable evidence handling
- MSSP environments require strict tenant segregation and client-safe evidence handling

This SOP ensures:

- Clear triggers and thresholds for L3 engagement
- Minimum L2 investigation and evidence preservation steps before escalation
- Standard escalation package (what L3 must receive)
- SLA-aligned acknowledgment and update expectations
- Clear ownership transfer and documentation standards

---

# 3. Scope

This SOP applies to escalation from L2 to L3 for:

| Investigation Type | Examples |
|---|---|
| Malware analysis | Unknown binaries/scripts, suspicious persistence, packers/obfuscation |
| Memory/disk forensics | Credential theft suspected, rootkits, in-memory execution |
| Advanced intrusion analysis | Lateral movement, privilege escalation, complex timelines |
| Cloud compromise | IAM privilege escalation, token abuse, suspicious API patterns |
| Data breach validation | Confirming exfil paths, staging artifacts, attacker tooling |
| Zero-day / novel TTP | Unrecognized exploitation behavior, emerging attack chains |
| Supply chain incidents | Vendor compromise indicators, signed malware, trusted update abuse |

Out of scope:

- L1→L2 escalation (separate SOP)
- L3→IR Team escalation (separate SOP)
- Routine tuning requests that do not require L3 forensics

References:  
`03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Investigation-SOP.md`  
`03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Advanced-Forensics-SOP.md`

---

# 4. Definitions

| Term | Definition |
|---|---|
| L3 | Advanced analyst/forensics function (malware analysis, memory/disk forensics, advanced hunting) |
| Escalation | Formal handoff to L3 with evidence package and defined request |
| Evidence package | Structured set of artifacts, logs, findings, and questions required for L3 work |
| Preservation | Actions taken to secure volatile and non-volatile evidence |
| Scope | The full set of affected hosts, users, services, and time range |
| IOC / TTP | Indicators of compromise and adversary behaviors |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| L2 Analyst | Primary investigator; prepares escalation package; ensures evidence preservation where feasible |
| L3 Analyst / Forensics Analyst | Acknowledges escalation; performs advanced analysis; documents findings and recommendations |
| SOC Lead | Oversees escalation quality and SLA; approves priority downgrades; coordinates P1/P2 workflows |
| IR Team Lead | Engaged when containment/major incident coordination is required; may direct L3 priorities |
| SIEM/EDR Engineers (as needed) | Support data extraction and telemetry validation |
| Evidence Custodian | Ensures evidence is stored securely and access-controlled |
| MSSP SDM (if applicable) | Ensures client scoping, approvals, and evidence segregation requirements |

Reference:
`00_GOVERNANCE/00.3_Roles-and-Responsibilities/RACI-Matrix-IR.xlsx`

---

# 6. Escalation Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Escalate with clear ask | L2 must state exactly what L3 is requested to do |
| Evidence first | Preserve volatile evidence before disruptive containment when possible |
| Don’t wait for perfection | For P1/P2, escalate early with best-available evidence and update as you go |
| Single owner | Ticket must clearly indicate current owner at every stage |
| Audit-ready | All major findings and decisions must be documented with UTC timestamps |
| Tenant-safe (MSSP) | Evidence, exports, and notes must be client-segregated and sanitized |

---

# 7. Escalation Triggers (When L2 Must Escalate to L3)

L2 must escalate to L3 when any of the following are true.

## 7.1 Mandatory Escalation Triggers

| Trigger | Examples |
|---|---|
| Advanced forensics required | Need memory analysis, disk imaging, artifact reconstruction |
| Unknown or novel malware | Packed payload, obfuscated script, unknown persistence |
| Credential theft suspected | LSASS access indicators, suspicious auth tokens, pass-the-hash |
| Rootkit/bootkit suspected | Kernel-level anomalies, hidden drivers |
| Lateral movement and domain risk | Multiple hosts affected, DC touched, privilege escalation |
| Zero-day suspected | Exploit behavior with no known signature/CVE context |
| Data exfil validation required | Need to confirm exfil method and data accessed/transferred |
| Supply chain compromise suspected | Signed malware, trusted tool misuse, vendor update anomalies |
| Incident scope unclear after 2–4 hours (P2+) | Cannot establish entry point or impacted assets with available data |
| High-risk system involved | Domain controllers, payment systems, core banking, IAM platforms |

## 7.2 Conditional Escalation Triggers

| Trigger | Examples |
|---|---|
| Repeated complex P3 activity | Persisting suspicious behavior across days |
| Need for advanced threat intel linkage | Actor/campaign mapping needed to inform strategy |
| Client requirement | Contract mandates L3 review for certain incident types |

---

# 8. L2 Pre-Escalation Checklist (Minimum Investigation Standard)

Before escalating, L2 must complete the following **unless escalation is urgent** (P1/P2 active compromise).

## 8.1 Mandatory Pre-Escalation Actions

| Action | Requirement |
|---|---|
| Validate severity and priority | Mandatory (reassess based on new findings) |
| Define timeline window | Mandatory (start/end in UTC; include ± context) |
| Identify affected entities | Mandatory (hosts, users, IPs, cloud resources) |
| Collect key telemetry | Mandatory (SIEM exports, EDR timelines, auth logs) |
| Preserve evidence references | Mandatory (paths/IDs; ensure tenant segregation) |
| Identify IOCs and suspected TTPs | Mandatory (even partial) |
| Document what is known vs unknown | Mandatory |
| Create hypothesis and test notes | Recommended (helps L3 focus) |

References:  
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md`

## 8.2 Stop Conditions (Escalate Immediately)

Escalate immediately if any apply:

- Active ransomware encryption
- Confirmed exfiltration
- Domain controller/identity system indicators
- Privileged credential compromise confirmed
- Active attacker interactive session confirmed
- Severe operational disruption ongoing

---

# 9. L2 → L3 Escalation Package (Mandatory Contents)

L2 must include an escalation package note in the ticket using the structure below.

## 9.1 Escalation Note Template (Mandatory)

**Escalation Summary (What + Why):**  
- `Short summary of incident and why L3 is needed`

**Current Severity / Priority:**  
- `P? – rationale (include any recent change + approval if downgrade)`

**Scope (Best Known):**  
- Hosts: `...`  
- Users/Accounts: `...`  
- Network Indicators: `IPs/domains/URLs...`  
- Cloud resources (if applicable): `tenant/subscription, role changes, keys...`

**Timeline (UTC):**  

- First seen: `...`  
- Key events: `...`  
- Last observed malicious activity: `...`

**What L2 Has Done:**  
- `Queries run, EDR checks, containment attempted, evidence collected`

**Key Findings (Confirmed vs Suspected):**  
- Confirmed: `...`  
- Suspected: `...`

**Evidence References (Must Be Clickable/Traceable):**  
- `SIEM export path/query`  
- `EDR detection IDs / timeline export`  
- `PCAP references` (if any)  
- `Log bundle hashes` (if evidence-grade)

**Requested L3 Actions (Clear Ask):**  
1. `Memory analysis for injected code and credential artifacts`  
2. `Malware triage of sample hash/file`  
3. `Disk artifact timeline to confirm persistence and entry point`  
4. `Attribution/campaign linkage (if required)`

**Constraints / Risks / Notes:**  
- `System criticality, downtime constraints, client restrictions, encryption status`

---

## 9.2 Minimum Evidence Requirements (By Scenario)

| Scenario | Minimum Evidence to Provide to L3 |
|---|---|
| Malware execution | Sample hash/path, process tree, parent process, network destinations, timeline export |
| Credential theft | Auth logs (IdP/AD), EDR telemetry around LSASS access, account list + privilege levels |
| Exfiltration | Proxy/firewall logs with bytes + destination, suspected data source paths, timeframe |
| Cloud compromise | Audit logs showing actions, affected principals/keys, resource change list |
| Lateral movement | Host-to-host connection logs, remote execution artifacts, affected systems list |

---

# 10. Escalation Execution Steps (Workflow)

## 10.1 Step-by-Step (Mandatory)

1. Update ticket with escalation package (Section 9)
2. Confirm priority and ensure SOC Lead is aware for P1/P2
3. Ensure evidence is stored in approved evidence repository and referenced in ticket
4. Assign ticket to named L3 analyst (or L3 queue per operating model)
5. Notify L3 via approved channel:
   - P1/P2: phone/on-call + chat mention + ticket assignment
   - P3/P4: ticket assignment + chat (as needed)
6. Record escalation timestamp (UTC), method, and recipient in ticket

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Escalation-Workflow.md`

---

# 11. SLA Requirements (L2 → L3)

## 11.1 Escalation Decision Time Targets

| Priority | L2 Escalation Decision Target |
|---|---:|
| P1 | Immediate |
| P2 | ≤ 1 hour |
| P3 | ≤ 4 hours |
| P4 | As needed (≤ 24 hours) |

## 11.2 L3 Acknowledgment Targets

| Priority | L3 Acknowledgment Target |
|---|---:|
| P1 | ≤ 15 minutes |
| P2 | ≤ 30 minutes |
| P3 | ≤ 2 hours |
| P4 | ≤ 4 hours |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

# 12. L3 Acknowledgment and Engagement Standards (Mandatory)

L3 must acknowledge in ticket with:

- Timestamp (UTC)
- Confirmation of ownership
- Planned actions
- Expected next update time (P1/P2)

Minimum acknowledgment format:
[YYYY-MM-DD HH:MM UTC] – [Name / L3] – Acknowledged escalation; taking ownership.
Planned actions: [1–3]. Evidence required (if any): [items]. Next update by: [time UTC].


---

# 13. Evidence Handling Requirements (During Escalation)

## 13.1 Evidence Integrity Controls

| Control | Requirement |
|---|---|
| Evidence stored in approved repository | Mandatory |
| Access restricted | Mandatory (especially P1/P2) |
| Hashing for evidence-grade packages | SHA256 mandatory |
| Chain of custody (CoC) when required | Mandatory for P1/P2 legal/regulatory sensitive cases |
| No evidence via email | Mandatory (use secure transfer only) |

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`

## 13.2 MSSP Evidence Segregation (Mandatory)

- Evidence paths must be client-specific
- Exports must not contain other client identifiers
- Access must be limited to authorized analysts for that tenant

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 14. Escalation Quality Standards (Good vs Bad)

## 14.1 Good Escalation Example (Acceptable)

- “P2 suspected credential theft: EDR telemetry shows LSASS access attempt on SRV-APP-01 at 04:10 UTC; admin user svc_backup used for interactive login; outbound to suspicious IP observed. Need L3 memory capture and analysis + disk artifact timeline to confirm persistence and entry point. Evidence: EDR IDs…, SIEM query…, log bundle hash…”

## 14.2 Poor Escalation Example (Not Acceptable)

- “Need L3. Please investigate.”

---

# 15. Dispute Handling and Rework

If L3 determines the escalation package is incomplete:

1. L3 documents missing items in ticket (specific, actionable)
2. L3 requests L2 to provide missing evidence/context
3. SOC Lead reviews recurring gaps and updates SOP/training
4. If delays impact SLA, SOC Manager notified

Reference:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`

---

# 16. Failure Handling (No L3 Response)

If L3 does not acknowledge within SLA:

1. L2 notifies SOC Lead immediately
2. SOC Lead pages alternate L3/on-call
3. For P1: ensure bridge call is active and IR Team Lead is informed
4. Document all attempts (time/method/result) in ticket

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md`

---

# 17. MSSP Multi-Tenant Requirements (Mandatory)

When escalating for MSSP clients:

| Requirement | Standard |
|---|---|
| Client ID verified in ticket | Mandatory |
| Evidence references are tenant-segregated | Mandatory |
| Client approvals required for forensics actions | Mandatory (contract-dependent) |
| Client notification requirement assessed | Mandatory for P1/P2 |
| No cross-tenant disclosure | Mandatory |

References:  
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`  
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 18. Related Documents

| Document | Path |
|---|---|
| L1 to L2 Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L1-to-L2-Escalation.md` |
| L3 to IR Team Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L3-to-IR-Team-Escalation.md` |
| Escalation Matrix – Master | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md` |
| L2 Investigation SOP | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Investigation-SOP.md` |
| L3 Advanced Forensics SOP | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Advanced-Forensics-SOP.md` |
| L3 Malware Analysis SOP | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Malware-Analysis-SOP.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| Tool Chain of Custody | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Tool-Chain-of-Custody.md` |
| Ticket Escalation Workflow | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Escalation-Workflow.md` |

---

# 19. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 28-May-2026 | SOC Lead / SOC Operations Lead | Initial version |

---

# 20. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**