# SOP: L3 Technical Report Writing Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – L3 Technical Report Writing Procedures |
| Document ID | SOC-L3-SOP-008 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / Incident Response Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the methodology, documentation standards, workflows, quality requirements, and approval procedures for Level 3 (L3) technical cybersecurity reporting.

Technical reporting is a critical activity within Incident Response (IR), Threat Intelligence (TI), Digital Forensics (DFIR), and SOC operations because reports become:

- Official investigation records
- Executive briefing material
- Legal evidence
- Audit evidence
- Regulatory documentation
- Lessons learned references
- Operational intelligence artifacts
- MSSP client deliverables

The purpose of technical reporting is to:

- Document incident findings accurately
- Provide evidence-based analysis
- Support executive decision-making
- Enable remediation and containment
- Maintain forensic integrity
- Support compliance obligations
- Improve future investigations

Improper reporting may result in:

- Misinterpretation of incidents
- Incomplete remediation
- Legal exposure
- Regulatory non-compliance
- Operational confusion
- Loss of forensic credibility
- Client dissatisfaction

This SOP ensures:

- Consistent reporting standards
- Accurate technical documentation
- Structured executive communication
- Audit-ready evidence presentation
- Proper approval and review processes
- Controlled information handling

---

# 3. Scope

This SOP applies to all L3 reporting activities involving:

| Report Type | Example |
|---|---|
| Incident reports | P1 ransomware |
| Forensic reports | Memory analysis |
| Malware analysis reports | Reverse engineering |
| Threat intelligence reports | IOC/TTP analysis |
| Attribution reports | Threat actor assessment |
| Root Cause Analysis (RCA) | Security control failures |
| Executive summaries | Leadership briefing |
| MSSP client reports | Customer reporting |
| Regulatory reporting support | CERT-In/RBI support |
| Threat hunting reports | Hunt findings |

---

## 3.1 Intended Report Audiences

| Audience | Purpose |
|---|---|
| SOC Analysts | Operational awareness |
| IR Teams | Investigation coordination |
| Executive Leadership | Strategic decisions |
| Legal and Compliance | Regulatory support |
| MSSP Clients | Client visibility |
| Auditors | Evidence review |
| Regulators | Compliance obligations |

---

# 4. Technical Reporting Philosophy (IMPORTANT)

Technical reporting must be:

- Accurate
- Evidence-based
- Clear
- Structured
- Defensible
- Actionable

L3 analysts must distinguish between:

| Type | Example |
|---|---|
| Confirmed facts | “EDR telemetry confirmed execution.” |
| Analytical assessment | “Likely credential compromise.” |
| Assumptions/speculation | Must be clearly labeled |

Reports must avoid:

| Poor Practice | Operational Risk |
|---|---|
| Unsupported conclusions | Incorrect decisions |
| Emotional language | Professional credibility loss |
| Excessive technical jargon | Executive confusion |
| Missing evidence references | Audit failure |
| Weak timelines | Investigation gaps |
| Unclear severity statements | Misaligned response |

Every report must answer:

1. What happened?
2. When did it happen?
3. How did it happen?
4. What was affected?
5. What evidence supports the findings?
6. What actions were taken?
7. What actions are recommended?

---

# 5. L3 Reporting Responsibilities

| Responsibility | Description |
|---|---|
| Technical documentation | Detailed reporting |
| Evidence referencing | Artifact validation |
| Timeline reconstruction | Chronological reporting |
| Executive communication | Strategic summaries |
| Corrective action reporting | Improvement planning |
| Quality assurance | Accuracy validation |
| Report classification | Data handling |
| Report archival | Secure retention |

---

# 6. Technical Reporting Workflow

| Phase | Objective | Primary Output |
|---|---|---|
| Phase 1 | Define Report Scope | Reporting requirements |
| Phase 2 | Gather Evidence | Supporting artifacts |
| Phase 3 | Build Timeline | Chronological analysis |
| Phase 4 | Draft Technical Findings | Investigation narrative |
| Phase 5 | Executive Summary Development | Leadership communication |
| Phase 6 | Quality Review | Accuracy validation |
| Phase 7 | Approval and Distribution | Authorized release |
| Phase 8 | Report Archival | Long-term retention |

---

# 7. Phase 1 – Define Report Scope

Define the purpose and audience of the report.

---

## 7.1 Report Scope Requirements

| Requirement | Purpose |
|---|---|
| Audience identified | Communication alignment |
| Classification assigned | Data protection |
| Incident scope validated | Accuracy |
| Evidence availability confirmed | Report completeness |
| Reporting deadlines identified | SLA/regulatory alignment |

---

## 7.2 Report Classification Levels

| Classification | Description |
|---|---|
| Internal | Internal operational use |
| Confidential | Sensitive investigations |
| Restricted | Executive/legal access only |
| Client Confidential | MSSP customer reporting |

---

## 7.3 Scope Definition Checklist

| Validation Item | Completed |
|---|---|
| Report objective defined | ☐ |
| Audience identified | ☐ |
| Classification assigned | ☐ |
| Timeline scope confirmed | ☐ |
| Evidence sources identified | ☐ |

---

# 8. Phase 2 – Gather Evidence

Reports must be evidence-driven.

---

## 8.1 Evidence Categories

| Evidence Type | Example |
|---|---|
| SIEM logs | Event correlation |
| EDR telemetry | Endpoint behavior |
| Firewall logs | Network activity |
| Memory artifacts | Credential dumping |
| Disk artifacts | Persistence |
| Malware analysis | IOC extraction |
| Threat intelligence | Threat actor correlation |

---

## 8.2 Evidence Handling Requirements

| Requirement | Standard |
|---|---|
| Evidence references documented | Mandatory |
| UTC timestamps used | Mandatory |
| Chain-of-custody maintained | Mandatory |
| Hashes included where applicable | Mandatory |
| Screenshots validated | Mandatory |

---

## 8.3 Evidence Tracking Table

| Evidence ID | Source | Description | Reference Location |
|---|---|---|---|
| | | | |

---

# 9. Phase 3 – Timeline Reconstruction (CRITICAL)

Every major report must include a validated timeline.

---

## 9.1 Timeline Objectives

| Objective | Purpose |
|---|---|
| Identify initial compromise | Root cause analysis |
| Track attacker progression | Incident reconstruction |
| Identify containment timing | Response assessment |
| Identify escalation timing | SLA review |

---

## 9.2 Timeline Event Categories

| Event Type | Example |
|---|---|
| Initial access | Phishing execution |
| Malware execution | PowerShell launch |
| Lateral movement | RDP access |
| Exfiltration | Cloud upload |
| Detection | SIEM alert |
| Containment | Host isolation |

---

## 9.3 Timeline Tracking Table

| Timestamp UTC | Event | Source | Severity | Evidence Ref |
|---|---|---|---|---|
| | | | | |

---

# 10. Phase 4 – Draft Technical Findings

Technical findings form the core of the report.

---

## 10.1 Technical Findings Structure

| Section | Purpose |
|---|---|
| Incident overview | High-level summary |
| Technical findings | Detailed analysis |
| Evidence summary | Supporting validation |
| Scope analysis | Impact review |
| IOC/TTP analysis | Threat assessment |
| Containment actions | Response review |

---

## 10.2 Technical Writing Standards

GOOD:
“EDR telemetry confirmed WINWORD.EXE spawned powershell.exe with Base64-encoded commands at 03:14 UTC. Network telemetry identified outbound HTTPS beaconing to known malicious IP address 185.x.x.x.”

BAD:
“Looks malicious and suspicious.”

---

## 10.3 Technical Findings Checklist

| Requirement | Completed |
|---|---|
| Findings evidence-based | ☐ |
| UTC timestamps included | ☐ |
| Technical accuracy validated | ☐ |
| IOC references included | ☐ |
| Scope analysis completed | ☐ |

---

# 11. Phase 5 – Executive Summary Development

Executive summaries must communicate business impact clearly.

---

## 11.1 Executive Summary Objectives

| Objective | Purpose |
|---|---|
| Communicate business risk | Leadership awareness |
| Summarize incident impact | Decision support |
| Explain remediation status | Operational visibility |
| Identify strategic risks | Governance support |

---

## 11.2 Executive Summary Requirements

| Requirement | Mandatory |
|---|---|
| Business impact summary | Yes |
| Incident severity | Yes |
| Systems affected | Yes |
| Data exposure status | Yes |
| Current containment status | Yes |
| Recommended next steps | Yes |

---

## 11.3 Executive Summary Example Areas

| Area | Example |
|---|---|
| Incident type | Ransomware |
| Business impact | ERP outage |
| Operational status | Contained |
| Regulatory impact | Under assessment |
| Executive action required | Approval for remediation |

---

# 12. Phase 6 – Quality Review

All reports must undergo technical review.

---

## 12.1 Quality Review Objectives

| Objective | Purpose |
|---|---|
| Validate accuracy | Prevent misinformation |
| Ensure evidence alignment | Audit readiness |
| Confirm clarity | Audience understanding |
| Validate classification | Data protection |

---

## 12.2 Quality Review Checklist

| Validation Item | Completed |
|---|---|
| Technical accuracy verified | ☐ |
| Evidence references validated | ☐ |
| Timeline reviewed | ☐ |
| Grammar/spelling reviewed | ☐ |
| Sensitive data reviewed | ☐ |
| Classification validated | ☐ |

---

## 12.3 Common Reporting Errors

| Error | Operational Risk |
|---|---|
| Unsupported conclusions | Misleading decisions |
| Weak evidence references | Audit failure |
| Missing timeline details | Investigation gaps |
| Overly technical executive summaries | Leadership confusion |
| Inconsistent timestamps | Timeline corruption |

---

# 13. Phase 7 – Approval and Distribution

Reports must follow controlled approval workflows.

---

## 13.1 Approval Matrix

| Report Type | Approval Required |
|---|---|
| Internal incident report | SOC Manager |
| Executive report | CISO |
| Regulatory-support report | Compliance Team |
| MSSP client report | Service Delivery Manager |
| Legal-sensitive report | Legal Counsel |

---

## 13.2 Distribution Controls

| Distribution Type | Restriction |
|---|---|
| Internal operational reports | Authorized teams only |
| Executive reports | Leadership only |
| Client reports | Client-specific only |
| Regulatory reports | Approved channels only |

---

## 13.3 Sensitive Information Controls

Do not include:

- Unnecessary credentials
- Sensitive personal information
- Cross-client MSSP data
- Internal-only investigative methods
- Unapproved attribution claims

---

# 14. Phase 8 – Report Archival

Reports must be retained securely.

---

## 14.1 Archival Requirements

| Requirement | Standard |
|---|---|
| Secure storage | Mandatory |
| Access restricted | Mandatory |
| Retention schedule followed | Mandatory |
| Version history maintained | Mandatory |
| Audit availability ensured | Mandatory |

---

## 14.2 Report Archive Table

| Report ID | Report Type | Classification | Retention Period |
|---|---|---|---|
| | | | |

Reference:
`11_ARCHIVE/11.1_Closed-Incidents/`

---

# 15. Report Types and Templates

Approved report types include:

---

## 15.1 Standard Report Templates

| Template | Path |
|---|---|
| Initial Incident Report | `07_REPORTING/07.1_Incident-Reports/Initial-Incident-Report-Template.md` |
| Interim Status Report | `07_REPORTING/07.1_Incident-Reports/Interim-Status-Report-Template.md` |
| Final Incident Report | `07_REPORTING/07.1_Incident-Reports/Final-Incident-Report-Template.md` |
| Executive Summary | `07_REPORTING/07.1_Incident-Reports/Executive-Summary-Template.md` |
| Technical Deep Dive | `07_REPORTING/07.1_Incident-Reports/Technical-Deep-Dive-Template.md` |

---

# 16. MSSP-Specific Reporting Considerations

For MSSP-managed environments:

| Requirement | Purpose |
|---|---|
| Maintain tenant segregation | Prevent data leakage |
| Follow client reporting SLA | Contract compliance |
| Use client-approved templates | Reporting consistency |
| Restrict cross-client visibility | Confidentiality |
| Maintain client branding requirements | Service alignment |

---

# 17. Common Technical Reporting Mistakes

| Mistake | Operational Risk |
|---|---|
| Unsupported findings | Incorrect remediation |
| Weak executive summaries | Leadership confusion |
| Missing evidence references | Audit failure |
| Inconsistent terminology | Miscommunication |
| Weak scope analysis | Incomplete response |
| Delayed reporting | SLA/regulatory impact |

---

# 18. Related Documents

| Document | Path |
|---|---|
| Final Incident Report Template | `07_REPORTING/07.1_Incident-Reports/Final-Incident-Report-Template.md` |
| Executive Summary Template | `07_REPORTING/07.1_Incident-Reports/Executive-Summary-Template.md` |
| Technical Deep Dive Template | `07_REPORTING/07.1_Incident-Reports/Technical-Deep-Dive-Template.md` |
| RCA Template | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md` |
| Lessons Learned Template | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md` |
| Audit Evidence Package | `07_REPORTING/07.4_Regulatory-Reports/Audit-Evidence-Package.md` |

---

# 19. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | SOC Manager / Incident Response Lead | Initial version |

---

# 20. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**
