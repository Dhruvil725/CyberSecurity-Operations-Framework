# L3 to IR Team Escalation

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – L3 to IR Team Escalation |
| Document ID | ESC-PATH-007 |
| Version | 1.0 |
| Effective Date | 28-May-2026 |
| Owner | IR Team Lead / SOC Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines the formal process for escalating an incident from **Level 3 (L3)** to the **Incident Response Team (IR Team)** for **major incident coordination and containment authority execution**.

L3→IR escalation is critical because:

- IR Team activation enables coordinated containment, eradication, and recovery across teams
- Major incidents require controlled decision-making, approvals, and stakeholder communications
- Evidence must be preserved correctly before actions that may alter or destroy artifacts
- Regulatory readiness (RBI/CERT-In or others) often depends on early IR involvement
- MSSP environments require tenant-safe execution and client approvals for impactful actions
- Audit readiness requires clear records of activation triggers, timelines, and authority

This SOP ensures:

- Clear triggers for IR Team activation
- Standard escalation package (incident brief + evidence + action requests)
- SLA-aligned activation and acknowledgment targets
- Controlled containment authority alignment (who can do what, when)
- Strong documentation and evidence traceability throughout the escalation

---

# 3. Scope

This SOP applies to escalation from L3 to IR Team for:

| Incident Type | Examples |
|---|---|
| Active compromise | Attacker interactive session, confirmed C2 at scale |
| Ransomware | Encryption, staging, mass file modifications |
| Data breach/exfiltration | Confirmed sensitive data access or transfer |
| Domain/privileged compromise | DA takeover, DC compromise, DCSync |
| Supply chain | Signed malware, compromised vendor tooling |
| Zero-day exploitation | Active exploitation of unknown/unpatched vulnerability |
| Cloud compromise | Root/API key compromise, mass resource changes |
| Multi-system incidents | Multiple hosts, segments, or client environments impacted |

Out of scope:

- Routine L3 investigations that do not require containment authority or crisis coordination
- Client-only incident command processes (unless contract places IR command with MSSP)

References:  
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Activation-Criteria.md`  
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md`

---

# 4. Definitions

| Term | Definition |
|---|---|
| IR Team | Dedicated incident response team responsible for coordinated containment/eradication/recovery |
| Activation | Formal engagement of IR Team with incident command structure |
| Incident Commander | Person leading incident response decisions (typically IR Team Lead for major incidents) |
| Containment authority | Approved right to isolate systems, disable accounts, block traffic, etc. |
| Major incident | Incident requiring coordinated response across multiple teams and leadership |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| L3 Analyst | Confirms escalation trigger; prepares escalation brief; preserves/links evidence; initiates escalation |
| IR Team Lead (Incident Commander) | Acknowledges activation; directs containment strategy; coordinates recovery; ensures governance |
| SOC Lead | Coordinates SOC resources; ensures ticket updates, SLA, and bridge call support |
| SOC Manager | Management coordination; ensures resourcing; supports executive escalation |
| Compliance/Legal (as needed) | Regulatory assessment, legal hold, law enforcement engagement |
| IT Ops / Network / Cloud Leads | Execute containment and recovery tasks as directed |
| MSSP SDM (if MSSP) | Client communication, approvals, and SLA compliance |
| Evidence Custodian | Secure storage, access control, CoC records and transfers |

References:  
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

# 6. Escalation Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Escalate on confirmation of compromise | Do not wait for full RCA before activating IR for P1/P2 |
| Preserve evidence before disruption | Capture volatile data/logs where feasible before isolation/shutdown |
| Provide a clear ask | IR escalation must specify what decision/action is needed |
| Single source of truth | Ticket must reflect real-time status; bridge call notes must be linked |
| Authority-based containment | Actions must follow containment authority matrix |
| Tenant-safe operations (MSSP) | Confirm tenant scope; do not mix evidence or communications across clients |
| Explicit timelines | Include “last known good,” “first seen,” and “last observed” timestamps (UTC) |

---

# 7. IR Activation Triggers (When L3 Must Escalate)

L3 must activate IR Team when any of the following applies.

## 7.1 Mandatory Activation Triggers (Do Not Delay)

| Trigger | Examples |
|---|---|
| P1 declared or strongly suspected | Ransomware encryption, DC compromise |
| Confirmed active attacker presence | Interactive shells, remote tool usage, confirmed beaconing |
| Confirmed data breach/exfiltration | Exfil tool observed, large outbound transfers confirmed malicious |
| Domain/privileged compromise confirmed | DA compromise, DCSync, golden ticket indicators |
| Multi-system spread | Multiple hosts/subnets impacted in short window |
| Critical system impacted | Identity, payment, core banking, production ERP |
| Immediate containment decisions needed | Need to isolate segments, shut services, mass credential resets |
| Regulatory reporting likely | RBI/CERT-In reportability threshold likely met |
| Client incident requires IR command (MSSP) | Contract requires major incident handling |

## 7.2 Conditional Activation Triggers

| Trigger | Examples |
|---|---|
| Persistent intrusion suspected | Evidence of long dwell time, multiple footholds |
| Supply chain suspicion | Trusted update channel compromised |
| Zero-day suspicion | Exploit behavior without known CVE, rapid containment needed |
| Significant reputational risk | Public claim of breach, extortion emails |

---

# 8. SLA Targets (L3 → IR Activation)

| Activity | Target Time |
|---|---:|
| L3 escalation decision (P1) | Immediate |
| IR Team Lead notified (P1) | ≤ 15 minutes |
| IR Team acknowledgment (P1) | ≤ 15 minutes |
| IR Team lead assumes command | ≤ 30 minutes |
| Bridge call active (P1) | ≤ 30 minutes |

For P2 with containment need:

- Notify IR Team Lead: **≤ 30 minutes**
- Acknowledgment: **≤ 30 minutes**

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

# 9. Pre-Escalation Requirements (L3 Minimum)

Before escalation (or in parallel for P1), L3 must ensure:

## 9.1 Mandatory Minimum Checks

| Check | Requirement |
|---|---|
| Confirm incident severity basis | Mandatory |
| Confirm affected assets/users | Mandatory (best known) |
| Confirm suspected entry vector | Recommended (if known) |
| Confirm evidence references exist | Mandatory (EDR/SIEM/log exports) |
| Confirm “first seen” and “last seen” in UTC | Mandatory |
| Confirm containment already executed (if any) | Mandatory |
| Confirm any active attacker activity | Mandatory (yes/no/unknown) |

## 9.2 Evidence Preservation (Best Effort, Priority-Driven)

For P1/P2 escalation, capture or initiate collection of:

- EDR timeline exports and detections
- SIEM raw events and correlation context
- Identity logs (AD/IdP/MFA logs)
- Firewall/proxy/DNS logs for malicious destinations
- Network capture (PCAP) if exfiltration suspected (if feasible)
- Memory capture if credential theft/in-memory execution suspected (if feasible)

References:  
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Memory-Acquisition-SOP.md`  
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Log-Collection-SOP.md`  
`04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Capture-SOP.md`

---

# 10. L3 → IR Escalation Package (Mandatory Contents)

L3 must add a structured escalation note to the ticket and notify IR Team Lead via approved channels.

## 10.1 Escalation Note Template (Mandatory)

**IR Activation Request:**  
- `Request IR Team activation for INC-[ID] due to: [trigger(s)]`

**Severity / Priority:**  
- `P1/P2 – rationale`

**Incident Summary (Executive-Friendly, 3–6 lines):**  
- `What happened, where, and current impact`

**Scope (Best Known):**  
- Hosts: `...`  
- Users/Accounts: `...`  
- Critical systems: `...`  
- Network/Cloud resources: `...`  

**Timeline (UTC):**  
- First seen: `...`  
- Detection time: `...`  
- Containment started: `...` (if any)  
- Last observed malicious activity: `...`

**Confirmed vs Suspected:**  
- Confirmed: `...`  
- Suspected: `...`

**Key Evidence References:**  
- SIEM: `query/export link + time window`  
- EDR: `detection IDs + timeline export link`  
- Network: `firewall/proxy logs + PCAP link (if any)`  
- Cloud/IdP: `audit log export link`  
- Evidence hashes: `SHA256 (if evidence-grade bundles)`  

**Actions Taken So Far:**  
- `Host isolated, account disabled, firewall block applied, etc.`  
- Include: executed by, authorized by, time (UTC)

**Immediate Risks:**  
- `Lateral movement risk, exfil risk, ransomware spread risk, outage risk`

**Requested IR Decisions / Actions (Clear Ask):**  
1. `Approve containment actions (list)`  
2. `Approve forensic collection scope (memory/disk/logs)`  
3. `Approve stakeholder notifications (management/client/regulatory readiness)`  

**Constraints / Business Impact Notes:**  
- `Criticality, downtime constraints, client restrictions, change window`

---

## 10.2 Minimum Evidence Requirements for IR Activation

| Scenario | Minimum Evidence to Provide |
|---|---|
| Ransomware | Host list impacted, ransomware note indicators, encryption events, process tree evidence, spread indicators |
| Data exfiltration | Destination(s), bytes/volume, timeframe, source host(s), authentication context, evidence of staging |
| Domain compromise | DC logs, privileged account evidence, EDR telemetry on DC, suspicious replication/auth events |
| Cloud compromise | Audit log actions, affected principals, key/token evidence, resource changes, IP/location context |
| Supply chain | Vendor update evidence, signed binary details, affected systems, initial infection chain evidence |

---

# 11. Escalation Execution Steps (Workflow)

## 11.1 Step-by-Step (Mandatory)

1. Confirm P1/P2 priority and notify SOC Lead (if not already engaged)
2. Update ticket with IR escalation package (Section 10)
3. Assign or link ticket to IR Team queue (as per tool workflow)
4. Notify IR Team Lead:
   - P1: **phone/on-call** + war room mention + ticket assignment
   - P2: phone/chat + ticket assignment (based on urgency)
5. Start/confirm bridge call (P1 mandatory)
6. Document:
   - Notification time (UTC)
   - Recipient and method
   - Acknowledgment time (UTC)
7. Maintain update cadence until IR Team assumes command

References:  
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Escalation-Workflow.md`  
`03_SOC-TIER-PROCEDURES/03.4_SOC-Lead-Procedures/SOCLead-P1-P2-Bridge-Call-SOP.md`

---

# 12. IR Team Acknowledgment Requirements (Mandatory)

IR Team Lead must acknowledge in ticket:

- Activation accepted (Yes/No)
- Incident commander assigned
- Immediate next actions and priorities
- Next update time (UTC)

Minimum acknowledgment format:
[YYYY-MM-DD HH:MM UTC] – [Name / IR Team Lead] – IR activated; assuming incident command.
Immediate actions: [1–3]. Evidence requests: [items]. Next update by: [time UTC].


---

# 13. Containment Authority and Approval Controls (Mandatory)

All containment actions initiated after IR activation must follow the containment authority matrix.

Minimum requirements:

| Action | Must Record in Ticket |
|---|---|
| Host isolation | executed by, authorized by, time (UTC), outcome |
| Account disable/reset | executed by, authorized by, time (UTC), outcome |
| Firewall blocks | rule ID/object, executed by, authorized by, time (UTC), expiry |
| Segmentation/quarantine | scope, executed by, authorized by, time (UTC), rollback plan |
| Service shutdown | business owner decision, time (UTC), rollback plan |

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

# 14. Evidence and Chain-of-Custody Requirements

## 14.1 CoC Trigger Conditions

Chain of custody is mandatory when:

- P1 incidents
- Potential legal/regulatory action
- Insider threat cases involving HR/legal
- Client contract requires forensic-grade evidence handling

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md`

## 14.2 Evidence Handling Rules (Mandatory)

- Evidence stored only in approved evidence repository
- Access restricted to IR/forensics personnel as required
- SHA256 hashes recorded for evidence-grade packages
- No evidence sharing via email or non-approved channels

---

# 15. MSSP Client Requirements (Mandatory)

For MSSP escalations:

## 15.1 Tenant Verification (Mandatory)

Before IR executes impactful actions:

- Confirm correct client tenant scope
- Confirm client approvals required for containment/forensics actions
- Confirm client communication obligations and contacts
- Confirm evidence segregation and export restrictions

References:  
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md`  
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

## 15.2 Client Approval Documentation

If client approval is required:

- Record request time (UTC)
- Record client contact (name/role)
- Record approval/denial and constraints
- Record action executed after approval

---

# 16. Failure Handling (IR Unreachable / Delayed Acknowledgment)

If IR Team does not acknowledge within SLA:

1. L3 notifies SOC Lead immediately
2. SOC Lead pages backup IR on-call
3. If still no response:
   - SOC Manager notified
   - CISO notified (P1)
4. For P1: continue containment under containment authority matrix if allowed
5. Document all attempts (time/method/result) in ticket

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md`

---

# 17. Common Mistakes and Controls

| Mistake | Risk | Control |
|---|---|---|
| Escalating without clear trigger | Delays and confusion | Use trigger list and document rationale |
| No clear “ask” to IR | Inefficient activation | Mandatory requested actions section |
| Missing evidence references | Rework and delay | Provide minimum evidence package |
| Containment executed without authorization | Compliance risk | Follow containment authority matrix |
| Evidence lost due to premature isolation | Forensic gaps | Preserve volatile evidence best effort |
| Cross-client evidence mixing (MSSP) | Compliance breach | Tenant verification + segregation controls |

---

# 18. Related Documents

| Document | Path |
|---|---|
| Emergency Escalation – P1 | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Emergency-Escalation-P1.md` |
| IR Team to Management Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/IR-Team-to-Management-Escalation.md` |
| Escalation Matrix – Master | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md` |
| L2 to L3 Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L2-to-L3-Escalation.md` |
| IRT Activation Criteria | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Activation-Criteria.md` |
| IRT Containment Authority Matrix | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| Disk Acquisition SOP | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Disk-Acquisition-SOP.md` |
| Memory Acquisition SOP | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Memory-Acquisition-SOP.md` |
| Internal-to-MSSP Escalation | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Internal-to-MSSP-Escalation.md` |

---

# 19. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 28-May-2026 | IR Team Lead / SOC Lead | Initial version |

---

# 20. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**