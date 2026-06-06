# GUIDE: EDR Deployment Coverage Check

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | GUIDE – EDR Deployment Coverage Check |
| Document ID | TOOL-EDR-003 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / Endpoint Security Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Monthly |

---

# 2. Purpose

This guide defines the standardized methodology to measure, validate, and report **EDR deployment coverage** and **sensor health** across the organization (and MSSP-managed clients, where applicable).

EDR coverage is foundational to detection and response. Gaps in coverage create:

- Endpoint blind spots (missed compromise)
- Reduced investigation quality (missing telemetry)
- Delayed containment (no remote response capability)
- Increased ransomware propagation risk
- Incomplete regulatory/audit evidence

This guide ensures:

- A repeatable coverage validation process
- Clear coverage definitions and KPIs
- Health checks for sensors/agents and telemetry pipelines
- A standard reporting template for SOC leadership
- A controlled exception process for non-covered assets
- MSSP tenant-safe coverage reporting

---

# 3. Scope

This guide applies to:

| Scope Area | Includes |
|---|---|
| Asset Types | Workstations, laptops, servers, VDI, jump hosts, privileged admin endpoints |
| OS Platforms | Windows, Linux, macOS (as supported) |
| Environments | Corporate, data center, cloud IaaS workloads, remote endpoints |
| MSSP | Client-specific coverage checks where contractually required |
| Telemetry | EDR sensor health + SIEM forwarding (if applicable) |

Out of scope (tracked separately as exceptions or alternate controls):

- OT/ICS devices where EDR is not supported
- Appliances where vendor disallows EDR installation
- Legacy systems where EDR is incompatible (must have compensating controls)

---

# 4. Definitions (Coverage and Health)

---

## 4.1 Coverage Definitions

| Term | Definition |
|---|---|
| Asset Inventory Coverage | Percentage of known assets that are represented in a reliable asset inventory/CMDB |
| EDR Deployment Coverage | Percentage of in-scope assets with EDR agent installed and registered |
| EDR Active Coverage | Percentage of in-scope assets with EDR agent installed AND currently online/healthy |
| EDR Telemetry Coverage | Percentage of in-scope assets that are actively sending telemetry/events |
| Protection Policy Coverage | Percentage of in-scope assets assigned to correct prevention/detection policy |
| Response Capability Coverage | Percentage of assets where isolation/live response actions are permitted per policy |

---

## 4.2 Health Definitions

| Health State | Meaning | Typical Action |
|---|---|---|
| Healthy | Online, current sensor, telemetry flowing | No action |
| Degraded | Online but missing telemetry, policy mismatch, or partial functionality | Investigate and remediate |
| Offline | Not communicating to EDR | Endpoint/Network troubleshooting |
| Unmanaged | Agent missing/unregistered | Deploy agent |
| Unsupported | OS/version not supported | Exception / compensating controls |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| SOC Lead | Reviews coverage dashboard; escalates critical gaps impacting response/SLA |
| Endpoint Security Lead | Owns EDR platform health, policies, sensor lifecycle |
| IT Operations / Desktop Support | Deploys agents, fixes endpoint-side issues |
| Server Operations | Deploys agents on servers, validates maintenance windows |
| Cloud Ops | Ensures coverage on cloud instances (gold images/agents) |
| SIEM Engineering | Confirms EDR-to-SIEM forwarding health (if integrated) |
| Compliance / Risk | Reviews exceptions and compensating controls for regulatory assets |
| MSSP Service Delivery | Coordinates client-specific coverage reporting and remediation |

---

# 6. Coverage Targets (Minimum Baselines)

Coverage targets should be defined per asset criticality tier.

## 6.1 Recommended Minimum Targets

| Asset Tier | Examples | EDR Deployment Coverage Target | EDR Active Coverage Target |
|---|---|---:|---:|
| Tier 0 (Critical Identity) | Domain controllers, IdP, PAM | 100% | 99–100% |
| Tier 1 (Business Critical) | Core production servers, finance systems | 100% | ≥ 98% |
| Tier 2 (Standard) | General servers/workstations | ≥ 98% | ≥ 95% |
| Tier 3 (Low/Non-critical) | Lab/test endpoints | ≥ 95% | ≥ 90% |

If targets are not met, a corrective action plan is mandatory.

---

# 7. Data Sources for Coverage Measurement

Coverage checks must reconcile multiple sources to avoid false confidence.

## 7.1 Required Data Sources (Recommended)

| Data Source | Purpose |
|---|---|
| Asset Inventory / CMDB | “What should exist” (authoritative list) |
| Directory services (AD/Entra) | Validates active endpoints and naming |
| EDR Console Inventory | “What is covered” + sensor state/version |
| Vulnerability Scanner (optional) | Secondary validation of agent presence |
| SIEM (if integrated) | Confirms telemetry flow for covered assets |

---

# 8. Coverage Check Frequency

| Check Type | Frequency | Owner |
|---|---|---|
| Daily “Critical Tier” health check | Daily | SOC Lead / Endpoint Security |
| Weekly full coverage check | Weekly | Endpoint Security |
| Monthly compliance-grade report | Monthly | SOC Manager / Endpoint Security |
| Post-change validation | After major rollout/patch | Endpoint Security |
| Post-incident validation | After major incident | IR Team / Endpoint Security |

---

# 9. EDR Coverage Check Workflow

| Phase | Objective | Output |
|---|---|---|
| Phase 1 | Confirm in-scope asset list | In-scope inventory baseline |
| Phase 2 | Extract EDR inventory & health | EDR device export/snapshot |
| Phase 3 | Reconcile inventory vs EDR | Coverage percentage + missing list |
| Phase 4 | Validate telemetry flow | “Active telemetry” confirmation |
| Phase 5 | Validate policy assignment | Policy coverage compliance |
| Phase 6 | Identify gaps and root causes | Gap categories + owners |
| Phase 7 | Remediation tracking | Action plan + due dates |
| Phase 8 | Reporting and sign-off | Monthly report + evidence |

---

# 10. Phase 1 – Confirm In-Scope Asset List

## 10.1 In-Scope Criteria

| Criteria | Include? |
|---|---|
| Corporate endpoints | Yes |
| Servers (where supported) | Yes |
| Cloud instances with persistent workloads | Yes |
| VDI endpoints | Yes |
| Jump boxes / admin workstations | Yes |
| BYOD | Only if managed and contracted |
| OT/ICS | Only if supported and approved |

## 10.2 In-Scope Register Template

| Asset ID | Hostname | Owner Team | OS | Criticality Tier | Environment | In Scope (Y/N) |
|---|---|---|---|---|---|---|
| | | | | | | |

---

# 11. Phase 2 – Extract EDR Inventory & Sensor Health

## 11.1 Required Export Fields (Minimum)

| Field | Why |
|---|---|
| Device/Agent ID | Unique tracking |
| Hostname | Reconciliation |
| OS / Version | Supportability |
| Sensor/Agent Version | Lifecycle compliance |
| Last Seen (UTC) | Offline detection |
| Health Status | Action routing |
| Policy Group | Control validation |
| Tags/Tenant | MSSP segregation |
| Network/Domain (if available) | Context |

---

# 12. Phase 3 – Inventory Reconciliation (Coverage Calculation)

## 12.1 Reconciliation Categories

| Category | Meaning |
|---|---|
| Covered & Healthy | Installed + online + healthy |
| Covered but Offline | Installed but not communicating |
| Covered but Degraded | Partial function / telemetry gaps |
| Not Covered | Missing agent / unregistered |
| Out of Scope | Not required / excluded |
| Exception | Approved non-coverage with compensating controls |

## 12.2 Coverage Summary Table (Monthly)

| Metric | Formula | Target | Current | Status |
|---|---|---:|---:|---|
| Deployment Coverage | (Installed / In-scope) * 100 | ≥ target |  |  |
| Active Coverage | (Healthy+Degraded / In-scope) * 100 | ≥ target |  |  |
| Healthy Rate | (Healthy / Installed) * 100 | ≥ 98% |  |  |
| Offline Rate | (Offline / Installed) * 100 | ≤ 2% |  |  |
| Exceptions Count | Approved exceptions | Minimised |  |  |

## 12.3 Missing Coverage Register

| Hostname/Asset ID | OS | Tier | Owner | Reason (If Known) | Ticket | ETA |
|---|---|---|---|---|---|---|
| | | | | | | |

---

# 13. Phase 4 – Telemetry Flow Validation (Critical)

Deployment alone is insufficient—telemetry must be flowing.

## 13.1 Telemetry Validation Checks

| Check | Success Criteria |
|---|---|
| Recent telemetry event exists | Events within last 15–60 minutes (per policy) |
| Alerts and detections generate | Test signal or known benign test |
| SIEM forwarding (if enabled) | Events visible in SIEM within latency threshold |
| Time sync | Timestamps consistent (UTC) |

## 13.2 Telemetry Health Table

| Hostname | Last Telemetry UTC | Latency | Status | Notes |
|---|---|---:|---|---|
| | | | | |

If telemetry is missing but agent is “online”, treat as **Degraded** and investigate pipeline/parsing.

---

# 14. Phase 5 – Policy Assignment Validation

Correct policy assignment is required for prevention, detection, and response.

## 14.1 Policy Coverage Checklist

| Control | Requirement | Completed |
|---|---|---|
| Prevention policy assigned | Correct policy group | ☐ |
| Detection rules enabled | Baseline + high-risk rules | ☐ |
| Isolation capability allowed | For response tiers | ☐ |
| Tamper protection enabled | Where supported | ☐ |
| Exclusions controlled | Only approved exclusions | ☐ |
| Server policies separate | Server-safe controls | ☐ |

## 14.2 Policy Mismatch Register

| Hostname | Current Policy | Required Policy | Risk | Owner | Ticket |
|---|---|---|---|---|---|
| | | | | | |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Exclusion-Management.md`

---

# 15. Phase 6 – Gap Root Cause Categorization

## 15.1 Standard Gap Categories

| Gap Category | Description | Typical Owner |
|---|---|---|
| Agent Not Installed | No sensor present | Desktop/Server Ops |
| Agent Unregistered | Installed but not visible | Endpoint Security |
| Offline Endpoint | Not checking in | Desktop/Network |
| Version Outdated | Sensor behind baseline | Endpoint Security |
| Policy Mismatch | Wrong group/policy | Endpoint Security |
| Telemetry Blocked | Network/proxy blocking | Network/Endpoint |
| Unsupported OS | Not supported | Risk/IT Governance |
| Exception Approved | Formal exception exists | Compliance/Risk |

## 15.2 Root Cause Register (Monthly)

| Asset | Gap Category | Root Cause Summary | Owner | Due Date | Status |
|---|---|---|---|---|---|
| | | | | | |

---

# 16. Phase 7 – Remediation and Tracking

Remediation must be tracked through closure.

## 16.1 Remediation Actions (Examples)

| Gap | Remediation Action |
|---|---|
| Agent missing | Deploy via MDM/SCCM/automation |
| Offline | Restore connectivity; check proxy/TLS |
| Degraded | Reinstall agent; fix service dependencies |
| Version outdated | Upgrade sensor; validate compatibility |
| Policy mismatch | Move device group; apply correct policy |
| Telemetry blocked | Update firewall/proxy allowlist |
| Unsupported OS | Implement compensating controls + exception |

## 16.2 Remediation Tracker

| Asset | Action | Owner | Priority | ETA | Ticket | Verified (Y/N) |
|---|---|---|---|---|---|---|
| | | | | | | |

---

# 17. Exception Handling (When Coverage Cannot Be Achieved)

Any asset not covered must have an approved exception and compensating controls.

## 17.1 Exception Requirements

| Requirement | Mandatory |
|---|---|
| Business justification | Yes |
| Risk assessment | Yes |
| Compensating controls defined | Yes |
| Expiry/review date | Yes |
| Approval recorded | Yes |

**Reference:**
- `00_GOVERNANCE/00.1_Policies/Policy-Exception-Register.md`
- `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Exclusion-Management.md`

## 17.2 Compensating Controls Examples

| Compensating Control | Example |
|---|---|
| Network segmentation | Isolate legacy host |
| Strict allowlisting | Application allowlist enforced |
| Enhanced logging | Sysmon + SIEM correlation |
| Vulnerability hardening | Patch cadence + config lockdown |
| Access restrictions | PAM-only access |

---

# 18. Reporting Template (Monthly)

## 18.1 Executive Coverage Summary

| Field | Value |
|---|---|
| Reporting Period | |
| Total In-Scope Assets | |
| Deployment Coverage % | |
| Active Coverage % | |
| Healthy Sensor % | |
| Critical Tier Gaps | |
| Open Exceptions | |
| Major Risks | |
| Actions in Progress | |

## 18.2 Tier Coverage Breakdown

| Tier | In-Scope | Installed | Active/Healthy | Coverage % | Target % | Status |
|---|---:|---:|---:|---:|---:|---|
| Tier 0 | | | | | | |
| Tier 1 | | | | | | |
| Tier 2 | | | | | | |
| Tier 3 | | | | | | |

## 18.3 Top Issues (Last 30 Days)

| Issue Type | Count | Primary Owner | Notes |
|---|---:|---|---|
| Agent missing | | | |
| Offline | | | |
| Degraded | | | |
| Policy mismatch | | | |
| Telemetry blocked | | | |

---

# 19. MSSP-Specific Coverage Requirements

For MSSP-managed environments:

| Requirement | Purpose |
|---|---|
| Tenant-segregated reporting | Prevent cross-client exposure |
| Client-specific targets | Contract and risk-based |
| Client-approved remediation windows | Operational alignment |
| Client notification for major gaps | SLA compliance |
| Evidence package per client | Audit and compliance |

**Client Coverage Table (Template)**

| Client | In-Scope Assets | Deployment % | Active % | Critical Gaps | SLA Risk | Action Owner |
|---|---:|---:|---:|---|---|---|
| | | | | | | |

---

# 20. Evidence and Audit Readiness

Maintain evidence for:

- Monthly coverage reports
- Export snapshots from EDR console (device inventory)
- Exception approvals
- Remediation tickets and closure evidence

Recommended storage location:
`11_ARCHIVE/11.3_Audit-Records/[YYYY]-EDR-Coverage/`

---

# 21. Related Documents

| Document | Path |
|---|---|
| EDR Alert Handling Guide | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Alert-Handling-Guide.md` |
| EDR Containment Commands | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Containment-Commands.md` |
| EDR Exclusion Management | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Exclusion-Management.md` |
| EDR Investigation Queries | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Investigation-Queries.md` |
| SIEM Integration Map | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Integration-Map.md` |
| Policy Exception Register | `00_GOVERNANCE/00.1_Policies/Policy-Exception-Register.md` |

---

# 22. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | Endpoint Security Lead | Initial version |

---

# 23. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**