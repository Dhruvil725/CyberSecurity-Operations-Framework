# SOP: Network Capture (PCAP) Procedure

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – Network Capture (PCAP) Procedure |
| Document ID | TOOL-FW-004 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | Network Security Lead / SOC Operations Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines the standardized procedure for performing network traffic captures (PCAP) to support security investigations, incident response, threat hunting, and forensic evidence preservation.

Network captures are critical because:

- They provide ground-truth evidence of network communications (C2, exfiltration, scanning)
- They support attribution of attacker infrastructure and methods
- They enable validation of IDS/IPS alerts and firewall logs
- They are frequently required as audit evidence for incident handling
- Mishandled captures can expose sensitive data and create compliance risk
- MSSP environments require strict tenant separation and controlled access

This SOP ensures:

- A controlled process for requesting and executing PCAP
- Proper scope definition and data minimization
- Safe capture methods that do not disrupt operations
- Correct handling, storage, and chain-of-custody where required
- Audit-ready documentation and evidence traceability
- Clear escalation steps and approvals for high-impact captures

---

# 3. Scope

This SOP applies to network capture activities across:

| Area | Included |
|---|---|
| Capture locations | Perimeter, DMZ, internal segments, data center, cloud (where supported), endpoint (if applicable) |
| Capture methods | SPAN/mirror ports, TAPs, firewall capture, IDS sensor capture, host-based capture |
| Use cases | Investigations (SIEM/EDR/IDS alerts), incident response, data exfil validation, malware traffic analysis |
| Environments | Internal SOC and MSSP-managed client environments |
| Evidence handling | PCAP storage, evidence logging, CoC (if required) |

Out of scope:

- Full packet forensic analysis methodology (covered by L2/L3 procedures)
- Long-term continuous packet capture solutions (handled as separate capability)

---

# 4. Definitions

| Term | Definition |
|---|---|
| PCAP | Packet Capture file containing network traffic |
| SPAN | Switch Port Analyzer (port mirroring) |
| TAP | Network Test Access Point (hardware traffic replication) |
| Capture filter | BPF filter to limit captured traffic |
| Evidence | Data preserved for investigation and audit/legal needs |
| CoC | Chain of Custody documentation for evidence integrity |
| Tenant | Client environment in MSSP multi-tenant operations |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| L1 Analyst | Create ticket; request capture; record initial context |
| L2 Analyst | Define capture scope/filters; analyze outputs; document findings |
| L3 Analyst | Forensic-grade capture guidance; advanced analysis; evidence validation |
| SOC Lead | Approve capture in P1/P2; coordinate bridge call; ensure SLA alignment |
| Network Security Engineer | Execute capture (SPAN/TAP/firewall capture); ensure minimal disruption |
| IR Team Lead | Approve forensic evidence capture; guide CoC requirements |
| SOC Manager | Oversight for high-risk/sensitive captures |
| MSSP Service Delivery | Coordinate client approvals and communications |

References:  
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Network-Evidence-SOP.md`

---

# 6. Network Capture Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Purpose-driven | Capture only what is needed for investigation |
| Minimize sensitive exposure | Use filters; limit duration; restrict access |
| Do not disrupt production | Avoid overload; coordinate change windows when needed |
| Preserve integrity | Record hashes and handling steps where evidence-grade |
| Document everything | Capture parameters must be recorded in ticket |
| Tenant segregation (MSSP) | Captures and storage must not mix clients |
| Legal/regulatory aware | Some captures may include sensitive/regulated data |

---

# 7. Capture Request Triggers

Network captures may be requested when:

| Trigger | Examples |
|---|---|
| Suspected C2 communication | Beaconing to suspicious IP/domain |
| Suspected data exfiltration | Large outbound transfer to unknown destination |
| IDS/IPS alert validation | Confirm exploit attempts and payloads |
| Malware behavior analysis | Confirm download, callbacks, encryption, lateral movement |
| DDoS investigation | Validate traffic patterns and sources |
| Lateral movement analysis | East-west traffic validation between zones |
| Regulatory/audit evidence | Preserve proof of communication and response actions |

---

# 8. Ticket Requirements (Mandatory)

Every capture must be tracked in a ticket.

Mandatory ticket fields:

| Field | Requirement |
|---|---|
| Incident/ticket reference | Mandatory |
| Reason for capture | Mandatory |
| Scope definition | Src/Dst IPs, ports, segments, interfaces |
| Capture method | SPAN/TAP/firewall/IDS/host-based |
| Capture start/end time (UTC) | Mandatory |
| Filter (BPF) | Mandatory (or justification if none) |
| Expected output location | Mandatory |
| Access restrictions | Mandatory (who can access) |
| Evidence classification | Mandatory (confidential/restricted) |
| CoC required? | Mandatory (Yes/No with rationale) |
| Approvals | Mandatory for sensitive/high-risk captures |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

# 9. Approval Requirements

## 9.1 Standard Captures

| Capture Type | Approval |
|---|---|
| Short duration, filtered capture on non-critical segment | L2 + SOC Lead |
| Capture involving sensitive segments (finance/core/PCI) | SOC Lead + SOC Manager |
| Capture requiring network config change (SPAN/TAP) | Network Security Lead |

## 9.2 Emergency Captures (P1/P2)

Emergency captures may be executed immediately if required for containment/investigation, but must be:

- Authorized by SOC Lead / IR Team Lead
- Documented in the ticket within 30–60 minutes

## 9.3 MSSP Captures (Client Environments)

| Condition | Requirement |
|---|---|
| Client approval required by contract | Mandatory before capture (unless P1 emergency clause exists) |
| Capture includes client regulated data | Mandatory compliance check |
| Storage location | Must be tenant-segregated |

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 10. Capture Planning (Mandatory)

Before capture execution, define:

## 10.1 Scope

| Item | Examples |
|---|---|
| Source | Host IP, subnet, VLAN |
| Destination | External IP/domain, internal server |
| Direction | Inbound/outbound/lateral |
| Protocols | TCP/UDP/ICMP/DNS/HTTP(S) |
| Time window | Start/end (UTC) |
| Duration | 5–15 min short; longer only if required |
| Sensor/interface | Firewall interface, switch port, IDS sensor |

## 10.2 Data Minimization (Mandatory)

- Use BPF filters whenever possible
- Avoid capturing unrelated traffic
- Prefer metadata logs if PCAP not strictly required
- Consider capturing headers-only when possible (platform dependent)

---

# 11. Capture Execution Procedures

> Use the method that matches your environment. Always document the chosen method and parameters.

## 11.1 Method A — Firewall Built-in Packet Capture (Generic)

Use when firewall supports packet capture on interfaces.

Steps:

1. Confirm interface and direction
2. Configure capture filter (src/dst IP, port, protocol)
3. Start capture and record start time (UTC)
4. Run for defined duration
5. Stop capture and export PCAP securely
6. Validate file integrity (hash if evidence-grade)
7. Store PCAP in evidence repository and reference in ticket

---

## 11.2 Method B — Switch SPAN / Port Mirroring

Use when capturing traffic for a specific host/port/VLAN.

Steps:

1. Identify target switch and port/VLAN
2. Identify collector port connected to capture host
3. Create SPAN session (source → destination)
4. Start capture on collector host
5. Monitor switch/collector performance (avoid saturation)
6. Stop capture, disable SPAN session immediately
7. Export PCAP and document changes in ticket

Mandatory:
- Disable SPAN after capture to avoid unintended monitoring exposure

---

## 11.3 Method C — Network TAP Capture

Use for high reliability captures where TAP exists.

Steps:

1. Identify TAP point and capture interface
2. Start capture with filter and time window
3. Stop capture; export PCAP; record times and interface details
4. Preserve evidence and document in ticket

---

## 11.4 Method D — IDS Sensor Capture

Use when IDS supports packet logging for alerts.

Steps:

1. Identify alert/event requiring packet extraction
2. Export packet logs/pcap segment related to alert
3. Preserve export and link to alert/ticket evidence

---

## 11.5 Method E — Host-Based Capture (Endpoint/Server)

Use when network-level capture is not available.

Steps:

1. Confirm authorization (sensitive systems require approval)
2. Run capture for defined interface and filter
3. Stop capture; transfer securely to evidence repository
4. Record command, filters, and time range in ticket

---

# 12. Filters (BPF) — Standard Examples

> Use as guidance; adapt to environment.

- Capture traffic to/from a specific IP:
  - `host 185.220.101.10`

- Capture outbound HTTPS to a destination:
  - `dst host 185.220.101.10 and tcp port 443`

- Capture DNS queries from a host:
  - `src host 10.10.5.12 and udp port 53`

- Capture SMB traffic (lateral movement):
  - `tcp port 445`

- Exclude internal noise (example):
  - `not net 10.0.0.0/8`

Mandatory:
- Record the exact filter used in the ticket

---

# 13. Evidence Handling and Storage

## 13.1 Evidence Classification

PCAP files may include credentials, PII, financial data, or proprietary information.

Minimum handling requirements:

- Store only in approved evidence repository
- Restrict access to authorized personnel
- Encrypt at rest and in transit
- Avoid email or unsecured file sharing

## 13.2 Chain of Custody (When Required)

CoC is required when:

- Incident is P1 with potential legal/regulatory action
- Law enforcement may be involved
- Client contract requires forensic-grade handling
- Evidence may be used in disciplinary actions (insider cases)

CoC steps (minimum):

1. Record collector name/time/tool/method
2. Compute hash (SHA256 recommended)
3. Store in secure evidence location
4. Record transfers with timestamps and recipients

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`

---

# 14. Analysis Handoff Requirements

If the capture is executed by Network Security Engineer, handoff to L2/L3 must include:

| Item | Requirement |
|---|---|
| Capture method and location | Mandatory |
| Interface/port/VLAN details | Mandatory |
| Start/end time (UTC) | Mandatory |
| Filter used | Mandatory |
| PCAP file path | Mandatory |
| Hash (if computed) | Mandatory where evidence-grade |
| Any anomalies during capture | Recommended |

---

# 15. SLA Targets (Guidance)

| Priority | Capture Start Target | Notes |
|---|---:|---|
| P1 | ≤ 30 minutes | Execute immediately if needed for containment |
| P2 | ≤ 2 hours | Coordinate with IR/SOC Lead |
| P3 | ≤ 8 hours | Schedule if change window required |
| P4 | ≤ 72 hours | Routine |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

# 16. MSSP Client Requirements (Mandatory)

For MSSP captures:

| Requirement | Standard |
|---|---|
| Tenant/client ID tagged | Mandatory |
| Client approval documented (if required) | Mandatory |
| Evidence stored in client-specific location | Mandatory |
| No cross-client data in capture files | Mandatory (scope carefully) |
| Client communication recorded | Mandatory where required |

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 17. Common Mistakes and Controls

| Mistake | Risk | Control |
|---|---|---|
| Capturing without filter | Excess sensitive data | Filters mandatory |
| Capturing too long | Storage + privacy risk | Time-box captures |
| Forgetting to disable SPAN | Continuous monitoring exposure | Post-capture checklist |
| Storing PCAP on analyst desktop | Evidence loss | Use evidence repository only |
| No timestamps | Audit failure | UTC timing mandatory |
| Cross-tenant capture (MSSP) | Compliance breach | Tenant scoping controls |

---

# 18. Related Documents

| Document | Path |
|---|---|
| Firewall Block Request SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Block-Request-SOP.md` |
| Firewall Rule Change Process | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Rule-Change-Process.md` |
| Network Isolation Procedure | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Isolation-Procedure.md` |
| IDS/IPS Tuning Guide | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/IDS-IPS-Tuning-Guide.md` |
| Network Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Network-Evidence-SOP.md` |
| Evidence Storage Policy | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md` |
| CoC Digital Evidence | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md` |
| Ticket Lifecycle SOP | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md` |

---

# 19. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 25-May-2026 | Network Security Lead / SOC Operations Lead | Initial version |

---

# 20. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**