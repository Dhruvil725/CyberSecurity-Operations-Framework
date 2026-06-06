# Threat Intelligence (TI) Integration with SIEM

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – TI Integration with SIEM |
| Document ID | TOOL-TI-003 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | SOC Manager / Threat Intelligence Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines how Threat Intelligence (TI) is integrated with the Security Information and Event Management (SIEM) platform to improve detection, triage, correlation, and response.

This integration is critical because:

- TI enrichment accelerates triage and improves analyst accuracy
- TI-driven correlation rules improve detection coverage for known threats
- Poorly tuned TI ingestion creates alert fatigue and resource waste
- SIEM correlation is often the central evidence layer for audits and incident reporting
- MSSP environments require strict tenant separation and client-specific rule baselines
- Reliable ingestion and retention are required for regulatory and forensic readiness

This SOP ensures:

- Standard ingestion and normalization of TI into SIEM
- Controlled use of TI for enrichment vs alerting vs correlation
- Defined thresholds and tuning guidance
- Consistent handling of SIEM alerts derived from TI
- Multi-tenant MSSP safe design patterns
- Audit-ready documentation for SIEM-based TI detections

---

# 3. Scope

This SOP applies to:

| Area | Included |
|---|---|
| TI content | IPs, domains, URLs, hashes, certificate fingerprints (if used), actor/campaign tags |
| SIEM functions | Enrichment, correlation rules, watchlists, threat hunting queries, dashboards |
| Data sources | Firewall, proxy, DNS, EDR, IAM, cloud logs, email security logs, web server logs |
| Environments | Internal SOC and MSSP-managed clients (multi-tenant) |
| Outputs | Alerts, dashboards, threat hunting leads, incident tickets |

Out of scope:

- EDR enforcement actions based on TI (covered in TI Integration with EDR)
- TI feed onboarding/retirement (covered in TI Feed Management)

---

# 4. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| TI Lead | Defines TI sources, scoring, TTL, tagging; approves promotion for alerting use |
| SIEM Engineer / Detection Engineer | Implements ingestion pipelines, lookup tables, correlation rules, dashboards |
| SOC Lead | Approves operational alerting thresholds and response procedures |
| L1 Analyst | Triage of SIEM alerts including TI context and evidence references |
| L2 Analyst | Deep investigation, correlation expansion, IOC validation feedback |
| L3 Analyst | Advanced analysis, threat hunting, detection improvement recommendations |
| IR Team Lead | Approves major incident escalation driven by TI-based detections |
| MSSP Service Delivery | Ensures client-specific baselines, SLAs, and communications |

References:
`04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Use-Cases-Master.md`  
`04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md`  
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Feed-Management.md`

---

# 5. Integration Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Enrichment-first | New TI feeds start as enrichment, not alerting |
| Confidence and context | Alerting requires confidence + context (asset criticality, event type, frequency) |
| TTL and aging | Indicators must expire; stale IOCs must not generate alerts |
| Source attribution | Every match must record the TI feed/source(s) |
| Noise control | Thresholds and allowlists must be used to reduce false positives |
| Multi-tenant segregation | TI data and rules must not cross client boundaries (MSSP) |
| Audit-ready | Logging, rule changes, and match evidence must be traceable |

---

# 6. Integration Architecture (Logical)

## 6.1 TI to SIEM Data Methods

| Method | Description | Recommended Use |
|---|---|---|
| Lookup tables / watchlists | SIEM-native lists for fast matching | IP/domain/hash matching in events |
| Enrichment API | SIEM queries TI platform on-demand | Analyst enrichment during triage |
| Ingest TI as event stream | TI indicators stored as indexed data | Advanced hunting/correlation (careful with cost) |
| SOAR-mediated ingestion | SOAR pushes curated IOCs to SIEM | High-control, low-noise workflows |

---

## 6.2 Matching Modes

| Mode | Purpose | Default |
|---|---|---|
| Enrichment | Add context to events (reputation, tags, confidence) | Enabled |
| Alert-only | Alert when a match occurs with minimal logic | Disabled by default |
| Correlation | Alert when match occurs + supporting context | Enabled for curated high-confidence IOCs |
| Hunting | Queries to find historical occurrences | Enabled |

---

# 7. Data Normalization Requirements (Mandatory)

Before matching TI against logs, normalize:

| Data Type | Normalization Rule |
|---|---|
| IP | Parse IPv4/IPv6; remove ports; validate formatting |
| Domain | Lowercase; strip trailing dots; extract root domain when needed |
| URL | Normalize scheme/host; decode safely; extract host and path |
| Hash | Identify MD5/SHA1/SHA256; validate length; canonical lowercase |
| Username | Normalize case and domain prefix; map to canonical identity |
| Hostname | Normalize FQDN vs short name; map to asset inventory tag |

Indicators failing validation must be rejected or quarantined (per TI Feed Management).

---

# 8. Confidence, Scoring, and Thresholds

## 8.1 Confidence Levels

Standard confidence mapping:

| Level | Definition | Default SIEM Use |
|---|---|---|
| High | Verified, reliable source; low expected FP | Correlation / alerting allowed |
| Medium | Generally reliable but may contain noise | Enrichment + limited correlation |
| Low | Unverified, high noise, broad lists | Enrichment only |

If numeric scoring exists, document conversion rules in TI platform and ingestion pipeline.

---

## 8.2 Default Thresholds for Alerting (Guidance)

Alerting should not be based on a single match unless risk justifies it.

Recommended minimum conditions:

| Indicator Type | Alerting Guidance |
|---|---|
| Hash | Single match may alert (if high confidence and execution event) |
| Domain/URL | Require supporting event (proxy/DNS + process/user context) |
| IP | Require repeated connections or high-risk destination + supporting telemetry |
| Email sender | Require additional phishing indicators; high FP risk |

---

# 9. Use Case Patterns (Standard)

## 9.1 Enrichment Pattern (Default)

Objective: Enrich alerts and investigations.

SIEM must display:

- IOC value and type
- TI source/feed
- Confidence
- Tags (malware family, actor, campaign)
- First seen / last seen (if available)
- TTL / expiry date
- Link to TI platform record (if applicable)

---

## 9.2 Correlation Pattern (Preferred for Alerting)

Objective: Reduce noise by combining TI match with behavioral/asset context.

Examples (conceptual):

- DNS query to TI domain **AND** process is suspicious (PowerShell, mshta, rundll32)
- Proxy connection to TI URL **AND** downloaded file executed
- Firewall outbound to TI IP **AND** from privileged server or DC
- Hash match **AND** execution on multiple hosts within 15 minutes (possible spread)

All correlation rules must be documented in the SIEM use case library.

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Use-Cases-Master.md`

---

## 9.3 Hunting Pattern

Objective: Find historical exposure.

Hunting queries should support:

- Search for IOC occurrences over time windows
- Pivoting on entities (host, user, process, IP)
- Summaries by asset criticality and user privilege
- Exportable evidence references for tickets

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Query-Library.md`

---

# 10. SIEM Implementation Workflow

## 10.1 Step 1 — Preconditions

| Item | Requirement |
|---|---|
| TI feed catalog entry exists | Mandatory |
| Intended SIEM use defined (enrich/alert/correlate/hunt) | Mandatory |
| Tenant scope defined (MSSP) | Mandatory |
| TTL and confidence mapping configured | Mandatory |
| Change ticket created | Mandatory for production |

---

## 10.2 Step 2 — Ingestion and Storage Strategy

Choose storage strategy based on volume:

| Feed Volume | Recommended Strategy |
|---|---|
| Low/Medium | SIEM lookup/watchlist |
| High | Curate in TI platform; push only high confidence subset to SIEM |
| Burst/volatile | Enrichment only; avoid heavy indexing |

Mandatory: deduplicate indicators and preserve multi-source attribution.

---

## 10.3 Step 3 — Matching Implementation

Implementation must include:

| Component | Requirement |
|---|---|
| Lookup/watchlist matching | Mandatory for IOC matching |
| TTL enforcement | Mandatory |
| Confidence threshold | Mandatory |
| Allowlist support | Mandatory |
| Source attribution fields | Mandatory |
| Logging of match events | Mandatory |

---

## 10.4 Step 4 — Rule Tuning and Testing

Before enabling production alerting:

| Task | Requirement |
|---|---|
| Run in monitor mode | Mandatory |
| Measure match/noise rate | Mandatory |
| Validate top matches | Mandatory |
| Adjust thresholds | Mandatory |
| Create rollback plan | Mandatory |
| SOC Lead approval | Mandatory |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md`

---

## 10.5 Step 5 — Production Enablement

Once approved:

- Enable correlation rule(s)
- Confirm alert routing to ticketing
- Confirm playbook linkage (where supported)
- Update SIEM use case documentation
- Enable dashboards for visibility

---

# 11. Alert Handling Requirements (TI-Based SIEM Alerts)

When a TI-based SIEM alert triggers, the ticket must include:

| Required Detail | Notes |
|---|---|
| Matched IOC value/type | Mandatory |
| TI source/feed | Mandatory |
| Confidence level | Mandatory |
| Event type and log source | DNS/proxy/firewall/EDR etc |
| Entity context | host/user/process |
| Asset criticality / user privilege | Mandatory |
| Match time (UTC) | Mandatory |
| Related events (if correlation) | Mandatory |
| Next steps | Escalation/containment/hunting |

References:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`  
`03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Alert-Handling-SOP.md`

---

# 12. MSSP Multi-Tenant Requirements (Mandatory)

For MSSP environments:

| Requirement | Standard |
|---|---|
| Separate watchlists per tenant | Mandatory |
| Separate rules per tenant (or tenant-aware filtering) | Mandatory |
| Tenant ID tagging on all events/alerts | Mandatory |
| No cross-tenant enrichment | Mandatory |
| Client-specific thresholds | Mandatory where contract requires |
| Per-tenant dashboards and reporting | Mandatory |

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 13. Change Management and Control

All SIEM TI changes must be controlled via ticket:

| Change Type | Requires Ticket | Approval |
|---|---|---|
| Add/modify TI lookup | Yes | SIEM Engineer + TI Lead |
| Enable/disable TI alert rule | Yes | SOC Lead |
| Modify thresholds/confidence | Yes | SOC Lead + TI Lead |
| Add allowlist exceptions | Yes | SOC Lead |
| Retire TI feed from SIEM | Yes | TI Lead |

Rule changes must record:

- Who changed it
- When (UTC)
- What changed
- Why (justification)
- Rollback method

---

# 14. Monitoring and Health Checks

Minimum monitoring requirements:

| Check | Requirement |
|---|---|
| TI lookup freshness | Mandatory |
| Lookup ingestion success | Mandatory |
| Match volume anomalies | Mandatory |
| Rule execution failures | Mandatory |
| Alert routing failures | Mandatory |
| TTL expiration functioning | Mandatory |

---

# 15. Troubleshooting Guide (Common Issues)

| Symptom | Likely Cause | Action |
|---|---|---|
| Sudden alert spike | Feed quality issue / threshold too low | Switch to enrichment; raise confidence threshold; add allowlist |
| No matches at all | Lookup not updating | Verify ingestion job and last updated time |
| Old IOCs triggering | TTL not enforced | Fix expiry logic; rebuild lookup |
| Many benign domains flagged | Open-source feed too broad | Filter categories; use high-confidence subset |
| High SIEM cost/latency | High-volume TI indexed | Move to lookup-only; curate; reduce retention |

---

# 16. Metrics and KPIs (Monthly Minimum)

Track per tenant (MSSP) and globally:

| KPI | Definition |
|---|---|
| Lookup freshness SLA | % time TI lookups updated within expected window |
| TI match rate | Matches/day by IOC type and confidence |
| Actionable rate | % matches resulting in TP investigation |
| False positive rate | % matches closed as FP/INFO |
| Rule precision | Alerts that are TP / total alerts |
| Time-to-triage improvement | Reduction in MTTA/MTTR where TI contributed |
| Top noisy indicators | Most frequent benign matches (tuning targets) |

---

# 17. Evidence and Audit Readiness

Maintain:

| Evidence | Where |
|---|---|
| Feed catalog and scoring policy | TI documentation |
| SIEM lookup configurations (sanitized exports) | SIEM admin records |
| Correlation rules and change logs | SIEM change history + tickets |
| Alert samples and tickets | Ticketing system |
| Dashboards/reports | SOC reporting folder |

---

# 18. Related Documents

| Document | Path |
|---|---|
| TI Feed Management | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Feed-Management.md` |
| TI IoC Handling SOP | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md` |
| TI Integration with EDR | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Integration-with-EDR.md` |
| TI Platform Usage Guide | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Platform-Usage-Guide.md` |
| SIEM Use Cases Master | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Use-Cases-Master.md` |
| SIEM Alert Tuning Guide | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md` |
| SIEM Query Library | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Query-Library.md` |
| L1 Alert Handling SOP | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Alert-Handling-SOP.md` |
| Ticket Fields Standards | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md` |
| Client Data Segregation Policy | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md` |

---

# 19. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 25-May-2026 | SOC Manager / Threat Intelligence Lead | Initial version |

---

# 20. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**