# Network Isolation Procedure

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – Network Isolation Procedure |
| Document ID | TOOL-FW-005 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | Network Security Lead / SOC Operations Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines how to safely isolate systems, segments, or network paths during suspected or confirmed security incidents to contain threats and prevent lateral movement, command-and-control (C2), and data exfiltration.

Network isolation is a high-impact action because:

- Isolation can disrupt business operations and critical services
- Incorrect isolation can remove visibility and hinder forensics
- Isolation changes require clear authority and documentation for audit readiness
- MSSP environments require strict tenant scoping to avoid cross-client impact
- Emergency isolation must be performed quickly but in a controlled manner

This SOP ensures:

- Consistent decision-making for when and how to isolate
- Clear roles, approvals, and authority for containment actions
- Standard isolation methods and rollback procedures
- Evidence preservation and visibility safeguards
- SLA-aligned execution for P1/P2 incidents
- Tenant-safe operations for MSSP clients

---

# 3. Scope

This SOP applies to isolation actions affecting:

| Isolation Target | Examples |
|---|---|
| Endpoint host | Workstation, server, VDI session |
| Network segment | VLAN, subnet, zone, security group |
| Account access path | Restricting access routes to critical services |
| Data center link/path | Segmentation firewall deny between zones |
| Cloud network | VPC/VNET route, security group egress restriction |
| Remote access | VPN user isolation, IP restriction, conditional access |

Out of scope:

- Physical isolation procedures (handled under physical security playbooks)
- Endpoint-only isolation performed purely via EDR (covered in EDR containment commands; referenced here)

---

# 4. Definitions

| Term | Definition |
|---|---|
| Isolation | Restricting communication of a host/segment to limit threat spread |
| Containment | Actions taken to limit attacker movement and impact |
| Quarantine VLAN | Network segment with limited access for investigation/remediation |
| EDR network isolation | Endpoint agent enforces network restrictions |
| Break-glass | Emergency authorization to act when approvers are unavailable |
| Critical services | Systems required for business continuity (core banking, payment, identity, etc.) |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| L1 Analyst | Identify isolation need; open/maintain ticket; notify SOC Lead |
| L2 Analyst | Validate compromise indicators; define scope; recommend isolation method |
| SOC Lead | Coordinate containment; confirm severity; initiate bridge call for P1 |
| IR Team | Authorize containment actions; coordinate forensics and recovery |
| Network Security Engineer | Implement network-level isolation (firewall/VLAN/route/security groups) |
| EDR Admin | Execute EDR network isolation (if used) |
| SOC Manager | Approves high-risk isolation (broad segment / business impact) |
| Business Owner / IT Ops | Supports service impact assessment and recovery coordination |
| MSSP Service Delivery | Ensures client approvals and communications are met |

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

# 6. Isolation Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Contain fast, contain safely | Time matters, but avoid uncontrolled outage |
| Least disruptive isolation | Isolate smallest scope that achieves containment |
| Preserve evidence | Collect logs/volatile evidence where feasible before isolation |
| Maintain visibility | Avoid isolating in a way that prevents monitoring/forensics entirely |
| Approved authority | Containment actions must be authorized and documented |
| Plan rollback | Always define rollback steps before implementation |
| Tenant scoping (MSSP) | Ensure isolation does not affect other clients |

---

# 7. Isolation Triggers (When to Isolate)

Isolation is recommended/required when:

| Trigger | Examples |
|---|---|
| Active compromise confirmed | Malware execution, ransomware encryption, active C2 |
| Lateral movement indicators | SMB/WMI/PSRemoting spread, multiple host hits |
| Data exfiltration suspected/confirmed | Large unusual outbound transfers |
| Privileged credential compromise | Domain admin theft, DC suspicious activity |
| Zero-day exploitation suspected | Rapid containment required |
| Insider threat with active data staging | Large file staging to removable media or cloud |

Reference:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Escalation-Criteria.md`

---

# 8. Isolation Decision Matrix (Guidance)

| Scenario | Recommended Isolation |
|---|---|
| Single infected workstation | EDR network isolation OR switch port shutdown (if needed) |
| Single critical server compromise | Segmentation firewall restrict to management + IR tools only |
| Multiple hosts infected in subnet | Quarantine VLAN + targeted egress blocks |
| Suspected exfiltration to external IP | Egress block at firewall + isolate source host(s) |
| Domain controller compromise | Segmentation lockdown + IR immediate involvement (P1) |
| Cloud instance compromise | Security group egress restriction + isolate instance in quarantine SG/VPC |

---

# 9. Approvals and Authority (Mandatory)

Isolation approvals depend on severity and scope.

## 9.1 Authority Matrix (Minimum)

| Action | Minimum Authorization |
|---|---|
| Isolate single non-critical endpoint | SOC Lead (P2/P3) / IR Team Lead (P1) |
| Isolate critical server | IR Team Lead + SOC Manager |
| Isolate subnet/VLAN/zone | SOC Manager + IR Team Lead |
| Isolate domain controller / identity systems | CISO notification + IR Team Lead |
| Break-glass isolation | SOC Lead + documented justification; post-approval review required |

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

## 9.2 MSSP Client Approvals

| Condition | Requirement |
|---|---|
| Client approval required (contract) | Mandatory unless emergency clause |
| Isolation impacts production services | Mandatory client notification |
| Client provides execution authority | Follow client RACI and escalation matrix |

Reference:
`09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/Client-Specific-Playbook-Guide.md`

---

# 10. Pre-Isolation Checklist (Mandatory)

Before isolating, record in ticket:

| Item | Requirement |
|---|---|
| Why isolation is needed | Mandatory |
| Scope (host/subnet/zone) | Mandatory |
| Business impact assessment | Mandatory (best effort for P1) |
| Evidence preserved (what/where) | Mandatory |
| Isolation method chosen | Mandatory |
| Approver name/time (UTC) | Mandatory |
| Rollback plan | Mandatory |
| Monitoring plan | Mandatory (what telemetry remains) |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

# 11. Isolation Methods (Standard Procedures)

## 11.1 Method A — EDR Network Isolation (Preferred for Endpoints)

Use when endpoint has EDR agent and isolation feature is supported.

Steps:

1. Confirm asset identity and owner
2. Confirm isolation will not break critical business operation (best effort)
3. Obtain authorization and record in ticket
4. Execute EDR isolation command
5. Validate isolation status in EDR console
6. Preserve EDR telemetry and initiate forensic steps
7. Maintain limited access (IR tools) if supported by EDR policy

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Containment-Commands.md`

---

## 11.2 Method B — Segmentation Firewall Isolation (Preferred for Servers)

Use when isolating a server while maintaining controlled access.

Steps:

1. Identify server IP and zone
2. Create a restrictive allowlist policy (management subnet + IR tools only)
3. Deny all other inbound/outbound traffic as required
4. Enable logging
5. Commit rule changes and verify hit counters
6. Monitor service health and attack traffic reduction
7. Update ticket with rule IDs and evidence

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Rule-Change-Process.md`

---

## 11.3 Method C — Quarantine VLAN / Network Reassignment

Use when multiple endpoints are impacted or when a “walled garden” is needed.

Steps:

1. Identify switch ports/host list
2. Create quarantine VLAN with limited routing:
   - Allowed: IR tools, patching, forensic collection endpoints
   - Denied: internet, lateral internal access (as required)
3. Move affected ports/hosts into quarantine VLAN
4. Verify isolation and essential access (IR/patch)
5. Update ticket with change details and timestamps
6. Plan remediation and staged return to production network

---

## 11.4 Method D — Switch Port Shutdown (Last Resort)

Use when EDR is unavailable and immediate containment is required.

Steps:

1. Confirm asset mapping to switch port
2. Obtain authorization
3. Disable port
4. Validate host disconnected
5. Document action and business impact
6. Coordinate remediation and controlled re-enable

---

## 11.5 Method E — Cloud Security Group / Route Isolation

Use for cloud-hosted assets.

Steps:

1. Identify affected instance and security group
2. Apply quarantine security group (restrictive)
3. Limit egress to IR tooling only (if needed)
4. Enable/confirm flow logs (visibility)
5. Document changes and validate effect
6. Maintain evidence and coordinate recovery

---

# 12. Visibility and Evidence Safeguards (Mandatory)

Isolation can reduce telemetry. Ensure:

| Safeguard | Requirement |
|---|---|
| Capture key logs before isolation (if feasible) | Recommended for P1/P2 |
| Preserve SIEM logs and EDR telemetry | Mandatory |
| Ensure IR access remains (where required) | Mandatory for remediation |
| PCAP capture if exfil suspected | Recommended |
| Record all actions with UTC timestamps | Mandatory |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md`  
`04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Capture-SOP.md`

---

# 13. Rollback / De-Isolation Procedure

De-isolation must occur only when:

- Threat eradication is completed
- Persistence removed
- Host is validated clean
- Monitoring plan is in place post-restoration

Rollback steps:

1. Obtain approval to restore connectivity (SOC Lead / IR Team Lead)
2. Remove quarantine policies / revert firewall rules / re-enable port
3. Validate system connectivity and service health
4. Continue heightened monitoring for 24–72 hours (depending on severity)
5. Document actions and results in ticket

Reference:
`02_PLAYBOOKS/` (recovery steps per incident type)

---

# 14. SLA Targets (Isolation Execution)

| Priority | Isolation Start Target | Notes |
|---|---:|---|
| P1 | ≤ 30 minutes | Emergency containment; bridge call typically active |
| P2 | ≤ 2 hours | Urgent containment |
| P3 | ≤ 8 hours | Planned within shift |
| P4 | As required | Preventive or informational |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

# 15. MSSP Multi-Tenant Requirements (Mandatory)

| Requirement | Standard |
|---|---|
| Client ID tagged | Mandatory |
| Isolation scoped to client tenant only | Mandatory |
| Client approval documented (contract dependent) | Mandatory |
| Client notification documented | Mandatory (P1/P2) |
| Evidence segregated | Mandatory |
| Cross-client impact assessment | Mandatory before network-level changes |

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md`

---

# 16. Common Mistakes and Controls

| Mistake | Risk | Control |
|---|---|---|
| Isolating too broadly | Unnecessary outage | Least disruptive isolation |
| Isolating without approval | Audit/compliance failure | Authority matrix enforced |
| Losing visibility after isolation | Investigation impact | Visibility safeguards |
| No rollback plan | Prolonged outage | Rollback mandatory |
| Cross-client isolation (MSSP) | Compliance breach | Tenant scoping controls |
| Forgetting to remove temporary isolation rules | Operational debt | Expiry + review tasks |

---

# 17. Related Documents

| Document | Path |
|---|---|
| Firewall Block Request SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Block-Request-SOP.md` |
| Firewall Rule Change Process | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Rule-Change-Process.md` |
| Network Capture SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Capture-SOP.md` |
| IDS/IPS Tuning Guide | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/IDS-IPS-Tuning-Guide.md` |
| EDR Containment Commands | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Containment-Commands.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| IRT Containment Authority Matrix | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md` |
| Cross-Client Incident Procedure | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md` |

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