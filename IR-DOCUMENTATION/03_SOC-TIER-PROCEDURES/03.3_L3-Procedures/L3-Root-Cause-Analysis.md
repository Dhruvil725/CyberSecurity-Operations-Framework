# SOP: L3 Root Cause Analysis Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – L3 Root Cause Analysis Procedures |
| Document ID | SOC-L3-SOP-006 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / Incident Response Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the methodology, workflows, analytical standards, and reporting requirements for Level 3 (L3) Root Cause Analysis (RCA) activities following cybersecurity incidents.

Root Cause Analysis is a structured process used to determine:

- How the incident occurred
- Why the incident occurred
- Which weaknesses enabled the compromise
- Which controls failed or were bypassed
- What allowed attacker persistence or escalation
- How recurrence can be prevented

Root Cause Analysis is a critical post-incident activity because containment alone does not eliminate organizational risk.

The objectives of RCA are to:

- Identify the original compromise vector
- Identify contributing security failures
- Determine process and control gaps
- Improve defensive capabilities
- Support executive and regulatory reporting
- Improve incident response maturity
- Prevent recurrence of similar incidents

Improper RCA processes may result in:

- Repeat compromise
- Incomplete remediation
- Missed security gaps
- Weak corrective actions
- Regulatory non-compliance
- Poor executive visibility
- Inaccurate lessons learned

This SOP ensures:

- Structured root cause investigations
- Consistent analytical methodology
- Accurate control gap identification
- Actionable remediation planning
- Audit-ready reporting
- Continuous improvement tracking

---

# 3. Scope

This SOP applies to Root Cause Analysis activities involving:

| Incident Type | Example |
|---|---|
| Ransomware incidents | Initial access analysis |
| Data breaches | Exfiltration pathway |
| Insider threats | Privilege misuse |
| Credential compromise | MFA bypass |
| Cloud compromise | IAM abuse |
| Malware outbreaks | Detection failure |
| Supply chain attacks | Trusted software abuse |
| Zero-day exploitation | Unpatched exposure |
| APT incidents | Multi-stage compromise |
| MSSP client incidents | Cross-tenant review |

---

## 3.1 RCA Inputs

| Source Type | Examples |
|---|---|
| SIEM logs | Event timelines |
| EDR telemetry | Endpoint behavior |
| Firewall logs | Traffic analysis |
| Forensic reports | Artifact findings |
| Malware analysis | Payload behavior |
| Threat intelligence | TTP correlation |
| Change management records | Configuration review |
| User activity logs | Access review |

---

# 4. Root Cause Analysis Philosophy (IMPORTANT)

Root Cause Analysis is not focused on assigning blame.

The purpose is to identify:

- Technical failures
- Process failures
- Detection failures
- Visibility gaps
- Configuration weaknesses
- Human process breakdowns
- Governance weaknesses

L3 analysts must focus on:

- Evidence-based findings
- Objective analysis
- Control effectiveness
- Attack progression
- Defensive gaps
- Risk reduction

Root Cause Analysis must answer:

1. How did the attacker gain access?
2. Why was the attack successful?
3. What allowed persistence or spread?
4. Why was detection delayed or bypassed?
5. Which corrective actions are required?

---

## 4.1 Common RCA Failures

| Poor Practice | Operational Risk |
|---|---|
| Stopping at the first finding | Incomplete remediation |
| Blaming individuals only | Missed systemic issues |
| Ignoring process failures | Repeat incidents |
| Weak timeline analysis | Incorrect conclusions |
| No corrective action tracking | Unresolved risks |
| No executive alignment | Governance gaps |

---

# 5. L3 Root Cause Analysis Responsibilities

| Responsibility | Description |
|---|---|
| Timeline reconstruction | Attack progression analysis |
| Initial access analysis | Entry point identification |
| Control failure analysis | Defensive gap identification |
| Persistence analysis | Long-term compromise review |
| Detection failure analysis | Monitoring gap review |
| Corrective action development | Remediation planning |
| Reporting | RCA documentation |
| Improvement tracking | Follow-up management |

---

# 6. Root Cause Analysis Workflow

| Phase | Objective | Primary Output |
|---|---|---|
| Phase 1 | Incident Review | Investigation scope |
| Phase 2 | Timeline Reconstruction | Attack chronology |
| Phase 3 | Initial Access Analysis | Entry vector identification |
| Phase 4 | Control Failure Analysis | Security gap assessment |
| Phase 5 | Impact and Scope Review | Business impact analysis |
| Phase 6 | Corrective Action Planning | Remediation actions |
| Phase 7 | Reporting and Approval | RCA report |
| Phase 8 | Improvement Tracking | Continuous improvement |

---

# 7. Phase 1 – Incident Review

The RCA process begins after containment and stabilization.

---

## 7.1 RCA Initiation Triggers

| Trigger | Reason |
|---|---|
| P1 incident closure | Mandatory RCA |
| Regulatory-impacting incident | Compliance requirement |
| Ransomware incident | Executive review |
| Data breach | Legal requirement |
| Recurring incident type | Pattern analysis |
| Detection failure | Control review |

---

## 7.2 Initial Review Checklist

| Validation Item | Completed |
|---|---|
| Incident scope reviewed | ☐ |
| Evidence sources identified | ☐ |
| Investigation reports reviewed | ☐ |
| Stakeholders identified | ☐ |
| Regulatory obligations reviewed | ☐ |

---

# 8. Phase 2 – Timeline Reconstruction (CRITICAL)

Timeline reconstruction is foundational to RCA.

---

## 8.1 Timeline Objectives

| Objective | Purpose |
|---|---|
| Identify initial compromise | Root cause identification |
| Track attacker progression | Threat analysis |
| Identify persistence timing | Long-term compromise review |
| Identify detection delays | Monitoring assessment |
| Identify response timing | IR effectiveness review |

---

## 8.2 Timeline Event Categories

| Event Type | Example |
|---|---|
| Initial access | Phishing click |
| Malware execution | Payload launch |
| Privilege escalation | Domain admin abuse |
| Lateral movement | SMB propagation |
| Exfiltration | Cloud upload |
| Detection | SIEM alert |
| Containment | Host isolation |

---

## 8.3 Timeline Tracking Table

| Timestamp UTC | Event | Source | Severity | Notes |
|---|---|---|---|---|
| | | | | |

---

# 9. Phase 3 – Initial Access Analysis

Determine how the attacker entered the environment.

---

## 9.1 Initial Access Categories

| Access Vector | Example |
|---|---|
| Phishing | Malicious attachment |
| Credential compromise | Password spray |
| Vulnerability exploitation | Unpatched server |
| Cloud misconfiguration | Public bucket |
| VPN compromise | MFA bypass |
| Insider activity | Unauthorized access |

---

## 9.2 Initial Access Analysis Questions

| Question | Objective |
|---|---|
| Was access preventable? | Control effectiveness |
| Was MFA enabled? | Authentication review |
| Was the vulnerability known? | Patch management review |
| Was user awareness involved? | Training assessment |

---

## 9.3 Common Root Cause Indicators

| Indicator | Potential Root Cause |
|---|---|
| Weak password policy | Credential compromise |
| Missing MFA | Account takeover |
| Unpatched systems | Vulnerability exploitation |
| Excessive privileges | Lateral movement |
| Weak logging | Detection failure |

---

# 10. Phase 4 – Control Failure Analysis

Determine which controls failed or were bypassed.

---

## 10.1 Security Control Categories

| Control Area | Example |
|---|---|
| Preventive controls | MFA |
| Detective controls | SIEM alerts |
| Corrective controls | EDR containment |
| Governance controls | Policy enforcement |
| Administrative controls | Access reviews |

---

## 10.2 Control Failure Analysis Table

| Control | Expected Function | Failure Identified | Impact |
|---|---|---|---|
| | | | |

---

## 10.3 Common Control Failures

| Failure Type | Example |
|---|---|
| Misconfiguration | Logging disabled |
| Missing coverage | No EDR installed |
| Weak monitoring | Alert not triggered |
| Excessive permissions | Privilege abuse |
| Delayed patching | Exploit success |

---

# 11. Phase 5 – Impact and Scope Review

Assess the full impact of the incident.

---

## 11.1 Impact Categories

| Category | Example |
|---|---|
| Operational impact | Service outage |
| Financial impact | Revenue loss |
| Regulatory impact | PII exposure |
| Client impact | MSSP customer disruption |
| Reputational impact | Public disclosure |

---

## 11.2 Scope Analysis Areas

| Area | Objective |
|---|---|
| Systems affected | Infrastructure impact |
| Accounts compromised | Identity impact |
| Data accessed | Regulatory review |
| Business services impacted | Operational review |

---

## 11.3 Scope Tracking Table

| Asset | Business Criticality | Impact Level | Recovery Status |
|---|---|---|---|
| | | | |

---

# 12. Phase 6 – Corrective Action Planning

Corrective actions must address root causes and contributing factors.

---

## 12.1 Corrective Action Categories

| Category | Example |
|---|---|
| Technical remediation | MFA enforcement |
| Detection improvements | New SIEM rules |
| Process improvements | Escalation changes |
| Policy updates | Access policy revision |
| Training improvements | User awareness |

---

## 12.2 Corrective Action Planning Table

| Action Item | Owner | Priority | Due Date | Status |
|---|---|---|---|---|
| | | | | |

---

## 12.3 Remediation Prioritization

| Priority | Description |
|---|---|
| Critical | Immediate business risk |
| High | Significant exposure |
| Medium | Moderate risk |
| Low | Long-term improvement |

---

# 13. Phase 7 – Reporting and Approval

RCA findings must be formally documented and approved.

---

## 13.1 RCA Report Requirements

| Requirement | Mandatory |
|---|---|
| Executive summary | Yes |
| Timeline reconstruction | Yes |
| Root cause findings | Yes |
| Control gap analysis | Yes |
| Scope assessment | Yes |
| Corrective actions | Yes |
| Lessons learned | Yes |

---

## 13.2 RCA Stakeholder Review

| Stakeholder | Purpose |
|---|---|
| SOC Manager | Operational review |
| IR Team Lead | Incident validation |
| CISO | Executive approval |
| Compliance Team | Regulatory alignment |
| IT Operations | Remediation planning |

---

## 13.3 Escalation Conditions

Immediate executive escalation required if:

| Condition | Escalation Target |
|---|---|
| Regulatory reporting required | Compliance Team |
| Critical infrastructure impacted | Executive Management |
| Significant financial impact | CISO |
| Multi-client MSSP impact | SOC Director |

---

# 14. Phase 8 – Improvement Tracking

Corrective actions must be tracked through completion.

---

## 14.1 Improvement Tracking Areas

| Area | Objective |
|---|---|
| Technical remediation | Risk reduction |
| Detection improvements | Faster detection |
| Process improvements | Operational maturity |
| Training improvements | Awareness enhancement |

---

## 14.2 Improvement Tracking Table

| Improvement Item | Owner | Status | Completion Date |
|---|---|---|---|
| | | | |

Reference:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx`

---

# 15. RCA Methodologies

Approved RCA methodologies include:

---

## 15.1 5-Why Analysis

Example:

| Question | Answer |
|---|---|
| Why was the account compromised? | Password stolen |
| Why was password stolen? | Phishing email |
| Why did phishing succeed? | Weak user awareness |
| Why was awareness weak? | Infrequent training |
| Why was training infrequent? | No formal schedule |

---

## 15.2 Fishbone Analysis Categories

| Category | Example |
|---|---|
| Technology | Missing EDR |
| Process | Weak escalation |
| People | Training gaps |
| Governance | Policy weakness |

---

# 16. MSSP-Specific RCA Considerations

For MSSP-managed environments:

| Requirement | Purpose |
|---|---|
| Maintain tenant segregation | Prevent data leakage |
| Review cross-client risk | Multi-tenant security |
| Follow contractual reporting obligations | SLA compliance |
| Provide client-specific corrective actions | Targeted remediation |
| Maintain client confidentiality | Compliance |

---

# 17. Common Root Cause Analysis Mistakes

| Mistake | Operational Risk |
|---|---|
| Focusing only on technical issues | Missed process failures |
| Weak timeline reconstruction | Incorrect conclusions |
| No remediation tracking | Repeat incidents |
| Weak executive reporting | Governance gaps |
| No detection improvement analysis | Continued blind spots |

---

# 18. Related Documents

| Document | Path |
|---|---|
| RCA Template | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md` |
| RCA 5-Why Template | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-5-Why-Template.md` |
| RCA Timeline Builder | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Timeline-Builder.md` |
| Lessons Learned Template | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md` |
| Detection Improvement Log | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md` |
| Security Improvement Register | `08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx` |

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