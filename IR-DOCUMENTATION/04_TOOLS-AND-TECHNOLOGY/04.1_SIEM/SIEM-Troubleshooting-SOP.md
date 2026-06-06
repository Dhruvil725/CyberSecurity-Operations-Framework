# SOP: SIEM Troubleshooting Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – SIEM Troubleshooting Procedures |
| Document ID | TOOL-SIEM-004 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / SIEM Engineering Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the standardized troubleshooting methodology for the SIEM platform and its integrations. It is designed to help SOC Operations and SIEM Engineering teams rapidly identify, isolate, and resolve SIEM issues that impact:

- Log ingestion and telemetry coverage
- Parsing and normalization
- Correlation rules and alerting
- Dashboards and reporting
- Search performance and availability
- Storage and retention compliance
- MSSP multi-tenant data segregation
- Audit-readiness and evidence reliability

SIEM troubleshooting is critical because SIEM degradation can cause:

- Detection blind spots (missed incidents)
- Delayed investigations (increased dwell time)
- SLA breaches (delayed response/notification)
- Compliance failures (missing required logs/retention)
- Increased false positives (parsing failures)
- Operational instability (indexing/search issues)

This SOP ensures:

- Consistent troubleshooting steps
- Clear ownership and escalation paths
- Accurate incident documentation
- Controlled change execution
- Audit-ready operational records

---

# 3. Scope

This SOP applies to troubleshooting of:

| Area | Examples |
|---|---|
| Ingestion failures | Logs not arriving from firewall/EDR |
| Integration failures | Cloud API auth failure |
| Parsing/normalization issues | Field extraction broken after vendor update |
| Correlation/alerting failures | Alerts not firing for known behavior |
| Alert noise spikes | Sudden false positives |
| Performance issues | Slow searches, backlog |
| Storage/retention issues | Index nearing capacity |
| Availability issues | SIEM UI down, collector down |
| Multi-tenant/MSSP issues | Cross-tenant index misrouting |
| Reporting issues | Dashboards empty, scheduled reports failing |

---

# 4. Definitions

| Term | Definition |
|---|---|
| Data Source | System generating logs (firewall, EDR, AD, Cloud) |
| Collector/Forwarder | Component that sends logs to SIEM (agent, syslog, API connector) |
| Parsing | Extracting fields from raw logs |
| Normalization | Mapping fields to a common schema |
| EPS | Events per second |
| Latency | Delay between event time and SIEM ingest time |
| Coverage Gap | Missing telemetry required for a use case |
| “Source Silence” | No events received from a data source |
| MSSP Tenant | A logically separated client environment within the SIEM |

---

# 5. Roles and Responsibilities

| Role | Responsibility |
|---|---|
| L1 SOC Analyst | Detect issue symptoms, open ticket, basic checks (dashboard/health page) |
| L2 SOC Analyst | Validate impact to investigations, confirm patterns, provide evidence |
| SOC Lead | Prioritize, assess SLA impact, coordinate escalation |
| SIEM Engineer | Technical troubleshooting and remediation |
| Detection Engineering Lead | Validate correlation/use-case impacts and rule tuning |
| Infrastructure/Platform Team | Underlying server, network, storage issues |
| Cloud Team | Cloud connector permissions, API issues |
| Network Team | Syslog routing, firewall rules, network path |
| Service Delivery (MSSP) | Client communications for monitoring gaps or SLA risk |
| CISO | Awareness for critical SIEM outages or regulatory-impacting gaps |

---

# 6. Troubleshooting Principles (IMPORTANT)

1. **Safety first:** Troubleshooting must not create new blind spots or cross-tenant exposure.
2. **Confirm impact:** Determine which sources/use cases/tenants are affected.
3. **Work from evidence:** Use timestamps, ingestion metrics, and raw event samples.
4. **Change control:** Any configuration change must be logged and approved as required.
5. **Restore visibility quickly:** If root cause takes time, implement temporary mitigations.
6. **Document everything:** Troubleshooting actions are audit evidence.

---

# 7. Severity Classification for SIEM Issues

| Severity | Description | Example | Response Target |
|---|---|---|---|
| SEV-1 (Critical) | SIEM unavailable OR critical sources offline OR cross-tenant risk | EDR + AD logs stopped | Immediate |
| SEV-2 (High) | Major degradation affecting key detections | CloudTrail ingestion delayed 6h | ≤ 30 min |
| SEV-3 (Medium) | Partial issues, limited coverage impact | Parsing errors on one sourcetype | ≤ 2 hours |
| SEV-4 (Low) | Cosmetic/reporting-only, no detection impact | Dashboard visualization issue | Next business day |

---

# 8. Standard Troubleshooting Workflow

| Phase | Objective | Output |
|---|---|---|
| Phase 1 | Identify and log symptoms | SIEM Troubleshooting Ticket |
| Phase 2 | Impact assessment | Affected sources/use cases/tenants |
| Phase 3 | Triage and classification | Severity + owner assigned |
| Phase 4 | Root cause investigation | Confirmed failure domain |
| Phase 5 | Mitigation and restoration | Visibility restored |
| Phase 6 | Validation | Health checks + test events |
| Phase 7 | Documentation and closure | RCA notes + prevention actions |

---

# 9. Phase 1 — Identify and Log Symptoms

## 9.1 Common Symptoms

| Symptom | Likely Area |
|---|---|
| No alerts firing at all | Correlation engine / ingestion |
| Dashboards show “0 events” | Ingestion / index / permissions |
| Events arriving but missing key fields | Parsing/normalization |
| Spike in false positives | Parser drift / environment change |
| Search is slow/timeouts | Capacity / index health |
| Data delayed (high latency) | Pipeline backlog / forwarder / API throttling |
| Tenant data mixed | MSSP segregation configuration issue |

## 9.2 Ticket Creation Requirements (Mandatory)

| Required Field | Description |
|---|---|
| Incident/Ticket ID | SIEM issue tracking |
| Reporter | Name/shift/team |
| Start time (UTC) | When the issue started |
| First detection time (UTC) | When noticed by SOC |
| Symptoms | What is wrong |
| Affected tenants | MSSP client list (if applicable) |
| Affected sources | Data source names |
| Evidence | Screenshots/log counts/alerts impacted |
| Business/SOC impact | Which detections/investigations affected |
| Severity | SEV-1 to SEV-4 |
| Escalations | Who was notified |

---

# 10. Phase 2 — Impact Assessment

## 10.1 Impact Assessment Checklist

| Item | Completed |
|---|---|
| Affected tenant(s) identified | ☐ |
| Affected data sources identified | ☐ |
| Affected use cases identified | ☐ |
| Time window of impact estimated | ☐ |
| SIEM ingestion latency measured | ☐ |
| Correlation/alerting impact checked | ☐ |
| SLA/regulatory risk assessed | ☐ |

## 10.2 Impact Matrix (Fill During Incident)

| Affected Area | Scope | Risk Level | Notes |
|---|---|---|---|
| Tenant(s) |  |  |  |
| Data sources |  |  |  |
| Use cases |  |  |  |
| Alerts |  |  |  |
| Reporting |  |  |  |

---

# 11. Phase 3 — Triage and Ownership

## 11.1 Assign the Failure Domain

| Failure Domain | Ownership (Primary) | Secondary |
|---|---|---|
| Data source offline | Source owner team | SOC Lead |
| Collector/forwarder down | SIEM Engineering | Platform team |
| Network path/syslog routing | Network team | SIEM Engineering |
| Cloud API auth/throttle | Cloud team | SIEM Engineering |
| Parsing broken | SIEM Engineering | Detection Engineering |
| Correlation engine failure | SIEM Engineering | Detection Engineering |
| Storage/capacity | Platform team | SIEM Engineering |
| MSSP segregation issue | SIEM Engineering + Security Governance | Service Delivery |

## 11.2 Escalation Requirements

| Condition | Escalate To | Timing |
|---|---|---|
| SEV-1 declared | SOC Manager + SIEM Lead + CISO | Immediate |
| Tenant segregation risk | SOC Manager + CISO + Legal (if needed) | Immediate |
| EDR/AD/Firewall logs offline | IR Lead + SOC Lead | Immediate |
| SLA breach imminent | SOC Lead + Service Delivery | Immediate |
| Regulatory log gaps suspected | Compliance | Within 30 min |

---

# 12. Phase 4 — Root Cause Investigation (Playbook by Problem Type)

## 12.1 Problem Type A — “No Logs from a Data Source” (Source Silence)

### Investigation Steps

| Step | Check | Expected Outcome |
|---|---|---|
| 1 | Confirm last event timestamp in SIEM | Identify silence start time |
| 2 | Verify ingestion metrics for that source | Confirm drop to zero |
| 3 | Confirm collector status (agent/syslog/API) | Collector healthy or failing |
| 4 | Validate network path (syslog TCP/TLS, firewall rules) | Connectivity confirmed |
| 5 | Validate source configuration changes | Identify recent changes |
| 6 | Validate credentials/certs (API/TLS) | Not expired/revoked |
| 7 | Perform controlled test event (where allowed) | Confirm restored ingestion |

### Evidence Table

| Data Source | Last Event UTC | Collector | Transport | Notes |
|---|---|---|---|---|
|  |  |  |  |  |

---

## 12.2 Problem Type B — “Logs Arrive but Fields are Missing” (Parsing/Normalization Failure)

### Common Causes

| Cause | Example |
|---|---|
| Vendor format change | Firmware update changed syslog format |
| Parser misconfiguration | Wrong sourcetype assigned |
| Multiline/log truncation | Application logs truncated |
| Encoding/time format change | Timestamp no longer ISO |
| Collector re-tagging | Forwarder rewriting fields |

### Investigation Steps

| Step | Check | Expected Outcome |
|---|---|---|
| 1 | Compare raw log samples: before vs after issue | Identify format change |
| 2 | Validate parsing rules/sourcetype mapping | Correct mapping applied |
| 3 | Check parser error dashboards | Error rate confirmed |
| 4 | Validate normalization field mapping | Required fields present |
| 5 | Update parser in test/staging (if available) | Correct extraction |
| 6 | Deploy parser update with change record | Production restored |
| 7 | Validate key detections impacted | Alerts now accurate |

### Parser Issue Tracking Table

| Sourcetype | Parsing Error % | First Seen UTC | Impacted Fields | Fix Applied |
|---|---:|---|---|---|
|  |  |  |  |  |

---

## 12.3 Problem Type C — “Alerts Not Firing” (Correlation/Use Case Failure)

### Investigation Steps

| Step | Check | Expected Outcome |
|---|---|---|
| 1 | Confirm logs exist for the behavior | Data present |
| 2 | Confirm rule enabled and scheduled | Rule active |
| 3 | Validate rule logic against current schema | Field names valid |
| 4 | Check rule execution errors | No runtime errors |
| 5 | Check lookups/feeds dependencies | TI lookups working |
| 6 | Validate time window and indexing delays | Delay accounted |
| 7 | Replay/test on known events (safe) | Alert triggers |

### Correlation Dependency Checklist

| Dependency | Status |
|---|---|
| Required index/sourcetype present | ☐ |
| Required normalized fields present | ☐ |
| Lookup tables available | ☐ |
| Threat intel enrichment operational | ☐ |
| Rule scheduler operating | ☐ |
| Permissions/roles correct | ☐ |

---

## 12.4 Problem Type D — “False Positive Spike / Alert Noise Surge”

### Common Causes

| Cause | Example |
|---|---|
| New IT activity | Patch rollout triggers scans |
| Baseline shifted | New business process |
| Parsing drift | Fields mis-mapped |
| TI feed contamination | Bad IOC list |
| Threshold too sensitive | Login failures threshold too low |

### Investigation Steps

| Step | Check | Expected Outcome |
|---|---|---|
| 1 | Quantify increase (volume, timeframe) | Measured delta |
| 2 | Identify top talkers (users/hosts/IPs) | Common patterns |
| 3 | Validate whether activity is legitimate | Confirm benign cause |
| 4 | Review parser correctness | Ensure fields accurate |
| 5 | Apply tuning (threshold/whitelist/suppression) | Noise reduced |
| 6 | Validate no detection gaps introduced | Detection preserved |
| 7 | Document tuning change | Audit trail created |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md`

---

## 12.5 Problem Type E — “High Ingestion Latency / Backlog”

### Common Causes

| Cause | Example |
|---|---|
| Forwarder queue backlog | Collector disk full |
| SIEM indexing saturation | EPS too high |
| Cloud API throttling | AWS rate limit |
| Network congestion | Packet loss |
| Storage I/O bottleneck | Indexer disk latency |

### Investigation Steps

| Step | Check | Expected Outcome |
|---|---|---|
| 1 | Measure latency (event_time vs ingest_time) | Quantified delay |
| 2 | Check EPS vs capacity baseline | Confirm overload |
| 3 | Check collector queues/health | Identify bottleneck |
| 4 | Check indexer/search head health | Resource constraints |
| 5 | Prioritize critical sources | Maintain detection |
| 6 | Implement temporary throttling or routing | Stabilize system |
| 7 | Capacity escalation | Plan scale/retention |

### Latency Tracking Table

| Source | Avg Latency | Max Latency | Start UTC | Current Status |
|---|---:|---:|---|---|
|  |  |  |  |  |

---

## 12.6 Problem Type F — “Search Performance Issues”

### Investigation Steps

| Step | Check | Expected Outcome |
|---|---|---|
| 1 | Confirm which searches are failing | Identify top offenders |
| 2 | Validate index selection/time range | Reduce scope |
| 3 | Check system health metrics | CPU/RAM/disk |
| 4 | Validate data model acceleration (if used) | Performance improved |
| 5 | Optimize heavy queries | Use indexed fields |
| 6 | Validate retention and storage | Reduce fragmentation |
| 7 | Escalate capacity if needed | Prevent recurrence |

---

## 12.7 Problem Type G — MSSP Tenant Segregation Risk (CRITICAL)

### Immediate Actions (Mandatory)

| Step | Action |
|---|---|
| 1 | Stop any automation that may propagate cross-tenant mixing |
| 2 | Restrict analyst access temporarily (least privilege) |
| 3 | Notify SOC Manager and CISO immediately |
| 4 | Identify affected tenants and time window |
| 5 | Preserve evidence (configs/log samples) for audit |
| 6 | Implement containment: isolate tenant pipelines/indexes |
| 7 | Validate restoration with controlled checks |

### Segregation Validation Table

| Tenant | Index/Workspace | Tag Used | Mixed Data Seen? | Action Taken |
|---|---|---|---|---|
|  |  |  |  |  |

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 13. Phase 5 — Mitigation and Restoration

## 13.1 Mitigation Priority

During major incidents, restore visibility in this order:

1. Identity (AD/Entra ID/MFA/VPN)
2. EDR/XDR telemetry
3. Perimeter firewall + proxy
4. Cloud audit logs (AWS/Azure/GCP/M365)
5. Critical server/application logs
6. Remaining sources

## 13.2 Mitigation Actions (Examples)

| Mitigation | When Used | Risk |
|---|---|---|
| Switch transport to TCP/TLS | Syslog packet loss | Requires coordination |
| Temporary increased buffer | Forwarder queue saturation | Disk utilization |
| Pause non-critical ingestion | Capacity overload | Reduced visibility |
| Fix parser mapping | Field loss | Must validate |
| Rotate/renew API credentials | Cloud auth failure | Access management |
| Scale indexers/storage | Sustained EPS growth | Change management |

---

# 14. Phase 6 — Validation

## 14.1 Validation Checklist (Mandatory)

| Validation Item | Completed |
|---|---|
| Ingestion restored for affected sources | ☐ |
| Parsing errors reduced to normal baseline | ☐ |
| Latency within acceptable thresholds | ☐ |
| Critical correlation rules validated | ☐ |
| Dashboards updated correctly | ☐ |
| MSSP tenant segregation validated (if applicable) | ☐ |
| Tickets updated with evidence and times | ☐ |

## 14.2 Post-Restore Verification Table

| Source | Events/Hour Normal? | Last Event UTC | Parsing OK? | Notes |
|---|---|---|---|---|
|  |  |  |  |  |

---

# 15. Phase 7 — Documentation and Closure

## 15.1 Required Closure Documentation

| Requirement | Mandatory |
|---|---|
| Start and end time (UTC) | Yes |
| Root cause | Yes (or “pending RCA”) |
| Affected sources and tenants | Yes |
| Actions taken | Yes |
| Evidence collected | Yes |
| Validation performed | Yes |
| Follow-up tasks | Yes |
| Preventive actions | Yes |

## 15.2 SIEM Troubleshooting Timeline Log

| Timestamp UTC | Action | Owner | Outcome |
|---|---|---|---|
|  |  |  |  |

## 15.3 Preventive Actions Register

| Preventive Action | Owner | Due Date | Status |
|---|---|---|---|
|  |  |  |  |

Reference:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

---

# 16. Troubleshooting Quick Reference (Summary)

| Issue | Fast Check | Likely Owner |
|---|---|---|
| No logs from source | Last event time, ingestion rate | SIEM Eng / Source owner |
| Fields missing | Raw sample vs parsed fields | SIEM Eng |
| Alerts not firing | Data present + rule enabled | SIEM Eng / Detection Eng |
| Noise spike | Top offenders + baseline shift | Detection Eng |
| High latency | backlog/queue/EPS health | SIEM Eng / Platform |
| Slow searches | query scope + health metrics | SIEM Eng / Platform |
| Tenant mixing | stop + isolate + escalate | SIEM Eng + CISO |

---

# 17. MSSP-Specific Requirements

For MSSP environments, SIEM troubleshooting must additionally ensure:

- Tenant segregation is preserved at all times
- Troubleshooting does not expose cross-client logs
- Client communications occur if monitoring gaps impact SLAs
- Client-specific integration health is validated independently
- Evidence is stored per client and per contract

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/`

---

# 18. Related Documents

| Document | Path |
|---|---|
| SIEM Integration Map | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Integration-Map.md` |
| SIEM Alert Tuning Guide | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md` |
| SIEM Query Library | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Query-Library.md` |
| SIEM Use Cases Master | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Use-Cases-Master.md` |
| Client Data Segregation Policy | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md` |
| SLA Breach Escalation Procedure | `00_GOVERNANCE/00.4_SLA-and-SLO/SLA-Breach-Escalation-Procedure.md` |

---

# 19. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | SIEM Engineering Lead | Initial version |

---

# 20. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**