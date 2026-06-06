# SOP: SOC Lead Client Communication Procedures (MSSP)

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – SOC Lead Client Communication Procedures (MSSP) |
| Document ID | SOC-LEAD-SOP-005 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / Service Delivery Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the operational methodology, communication standards, escalation procedures, stakeholder management requirements, and reporting workflows for SOC Lead client communication activities within MSSP-managed environments.

Client communication is one of the most critical responsibilities in MSSP operations because communication quality directly impacts:

- Client trust
- SLA compliance
- Incident response effectiveness
- Regulatory obligations
- Executive confidence
- Contractual obligations
- Business continuity
- Reputation management

The SOC Lead is responsible for ensuring clients receive:

- Accurate incident information
- Timely escalation notifications
- Clear business impact updates
- Actionable remediation guidance
- Consistent communication cadence
- Controlled information disclosure

Improper client communication may result in:

- SLA violations
- Client dissatisfaction
- Escalation delays
- Misunderstanding of risk
- Legal exposure
- Reputational damage
- Contractual disputes

This SOP ensures:

- Structured client communication workflows
- Consistent notification standards
- Proper escalation handling
- Controlled information sharing
- Audit-ready communication records
- MSSP contractual compliance

---

# 3. Scope

This SOP applies to MSSP client communication activities involving:

| Communication Type | Example |
|---|---|
| Initial incident notification | P1 ransomware |
| Escalation communication | Domain compromise |
| Ongoing status updates | Active investigation |
| Executive communication | Business impact |
| SLA notifications | Response tracking |
| Regulatory-impacting incidents | Data breach |
| Service disruption notifications | Monitoring outage |
| Incident closure communication | Resolution updates |
| Threat advisory communication | Sector-wide threats |
| Emergency communications | Active attacker |

---

## 3.1 Communication Stakeholders

| Stakeholder | Purpose |
|---|---|
| Client SOC Teams | Operational coordination |
| Client IT Teams | Remediation support |
| Client Management | Business visibility |
| Client Executives | Strategic awareness |
| MSSP Analysts | Investigation coordination |
| MSSP Service Delivery | SLA oversight |
| MSSP Management | Escalation management |

---

# 4. Client Communication Philosophy (IMPORTANT)

Client communication must be:

- Accurate
- Timely
- Professional
- Clear
- Action-oriented
- Evidence-based

SOC Leads must ensure communication:

- Avoids speculation
- Avoids unsupported attribution
- Avoids excessive technical jargon
- Maintains client confidence
- Supports decision-making
- Aligns with contractual obligations

The objective is to ensure clients understand:

1. What happened
2. What is currently known
3. What systems are affected
4. What actions are being taken
5. What actions are recommended
6. What business risks exist
7. What the next update timeline is

SOC Leads must avoid:

| Poor Practice | Operational Risk |
|---|---|
| Delayed communication | SLA breach |
| Inconsistent messaging | Client confusion |
| Unsupported conclusions | Loss of credibility |
| Excessive technical detail | Executive misunderstanding |
| Missing update cadence | Operational frustration |

---

# 5. SOC Lead Client Communication Responsibilities

| Responsibility | Description |
|---|---|
| Incident notification | Client awareness |
| Escalation communication | Priority coordination |
| Status updates | Operational visibility |
| Executive briefing coordination | Leadership communication |
| SLA communication | Compliance tracking |
| Communication documentation | Audit readiness |
| Client expectation management | Service coordination |
| Closure communication | Incident resolution |

---

# 6. Client Communication Workflow

| Phase | Objective | Primary Output |
|---|---|---|
| Phase 1 | Incident Communication Assessment | Notification scope |
| Phase 2 | Initial Client Notification | Incident awareness |
| Phase 3 | Ongoing Status Communication | Operational updates |
| Phase 4 | Escalation and Executive Communication | Leadership visibility |
| Phase 5 | Resolution Communication | Incident closure |
| Phase 6 | Communication Documentation | Audit records |

---

# 7. Phase 1 – Incident Communication Assessment

Determine communication requirements based on incident severity and contractual obligations.

---

## 7.1 Communication Assessment Areas

| Area | Objective |
|---|---|
| Incident severity | Notification urgency |
| Client SLA | Communication timing |
| Regulatory exposure | Compliance coordination |
| Business impact | Executive involvement |
| Client environment impact | Scope analysis |

---

## 7.2 Initial Assessment Checklist

| Validation Item | Completed |
|---|---|
| Severity validated | ☐ |
| Client impacted confirmed | ☐ |
| SLA reviewed | ☐ |
| Communication contacts identified | ☐ |
| Escalation requirements reviewed | ☐ |

---

## 7.3 Immediate Notification Triggers

Immediate client communication required if:

| Trigger | Risk |
|---|---|
| Active ransomware | Business disruption |
| Data exfiltration | Regulatory exposure |
| Domain compromise | Enterprise-wide risk |
| Cloud admin compromise | Infrastructure impact |
| MSSP monitoring outage | Visibility loss |

Reference:
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`

---

# 8. Phase 2 – Initial Client Notification

The SOC Lead coordinates initial incident communication.

---

## 8.1 Initial Notification Objectives

| Objective | Purpose |
|---|---|
| Inform client rapidly | Situational awareness |
| Establish incident severity | Risk visibility |
| Provide initial scope | Operational context |
| Confirm next update timing | Communication cadence |

---

## 8.2 Initial Notification Requirements

| Requirement | Mandatory |
|---|---|
| Incident summary | Yes |
| Severity classification | Yes |
| Impacted assets | Yes |
| Current containment status | Yes |
| Recommended actions | Yes |
| Next update timing | Yes |

---

## 8.3 Initial Notification Table

| Communication Area | Example |
|---|---|
| Incident Type | Ransomware |
| Severity | P1 |
| Affected Systems | FIN-SRV-01 |
| Current Status | Under investigation |
| Immediate Actions | Host isolated |

---

## 8.4 Communication Timing Standards

| Severity | Notification Timing |
|---|---|
| P1 | Immediate |
| P2 | Within SLA |
| P3 | Standard reporting cycle |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/MSSP-Client-Notification-Template.md`

---

# 9. Phase 3 – Ongoing Status Communication

SOC Lead maintains communication cadence throughout the incident.

---

## 9.1 Status Update Objectives

| Objective | Purpose |
|---|---|
| Maintain client awareness | Transparency |
| Reduce uncertainty | Operational confidence |
| Communicate containment progress | Incident visibility |
| Track remediation progress | Recovery coordination |

---

## 9.2 Standard Update Areas

| Area | Example |
|---|---|
| Investigation findings | IOC identification |
| Scope changes | Additional hosts impacted |
| Containment progress | Isolation completed |
| Risk assessment | Data exposure review |
| Pending actions | Memory acquisition |

---

## 9.3 Update Frequency Standards

| Severity | Update Frequency |
|---|---|
| P1 | Every 30 minutes |
| P2 | Every 1 hour |
| P3 | As agreed/SLA-driven |

---

## 9.4 Status Update Tracking Table

| Timestamp UTC | Update Provided By | Status Summary |
|---|---|---|
| | | |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Status-Update-Template-30min.md`

---

# 10. Phase 4 – Escalation and Executive Communication

Executive communication is required for major incidents.

---

## 10.1 Executive Escalation Triggers

| Trigger | Reason |
|---|---|
| Critical business disruption | Operational impact |
| Data breach | Regulatory exposure |
| Regulatory reporting requirement | Compliance |
| Public disclosure risk | Reputation management |
| Widespread compromise | Enterprise risk |

---

## 10.2 Executive Communication Requirements

| Requirement | Mandatory |
|---|---|
| Business impact summary | Yes |
| Operational status | Yes |
| Risk assessment | Yes |
| Current containment status | Yes |
| Strategic recommendations | Yes |

---

## 10.3 Executive Communication Standards

Executive communications should:

- Use business-focused language
- Minimize unnecessary technical detail
- Focus on operational impact
- Clearly identify current risks
- Explain remediation progress

---

## 10.4 Executive Communication Table

| Area | Example |
|---|---|
| Business Impact | ERP unavailable |
| Current Risk | Contained |
| Regulatory Exposure | Under review |
| Next Steps | Restoration validation |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Management-Notification-Template.md`

---

# 11. Phase 5 – Resolution Communication

SOC Lead coordinates formal incident closure communication.

---

## 11.1 Resolution Communication Objectives

| Objective | Purpose |
|---|---|
| Confirm incident closure | Operational clarity |
| Summarize remediation | Recovery validation |
| Identify lessons learned | Improvement awareness |
| Outline follow-up actions | Long-term remediation |

---

## 11.2 Closure Communication Requirements

| Requirement | Mandatory |
|---|---|
| Incident summary | Yes |
| Root cause summary | Yes |
| Remediation actions | Yes |
| Current operational status | Yes |
| Follow-up actions | Yes |

---

## 11.3 Closure Validation Checklist

| Validation Item | Completed |
|---|---|
| Incident contained | ☐ |
| Systems restored | ☐ |
| Client acknowledged closure | ☐ |
| Documentation completed | ☐ |
| RCA scheduled/completed | ☐ |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Incident-Closure-Notification.md`

---

# 12. Phase 6 – Communication Documentation

All client communication must be documented.

---

## 12.1 Documentation Requirements

| Requirement | Mandatory |
|---|---|
| Communication timestamps | Yes |
| Participants documented | Yes |
| Updates recorded | Yes |
| Escalation records | Yes |
| SLA timing evidence | Yes |

---

## 12.2 Communication Tracking Table

| Timestamp UTC | Communication Type | Recipient | Summary |
|---|---|---|---|
| | | | |

---

# 13. Communication Security and Confidentiality

Client communication must follow strict confidentiality requirements.

---

## 13.1 Confidentiality Rules

| Rule | Requirement |
|---|---|
| No cross-client data sharing | Mandatory |
| Use approved communication channels | Mandatory |
| Restrict sensitive evidence sharing | Mandatory |
| Validate recipient authorization | Mandatory |

---

## 13.2 Approved Communication Channels

| Channel | Usage |
|---|---|
| Secure email | Formal communication |
| Client portal | Incident tracking |
| Secure bridge call | Major incidents |
| Ticketing platform | Operational coordination |

---

# 14. SLA and Communication Oversight

SOC Lead monitors communication SLA compliance.

---

## 14.1 Communication SLA Areas

| Area | Example |
|---|---|
| Initial notification timing | P1 response |
| Update frequency | Ongoing communication |
| Closure notification timing | Incident completion |

---

## 14.2 SLA Breach Escalation Conditions

Immediate escalation required if:

| Condition | Escalation Target |
|---|---|
| Initial notification delayed | Service Delivery Manager |
| Update cadence missed | SOC Manager |
| Client dissatisfaction escalated | MSSP Management |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/MSSP-Client-SLA-Template.md`

---

# 15. MSSP Multi-Client Communication Considerations

Additional controls apply during multi-client incidents.

---

## 15.1 Multi-Client Communication Rules

| Requirement | Purpose |
|---|---|
| Maintain tenant segregation | Prevent data leakage |
| Restrict cross-client visibility | Confidentiality |
| Coordinate notifications independently | SLA compliance |
| Validate evidence segregation | Audit readiness |

---

## 15.2 Multi-Client Escalation Triggers

Immediate management escalation required if:

- Cross-client compromise suspected
- Shared infrastructure impacted
- Multi-client SLA risk exists
- Widespread MSSP outage occurs

---

# 16. Common Client Communication Mistakes

| Mistake | Operational Risk |
|---|---|
| Delayed notification | SLA breach |
| Unsupported conclusions | Client mistrust |
| Weak update cadence | Communication breakdown |
| Excessive technical language | Executive confusion |
| Cross-client information leakage | Compliance violation |
| Weak documentation | Audit gaps |

---

# 17. Related Documents

| Document | Path |
|---|---|
| MSSP Client Notification Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/MSSP-Client-Notification-Template.md` |
| Management Notification Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Management-Notification-Template.md` |
| Incident Closure Notification | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Incident-Closure-Notification.md` |
| MSSP Client Contacts | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/MSSP-Client-Contacts.md` |
| MSSP Client SLA Template | `00_GOVERNANCE/00.4_SLA-and-SLO/MSSP-Client-SLA-Template.md` |
| Client Escalation Matrix | `09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/[CLIENT-NAME]/Client-Escalation-Matrix.md` |

---

# 18. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | SOC Manager / Service Delivery Lead | Initial version |

---

# 19. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**