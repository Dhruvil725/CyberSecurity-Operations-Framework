# Threat Intelligence (TI) Integration with EDR

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – TI Integration with EDR |
| Document ID | TOOL-TI-002 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | SOC Manager / Threat Intelligence Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines how Threat Intelligence (TI) is integrated with the Endpoint Detection & Response (EDR) platform to improve detection, investigation, and response outcomes.

This integration is critical because:

- TI enrichment improves analyst decision-making and reduces time-to-triage
- IOC matches can detect known threats earlier in the kill chain
- Automated response (block/quarantine/isolate) must be controlled to avoid business disruption
- MSSP environments require strict tenant segregation and controlled policy deployment
- Audit and compliance require traceable intelligence sources and documented actions

This SOP ensures:

- Standard, repeatable TI → EDR integration
- Clear rules for enrichment vs alerting vs blocking
- Safe, approved workflows for automated containment
- Documented change control and rollback
- Monitoring of integration health and performance
- Evidence capture for audits and incident reporting

---

# 3. Scope

This SOP applies to:

| Area | Included |
|---|---|
| TI content | IPs, domains, URLs, file hashes, certificates (if supported), attack patterns |
| EDR capabilities | IOC match alerts, reputation lookups, blocklists, quarantine, isolate host, kill process |
| Deployment | Internal SOC and MSSP-managed clients (multi-tenant) |
| Use cases | Enrichment, detections/correlations, prevention controls, threat hunting |

Out of scope:

- Detailed incident response steps after an EDR detection (see playbooks)
- SIEM correlation logic (covered in TI Integration with SIEM)

---

# 4. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| Threat Intelligence (TI) Lead | Defines feed sources, confidence scoring, TTL, and promotion rules |
| EDR Admin | Implements IOC ingestion, policies, exceptions, and rollout/rollback |
| SOC Lead | Approves alerting thresholds; ensures operational readiness |
| L2 Analyst | Validates IOC matches during investigations; recommends tuning/allowlisting |
| L3 Analyst | Validates high-impact IOC decisions; supports forensic verification |
| IR Team Lead | Approves automated containment/blocking for P1/P2 risk scenarios |
| MSSP Service Delivery | Ensures client-specific policies and SLAs are met; change communications |
| Compliance / Legal (as needed) | Reviews licensing constraints and regulatory considerations |

References:
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Feed-Management.md`  
`04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Exclusion-Management.md`  
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

# 5. Integration Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Enrichment-first | New TI sources start as enrichment before enforcement |
| Confidence-driven | Actions depend on confidence + context (asset criticality, user privilege, prevalence) |
| TTL enforced | All IOC policies must have expiration/review timelines |
| Safe automation | Blocking/quarantine requires approvals and rollback plan |
| Audit-ready | Every IOC used for enforcement must be traceable to a TI source and change record |
| MSSP segregation | Tenant policies must be separated; no cross-client leakage |
| Least disruption | Prefer alerting over blocking unless risk justifies enforcement |

---

# 6. Integration Architecture (Logical)

## 6.1 Data Flows

| Flow | Description |
|---|---|
| TI Platform → EDR | Push/pull IOCs (hashes/domains/IPs) and tags/confidence |
| EDR → SOC Ticketing | IOC match alerts open/update tickets |
| EDR → SIEM (optional) | EDR telemetry and alerts forwarded to SIEM for correlation |
| SOC Analyst → TI Platform | Feedback loop: add disposition (TP/FP), enrichment notes, sightings |

---

## 6.2 IOC Categories in EDR

EDR must support at least the following IOC handling categories (names vary by vendor):

| Category | Purpose | Default Mode |
|---|---|---|
| Reputation / Enrichment | Add context to detections and telemetry | Enabled |
| Alert-only IOCs | Generate alerts on match | Enabled (for medium/high confidence) |
| Block/Prevent IOCs | Prevent execution/connection | Disabled by default |
| Watchlist / Hunting | Query/hunt for historic sightings | Enabled |

---

# 7. IOC Types and Handling Rules

## 7.1 Supported IOC Types (Standard)

| IOC Type | EDR Use | Notes |
|---|---|---|
| File hash (SHA256 preferred) | Block / Alert / Hunt | Highest reliability for file-based threats |
| Domain | Alert / Block (caution) | Domains can be shared/benign; high FP risk |
| URL | Alert / Block (caution) | Prefer domain extraction + path where supported |
| IP address | Alert / Block (caution) | IPs are volatile; enforce shorter TTL |
| Certificate fingerprint | Alert / Block (if supported) | Lower FP if tied to malware family |
| Process/command patterns | Alert / Hunt | Typically not “IOC” but behavior-based patterns |

---

## 7.2 TTL Guidance (Mandatory)

EDR-enforced IOC policies must expire or be reviewed:

| IOC Type | Default TTL | Enforcement Guidance |
|---|---|---|
| Hash | 180 days | Safe for block if confidence is high |
| Domain | 30 days | Prefer alerting; block only with validation |
| URL | 14 days | Prefer alerting; block only if high confidence |
| IP | 7–14 days | Prefer alerting; block only if verified |
| Certificate | 180 days | Block only if tied to verified malware |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Feed-Management.md`

---

# 8. Onboarding TI into EDR (Implementation Workflow)

## 8.1 Step 1 — Preconditions Checklist

| Item | Requirement |
|---|---|
| EDR tenant(s) identified | Mandatory |
| Integration method decided (API/push/pull) | Mandatory |
| Authentication configured (token/service account) | Mandatory |
| Role-based access validated | Mandatory |
| Change record created (for production) | Mandatory |
| Rollback plan documented | Mandatory |
| MSSP tenant segregation confirmed | Mandatory (MSSP only) |

---

## 8.2 Step 2 — Mapping and Normalization

Ensure the following mapping is configured:

| TI Field | EDR Field | Requirement |
|---|---|---|
| Indicator value | IOC value | Mandatory |
| Indicator type | IOC type | Mandatory |
| Source feed name | IOC source / tag | Mandatory |
| Confidence score | IOC severity/confidence | Mandatory |
| First seen / last seen | Validity window | Recommended |
| TTL | Expiration date | Mandatory |
| Tags (malware family, actor, campaign) | Labels/tags | Recommended |
| TLP (if used) | Visibility/sharing restrictions | As applicable |

Normalization requirements:

- Lowercase domains
- Validate hash types and lengths
- Remove invalid/empty records
- Deduplicate by value + type
- Preserve source attribution (multi-source support)

---

## 8.3 Step 3 — Enrichment Mode Deployment (Default)

Deploy IOC sets initially in **enrichment** (no prevention impact):

| Control | Requirement |
|---|---|
| Enrichment enabled | Mandatory |
| Alert-only disabled unless approved | Recommended |
| Block/prevent disabled | Mandatory |
| TTL applied | Mandatory |
| Logging enabled | Mandatory |

Objective: confirm match rates and noise levels before enforcement.

---

## 8.4 Step 4 — Alerting Mode Deployment (Controlled)

Alerting mode may be enabled after pilot validation.

Alerting requirements:

| Requirement | Standard |
|---|---|
| Confidence threshold defined | Mandatory |
| Allowlist exceptions in place | Mandatory (if known benign overlap exists) |
| Ticketing integration verified | Mandatory |
| SOC Lead approval | Mandatory |
| Update/rollback plan documented | Mandatory |

---

## 8.5 Step 5 — Blocking/Prevention Mode Deployment (High Control)

Blocking is allowed only for high-confidence indicators with validated low false positive risk.

Blocking requirements (Mandatory):

| Requirement | Standard |
|---|---|
| High confidence source (documented) | Mandatory |
| Validation performed (see Section 11) | Mandatory |
| IR Team Lead approval | Mandatory |
| SOC Manager approval (MSSP: client approval where required) | Mandatory |
| Rollback steps tested | Mandatory |
| Change window respected | Mandatory (except emergency P1) |
| Post-deployment monitoring | Mandatory |

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

# 9. Policy Design Standards (EDR IOC Sets)

## 9.1 IOC Set Naming Standard (Mandatory)

Use:

`TI-[FEED/PROGRAM]-[MODE]-[TENANT]-[YYYYMMDD]`

Examples:

- `TI-Commercial-ENRICH-Internal-20260525`
- `TI-ISAC-ALERT-ClientABC-20260525`
- `TI-IR-Block-Internal-20260525`

---

## 9.2 Recommended Confidence Thresholds

| Mode | Minimum Confidence | Notes |
|---|---|---|
| Enrichment | Any | Log and tag only |
| Alert-only | Medium | Tune based on noise |
| Block/Prevent | High | Block only after validation |

If the TI provider uses a numeric score, document the conversion to Low/Medium/High in the TI platform.

---

## 9.3 Exceptions / Allowlisting Rules

Allowlisting must be controlled:

| Requirement | Standard |
|---|---|
| Allowlist entry must be ticketed | Mandatory |
| Allowlist must include justification | Mandatory |
| Allowlist must be time-bound (expiry) | Mandatory |
| SOC Lead approval | Mandatory |
| Quarterly review | Mandatory |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Exclusion-Management.md`

---

# 10. Alert-to-Ticket Workflow (Mandatory)

When EDR generates an IOC match alert:

| Step | Action | Owner |
|---|---|---|
| 1 | EDR alert ingested | Platform integration |
| 2 | Ticket created/updated in ticketing tool | Automation / L1 |
| 3 | Ticket fields populated (host/user/IOC/source/confidence) | Automation / L1 |
| 4 | L1 triage and severity assignment | L1 |
| 5 | Escalate per severity | L1/SOC Lead |
| 6 | Investigation and containment actions recorded | L2/L3/IR |
| 7 | Disposition feedback sent to TI platform (TP/FP) | L2/TI Lead |

Ticket must include at minimum:

- IOC value and type
- TI source/feed name
- Confidence level
- Match context (process, file path, network destination)
- Timestamp (UTC)
- Asset criticality and user privilege

References:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`  
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`

---

# 11. Validation Requirements (Before Blocking)

Before any IOC is promoted to blocking/prevention, perform validation:

## 11.1 Validation Checklist

| Check | Requirement |
|---|---|
| IOC exists in at least one reputable source | Mandatory |
| IOC is not present in known benign lists (where applicable) | Mandatory |
| IOC recency verified (not stale) | Mandatory |
| Impact assessment completed | Mandatory |
| Test in monitor/alert mode first (where feasible) | Recommended |
| Client/business owner impact approval (MSSP/critical apps) | Mandatory where applicable |

## 11.2 False Positive Risk Controls

| IOC Type | FP Risk | Control |
|---|---|---|
| Domain/URL | High | Alert first; validate; short TTL; allowlist |
| IP | Medium/High | Short TTL; verify ownership/ASN; alert first |
| Hash | Low/Medium | Block if high confidence; verify prevalence and file signer if possible |
| Certificate | Low/Medium | Validate chain/context; use with caution |

---

# 12. MSSP Multi-Tenant Requirements (Mandatory)

For MSSP operations:

| Requirement | Standard |
|---|---|
| No cross-tenant IOC policies | Mandatory |
| Tenant tagging on every IOC set | Mandatory |
| Client-specific allowlists | Mandatory |
| Client approval for blocking (contract-dependent) | Mandatory |
| Separate reporting per tenant | Mandatory |
| Evidence segregation | Mandatory |

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 13. Change Management and Emergency Changes

## 13.1 Standard Change Process

All production changes must be tracked via ticket:

| Change | Requirement |
|---|---|
| Add new feed IOC set | Ticket + approval |
| Change thresholds | Ticket + approval |
| Enable alerting | Ticket + SOC Lead approval |
| Enable blocking | Ticket + IR Team Lead approval |
| Add allowlist exception | Ticket + SOC Lead approval |
| Retire IOC set | Ticket + documentation |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`

---

## 13.2 Emergency Change (P1)

Emergency blocking (e.g., active ransomware campaign) is allowed only when:

| Requirement | Standard |
|---|---|
| Incident declared P1 | Mandatory |
| IR Team Lead authorization | Mandatory |
| SOC Manager notification | Mandatory |
| Rollback plan ready | Mandatory |
| Post-change review completed within 24–48 hours | Mandatory |

---

# 14. Monitoring, Health Checks, and Troubleshooting

## 14.1 Integration Health Checks (Minimum)

| Check | Requirement |
|---|---|
| Last TI sync time | Mandatory |
| IOC ingestion success/failure rate | Mandatory |
| Policy deployment status | Mandatory |
| API auth status | Mandatory |
| Alert delivery to ticketing/SIEM | Mandatory |
| Volume anomalies | Mandatory |

## 14.2 Common Issues and Resolution

| Symptom | Likely Cause | Action |
|---|---|---|
| No IOC updates in EDR | API token expired / connector down | Renew token; restart connector; verify logs |
| High false positives | Low-quality feed / threshold too low | Increase threshold; switch to enrichment; add allowlist |
| Blocking causing disruption | IOC too broad (domain/IP) | Disable blocking set; rollback; shorten TTL; validate |
| Duplicate alerts | Multiple feeds same IOC | Dedup rules; consolidate IOC sets |
| Missing source attribution | Mapping misconfigured | Fix mapping; re-sync; update schema |

---

# 15. Metrics and KPIs (Monthly Minimum)

Track these KPIs per tenant (MSSP) and globally:

| KPI | Definition |
|---|---|
| IOC sync success rate | Successful updates / total attempts |
| IOC match rate | Matches per day/week by type |
| Actionable match rate | Matches leading to TP investigations |
| False positive rate | Matches assessed as benign |
| Prevention efficacy | Blocked executions/connections confirmed malicious |
| Time-to-detect improvement | Delta in MTTA/MTTR where TI contributed |
| Rollback count | Number of emergency/failed deployments |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`

---

# 16. Evidence and Audit Readiness

Maintain evidence for:

| Evidence | Where |
|---|---|
| Feed sources and licenses | Feed catalog / contracts |
| IOC set configurations (sanitized exports) | EDR admin records |
| Change approvals | Ticketing system |
| Blocking approvals | Ticket + IR authorization record |
| Match logs and disposition | EDR logs + ticket references |
| MSSP tenant segregation proof | Tenant config snapshots (sanitized) |

---

# 17. Related Documents

| Document | Path |
|---|---|
| TI Feed Management | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Feed-Management.md` |
| TI IoC Handling SOP | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md` |
| TI Integration with SIEM | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Integration-with-SIEM.md` |
| TI Platform Usage Guide | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Platform-Usage-Guide.md` |
| EDR Alert Handling Guide | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Alert-Handling-Guide.md` |
| EDR Exclusion Management | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Exclusion-Management.md` |
| Ticket Fields Standards | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md` |
| Ticket Escalation Workflow | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Escalation-Workflow.md` |
| IRT Containment Authority Matrix | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md` |
| Client Data Segregation Policy | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md` |

---

# 18. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 25-May-2026 | SOC Manager / Threat Intelligence Lead | Initial version |

---

# 19. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**