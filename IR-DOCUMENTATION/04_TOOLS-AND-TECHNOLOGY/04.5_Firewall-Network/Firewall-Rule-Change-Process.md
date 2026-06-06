# Firewall Rule Change Process

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – Firewall Rule Change Process |
| Document ID | TOOL-FW-002 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | Network Security Lead / SOC Operations Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines the controlled process for requesting, approving, implementing, validating, documenting, and rolling back firewall rule changes.

Firewall rule changes are high-risk because:

- Incorrect rules can cause outages, performance degradation, or security exposure
- Uncontrolled changes create audit failures and compliance issues
- Rule sprawl and poor documentation degrade firewall effectiveness over time
- MSSP environments require client-specific governance and segregation
- Emergency incident-driven changes must be fast but controlled

This SOP ensures:

- Standard change control for firewall rules
- Clear approval and implementation responsibilities
- Risk-based validation and testing
- Consistent documentation and audit readiness
- Safe rollback procedures
- Alignment with SOC ticketing and incident response workflows

---

# 3. Scope

This SOP applies to:

| Area | Included |
|---|---|
| Devices | Perimeter firewalls, internal firewalls, segmentation firewalls, cloud firewall equivalents (if managed) |
| Change types | Add/modify/delete rules, address objects, service objects, NAT (if security-driven), logging changes |
| Change categories | Standard, normal, emergency (incident-driven) |
| Environments | Internal SOC and MSSP-managed client environments |
| Integrations | SIEM logging, IDS/IPS, EDR containment workflows (as applicable) |

Out of scope:

- Major redesign projects (handled as separate project governance)
- Non-security IT network changes unless routed through SOC per policy

---

# 4. Definitions

| Term | Definition |
|---|---|
| Rule | Firewall policy statement controlling traffic |
| Object | Address/service/group referenced by rules |
| Change record | Ticket documenting requested change, approvals, and evidence |
| Emergency change | Change required immediately to reduce active threat risk |
| Backout / rollback | Steps to revert change to previous state |
| Least privilege | Allow only the minimum traffic required |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| Requester (SOC/L2/L3/IR) | Submits change request with justification and scope |
| SOC Lead | Validates security need; confirms severity; coordinates emergency changes |
| Network Security Engineer / Firewall Admin | Implements change; validates; documents; manages rollback |
| IR Team Lead | Approves emergency containment and high-risk security changes |
| SOC Manager | Oversight; approval for high-impact/broad changes |
| Business Owner / Application Owner | Approves business-impacting changes (where applicable) |
| MSSP Service Delivery | Coordinates client approvals, change windows, and communications |

References:  
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`  
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

# 6. Change Management Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Ticket required | No firewall changes without a tracked ticket (except documented break-glass) |
| Least privilege | Rules must be as narrow as possible |
| Default deny remains | Do not weaken baseline segmentation without explicit approval |
| Logging required | Security-relevant rules must log (deny preferred) |
| Documentation required | Rule description must include ticket ID and purpose |
| Validation before enforcement | TI-based blocks must follow IoC handling validation |
| Rollback prepared | Rollback plan must exist for every change |
| Periodic review | Rules must be reviewed for necessity and expiry |

---

# 7. Change Types

| Change Type | Description | Examples |
|---|---|---|
| Add | Introduce new rule/object | Allow vendor IP to specific service |
| Modify | Update existing rule | Add destination host; change port |
| Delete | Remove obsolete rule | Retire old application rule |
| Temporary | Time-bound rule | Emergency block with expiry |
| Emergency | Immediate security containment | Block C2 IP during incident |

---

# 8. Request Requirements (Mandatory)

All requests must be submitted via ticket with the following minimum fields.

## 8.1 Mandatory Request Fields

| Field | Requirement |
|---|---|
| Change title | Clear summary + target system |
| Change category | Standard/Normal/Emergency |
| Priority | P1–P4 (aligned to incident severity where applicable) |
| Business justification | Why change is required |
| Security justification | Threat/risk being addressed |
| Source and destination | IP/CIDR/objects/zones |
| Service/protocol/port | Specifics required |
| Direction | Ingress/Egress/Internal |
| Environment | Prod/Dev/DR |
| Requested start time (UTC) | Mandatory |
| Requested end time / expiry (UTC) | Mandatory for temporary rules |
| Impact assessment | Expected service impact |
| Validation evidence | SIEM/EDR/TI references (as applicable) |
| Approver(s) | Named approvers required |
| Rollback plan | Required summary |

References:  
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`  
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md`

---

# 9. Approval Workflow

## 9.1 Standard / Normal Changes

| Step | Action | Owner |
|---|---|---|
| 1 | Create change ticket | Requester |
| 2 | Validate scope, least privilege, and risk | Firewall Admin + SOC Lead |
| 3 | Approve change | SOC Lead (security) + Business Owner (impact) |
| 4 | Schedule change window | Firewall Admin + Requester |
| 5 | Implement change | Firewall Admin |
| 6 | Validate functionality and logging | Firewall Admin + SOC |
| 7 | Document evidence and close ticket | Firewall Admin + SOC Lead |

## 9.2 Emergency Changes (Incident-Driven)

Emergency changes are allowed when required to stop active threat activity.

Minimum approvals:

| Change | Approval |
|---|---|
| Containment block for P1 | IR Team Lead (or SOC Lead if IR unavailable) |
| Broad scope change (CIDR/ASN/GEO) | SOC Manager + IR Team Lead |
| Change impacting critical business service | SOC Manager + Business Owner (if time permits) |

Emergency documentation must be completed within **60 minutes** of execution.

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Block-Request-SOP.md`

---

# 10. Implementation Procedure (Firewall Admin)

## 10.1 Pre-Implementation Checklist (Mandatory)

| Check | Requirement |
|---|---|
| Ticket approved and complete | Mandatory |
| Confirm rule intent (allow/deny) | Mandatory |
| Confirm objects and groups | Mandatory |
| Confirm zones/interfaces | Mandatory |
| Confirm NAT implications (if applicable) | Mandatory |
| Confirm logging settings | Mandatory |
| Confirm expiry for temporary rules | Mandatory |
| Export/snapshot current config | Mandatory |
| Rollback steps prepared | Mandatory |
| Change window confirmed | Mandatory (unless emergency) |

## 10.2 Rule Standards (Mandatory)

| Standard | Requirement |
|---|---|
| Least privilege | Narrow src/dst/service |
| Proper placement | Above broad allow rules; below critical denies as appropriate |
| Naming and description | Must include ticket ID, owner, purpose, expiry |
| Logging | Deny rules must log; allow rules log as per policy |
| Temporary rule expiry | Mandatory (where supported) |
| Object reuse | Prefer objects/groups over raw IPs for manageability |

### Rule Description Standard (Mandatory)

`[TicketID] [Purpose] [Requester] [Approver] [Expiry UTC (if any)]`

Example:  
`CHG-2026-0044 Allow vendor SFTP to APP-SRV-01 Requested-L2 Approved-SOCLead Exp-2026-06-01T00:00Z`

---

# 11. Validation and Verification

## 11.1 Functional Validation (Mandatory)

| Validation | Requirement |
|---|---|
| Confirm rule committed successfully | Mandatory |
| Confirm rule hit counters/logs | Mandatory |
| Confirm intended traffic allowed/blocked | Mandatory |
| Confirm no unintended traffic impact | Mandatory |
| Confirm SIEM receives firewall logs | Mandatory (if integrated) |

## 11.2 Security Validation (Recommended)

| Validation | Guidance |
|---|---|
| Confirm no new broad allow exposures | Review rule order and objects |
| Confirm segmentation intent preserved | Validate inter-zone paths |
| Confirm no overlap with existing controls | Check IDS/IPS/EDR overlaps |

---

# 12. Rollback Procedure (Mandatory)

Rollback must be available for every change.

Rollback triggers:

- Unplanned outage
- Misconfiguration detected
- Increased security risk discovered
- False positive enforcement impact

Rollback steps:

1. Notify SOC Lead immediately
2. Disable or revert rule/object changes
3. Commit rollback and confirm restoration
4. Preserve evidence (before/after config references)
5. Document rollback in ticket (who/when/why/outcome)
6. Create follow-up action item for remediation

---

# 13. Temporary Rules and Expiry Management

Temporary rules must include:

| Requirement | Standard |
|---|---|
| Expiry date/time (UTC) | Mandatory |
| Review owner | Mandatory |
| Auto-expiry enabled (if supported) | Recommended |
| Reminder ticket/task | Mandatory if no auto-expiry |

If a temporary rule must be extended, it requires:

- New approval
- Updated expiry
- Documented justification

---

# 14. Periodic Rule Review (Governance)

Firewall rules must be reviewed:

| Review Type | Frequency | Owner |
|---|---|---|
| Temporary rule review | Weekly | Firewall Admin |
| High-risk rule review | Monthly | Network Security Lead + SOC Lead |
| Full rulebase review | Quarterly | Network Security Lead |

Review outputs:

- Rules to retire
- Rules to tighten (least privilege)
- Logging gaps
- Orphaned objects/groups
- Findings tracked in improvement register

Reference:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Control-Gap-Tracker.xlsx`

---

# 15. MSSP Client Requirements

For MSSP-managed clients:

| Requirement | Standard |
|---|---|
| Client ID and environment tagged | Mandatory |
| Client change window respected | Mandatory (non-emergency) |
| Client approval recorded (as contract requires) | Mandatory |
| Evidence segregated | Mandatory |
| Tenant-specific implementation | Mandatory |
| Client notification documented | Mandatory |

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 16. Common Mistakes and Controls

| Mistake | Risk | Control |
|---|---|---|
| Adding broad allow rules | Increased attack surface | Least privilege + approval |
| No ticket / missing approvals | Audit failure | Ticket mandatory |
| No rollback plan | Extended outage | Rollback mandatory |
| Temporary rules never removed | Rule sprawl | Expiry management |
| Logging disabled | Loss of evidence | Logging standards |
| Cross-client rule changes (MSSP) | Compliance breach | Tenant scoping |

---

# 17. Related Documents

| Document | Path |
|---|---|
| Firewall Block Request SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Block-Request-SOP.md` |
| Network Isolation Procedure | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Isolation-Procedure.md` |
| IDS/IPS Tuning Guide | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/IDS-IPS-Tuning-Guide.md` |
| Network Capture SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Capture-SOP.md` |
| Ticket Lifecycle SOP | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md` |
| Internal SLA Definitions | `00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md` |
| TI IoC Handling SOP | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md` |

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