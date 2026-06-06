# GUIDE: SIEM Integration Map

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | GUIDE – SIEM Integration Map |
| Document ID | TOOL-SIEM-002 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / SIEM Engineering Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This document defines the operational architecture, data source integrations, log ingestion standards, integration health monitoring procedures, and governance requirements for the SIEM platform integration ecosystem.

The SIEM integration map is a critical operational reference that provides:

- Complete visibility into all data sources feeding the SIEM
- Integration health status
- Log ingestion coverage validation
- Detection capability dependency tracking
- Troubleshooting reference
- Compliance evidence for audit activities
- Gap analysis support
- Onboarding reference for new integrations

The SIEM is only as effective as the data it receives.

Missing or degraded integrations directly impact:

- Detection capability
- Incident investigation quality
- Threat hunting effectiveness
- Compliance monitoring
- SLA compliance
- Regulatory reporting accuracy

This guide ensures:

- Comprehensive integration documentation
- Integration health visibility
- Standardized onboarding procedures
- Audit-ready integration records
- Continuous coverage monitoring
- Gap identification and remediation

---

# 3. Scope

This guide applies to all SIEM data integrations involving:

| Integration Category | Example |
|---|---|
| Endpoint security | EDR telemetry |
| Network security | Firewall logs |
| Identity and access | Active Directory |
| Cloud platforms | AWS CloudTrail |
| Application security | Web server logs |
| Email security | Exchange logs |
| Threat intelligence | IOC feeds |
| Vulnerability management | Scan results |
| Physical security | Badge access |
| OT/ICS | Industrial systems |

---

## 3.1 Applicable SIEM Platforms

| Platform | Version |
|---|---|
| Splunk Enterprise/Cloud | Current |
| Microsoft Sentinel | Current |
| IBM QRadar | Current |
| Elastic SIEM | Current |
| Other approved platforms | Current |

---

# 4. Integration Architecture Overview

The SIEM integration architecture consists of the following layers.

---

## 4.1 Integration Architecture Layers

| Layer | Description |
|---|---|
| Data Sources | Systems generating security events |
| Collection Methods | Agents, APIs, Syslog, connectors |
| Transport Layer | Network paths to SIEM |
| Normalization | Log parsing and field mapping |
| Correlation Engine | Detection rules and use cases |
| Analytics | Dashboards and reporting |

---

## 4.2 Collection Method Categories

| Collection Method | Usage |
|---|---|
| Syslog (UDP/TCP) | Network devices |
| Agent-based collection | Endpoints |
| API integration | Cloud platforms |
| File-based collection | Application logs |
| Database connectors | CMDB, ticketing |
| Native connectors | Vendor-specific |

---

# 5. Data Source Integration Register

---

## 5.1 Endpoint Integrations

| Data Source | Collection Method | Log Types | Criticality | Status |
|---|---|---|---|---|
| Windows Endpoints | Agent/WEC | Security, System, Application | Critical | Active |
| Linux Endpoints | Syslog/Agent | Auth, Syslog, Audit | Critical | Active |
| macOS Endpoints | Agent | Unified Log | High | Active |
| EDR Platform | API/Agent | Alerts, Telemetry | Critical | Active |
| Antivirus Platform | API/Agent | Detections | High | Active |

---

## 5.2 Network Integrations

| Data Source | Collection Method | Log Types | Criticality | Status |
|---|---|---|---|---|
| Perimeter Firewall | Syslog | Traffic, Threat | Critical | Active |
| Internal Firewall | Syslog | Traffic | Critical | Active |
| IDS/IPS | Syslog | Alerts | Critical | Active |
| VPN Gateway | Syslog | Authentication | Critical | Active |
| Network Switches | Syslog | MAC, SNMP | Medium | Active |
| Wireless Controller | Syslog | Association, Auth | Medium | Active |
| Network Flow | NetFlow/sFlow | Traffic patterns | High | Active |

---

## 5.3 Identity and Access Integrations

| Data Source | Collection Method | Log Types | Criticality | Status |
|---|---|---|---|---|
| Active Directory | WEC/API | Authentication, Changes | Critical | Active |
| Microsoft Entra ID | API | Sign-ins, Audit | Critical | Active |
| LDAP | Syslog | Authentication | High | Active |
| MFA Platform | API | Authentication | Critical | Active |
| PAM Solution | API/Syslog | Privileged access | Critical | Active |
| SSO Platform | API | Authentication | High | Active |

---

## 5.4 Cloud Platform Integrations

| Data Source | Collection Method | Log Types | Criticality | Status |
|---|---|---|---|---|
| AWS VPC Flow Logs | S3/API | Network traffic | High | Active |
| AWS GuardDuty | API | Threat detections | Critical | Active |
| Azure Activity Logs | API | Management events | Critical | Active |
| Azure Defender | API | Security alerts | Critical | Active |
| GCP Audit Logs | API | Admin activity | Critical | Active |
| GCP Security Command | API | Findings | High | Active |
| AWS CloudTrail | API | Management events | Critical | Active |
| M365 Unified Audit | API | User activity | Critical | Active |

---

## 5.5 Application Integrations

| Data Source | Collection Method | Log Types | Criticality | Status |
|---|---|---|---|---|
| Web Application Firewall | Syslog/API | Traffic, Alerts | Critical | Active |
| Web Server | Syslog/File | Access, Error | High | Active |
| Database Server | Syslog/Agent | Query, Auth | High | Active |
| Email Gateway | API/Syslog | Mail flow, Threats | Critical | Active |
| DLP Solution | API | Policy violations | High | Active |
| CASB Platform | API | Cloud activity | High | Active |

---

## 5.6 Security Tool Integrations

| Data Source | Collection Method | Log Types | Criticality | Status |
|---|---|---|---|---|
| Vulnerability Scanner | API | Scan results | High | Active |
| Threat Intelligence | API/STIX | IOC feeds | Critical | Active |
| SOAR Platform | API/Bidirectional | Case data | High | Active |
| Ticketing System | API | Incident data | Medium | Active |
| CMDB | API | Asset data | Medium | Active |

---

# 6. Integration Health Monitoring

Monitoring integration health is a critical operational activity.

---

## 6.1 Health Monitoring Objectives

| Objective | Purpose |
|---|---|
| Detect data source failures | Visibility maintenance |
| Identify ingestion delays | Timeliness assurance |
| Validate log volume | Coverage confirmation |
| Detect parsing failures | Data quality |
| Monitor license limits | Capacity management |

---

## 6.2 Health Monitoring Frequency

| Check Type | Frequency |
|---|---|
| Critical source monitoring | Every 15 minutes |
| High priority sources | Every 30 minutes |
| Standard sources | Hourly |
| Full integration audit | Daily |
| Capacity review | Weekly |

---

## 6.3 Integration Health Dashboard Areas

| Area | Monitoring Metric |
|---|---|
| Log ingestion rate | Events per second |
| Data source status | Active/Inactive |
| Parsing error rate | Error percentage |
| Ingestion delay | Latency measurement |
| License utilization | Capacity percentage |

---

## 6.4 Integration Health Status Table

| Data Source | Status | Last Event UTC | Events/Hour | Parsing Errors |
|---|---|---|---|---|
| | | | | |

---

# 7. Integration Failure Response

Integration failures must be detected and resolved rapidly.

---

## 7.1 Failure Severity Classification

| Severity | Description |
|---|---|
| Critical | Critical data source offline |
| High | Important data source degraded |
| Medium | Non-critical source offline |
| Low | Minor parsing errors |

---

## 7.2 Failure Response Procedures

| Severity | Response Time | Escalation |
|---|---|---|
| Critical | Immediate | SOC Lead + IT Operations |
| High | Within 30 minutes | SOC Lead |
| Medium | Within 2 hours | Analyst |
| Low | Next business day | Standard workflow |

---

## 7.3 Common Failure Types

| Failure Type | Common Cause | Resolution |
|---|---|---|
| No events received | Network issue | Verify connectivity |
| Parsing errors | Format change | Update parser |
| Authentication failure | Credential expiry | Renew credentials |
| Volume spike | Attack activity | Investigate and tune |
| Volume drop | Source offline | Validate source |

---

## 7.4 Integration Failure Tracking Table

| Data Source | Failure Type | Detection Time UTC | Resolution Time | Root Cause |
|---|---|---|---|---|
| | | | | |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Troubleshooting-SOP.md`

---

# 8. Log Normalization Standards

All ingested logs must be normalized to a consistent field schema.

---

## 8.1 Required Normalized Fields

| Field | Description |
|---|---|
| timestamp | UTC event time |
| source_ip | Source IP address |
| destination_ip | Destination IP |
| user | Username |
| hostname | System name |
| event_type | Event category |
| severity | Event severity |
| action | Action taken |
| outcome | Success/failure |
| log_source | Originating system |

---

## 8.2 Timestamp Standards

| Requirement | Standard |
|---|---|
| All timestamps | UTC |
| Format | ISO 8601 |
| Timezone offset | Normalized to UTC |
| Clock synchronization | NTP required |

---

## 8.3 Common Parsing Issues

| Issue | Impact | Resolution |
|---|---|---|
| Incorrect timestamp format | Timeline errors | Update parser |
| Missing field mapping | Detection failure | Update field map |
| Encoding issues | Data corruption | Encoding correction |
| Log truncation | Incomplete events | Buffer adjustment |

---

# 9. New Integration Onboarding

New data sources follow a structured onboarding process.

---

## 9.1 Onboarding Workflow

| Phase | Objective |
|---|---|
| Requirement definition | Integration scope |
| Technical design | Architecture planning |
| Lab testing | Validation |
| Parser development | Normalization |
| Use case alignment | Detection mapping |
| Production deployment | Integration activation |
| Health monitoring | Operational validation |

---

## 9.2 Onboarding Checklist

| Validation Item | Completed |
|---|---|
| Data source documented | ☐ |
| Collection method confirmed | ☐ |
| Network path validated | ☐ |
| Parser tested | ☐ |
| Field mapping validated | ☐ |
| Use cases identified | ☐ |
| Health monitoring configured | ☐ |

---

## 9.3 Integration Onboarding Table

| Data Source | Collection Method | Onboarding Date | Owner | Status |
|---|---|---|---|---|
| | | | | |

---

# 10. Integration Coverage Gap Analysis

Regular gap analysis identifies missing telemetry.

---

## 10.1 Gap Analysis Areas

| Area | Objective |
|---|---|
| Missing data sources | Coverage gaps |
| Degraded integrations | Partial visibility |
| Parsing failures | Quality gaps |
| Use case dependencies | Detection gaps |

---

## 10.2 Gap Analysis Table

| Coverage Area | Required | Current Status | Gap Risk | Action |
|---|---|---|---|---|
| | | | | |

---

## 10.3 Coverage Risk Categories

| Risk Category | Example |
|---|---|
| Critical gap | No EDR integration |
| High gap | Cloud logs missing |
| Medium gap | Application logs partial |
| Low gap | Non-critical system missing |

---

# 11. Capacity and Licensing Management

SIEM capacity must be managed proactively.

---

## 11.1 Capacity Monitoring Areas

| Area | Metric |
|---|---|
| Daily log volume | GB/day |
| Events per second | EPS |
| License utilization | Percentage |
| Storage utilization | Capacity |
| Retention compliance | Days |

---

## 11.2 Capacity Threshold Alerts

| Threshold | Action |
|---|---|
| 75% license utilization | Review and plan |
| 90% license utilization | Immediate escalation |
| Storage 80% | Expansion planning |
| EPS spike | Investigate source |

---

## 11.3 Capacity Tracking Table

| Metric | Current | Threshold | Status |
|---|---|---|---|
| | | | |

---

# 12. MSSP-Specific Integration Considerations

For MSSP-managed environments:

| Requirement | Purpose |
|---|---|
| Maintain tenant separation | Data isolation |
| Client-specific integration documentation | Audit readiness |
| Restrict cross-tenant visibility | Compliance |
| Monitor client integration health | Service quality |
| Document client data retention | Contract compliance |

---

# 13. Common Integration Mistakes

| Mistake | Operational Risk |
|---|---|
| Missing critical data sources | Detection gaps |
| No integration health monitoring | Silent failures |
| Weak parser maintenance | Data quality issues |
| No capacity planning | License breach |
| Poor documentation | Audit failures |

---

# 14. Related Documents

| Document | Path |
|---|---|
| SIEM Alert Tuning Guide | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md` |
| SIEM Use Cases Master | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Use-Cases-Master.md` |
| SIEM Query Library | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Query-Library.md` |
| SIEM Troubleshooting SOP | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Troubleshooting-SOP.md` |
| TI Integration with SIEM | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Integration-with-SIEM.md` |
| L2 SIEM Deep Investigation | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-SIEM-Deep-Investigation.md` |

---

# 15. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | SOC Manager / SIEM Engineering Lead | Initial version |

---

# 16. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**