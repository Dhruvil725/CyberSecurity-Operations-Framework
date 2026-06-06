# Threat Intelligence (TI) Feed Management

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – Threat Intelligence Feed Management |
| Document ID | TOOL-TI-001 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | SOC Manager / Threat Intelligence Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines the standard process for onboarding, validating, maintaining, monitoring, and retiring Threat Intelligence (TI) feeds used by the SOC.

Effective feed management is critical because:

- Poor-quality feeds create alert fatigue and false positives
- Feed outages reduce detection coverage and increase risk exposure
- Licensing and usage violations create compliance and legal exposure
- Incorrect confidence/scoring drives incorrect prioritization
- MSSP environments require strict tenant segregation for TI enrichment
- Audit readiness depends on documented TI sources and handling processes

This SOP ensures:

- Controlled onboarding and change management for TI feeds
- Consistent feed quality assessment and tuning
- Reliable ingestion into TI platform, SIEM, and EDR
- Clear ownership and accountability
- Measurable performance, health monitoring, and reporting
- Documented evidence for audits and client reviews

---

# 3. Scope

This SOP applies to:

| Area | Included |
|---|---|
| Feed types | Commercial, open-source, ISAC/ISAO, government, vendor, internal |
| Indicator types | IP, domain, URL, hash, email, certificate, user-agent, YARA/Sigma (where applicable) |
| Ingestion methods | API, TAXII, SFTP, email, manual upload |
| Platforms | TI Platform, SIEM, EDR, SOAR (if applicable) |
| Environments | Internal SOC, MSSP multi-tenant SOC, client environments |
| Lifecycle stages | Evaluate → Onboard → Validate → Operate → Monitor → Tune → Retire |

Out of scope:

- Technical investigation steps for individual indicators (covered in IoC SOP)
- Incident response actions triggered by TI matches (covered in playbooks)

---

# 4. Definitions

| Term | Definition |
|---|---|
| Feed | A source of TI content delivered on a schedule or in near-real-time |
| Indicator (IoC) | Observable artifact that may indicate malicious activity |
| TTP | Tactics, Techniques, and Procedures (behavioral intelligence) |
| Confidence | Likelihood that TI content is accurate/reliable |
| Fidelity | Signal usefulness for detection (low noise, actionable) |
| TTL | Time-to-live; duration an indicator remains valid |
| Enrichment | Adding context (reputation, geo, ASN, actor, campaigns) |
| STIX/TAXII | Standard format/transport for TI sharing |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| TI Lead | Own feed catalog, approve onboarding/retirement, set scoring policy, quarterly review |
| SOC Lead | Ensure operational impact is acceptable, approve alerting use-cases derived from feeds |
| L2 Analyst | Validate feed utility during investigations, report false positive patterns, recommend tuning |
| Detection Engineer / SIEM Engineer | Implement feed ingestion to SIEM, manage correlation rules, manage allowlist logic |
| EDR Admin | Implement block/alert policies derived from TI where supported, ensure safe deployment |
| MSSP Service Delivery | Confirm client contractual constraints, client-specific feed usage approvals |
| Compliance / Legal (as needed) | Review licensing terms, data handling restrictions, regulatory implications |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Platform-Usage-Guide.md`

---

# 6. Feed Management Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Quality over quantity | Only onboard feeds with measurable value |
| Document everything | Each feed must have a recorded profile in the feed catalog |
| Default to enrichment, not blocking | Feeds must not directly block traffic without validation and approval |
| Scoring must be consistent | Apply standard confidence and severity scoring |
| TTL is mandatory | Indicators must expire or be reviewed to prevent stale intelligence |
| Segregation for MSSP | Do not cross-enrich between clients unless explicitly permitted |
| Licensing compliance | Use feeds only within permitted scope and storage terms |
| Monitoring is continuous | Feed health and freshness must be monitored and alerted |

---

# 7. TI Feed Catalog (Mandatory Record)

Every feed must be registered in the **TI Feed Catalog** (maintained in the TI platform or controlled document).

Minimum fields:

| Field | Requirement |
|---|---|
| Feed Name | Mandatory |
| Provider | Mandatory |
| Feed Type | Commercial / Open / ISAC / Vendor / Internal |
| Indicator Types | IP/Domain/URL/Hash/etc |
| Delivery Method | API/TAXII/SFTP/Manual |
| Update Frequency | Real-time / Hourly / Daily / Weekly |
| Expected Volume | Approx. count/day |
| Confidence Baseline | High/Medium/Low |
| Intended Use | Enrichment / Alerting / Hunting / Blocking |
| TTL Policy | Default TTL per indicator type |
| Data Handling | Storage limits, redistribution rules, PII restrictions |
| Owner | Named owner |
| Onboard Date | Mandatory |
| Review Date | Next scheduled review |
| Status | Active / Degraded / Retired |

---

# 8. Feed Onboarding Workflow

## 8.1 Step 1 — Request and Intake

Feed onboarding may be initiated by TI Lead, SOC Lead, Detection Engineering, or client request (MSSP).

Minimum intake data:

| Item | Requirement |
|---|---|
| Business justification | Mandatory |
| Source/provider details | Mandatory |
| Licensing/terms | Mandatory (if commercial) |
| Intended use | Mandatory |
| Target platforms | Mandatory (TI Platform/SIEM/EDR) |
| Client scope (MSSP) | Mandatory (which tenant(s)) |

---

## 8.2 Step 2 — Risk and Compliance Review

Mandatory checks:

| Check | Requirement |
|---|---|
| License allows storage and internal use | Mandatory |
| Redistribution permitted/forbidden documented | Mandatory |
| Data includes PII or restricted data | Mandatory |
| Export control / jurisdiction limitations | As applicable |
| Provider credibility verification | Mandatory |

If any restriction exists, document it in the feed catalog and enforce in platform configuration (retention, sharing, export).

---

## 8.3 Step 3 — Technical Evaluation (Pilot)

Run a pilot before production onboarding.

Pilot evaluation criteria:

| Metric | Target / Guidance |
|---|---|
| Indicator validity | Sample test shows low invalid entries |
| Detection value | Produces actionable matches or enriches investigations |
| Noise rate | False positive rate acceptable for use-case |
| Freshness | Indicators updated as claimed |
| Overlap | Acceptable duplication with existing feeds |
| Format quality | Correct STIX/CSV/JSON, valid fields, consistent schema |
| Operational impact | Ingestion does not overload SIEM/EDR or correlation pipelines |

Pilot duration guidance: **7–14 days**, unless urgent.

---

## 8.4 Step 4 — Scoring and Normalization Setup

Each feed must have:

- Confidence baseline (provider reliability)
- Indicator confidence mapping (if provider supplies scores)
- Default TTL by indicator type
- Normalization rules (canonical domain format, IP validation, hash type identification)
- Deduplication logic (hash/IP/domain duplicates merged with source attribution)

---

## 8.5 Step 5 — Production Onboarding

Production onboarding includes:

| Task | Owner | Requirement |
|---|---|---|
| Configure ingestion connector | TI Lead / Engineer | Mandatory |
| Map fields to platform schema | TI Lead / Engineer | Mandatory |
| Enable validation rules | TI Lead | Mandatory |
| Configure TTL and expiration | TI Lead | Mandatory |
| Configure tags and source attribution | TI Lead | Mandatory |
| Configure SIEM integration | SIEM Engineer | As required |
| Configure EDR integration | EDR Admin | As required |
| Enable monitoring & alerts | TI Lead / SOC Lead | Mandatory |
| Document feed in catalog | TI Lead | Mandatory |

References:
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Integration-with-SIEM.md`  
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Integration-with-EDR.md`

---

# 9. Indicator Validation Rules (Mandatory)

Minimum validation checks at ingestion:

| Indicator Type | Validation Rules (Minimum) |
|---|---|
| IP | Valid IPv4/IPv6 format; exclude RFC1918 unless explicitly intended |
| Domain | Valid FQDN; normalized to lowercase; strip trailing dot |
| URL | Valid scheme and host; normalize; optionally extract domain |
| Hash | Validate length/type (MD5/SHA1/SHA256); reject malformed |
| Email | Validate structure; normalize case; note that email alone may be low confidence |
| Certificate | Validate fingerprint format; check encoding |

Indicators failing validation must be:

- Dropped, or
- Quarantined for review (preferred for commercial feeds where formatting issues occur)

---

# 10. TTL and Expiration Policy (Mandatory)

Default TTL guidance (can be adjusted per feed):

| Indicator Type | Default TTL | Notes |
|---|---|---|
| IP | 7–14 days | IPs change frequently; stale IPs create noise |
| Domain | 30 days | Domains have longer malicious lifetimes |
| URL | 14 days | URLs are often short-lived |
| Hash | 180 days | Hashes remain relevant longer; still review periodically |
| Email sender | 30 days | Use with caution; high FP risk |
| JA3/JA4 / user-agent | 30 days | High noise; use for hunting/enrichment |

All TTL exceptions must be documented in the feed catalog.

---

# 11. Operational Monitoring (Feed Health)

## 11.1 Mandatory Health Checks

Feed health must be monitored continuously (automated where possible):

| Check | Requirement |
|---|---|
| Last successful pull time | Mandatory |
| Feed freshness (last updated indicator) | Mandatory |
| Ingestion volume deviation | Mandatory |
| Error rate (parsing/validation failures) | Mandatory |
| Connector authentication health | Mandatory |
| SIEM/EDR downstream delivery status | Mandatory (if integrated) |

## 11.2 Feed Health Status States

| Status | Definition | Action |
|---|---|---|
| Active | Ingesting normally within expected baseline | No action |
| Degraded | Partial ingestion or abnormal volume/freshness | Investigate within 24 hours |
| Outage | No ingestion beyond threshold | Escalate immediately |
| Retired | Feed disabled permanently | Remove connectors and references |

## 11.3 Outage Thresholds

Recommended thresholds (adjust as needed):

| Update Frequency | Outage Threshold |
|---|---|
| Real-time / Hourly | 2 hours without successful pull |
| Daily | 36 hours without successful pull |
| Weekly | 10 days without successful pull |

---

# 12. Feed Tuning and Noise Control

## 12.1 Noise Reduction Controls

To reduce false positives and alert fatigue, implement:

- Allowlisting for known good domains/IPs (documented and reviewed)
- Internal ranges exclusion (unless explicitly targeted)
- Sector-specific filtering (BFSI vs general)
- Confidence thresholding (only alert above threshold; enrich below threshold)
- Category filtering (malware vs spam vs scanning, etc.)
- Geo/ASN restrictions (if appropriate and approved)

All tuning must be documented as a change record linked to the feed catalog entry.

---

## 12.2 Promotion Rules (Enrichment → Alerting → Blocking)

Default posture:

1. **Enrichment** (default for new feeds)
2. **Alerting** (after pilot proves value)
3. **Blocking** (only after validation and approvals)

Blocking requirements (mandatory):

| Requirement | Standard |
|---|---|
| Feed has high confidence and low noise | Mandatory |
| Impact assessment completed | Mandatory |
| SOC Lead approval | Mandatory |
| IR Team Lead approval (for automated containment/block) | Mandatory |
| Rollback plan exists | Mandatory |
| Change record created | Mandatory |

---

# 13. MSSP Multi-Tenant Requirements

For MSSP operations:

| Requirement | Standard |
|---|---|
| Tenant segregation | TI enrichment and indicator storage must not leak between clients |
| Client-specific feed usage | Only permitted feeds applied to each client |
| Client data tagging | Indicators and matches must include client/tenant ID |
| Cross-client intelligence sharing | Prohibited unless contractually allowed and approved |
| Client reporting | Feed usage and match stats available per client |

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 14. Feed Retirement Process

Feeds must be retired when:

- License expires or contract ends
- Feed quality degrades consistently
- Provider becomes unreliable
- Feed overlaps with superior feed
- Feed creates unacceptable operational noise
- Feed is replaced by a new version/source

Retirement steps:

| Step | Action | Requirement |
|---|---|---|
| 1 | Mark feed as “Retirement Candidate” | Mandatory |
| 2 | Notify SOC Lead and Detection Engineering | Mandatory |
| 3 | Disable alerting rules dependent on feed (if any) | Mandatory |
| 4 | Disable ingestion connector | Mandatory |
| 5 | Remove from SIEM/EDR pipelines (if applicable) | Mandatory |
| 6 | Update feed catalog status to “Retired” | Mandatory |
| 7 | Apply retention/licensing policy to stored data | Mandatory |
| 8 | Document retirement reason and date | Mandatory |

---

# 15. Metrics and KPIs (Feed Program Health)

Minimum KPIs tracked monthly:

| KPI | Definition |
|---|---|
| Feed uptime | % time feed is ingesting successfully |
| Freshness | Average time since last update |
| Valid indicator rate | % indicators passing validation |
| Duplicate rate | % indicators overlapping with existing sources |
| Actionable match rate | Matches that led to investigation or improvement |
| Noise rate | Matches assessed as benign/FP |
| Time-to-restore | Time to recover from feed outages |

---

# 16. Evidence and Audit Readiness

Maintain the following evidence:

| Evidence | Where |
|---|---|
| Feed catalog entries | TI platform / controlled register |
| Licensing documentation | Contract repository / TI documentation |
| Change records | Ticketing system |
| Outage records | Tickets and monitoring logs |
| Monthly KPI reports | SOC reporting folder |
| Integration proof | SIEM/EDR connector configs (sanitized exports) |

---

# 17. Related Documents

| Document | Path |
|---|---|
| TI IoC Handling SOP | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md` |
| TI Platform Usage Guide | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Platform-Usage-Guide.md` |
| TI Integration with SIEM | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Integration-with-SIEM.md` |
| TI Integration with EDR | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Integration-with-EDR.md` |
| SIEM Use Cases Master | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Use-Cases-Master.md` |
| EDR Alert Handling Guide | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Alert-Handling-Guide.md` |
| Client Data Segregation Policy | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md` |
| Internal SLA Definitions | `00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md` |

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