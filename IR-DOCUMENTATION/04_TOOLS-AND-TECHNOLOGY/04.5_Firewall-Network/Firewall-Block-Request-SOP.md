# SOP: Firewall Block Request

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – Firewall Block Request |
| Document ID | TOOL-FW-001 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | Network Security Lead / SOC Operations Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines the standard process to request, validate, approve, implement, verify, document, and roll back firewall blocks initiated due to security alerts, confirmed incidents, threat intelligence (TI), or operational risk mitigation.

Firewall blocks are high-impact actions because:

- Incorrect blocks can disrupt business services and client connectivity
- Unvalidated IoCs (IPs/domains/URLs) can create false positives and outages
- Regulatory and audit readiness requires documented approvals and evidence
- MSSP environments require strict client scoping and segregation
- Emergency blocks must be controlled but fast for active attacks

This SOP ensures:

- Consistent request format and required fields
- Risk-based validation and approval workflow
- Safe implementation with rollback planning
- Audit-ready records (who/what/when/why)
- SLA-aligned execution for P1/P2 incidents
- Tenant-safe deployment for MSSP clients

---

# 3. Scope

This SOP applies to firewall block actions across:

| Area | Included |
|---|---|
| Technologies | Perimeter firewalls, internal segmentation firewalls, cloud security groups (where managed) |
| Block types | IP blocks, port/protocol blocks, geo/ASN blocks (if used), egress restrictions |
| Trigger types | SIEM alerts, EDR investigations, TI IoC matches, incident response containment |
| Environments | Internal SOC operations and MSSP-managed client environments |
| Change type | Emergency (P1/P2) and standard (planned) firewall rule changes |

Out of scope:

- Long-term firewall architecture redesign
- Routine non-security network change management (unless tied to security risk)

---

# 4. Definitions

| Term | Definition |
|---|---|
| Block request | A formal request to deny traffic based on a security requirement |
| IoC | Indicator of Compromise (IP/domain/URL/hash etc.) |
| Egress block | Blocking outbound traffic from internal to external destinations |
| Ingress block | Blocking inbound traffic from external to internal destinations |
| Segmentation block | Blocking lateral/internal traffic between zones |
| Emergency change | Security-driven change required to stop active threat activity |
| Rollback | Reverting a firewall change to restore prior state |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| L1 Analyst | Create ticket; capture IoC(s) and evidence; route to SOC Lead |
| L2 Analyst | Validate IoC context; scope impacted assets; recommend block type |
| SOC Lead | Confirm severity; approve routing; coordinate bridge call for P1/P2 |
| Network Security Engineer / Firewall Admin | Implement rule; verify; document change; execute rollback if needed |
| IR Team | Authorize containment actions for P1/P2; ensure evidence preservation |
| SOC Manager | Oversight; approve high-risk blocks; ensure SLA compliance |
| MSSP Service Delivery | Confirm client approvals and communication requirements |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`  
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

# 6. Firewall Block Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Validate before block | Do not block based solely on low-confidence IoCs |
| Least disruption | Prefer narrow, scoped blocks over broad blocks |
| Time-bound where possible | Apply TTL/expiry for IoC-based blocks unless justified |
| Document approvals | Every block must have recorded authorization |
| Maintain rollback | A rollback plan must exist before implementation |
| Evidence first | Preserve logs/evidence before making changes that may remove telemetry |
| MSSP segregation | Blocks must be tenant/client scoped and documented |

---

# 7. Block Request Triggers

Firewall blocks may be requested due to:

| Trigger | Examples |
|---|---|
| Confirmed incident containment | Active C2, data exfiltration, ransomware beaconing |
| Threat intelligence | High-confidence malicious IP/domain infrastructure |
| SIEM correlation alerts | Repeated outbound to malicious IP across hosts |
| DDoS mitigation | Temporary ingress blocks / rate-limits (where supported) |
| Lateral movement containment | Segmentation blocks between zones |
| Compromised account activity | Restrict access pathways from suspect subnets |

---

# 8. Ticket Requirements (Mandatory)

Every firewall block request must be tracked in a ticket.

## 8.1 Ticket Type and Priority

| Condition | Ticket Priority |
|---|---|
| Active compromise / exfiltration / ransomware | P1 |
| Likely compromise / privileged risk | P2 |
| Suspicious but unconfirmed | P3 |
| Preventive / informational | P4 |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Priority-Matrix.md`

## 8.2 Mandatory Ticket Fields for Firewall Block Requests

| Field | Requirement |
|---|---|
| Ticket title | Must include `Firewall Block Request` + target |
| Detection time (UTC) | Mandatory |
| Requested block type | Ingress / Egress / Segmentation |
| Target indicator(s) | IP/CIDR, port, protocol, direction |
| Source scope | Which networks/hosts should be protected |
| Business justification | Why block is needed |
| Evidence references | SIEM event IDs, EDR telemetry, PCAP (if available) |
| Confidence level | High/Medium/Low with rationale |
| Requested duration | Temporary (TTL) or permanent (justification required) |
| Approver(s) | Named approver(s) required |
| Implementation owner | Firewall admin assigned |
| Rollback plan | Required summary |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

# 9. Validation Requirements (Before Implementation)

Validation is mandatory for all block requests except **emergency P1 containment**, where validation may occur in parallel but must be documented ASAP.

## 9.1 IoC Validation Checklist

| Check | Requirement |
|---|---|
| IoC format valid (IP/CIDR, port, protocol) | Mandatory |
| IoC confidence and source documented | Mandatory |
| Recency/TTL considered | Mandatory |
| Internal business dependencies checked (apps/vendors) | Mandatory |
| Over-block risk assessed (shared hosting/CDN) | Mandatory |
| Existing allowlist/exception considered | Mandatory |
| Determine scope (global vs segment-specific) | Mandatory |

## 9.2 Risk Assessment (Minimum)

| Risk Area | Considerations |
|---|---|
| Business impact | What services may be affected? |
| Security benefit | Does block stop confirmed malicious activity? |
| Breadth | Single IP vs /24 vs ASN vs geo |
| Direction | Prefer egress blocks for compromised host containment when possible |
| Monitoring impact | Will block reduce visibility into attacker behavior? |

---

# 10. Approval Workflow

## 10.1 Standard Change (Non-Emergency)

| Step | Action | Owner |
|---|---|---|
| 1 | L1/L2 creates block request ticket | L1/L2 |
| 2 | Validate IoC and scope | L2 |
| 3 | Approve block request | SOC Lead (P2–P4) / SOC Manager (high-risk) |
| 4 | Implement rule in firewall | Firewall Admin |
| 5 | Verify and monitor | Firewall Admin + SOC |
| 6 | Document implementation details | Firewall Admin |
| 7 | Close ticket after validation | SOC Lead |

## 10.2 Emergency Change (P1)

Emergency blocks are allowed when immediate containment is required.

Mandatory approvals:

| Action | Minimum Approval |
|---|---|
| Emergency containment block | IR Team Lead (or SOC Lead if IR unavailable, with documented justification) |
| Broad block (CIDR/ASN/GEO) | SOC Manager + IR Team Lead |
| Blocking critical vendor/service | SOC Manager + Business Owner (if time permits) |

Emergency documentation must be completed within **60 minutes** of action.

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

# 11. Implementation Procedure (Firewall Admin)

## 11.1 Pre-Change Checklist (Mandatory)

| Item | Requirement |
|---|---|
| Confirm ticket approval recorded | Mandatory |
| Confirm exact rule targets (IP/CIDR/port/protocol) | Mandatory |
| Confirm direction (ingress/egress) | Mandatory |
| Confirm scope (zones, interfaces, address objects) | Mandatory |
| Confirm duration (temporary/permanent) | Mandatory |
| Prepare rollback steps | Mandatory |
| Snapshot/export current config (where supported) | Mandatory |
| Identify change window (if non-emergency) | Mandatory |

## 11.2 Rule Design Standards

| Standard | Requirement |
|---|---|
| Use address objects/groups | Preferred (simplifies lifecycle) |
| Add comment/description | Mandatory (ticket ID + reason + expiry) |
| Place rule with least privilege | Mandatory |
| Avoid broad blocks unless justified | Mandatory |
| Prefer deny with logging enabled | Mandatory (unless platform constraints) |
| Set expiry/TTL when supported | Mandatory for IoC-based blocks |

### Rule Comment Standard (Mandatory)

Include:

`[TicketID] [Reason] [Requester] [Approver] [Expiry UTC]`

Example:
`INC-2026-0102 Egress block to C2 IP TI-high L2-A.Kumar Approved-SOCLead 2026-06-01T00:00Z`

## 11.3 Implementation Steps (Generic)

1. Create/verify address/service objects
2. Implement deny rule with logging
3. Commit/publish change
4. Verify rule hit counters/logs
5. Validate business services unaffected (as feasible)
6. Update ticket with implementation evidence

---

# 12. Verification and Post-Change Monitoring

## 12.1 Mandatory Verification

| Verification | Requirement |
|---|---|
| Rule exists and is enabled | Mandatory |
| Logging enabled and visible | Mandatory |
| Correct scope applied | Mandatory |
| Rule is hit when expected (if applicable) | Recommended |
| No unintended outage observed | Mandatory (monitor for defined period) |

## 12.2 Monitoring Window Guidance

| Priority | Minimum Monitoring Window |
|---|---|
| P1 | Continuous during incident + 2 hours post-change |
| P2 | 1–2 hours post-change |
| P3/P4 | 30 minutes post-change |

---

# 13. Rollback Procedure

Rollback must be executed if:

- Business outage occurs
- False positive is confirmed
- Wrong scope applied
- Rule creates unexpected side effects

Rollback steps:

1. Notify SOC Lead immediately (bridge call for P1)
2. Disable or remove rule (as per rollback plan)
3. Confirm service restoration
4. Preserve evidence of rollback (timestamps, screenshots/logs)
5. Update ticket with root cause of rollback
6. Create follow-up tuning/validation task if required

Rollback must be documented with:

- Who executed rollback
- Who authorized rollback
- Time (UTC)
- Reason
- Outcome

---

# 14. SLA Requirements (Execution Targets)

These targets align to incident severity:

| Priority | Approval Target | Implementation Target |
|---|---:|---:|
| P1 | ≤ 15 minutes | ≤ 30 minutes |
| P2 | ≤ 30 minutes | ≤ 60 minutes |
| P3 | ≤ 4 hours | ≤ 8 hours |
| P4 | ≤ 24 hours | ≤ 72 hours |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

# 15. MSSP Client-Specific Requirements

For MSSP clients:

| Requirement | Standard |
|---|---|
| Client ID tagged in ticket | Mandatory |
| Scope limited to client tenant | Mandatory |
| Client approval required (contract-dependent) | Mandatory where applicable |
| Client communications documented | Mandatory |
| Evidence segregated per client | Mandatory |
| Client change windows respected (non-emergency) | Mandatory |

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 16. Common Mistakes and Controls

| Mistake | Risk | Control |
|---|---|---|
| Blocking broad CIDRs without validation | Outage | Validation + SOC Manager approval |
| Missing expiry/TTL | Long-term disruption | TTL mandatory |
| No logging on deny rule | Loss of evidence | Logging mandatory |
| No documented approval | Audit failure | Ticket approvals mandatory |
| Wrong direction (ingress vs egress) | Ineffective containment | Pre-change checklist |
| Cross-client block applied (MSSP) | Compliance breach | Tenant scoping mandatory |

---

# 17. Related Documents

| Document | Path |
|---|---|
| Firewall Rule Change Process | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Rule-Change-Process.md` |
| Network Isolation Procedure | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Isolation-Procedure.md` |
| IDS/IPS Tuning Guide | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/IDS-IPS-Tuning-Guide.md` |
| TI IoC Handling SOP | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md` |
| Ticket Lifecycle SOP | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md` |
| Ticket Fields Standards | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md` |
| Escalation Matrix Master | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md` |
| IRT Containment Authority Matrix | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md` |

---

# 18. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 25-May-2026 | Network Security Lead / SOC Operations Lead | Initial version |

---

# 19. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**