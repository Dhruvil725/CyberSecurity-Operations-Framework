# SOP: L3 Threat Intelligence Integration Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – L3 Threat Intelligence Integration Procedures |
| Document ID | SOC-L3-SOP-005 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / Threat Intelligence Lead |
| Approved By | IR Team Lead / CISO |
| Classification | Internal – Restricted Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the operational methodology, workflows, intelligence handling procedures, and escalation requirements for Level 3 (L3) threat intelligence integration activities.

Threat Intelligence (TI) integration is the process of collecting, validating, correlating, enriching, and operationalizing intelligence related to:

- Threat actors
- Indicators of compromise (IOCs)
- Malware campaigns
- Adversary tactics, techniques, and procedures (TTPs)
- Infrastructure abuse
- Vulnerabilities and exploits
- Emerging attack trends

Threat intelligence integration supports:

- Incident response investigations
- Threat hunting operations
- Detection engineering
- Malware analysis
- Attribution analysis
- Executive risk awareness
- Regulatory reporting
- MSSP client advisories

The objectives of this SOP are to:

- Standardize threat intelligence operations
- Ensure intelligence quality and validation
- Improve detection and response capability
- Support rapid threat correlation
- Enable proactive defense improvements
- Maintain intelligence handling security

Improper intelligence handling may result in:

- False positives
- Missed threat detection
- Incorrect attribution
- Intelligence contamination
- Unvalidated IOC deployment
- Operational disruption
- Client misinformation

This SOP ensures:

- Structured intelligence processing
- Accurate IOC validation
- Controlled intelligence distribution
- Proper escalation and reporting
- Audit-ready intelligence management

---

# 3. Scope

This SOP applies to threat intelligence activities involving:

| Intelligence Area | Example |
|---|---|
| IOC analysis | Malicious IPs |
| Malware intelligence | Malware family tracking |
| Threat actor analysis | APT profiling |
| Vulnerability intelligence | Active exploit tracking |
| Campaign tracking | Multi-stage attacks |
| Infrastructure analysis | C2 infrastructure |
| Dark web monitoring | Credential exposure |
| Cloud threat intelligence | IAM abuse |
| Sector intelligence | BFSI threats |
| MSSP intelligence sharing | Client advisories |

---

## 3.1 Intelligence Sources Covered

| Source Type | Examples |
|---|---|
| Commercial TI feeds | Recorded Future |
| Open-source intelligence (OSINT) | AbuseIPDB |
| Government advisories | CERT-In |
| Vendor advisories | Microsoft, Cisco |
| Internal intelligence | SOC investigations |
| Malware sandboxes | Behavioral analysis |
| Information sharing groups | ISAC feeds |

---

# 4. Threat Intelligence Philosophy (IMPORTANT)

Threat intelligence is not simply collecting IOCs.

The objective is to understand:

- Who the attacker is
- What the attacker targets
- How the attacker operates
- Which infrastructure is used
- Which techniques are employed
- What business risks exist
- Which defensive actions are required

Threat intelligence must be:

- Actionable
- Validated
- Contextual
- Timely
- Relevant
- Operationally useful

L3 analysts must avoid:

| Poor Practice | Operational Risk |
|---|---|
| Blind IOC blocking | Business disruption |
| Unvalidated intelligence | False positives |
| Ignoring context | Inaccurate prioritization |
| Weak IOC expiration handling | Alert fatigue |
| Poor attribution assumptions | Strategic error |

---

# 5. L3 Threat Intelligence Responsibilities

| Responsibility | Description |
|---|---|
| IOC validation | Threat verification |
| Intelligence enrichment | Context addition |
| Threat actor tracking | Campaign analysis |
| Intelligence correlation | Multi-source analysis |
| Detection support | Rule enhancement |
| Threat hunting support | IOC/TTP hunting |
| Reporting | Intelligence dissemination |
| Escalation | Critical threat notification |

---

# 6. Threat Intelligence Integration Workflow

| Phase | Objective | Primary Output |
|---|---|---|
| Phase 1 | Intelligence Intake | Intelligence scope |
| Phase 2 | Validation and Triage | Verified intelligence |
| Phase 3 | IOC and TTP Enrichment | Operational intelligence |
| Phase 4 | Correlation and Analysis | Threat assessment |
| Phase 5 | Detection Integration | Security improvements |
| Phase 6 | Threat Hunting Support | Proactive detection |
| Phase 7 | Escalation and Reporting | Stakeholder notification |
| Phase 8 | Intelligence Archival | Long-term retention |

---

# 7. Phase 1 – Intelligence Intake

Threat intelligence begins with intake and source validation.

---

## 7.1 Intelligence Intake Sources

| Source | Purpose |
|---|---|
| Threat feeds | IOC acquisition |
| Incident investigations | Internal intelligence |
| Malware analysis | IOC extraction |
| Government advisories | Regulatory awareness |
| Vendor notifications | Emerging threats |
| Threat hunting findings | Internal discoveries |

---

## 7.2 Intake Validation Checklist

| Validation Item | Completed |
|---|---|
| Source credibility reviewed | ☐ |
| Intelligence timestamp validated | ☐ |
| Threat relevance assessed | ☐ |
| Initial severity assigned | ☐ |
| Duplicate intelligence checked | ☐ |

---

## 7.3 Intelligence Categorization

| Category | Example |
|---|---|
| Tactical intelligence | IOC feeds |
| Operational intelligence | Campaign tracking |
| Strategic intelligence | Threat trends |
| Technical intelligence | Malware behavior |

---

# 8. Phase 2 – Validation and Triage

All intelligence must be validated before operational use.

---

## 8.1 Validation Objectives

| Objective | Purpose |
|---|---|
| Verify IOC legitimacy | Prevent false positives |
| Validate threat relevance | Operational usefulness |
| Assess confidence level | Risk prioritization |
| Determine severity | Escalation readiness |

---

## 8.2 IOC Validation Requirements

| Requirement | Mandatory |
|---|---|
| IOC source reviewed | Yes |
| Reputation validated | Yes |
| Internal sightings checked | Yes |
| False positive review completed | Yes |
| Expiration assessed | Yes |

---

## 8.3 Intelligence Confidence Levels

| Confidence Level | Meaning |
|---|---|
| High | Multiple trusted sources |
| Medium | Single trusted source |
| Low | Unverified or weak evidence |

---

## 8.4 IOC Validation Table

| IOC | Type | Confidence | Source | Validated |
|---|---|---|---|---|
| | | | | |

---

# 9. Phase 3 – IOC and TTP Enrichment

Enrichment adds operational context to intelligence.

---

## 9.1 IOC Categories

| IOC Type | Example |
|---|---|
| IP address | C2 infrastructure |
| Domain | Phishing domain |
| File hash | Malware sample |
| URL | Payload delivery |
| Registry key | Persistence |
| Mutex | Malware identifier |

---

## 9.2 TTP Mapping Areas

| MITRE Category | Example |
|---|---|
| Initial Access | Phishing |
| Execution | PowerShell |
| Persistence | Scheduled task |
| Credential Access | LSASS dumping |
| Exfiltration | Cloud upload |

---

## 9.3 Enrichment Sources

| Source | Purpose |
|---|---|
| VirusTotal | Malware intelligence |
| AbuseIPDB | Reputation review |
| Sandbox analysis | Behavioral analysis |
| Internal telemetry | Sightings review |
| Threat reports | Campaign analysis |

---

# 10. Phase 4 – Correlation and Analysis

Correlate intelligence with internal telemetry.

---

## 10.1 Correlation Objectives

| Objective | Purpose |
|---|---|
| Detect active compromise | Threat validation |
| Identify related activity | Scope determination |
| Detect persistence | Long-term compromise |
| Identify lateral movement | Spread analysis |

---

## 10.2 Correlation Sources

| Source | Investigation Use |
|---|---|
| SIEM | Event correlation |
| EDR | Endpoint telemetry |
| DNS logs | Beaconing analysis |
| Firewall logs | Traffic analysis |
| Cloud logs | IAM abuse |

---

## 10.3 High-Risk Intelligence Indicators

Immediate escalation required if:

| Indicator | Risk |
|---|---|
| Active ransomware IOC match | Business disruption |
| Domain admin compromise IOC | Enterprise risk |
| Known APT infrastructure | Strategic threat |
| Data exfiltration IOC match | Regulatory exposure |

---

# 11. Phase 5 – Detection Integration

Threat intelligence must improve security monitoring capability.

---

## 11.1 Detection Integration Areas

| Area | Example |
|---|---|
| SIEM correlation rules | IOC detection |
| EDR detections | Malware behavior |
| Firewall blocking | Malicious IPs |
| DNS filtering | Malicious domains |
| Email filtering | Phishing indicators |

---

## 11.2 Detection Improvement Checklist

| Improvement Item | Completed |
|---|---|
| SIEM rules updated | ☐ |
| EDR detections updated | ☐ |
| IOC feeds refreshed | ☐ |
| Firewall blocks implemented | ☐ |
| Alert severity reviewed | ☐ |

Reference:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

---

# 12. Phase 6 – Threat Hunting Support

Threat intelligence supports proactive threat hunting.

---

## 12.1 Threat Hunting Objectives

| Objective | Purpose |
|---|---|
| Detect active threats | Early compromise detection |
| Identify IOC matches | Threat validation |
| Detect stealth activity | Hidden compromise |
| Validate detections | Monitoring effectiveness |

---

## 12.2 Hunting Areas

| Hunt Area | Example |
|---|---|
| IOC matching | Known malware |
| TTP hunting | PowerShell abuse |
| Beaconing detection | C2 communication |
| Credential abuse | Privileged misuse |

---

## 12.3 Threat Hunting Escalation Triggers

Immediate escalation required if:

- Active IOC matches identified
- Threat actor infrastructure detected
- Domain compromise indicators found
- Widespread malware sightings detected

---

# 13. Phase 7 – Escalation and Reporting

Critical intelligence findings must be escalated immediately.

---

## 13.1 Escalation Matrix

| Condition | Escalation Target |
|---|---|
| Active compromise indicators | IR Team |
| Sector-wide threat advisory | Executive Management |
| Regulatory-impacting threat | Compliance Team |
| Active APT activity | CISO |
| Multi-client MSSP threat | SOC Lead |

---

## 13.2 Reporting Requirements

| Requirement | Mandatory |
|---|---|
| Intelligence summary | Yes |
| IOC list | Yes |
| TTP mapping | Yes |
| Severity assessment | Yes |
| Recommended actions | Yes |
| Scope analysis | Yes |

---

## 13.3 Intelligence Distribution Controls

| Distribution Type | Restriction |
|---|---|
| Internal SOC | Authorized personnel |
| MSSP clients | Client-specific only |
| Executive reporting | Approved summaries |
| External sharing | Legal approval required |

---

# 14. Phase 8 – Intelligence Archival

Threat intelligence artifacts must be retained securely.

---

## 14.1 Archival Requirements

| Requirement | Standard |
|---|---|
| Secure storage | Mandatory |
| Access control | Restricted |
| Retention schedule | Mandatory |
| IOC lifecycle tracking | Mandatory |
| Source attribution maintained | Mandatory |

---

## 14.2 Intelligence Tracking Table

| Intelligence ID | Source | Severity | Retention Period |
|---|---|---|---|
| | | | |

---

# 15. Threat Intelligence Quality Assurance

Threat intelligence quality must be reviewed continuously.

---

## 15.1 Quality Review Areas

| Area | Objective |
|---|---|
| False positive rate | Accuracy review |
| IOC expiration | Relevance validation |
| Source reliability | Trust assessment |
| Detection effectiveness | Operational value |

---

## 15.2 KPI Examples

| KPI | Objective |
|---|---|
| IOC hit rate | Detection effectiveness |
| False positive percentage | Accuracy |
| Time-to-deployment | Operational speed |
| Threat hunts initiated | Proactive maturity |

---

# 16. MSSP-Specific Threat Intelligence Considerations

For MSSP-managed environments:

| Requirement | Purpose |
|---|---|
| Maintain tenant segregation | Prevent data leakage |
| Share intelligence selectively | Client relevance |
| Protect client-sensitive intelligence | Confidentiality |
| Follow client contractual obligations | SLA compliance |
| Restrict cross-client visibility | Compliance |

---

# 17. Common Threat Intelligence Mistakes

| Mistake | Operational Risk |
|---|---|
| Blind IOC deployment | False positives |
| Weak source validation | Poor intelligence quality |
| No IOC expiration review | Alert fatigue |
| Weak context analysis | Inaccurate prioritization |
| Delayed intelligence distribution | Increased exposure |

---

# 18. Related Documents

| Document | Path |
|---|---|
| L2 Threat Hunting Procedures | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Threat-Hunting-Procedures.md` |
| L3 Attribution Analysis | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Attribution-Analysis.md` |
| TI Feed Management | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Feed-Management.md` |
| TI IOC Handling SOP | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md` |
| IoC Output Register | `08_POST-INCIDENT/08.4_Threat-Intel-Output/IoC-Output-Register.md` |
| Threat Actor Profile Template | `08_POST-INCIDENT/08.4_Threat-Intel-Output/Threat-Actor-Profile-Template.md` |

---

# 19. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | SOC Manager / Threat Intelligence Lead | Initial version |

---

# 20. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**