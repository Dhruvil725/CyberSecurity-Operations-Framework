# IDS/IPS Tuning Guide

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Guide – IDS/IPS Tuning |
| Document ID | TOOL-FW-003 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | Network Security Lead / SOC Operations Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This guide defines the standard approach for tuning Intrusion Detection Systems (IDS) and Intrusion Prevention Systems (IPS) to ensure high-fidelity detections with minimal business disruption.

IDS/IPS tuning is critical because:

- Excessive false positives create alert fatigue and reduce detection effectiveness
- Over-aggressive IPS blocking can disrupt business services and client operations
- Untuned signatures lead to missed detections and poor incident response outcomes
- Audit and regulatory reviews require demonstrable monitoring and control management
- MSSP environments require client-specific baselines, segregation, and change controls
- Tuning must remain aligned to threat landscape changes and emerging TTPs

This guide ensures:

- A consistent tuning lifecycle (baseline → evaluate → implement → validate → monitor)
- Clear decision rules for alert-only vs prevention mode
- Documented exceptions, suppressions, and allowlists with expiry
- Change management, approvals, and rollback planning
- Measurable performance metrics and continuous improvement

---

# 3. Scope

This guide applies to:

| Area | Included |
|---|---|
| Technologies | Network IDS, Network IPS, inline IPS, virtual/cloud IDS/IPS (where managed) |
| Content | Signatures/rules, policy settings, thresholds, exceptions, allowlists |
| Traffic domains | Perimeter, inter-zone/segmentation, data center, cloud VPC/VNET (as applicable) |
| Outputs | Alerts to SIEM/ticketing, blocks/drops (IPS), dashboards and reports |
| Environments | Internal SOC monitoring and MSSP-managed client environments |

Out of scope:

- Full network architecture redesign
- Endpoint-based detection tuning (EDR tuning is handled separately)
- WAF tuning (covered in web application controls, if applicable)

---

# 4. Definitions

| Term | Definition |
|---|---|
| IDS | Intrusion Detection System (alerts on suspicious activity) |
| IPS | Intrusion Prevention System (can block/drop traffic inline) |
| Signature / Rule | Detection logic for known exploit/TTP patterns |
| Policy | Grouping of signatures and actions applied to traffic |
| Suppression | Preventing alerts for specific benign patterns while keeping signature active |
| Exception | A documented deviation allowing traffic/behavior otherwise flagged |
| Allowlist | Approved list of IPs/domains/services exempted from certain detections/actions |
| False Positive (FP) | Alert triggered by benign activity |
| True Positive (TP) | Alert triggered by malicious activity |
| Noise | High-volume, low-value alerting reducing operational effectiveness |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| SOC Lead | Defines tuning priorities; approves alerting thresholds; ensures operational readiness |
| Network Security Lead | Owns IDS/IPS policy baseline and tuning governance |
| IDS/IPS Engineer / Network Security Engineer | Implements tuning, suppressions, policy changes, and rollback |
| L1 Analyst | Triage IDS/IPS alerts; identify noise patterns; escalate tuning candidates |
| L2 Analyst | Investigate alerts; confirm FP/TP; provide tuning recommendations and evidence |
| L3 Analyst | Validate advanced detections; advise on exploit/zero-day patterns and coverage gaps |
| TI Lead | Provides TI-driven priorities for rules/signatures and watchlists |
| IR Team Lead | Approves IPS prevention changes with business impact risk; supports emergency tuning |
| MSSP Service Delivery | Coordinates client approvals, change windows, and client-specific baselines |

References:  
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`  
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Feed-Management.md`

---

# 6. IDS/IPS Tuning Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Detection quality first | Reduce noise while preserving true detection coverage |
| Prevention requires higher bar | IPS blocking must be validated and approved |
| Least exception | Prefer precise suppressions over broad disablement |
| Time-bound exceptions | All allowlists/exceptions must have expiry and review |
| Evidence-based tuning | All tuning decisions must reference tickets and validation evidence |
| Maintain visibility | Avoid tuning that removes investigative telemetry without alternate coverage |
| Segregation (MSSP) | Client policies must be isolated; no cross-tenant tuning without approval |
| Continuous improvement | Tuning is ongoing; review regularly and after major incidents |

---

# 7. IDS/IPS Tuning Lifecycle

| Stage | Objective | Output |
|---|---|---|
| Stage 1 | Baseline | Known-good policies, default severities, initial allowlists |
| Stage 2 | Measure | Noise, alert rates, false positive drivers, coverage gaps |
| Stage 3 | Tune | Threshold changes, suppressions, rule actions, exception creation |
| Stage 4 | Validate | Functional and security validation; ensure no missed coverage |
| Stage 5 | Monitor | Ongoing health and performance tracking |
| Stage 6 | Review | Quarterly review; retire stale exceptions; align to threat landscape |

---

# 8. Baseline Configuration Standards

## 8.1 Policy Baseline (Minimum)

| Baseline Item | Requirement |
|---|---|
| Severity mapping defined | Mandatory |
| Signature categories reviewed | Mandatory |
| Default action = alert (IDS) | Mandatory |
| Default action = alert for most IPS rules | Mandatory |
| Logging enabled for alert and block actions | Mandatory |
| Time synchronization (NTP) | Mandatory |
| SIEM forwarding verified | Mandatory |
| Rule update mechanism documented | Mandatory |

## 8.2 Severity Mapping (Guidance)

| IDS/IPS Severity | Typical Meaning | Default SOC Priority Guidance |
|---|---|---|
| Critical | Exploit attempt with high confidence / active compromise indicator | P1/P2 (context-dependent) |
| High | Likely malicious activity or known exploit pattern | P2 |
| Medium | Suspicious behavior needing investigation | P3 |
| Low/Info | Scan/noise/informational | P4 (often tuned/suppressed) |

Reference:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`  
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Priority-Matrix.md`

---

# 9. Tuning Inputs (What to Use)

Tuning must be driven by:

| Input | Examples |
|---|---|
| Alert outcomes | FP/TP dispositions from tickets |
| Attack surface changes | New internet-facing services, network segmentation changes |
| Threat intelligence | Active exploit campaigns, new ransomware infra, emerging CVEs |
| Incident learnings | Post-incident detections missed or too noisy |
| Asset context | Critical servers, DCs, payment systems, SWIFT, core banking |
| Telemetry changes | New log sources, encryption adoption, NAT changes |

References:  
`08_POST-INCIDENT/08.1_Lessons-Learned/`  
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

---

# 10. Tuning Techniques (Standard Options)

## 10.1 Recommended Tuning Actions (Least to Most Impact)

| Tuning Action | Impact | When to Use |
|---|---|---|
| Add context-based correlation in SIEM | Low | High noise but still valuable indicator |
| Suppression by src/dst/service | Low/Medium | Known benign recurring traffic triggers signature |
| Threshold increase (rate-based) | Medium | Scan noise or bursty benign events |
| Exception for specific application flow | Medium/High | Business-critical traffic incorrectly flagged |
| Disable signature (temporary) | High | Verified broken/noisy signature with no value |
| Switch IPS rule from alert → block | High | Only for high confidence, validated low FP |

## 10.2 Suppression and Exception Standards (Mandatory)

All suppressions/exceptions must:

- Reference a ticket ID
- Include justification (why benign)
- Include scope (src/dst/service/app)
- Include expiry/review date (UTC)
- Include approver name
- Be as narrow as possible

---

# 11. Alert Triage Feedback Loop (Mandatory)

IDS/IPS tuning depends on SOC feedback.

## 11.1 Ticket Requirements for IDS/IPS Alerts

Tickets created from IDS/IPS alerts must include:

| Field | Requirement |
|---|---|
| Signature/rule ID and name | Mandatory |
| Sensor location | Mandatory (perimeter/DC/segmentation/cloud) |
| Direction | Inbound/Outbound/Lateral |
| Source/Destination IP/Port/Protocol | Mandatory |
| Timestamp (UTC) | Mandatory |
| Asset criticality | Mandatory |
| Disposition (TP/FP/Unknown) | Mandatory after investigation |
| Evidence references | SIEM queries, pcap, firewall logs, EDR telemetry |
| Tuning recommendation | Required if FP or noisy |

References:  
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`  
`04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Capture-SOP.md`

---

# 12. IPS Prevention Mode Governance

## 12.1 When IPS Blocking is Allowed (Mandatory)

IPS blocking can be enabled only when:

| Requirement | Standard |
|---|---|
| Signature has high confidence and low FP history | Mandatory |
| Business impact assessed | Mandatory |
| Staging/monitor validation completed | Mandatory (unless emergency) |
| Rollback plan documented | Mandatory |
| IR Team Lead approval | Mandatory |
| SOC Manager approval for broad/high-impact enforcement | Mandatory |

## 12.2 Emergency IPS Blocking (P1)

Emergency IPS blocking may be applied during active exploitation when immediate risk reduction is required.

Mandatory conditions:

| Requirement | Standard |
|---|---|
| P1 incident declared or active exploit confirmed | Mandatory |
| IR Team Lead authorization | Mandatory |
| Documentation completed within 60 minutes | Mandatory |
| Post-change review within 24–48 hours | Mandatory |
| Rollback readiness | Mandatory |

---

# 13. Signature Update Management

IDS/IPS signatures are updated frequently and may change alert behavior.

## 13.1 Update Process (Minimum)

| Step | Action | Owner |
|---|---|---|
| 1 | Review vendor update notes | IDS/IPS Engineer |
| 2 | Apply update in staging (if available) | IDS/IPS Engineer |
| 3 | Monitor impact (alert rate changes) | SOC Lead + IDS/IPS Engineer |
| 4 | Promote to production | IDS/IPS Engineer |
| 5 | Document change and observed impact | IDS/IPS Engineer |

## 13.2 Post-Update Monitoring (Mandatory)

After signature updates, monitor for:

- Alert spikes
- New false positive patterns
- Performance degradation (CPU/memory/latency)
- Block events impacting services (IPS)

Create tuning tickets for abnormal behavior.

---

# 14. Change Management and Documentation

All tuning changes must be tracked via ticket/change record.

## 14.1 Mandatory Fields for Tuning Changes

| Field | Requirement |
|---|---|
| Change type | Suppression / threshold / disable / action change |
| Affected signatures/policies | Mandatory |
| Scope | Sensor(s), zones, networks, apps |
| Justification | FP reduction / coverage improvement / incident containment |
| Evidence | Ticket references, pcap, logs, vendor advisory |
| Approvals | Named approver(s) |
| Start time (UTC) | Mandatory |
| Expiry/review time (UTC) | Mandatory for temporary changes |
| Rollback plan | Mandatory |
| Validation plan | Mandatory |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`

---

# 15. Validation Procedures (Mandatory)

## 15.1 Functional Validation

| Validation | Requirement |
|---|---|
| Confirm rule/policy change applied | Mandatory |
| Confirm expected alerting reduced or behavior changed | Mandatory |
| Confirm SIEM ingestion still working | Mandatory |
| Confirm no sensor performance degradation | Mandatory |

## 15.2 Security Validation

| Validation | Requirement |
|---|---|
| Confirm critical detections remain active | Mandatory |
| Confirm no unintended blind spots created | Mandatory |
| Validate with test traffic (if available) | Recommended |
| Confirm that disabling/suppressing has compensating control | Mandatory if high-risk |

---

# 16. MSSP Multi-Tenant Requirements (Mandatory)

For MSSP environments:

| Requirement | Standard |
|---|---|
| Client-specific baselines | Mandatory |
| No cross-client allowlists | Mandatory |
| Client change window compliance | Mandatory (non-emergency) |
| Client approvals documented (contract-dependent) | Mandatory |
| Client reporting per tenant | Mandatory |
| Evidence segregation | Mandatory |

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 17. Metrics and KPIs (Minimum Monthly)

Track per sensor and per tenant (MSSP):

| KPI | Definition |
|---|---|
| Alert volume | Alerts/day by severity and signature |
| False positive rate | % alerts closed as FP/INFO |
| True positive rate | % alerts confirmed malicious |
| Top noisy signatures | Highest volume low-value rules |
| Mean time to tune | Time from identification to tuning deployment |
| Prevention events (IPS) | Blocks/drops per rule with validation outcomes |
| Coverage gaps | Missed detections found during incidents/hunts |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`

---

# 18. Evidence and Audit Readiness

Maintain evidence for:

| Evidence | Where |
|---|---|
| Policy baselines and exports (sanitized) | IDS/IPS admin repository |
| Change tickets and approvals | Ticketing system |
| Suppression/exception list with expiry | IDS/IPS configuration + register |
| Post-change validation notes | Tickets and SOC reports |
| Incident linkage | Incident tickets + final reports |
| KPI reports | SOC reporting folder |

---

# 19. Common Tuning Mistakes

| Mistake | Risk | Control |
|---|---|---|
| Disabling signatures permanently without review | Blind spots | Time-bound disable + quarterly review |
| Broad allowlists (entire subnets/vendors) | Exposure | Least exception + approvals |
| IPS blocking without validation | Outage | Prevention governance and rollback |
| No expiry dates | Rule sprawl | TTL/expiry mandatory |
| Tuning without ticket | Audit failure | Ticket mandatory |
| Not correlating with asset criticality | Misprioritization | Asset context required |

---

# 20. Related Documents

| Document | Path |
|---|---|
| Firewall Block Request SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Block-Request-SOP.md` |
| Firewall Rule Change Process | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Rule-Change-Process.md` |
| Network Capture SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Capture-SOP.md` |
| Network Isolation Procedure | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Isolation-Procedure.md` |
| SIEM Alert Tuning Guide | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md` |
| TI Feed Management | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Feed-Management.md` |
| Ticket Lifecycle SOP | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md` |
| Severity Classification Guide | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md` |

---

# 21. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 25-May-2026 | Network Security Lead / SOC Operations Lead | Initial version |

---

# 22. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**