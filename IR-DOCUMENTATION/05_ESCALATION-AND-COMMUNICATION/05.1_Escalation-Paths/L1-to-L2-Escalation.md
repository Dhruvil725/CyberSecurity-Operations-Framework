# L1 to L2 Escalation

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – L1 to L2 Escalation |
| Document ID | ESC-PATH-005 |
| Version | 1.0 |
| Effective Date | 28-May-2026 |
| Owner | SOC Operations Lead / SOC Lead |
| Approved By | SOC Manager |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines the standard process for escalating security alerts and tickets from **Level 1 (L1) SOC Analysts** to **Level 2 (L2) SOC Analysts**.

L1→L2 escalation is critical because:

- L2 investigations require stronger evidence packaging and clarity of handoff
- Incorrect escalation creates delays, duplicated work, and SLA breaches
- Missed escalation can result in undetected compromise and increased attacker dwell time
- Audit readiness requires a documented ownership transfer and decision rationale
- MSSP operations require tenant-accurate, client-safe handoffs

This SOP ensures:

- Clear triggers for escalation
- Minimum investigation expectations for L1 before escalation
- Standard escalation package (what L2 must receive)
- SLA-aligned acknowledgment and response targets
- Audit-ready documentation in the ticketing system

---

# 3. Scope

This SOP applies to L1-to-L2 escalation for:

| Ticket Type | Examples |
|---|---|
| SIEM alerts | Suspicious auth, impossible travel, anomalous DNS/proxy |
| EDR alerts | Malware detection, suspicious process chains, persistence indicators |
| User/client reported incidents | Phishing clicks, suspected compromise |
| Threat intel matches | High-confidence IoC seen in client telemetry |
| Hunting outputs (initial) | L1 findings requiring validation/scope |

Out of scope:

- L2 to L3 escalation (separate SOP)
- False positive closure standards (covered in L1 procedures and ticket SOP)
- IR Team activation (covered in L3→IR escalation SOP and P1 escalation)

References:  
`03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Alert-Handling-SOP.md`  
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`

---

# 4. Definitions

| Term | Definition |
|---|---|
| Escalation | Formal handoff of a ticket for deeper investigation |
| Acknowledgment | L2 confirms receipt and takes ownership of the ticket |
| TP | True Positive (malicious/confirmed suspicious activity) |
| FP | False Positive (benign activity) |
| Suspected TP | Not fully confirmed but risk is high enough to require L2 |
| Evidence package | Structured set of notes, artifacts, queries, and context supporting escalation |
| SLA | Escalation time targets and response commitments |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| L1 Analyst | Triage, initial validation, documentation, severity proposal, escalation package creation |
| L2 Analyst | Acknowledge escalation, assume ownership, deepen investigation, update scope and severity |
| SOC Lead | Oversight of escalation quality, SLA monitoring, dispute resolution, P1/P2 coordination |
| SOC Manager | Escalation governance, quality review, SLA breach management |
| MSSP SDM (if MSSP) | Ensures correct client scoping and client notification requirements are met |

Reference:
`00_GOVERNANCE/00.3_Roles-and-Responsibilities/RACI-Matrix-IR.xlsx`

---

# 6. Escalation Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Escalate with evidence | Escalation must include concrete observations and references |
| Do not over-triage | L1 must not spend excessive time if risk is high—escalate early |
| Ownership must be explicit | Ticket must be reassigned to a named L2 owner |
| SLA clock continues | Escalation does not reset SLAs |
| Clear FP/TP reasoning | If L1 believes FP, closure must be justified; if unsure, escalate |
| Tenant-safe (MSSP) | Verify client/tenant before escalation and evidence linking |

---

# 7. Escalation Triggers (When L1 Must Escalate)

L1 must escalate to L2 when any of the following applies.

## 7.1 Mandatory Escalation Triggers (Do Not Delay)

| Trigger | Examples |
|---|---|
| Priority is P1 or P2 | Any suspected critical/high incident |
| Privileged account involved | Admin/Domain Admin/Global Admin suspicious activity |
| Multiple alerts correlated | Same user/host across multiple detections in short period |
| Malware indicators present | EDR malware/quarantine + suspicious process tree |
| Lateral movement suspected | SMB/WMI/PSRemoting, multiple hosts contacted |
| Data exfiltration suspected | Large outbound transfer, unusual cloud downloads |
| Credential compromise suspected | MFA fatigue, impossible travel + token anomalies |
| Evidence preservation needed | Need log export, memory capture, disk imaging decision |
| L1 uncertainty remains | Cannot confidently classify as FP/benign |

## 7.2 Conditional Escalation Triggers

| Trigger | Examples |
|---|---|
| Repeated P3 alerts for same entity | Same host/user shows recurring suspicious behavior |
| IOC match requires validation | Medium confidence TI match needs scoping |
| Client requests deeper investigation | MSSP client asks for advanced analysis |

---

# 8. L1 Pre-Escalation Checklist (Minimum Triage Standard)

Before escalating, L1 must complete these steps **unless doing so would delay urgent containment**.

## 8.1 Mandatory Checks (Minimum)

| Check | Requirement |
|---|---|
| Verify alert details | Confirm rule name, time, source, key fields |
| Identify affected entities | Hostname/IP/user/account/application |
| Check asset criticality | Critical/High/Medium/Low |
| Check user privilege | Standard/Privileged/Admin |
| Review related alerts | Same entity ±24 hours (or per SOP) |
| Quick EDR/SIEM pivot | Process tree / auth pattern / network destination |
| Decide severity proposal | P1/P2/P3/P4 with rationale |

Reference:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

## 8.2 Stop Conditions (Escalate Immediately)

Escalate immediately without completing all checks if:

- Ransomware indicators exist
- Domain controller/identity system involved
- Exfiltration evidence appears
- Business outage is ongoing
- Privileged account is actively compromised

---

# 9. L1 → L2 Escalation Package (Mandatory Contents)

Before assigning/escalating, L1 must add an escalation note to the ticket using the structure below.

## 9.1 Escalation Note Template (Mandatory)

**Escalation Summary (1–3 lines):**  
- `What happened + why this needs L2`

**Severity Proposal:**  
- `P? – rationale`

**Entities:**  
- Host(s): `...`  
- User(s): `...`  
- IP(s)/Domain(s): `...`  

**Timeline (UTC):**  
- Detection: `...`  
- Key events: `...`  

**What L1 Checked:**  
- `SIEM query/runbook steps, EDR checks performed, related alerts checked`

**Key Findings:**  
- `Observed behaviors, suspicious parent/child process, unusual auth, destinations`

**Evidence References:**  
- `Alert IDs, query links, screenshots, EDR detection IDs, file hashes`

**Recommended Next Steps for L2:**  
- `Scope expansion ideas, hunting pivots, containment considerations`

## 9.2 Minimum Evidence References (By Source)

| Source | Minimum Evidence |
|---|---|
| SIEM | Rule name, event IDs, query used, time window |
| EDR | Detection ID, process tree snapshot, file hash/path, network connections |
| Email/Phishing | Email headers, sender, URLs, user action (clicked/submitted) |
| Cloud | Audit log event IDs, affected account, actions performed |
| Network | Firewall/proxy logs, destination, bytes transferred |

---

# 10. Escalation Execution Steps (Workflow)

## 10.1 Step-by-Step (Mandatory)

1. Update ticket with escalation package note (Section 9)
2. Set/confirm severity and priority
3. Attach/link evidence artifacts in tenant-safe evidence storage
4. Assign ticket to named L2 analyst (or L2 queue per operations model)
5. Notify L2 via approved channel:
   - P1/P2: phone/on-call + chat mention + ticket assignment
   - P3/P4: ticket assignment + chat (as needed)
6. Record escalation time (UTC) and notification method in ticket

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Escalation-Workflow.md`

---

# 11. SLA Requirements (L1 → L2)

## 11.1 Escalation Decision Time Targets

| Priority | L1 Escalation Decision Target |
|---|---:|
| P1 | Immediate |
| P2 | ≤ 30 minutes |
| P3 | ≤ 2 hours |
| P4 | ≤ 4 hours (if escalation needed) |

## 11.2 L2 Acknowledgment Targets

| Priority | L2 Acknowledgment Target |
|---|---:|
| P1 | ≤ 15 minutes |
| P2 | ≤ 30 minutes |
| P3 | ≤ 2 hours |
| P4 | ≤ 4 hours |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

# 12. L2 Acknowledgment and Ownership Transfer (Mandatory)

L2 must:

- Acknowledge in ticket with timestamp (UTC)
- Confirm ownership by updating “Assigned To”
- Confirm next planned action and expected next update time (P1/P2)

Minimum L2 acknowledgment note:
[YYYY-MM-DD HH:MM UTC] – [Name / L2] – Acknowledged escalation. Taking ownership.
Next steps: [1–3 actions]. Next update by: [time UTC].


---

# 13. Escalation Quality Standards (Good vs Bad)

## 13.1 Good Escalation Example

- “EDR detected encoded PowerShell spawned by WINWORD.EXE on FIN-WS-12 at 03:14 UTC. User jsmith. Outbound to suspicious IP observed in proxy logs. No other hosts seen yet. Proposed P2. Evidence: EDR detection ID…, SIEM query…, proxy log export…”

## 13.2 Poor Escalation Example (Not Acceptable)

- “Looks suspicious. Please check.”

---

# 14. Misclassification and Dispute Handling

If L2 believes escalation was unnecessary or incomplete:

1. L2 documents missing items in ticket
2. L2 requests additional info from L1 (do not bounce ticket without note)
3. SOC Lead reviews patterns (training/tuning needs)
4. If repeated: create improvement action (training, runbook updates)

Reference:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

---

# 15. Failure Handling (No L2 Response)

If L2 does not acknowledge within SLA:

1. L1 notifies SOC Lead immediately
2. SOC Lead assigns alternate L2 or escalates to SOC Manager
3. For P1: initiate bridge call if not already active
4. Document all attempts (time/method) in ticket

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md`

---

# 16. MSSP Multi-Tenant Requirements (Mandatory)

When escalating for MSSP clients:

| Requirement | Standard |
|---|---|
| Client ID present and verified | Mandatory |
| Evidence links are tenant-segregated | Mandatory |
| No cross-client details in notes | Mandatory |
| Client notification requirement assessed | Mandatory for P1/P2 |
| Client instructions recorded | Mandatory if client actions required |

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`  
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`

---

# 17. Related Documents

| Document | Path |
|---|---|
| Ticket Escalation Workflow | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Escalation-Workflow.md` |
| Ticket Lifecycle SOP | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md` |
| Ticket Fields Standards | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md` |
| Severity Classification Guide | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md` |
| Escalation Matrix – Master | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md` |
| L1 Alert Handling SOP | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Alert-Handling-SOP.md` |
| L2 Investigation SOP | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Investigation-SOP.md` |
| Internal-to-MSSP Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md` |

---

# 18. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 28-May-2026 | SOC Operations Lead / SOC Lead | Initial version |

---

# 19. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**