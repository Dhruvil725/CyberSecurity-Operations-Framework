# Threat Intelligence (TI) IoC Handling SOP

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – TI Indicator of Compromise (IoC) Handling |
| Document ID | TOOL-TI-004 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | SOC Manager / Threat Intelligence Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines how Indicators of Compromise (IoCs) are received, validated, enriched, prioritized, disseminated, actioned, tracked, and retired across the SOC.

Proper IoC handling is critical because:

- Incorrect IoCs cause false positives and operational disruption
- Stale indicators reduce accuracy and waste analyst time
- Poor attribution and tagging reduces investigation speed and audit quality
- Enforcement actions (block/quarantine/isolate) require strict controls and approvals
- MSSP environments require tenant segregation and client-specific dissemination rules
- Audit and regulatory readiness requires traceable intelligence sources and documented actions

This SOP ensures:

- Standardized IoC intake and validation
- Confidence scoring and TTL enforcement
- Consistent dissemination to SIEM/EDR and hunting workflows
- Controlled approval for prevention/blocking actions
- Evidence traceability and audit-ready records
- Continuous improvement via feedback loops from investigations

---

# 3. Scope

This SOP applies to IoCs handled by the SOC for internal and MSSP-managed clients.

| IoC Type | Examples |
|---|---|
| Network | IP, domain, URL, ASN (as context) |
| File | SHA256/SHA1/MD5 hashes, file names (context only) |
| Email | Sender address/domain, reply-to, message IDs (where available) |
| Cloud | Malicious tenant IDs, access keys (handle as sensitive) |
| Certificate | Fingerprints (if supported) |
| Behavioral (context) | Mutex, registry keys, process patterns (not primary IoC) |

In scope sources:

- TI platform feeds (commercial/open-source/ISAC/vendor)
- Incident investigations (L2/L3/IR outputs)
- Threat hunting outputs
- Client-provided indicators (MSSP)
- Law enforcement or regulator advisories (where applicable)

Out of scope:

- Full malware reverse engineering process (handled under L3 procedures)
- Case management for incidents (handled via ticket lifecycle SOP)

---

# 4. Definitions

| Term | Definition |
|---|---|
| IoC | Observable artifact potentially indicating malicious activity |
| Sighting | Evidence that an IoC appears in logs/telemetry |
| Disposition | Final assessment of IoC (Malicious/Benign/Uncertain) |
| Confidence | Likelihood that the IoC is correct and relevant |
| TTL | Time-to-live; duration IoC remains active before expiry/review |
| TLP | Traffic Light Protocol (TLP:CLEAR/GREEN/AMBER/RED) controlling sharing |
| Enrichment | Additional context (reputation, whois, geo, ASN, malware family) |
| Dissemination | Pushing IoCs to SIEM/EDR/watchlists or sharing with stakeholders |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| TI Lead | Owns IoC handling program, scoring policy, dissemination approvals, quarterly review |
| SOC Lead | Approves alerting thresholds and operational deployment schedules |
| L1 Analyst | Creates tickets for TI matches; performs initial triage and escalations |
| L2 Analyst | Validates sightings, performs log/EDR checks, provides feedback (TP/FP) |
| L3 Analyst | Advanced validation, forensics correlation, malware analysis input |
| SIEM Engineer / Detection Engineer | Implements IoC lists/lookups, correlation rules, tuning, TTL enforcement |
| EDR Admin | Implements IoCs in EDR (enrich/alert/block), manages allowlists/exceptions |
| IR Team Lead | Approves blocking/preventive actions and emergency containment |
| MSSP Service Delivery | Ensures client scoping, dissemination rules, and client notifications |
| Compliance/Legal (as needed) | Advises on sharing restrictions, regulatory requirements, licensing |

---

# 6. IoC Handling Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Traceability | Every IoC must have a source reference and ingestion record |
| Validation before action | Do not block/enforce based on unvalidated IoCs |
| TTL mandatory | All IoCs must have an expiry or review date |
| Source attribution | Preserve feed/provider + collection context |
| Segregation | MSSP: No cross-client IoC dissemination unless explicitly approved |
| Evidence first | If IoC comes from an incident, preserve evidence before broad changes |
| Minimize disruption | Default to enrichment and alerting; blocking only with approval |
| Feedback loop | Analysts must record disposition outcomes for continuous tuning |

---

# 7. IoC Lifecycle Stages

| Stage | Description | Output |
|---|---|---|
| Stage 1 | Intake | IoC record created |
| Stage 2 | Validation | Format and plausibility checks |
| Stage 3 | Enrichment | Context added (confidence/tags) |
| Stage 4 | Prioritization | Scoring and action decision |
| Stage 5 | Dissemination | SIEM/EDR/watchlists/hunting |
| Stage 6 | Monitoring | Track sightings, noise, value |
| Stage 7 | Retirement | Expiry, revoke, or archive |

---

# 8. Stage 1 — IoC Intake

## 8.1 Intake Channels

| Channel | Examples |
|---|---|
| Automated feed ingestion | TAXII/API feeds into TI platform |
| Incident-generated | Hash/IP/domain extracted during investigation |
| Client provided (MSSP) | Client shares IOC list for validation |
| Threat hunting output | New suspicious infra discovered |
| Advisory/notification | CERT/Regulator/Vendor advisory |

## 8.2 Mandatory Intake Fields (IoC Record)

| Field | Requirement |
|---|---|
| IoC Value | Mandatory |
| IoC Type | Mandatory |
| Source | Mandatory (feed/provider/ticket/advisory) |
| First Seen (UTC) | Mandatory (if known) |
| Intake Time (UTC) | Mandatory |
| Collector/Submitter | Mandatory (name/team) |
| Tenant/Client ID (MSSP) | Mandatory (if applicable) |
| TLP | Mandatory (if provided) |
| Initial Confidence | Mandatory (pre-enrichment) |
| Intended Use | Enrichment / Alerting / Hunting / Blocking |
| TTL / Expiry Date | Mandatory (initial default acceptable) |

---

# 9. Stage 2 — Validation (Mandatory)

Validation must be performed before dissemination to SIEM/EDR as an alerting or blocking control.

## 9.1 Format Validation Rules

| IoC Type | Minimum Validation |
|---|---|
| IP | Valid IPv4/IPv6; exclude private ranges unless explicitly intended |
| Domain | Valid FQDN; normalized lowercase; remove trailing dot |
| URL | Valid scheme/host; normalize; safely decode; extract host |
| Hash | Validate length/type; reject malformed; prefer SHA256 |
| Email | Validate structure; normalize; high FP risk—use with caution |
| Certificate fingerprint | Validate hex formatting and length |

Invalid indicators must be marked **REJECTED** with reason and not disseminated.

## 9.2 Plausibility and Safety Checks

| Check | Requirement |
|---|---|
| Recency | IoC not older than TTL policy without justification |
| Benign overlap | Check known-safe lists/allowlists where available |
| Broadness | Avoid high-impact broad IOCs (e.g., shared CDN domains) |
| Context | Determine whether IoC is a direct indicator or merely contextual |

---

# 10. Stage 3 — Enrichment

Enrichment must add context required for correct prioritization and tuning.

## 10.1 Minimum Enrichment Fields

| Field | Requirement |
|---|---|
| Confidence (final) | Mandatory |
| Severity / Risk rating | Mandatory |
| Tags | Malware family / actor / campaign / technique (as available) |
| Source attribution | Mandatory (multi-source supported) |
| Geo/ASN/WHOIS (network IoCs) | Recommended |
| Prevalence (internal sightings) | Recommended |
| Related incidents/tickets | Mandatory if IoC originates internally |
| Notes | Recommended (analyst context) |

## 10.2 Confidence Scoring Standard

Use these baseline levels:

| Confidence | Meaning | Typical Use |
|---|---|---|
| High | Verified source and consistent context | Correlation / controlled enforcement |
| Medium | Likely malicious but may include noise | Enrichment + selective alerting |
| Low | Unverified or broad lists | Enrichment only |

If a provider supplies numeric scores, map them to Low/Medium/High and document mapping in TI platform settings.

---

# 11. Stage 4 — Prioritization and Action Decision

## 11.1 Action Decision Matrix (Guidance)

| Confidence | Asset Context | Recommended Action |
|---|---|---|
| High | Critical asset / privileged user | Alert + consider blocking (with approval) |
| High | Standard asset | Alert + hunting; blocking if validated |
| Medium | Any | Enrichment + correlation-based alerting |
| Low | Any | Enrichment only; no alerting/blocking |

## 11.2 Special High-Risk Conditions (Escalate)

Escalate to SOC Lead / IR Team for decision if any apply:

- IoC linked to ransomware campaigns
- IoC indicates active C2 infrastructure
- IoC appears on domain controller / privileged hosts
- IoC is being considered for blocking in production
- IoC relates to regulatory-reportable incidents (data breach indicators)

---

# 12. Stage 5 — Dissemination (Controlled)

## 12.1 Dissemination Targets

| Target | Method | Use |
|---|---|---|
| TI platform | Master record | Source of truth |
| SIEM | Lookup/watchlist + correlation rules | Detection/hunting |
| EDR | Enrichment/alert/block lists | Endpoint detection/prevention |
| SOC analysts | Daily/weekly bulletin | Awareness + hunting |
| MSSP clients | Client notifications (contract-defined) | Client action and awareness |

References:
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Integration-with-SIEM.md`  
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Integration-with-EDR.md`

## 12.2 Dissemination Controls (Mandatory)

| Control | Requirement |
|---|---|
| TTL/expiry applied | Mandatory |
| Source attribution preserved | Mandatory |
| Tenant/client tagging applied (MSSP) | Mandatory |
| Allowlist logic available | Mandatory for domain/IP based actions |
| Change record for enforcement | Mandatory for alerting/blocking deployment |
| Rollback plan for blocking | Mandatory |

## 12.3 Blocking / Prevention Approval (Mandatory)

Blocking (EDR prevent, firewall block, DNS sinkhole) requires:

| Requirement | Standard |
|---|---|
| High confidence IoC | Mandatory |
| Validation completed | Mandatory |
| Impact assessment documented | Mandatory |
| IR Team Lead approval | Mandatory |
| SOC Manager approval for broad controls | Mandatory |
| MSSP client approval where contract requires | Mandatory |
| Change ticket created | Mandatory |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Block-Request-SOP.md`  
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

# 13. Stage 6 — Monitoring and Feedback Loop

## 13.1 Sighting Monitoring

Track:

| Item | Requirement |
|---|---|
| Match volume trends | Mandatory |
| TP/FP outcomes | Mandatory |
| Top noisy indicators | Mandatory |
| Missed detections (post-incident) | Recommended |
| TTL effectiveness | Mandatory |

## 13.2 Analyst Feedback Requirements (Mandatory)

For IoC matches that generate tickets, analysts must record:

- Disposition: TP/FP/INFO
- Rationale
- Evidence references (SIEM queries, EDR telemetry)
- Recommendation: keep/expire/tune/allowlist/escalate

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md`

---

# 14. Stage 7 — IoC Retirement / Expiry

IoCs must be retired when:

- TTL expires and no recent sightings justify extension
- IoC determined benign/false positive
- IoC replaced by better indicator (e.g., hash replaced by cert)
- Provider retracts/corrects the IoC
- Blocking caused disruption and is rolled back

Retirement requirements:

| Requirement | Standard |
|---|---|
| Record retirement timestamp (UTC) | Mandatory |
| Record retirement reason | Mandatory |
| Remove from SIEM/EDR enforcement lists | Mandatory |
| Retain audit trail of prior use | Mandatory |
| Update allowlists if needed | As applicable |

---

# 15. MSSP Multi-Tenant Requirements (Mandatory)

For MSSP operations:

| Requirement | Standard |
|---|---|
| Tenant scoping at intake | Mandatory |
| No cross-tenant dissemination | Mandatory unless explicitly approved |
| Client-specific TTL/thresholds (if contract requires) | Mandatory |
| Client communication documented | Mandatory when IoC impacts client |
| Evidence segregation per client | Mandatory |
| Client export restrictions (TLP/licensing) enforced | Mandatory |

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 16. Documentation Standards (IoC Record Minimum)

Every IoC record must include at least:

| Field | Requirement |
|---|---|
| IoC value/type | Mandatory |
| Source + date | Mandatory |
| Confidence | Mandatory |
| TTL/expiry | Mandatory |
| Tags | Recommended |
| Dissemination targets | Mandatory (where pushed) |
| Change ticket reference (if enforcement) | Mandatory |
| Related incident/ticket references | Mandatory (if applicable) |
| Disposition outcomes | Mandatory (if sightings occurred) |

---

# 17. Common IoC Handling Mistakes

| Mistake | Risk | Control |
|---|---|---|
| Blocking domains/IPs without validation | Business disruption | Approval + impact assessment |
| No TTL/expiry | Stale indicators create noise | TTL mandatory |
| Missing source attribution | Audit gaps | Source mandatory |
| Mixing client IoCs across tenants | Compliance breach | Tenant segregation |
| Treating low-confidence feeds as high-confidence | Alert fatigue | Confidence thresholds |
| Not recording dispositions | No improvement loop | Mandatory feedback |

---

# 18. Related Documents

| Document | Path |
|---|---|
| TI Feed Management | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Feed-Management.md` |
| TI Integration with SIEM | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Integration-with-SIEM.md` |
| TI Integration with EDR | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Integration-with-EDR.md` |
| TI Platform Usage Guide | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Platform-Usage-Guide.md` |
| Ticket Lifecycle SOP | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md` |
| Ticket Fields Standards | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md` |
| Firewall Block Request SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Block-Request-SOP.md` |
| SIEM Alert Tuning Guide | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
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
