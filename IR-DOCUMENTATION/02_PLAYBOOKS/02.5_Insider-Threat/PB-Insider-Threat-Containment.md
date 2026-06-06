# Playbook: Insider Threat – Containment

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Insider Threat (Containment) |
| Document ID | IR-PB-INS-005 |
| Version | 1.0 |
| Effective Date | 16-May-2026 |
| Owner | IR Team Lead / SOC Lead |
| Approved By | CISO |
| Classification | Strictly Confidential |
| Review Cycle | Quarterly and after any P1/P2 insider threat incident |

---

## 2. Purpose

This document defines the containment procedures for insider threat incidents.

Containment focuses on:
- preventing further data theft or sabotage
- restricting unauthorized access
- preserving forensic evidence
- minimizing operational disruption
- protecting business-critical systems
- coordinating safely with HR and Legal

Unlike external attacker containment, insider threat containment must be:
- discreet
- legally defensible
- carefully coordinated
- minimally disruptive where possible

Improper containment may:
- alert the subject prematurely
- trigger evidence destruction
- create HR or legal complications
- impact legitimate business operations
- compromise the investigation

---

## 3. Scope

Applies to:
- malicious insider investigations
- suspected data theft
- privileged misuse
- sabotage attempts
- unauthorized cloud sharing
- insider-assisted breaches
- employee account misuse
- contractor or vendor misuse

Includes:
- endpoint restrictions
- account access restrictions
- DLP enforcement
- cloud access restriction
- removable media restriction
- privileged access suspension

---

## 4. Containment Principles

| Principle | Description |
|-----------|-------------|
| Preserve Evidence First | Do not destroy forensic artifacts |
| Minimize Alerting the Subject | Avoid premature confrontation |
| Coordinate with HR and Legal | Required for employee-impacting actions |
| Restrict Least Privilege First | Reduce unnecessary disruption |
| Document Every Action | Maintain defensibility |
| Protect Critical Data | Prioritize sensitive assets |

---

## 5. Containment Priority Order

| Priority | Objective | Example Actions |
|----------|-----------|----------------|
| P0 | Stop active exfiltration | Block uploads/transfers |
| P1 | Protect sensitive systems | Restrict privileged access |
| P2 | Preserve evidence | Snapshot logs and devices |
| P3 | Restrict unauthorized sharing | Disable links/forwarding |
| P4 | Prevent sabotage | Restrict admin functions |
| P5 | Reduce lateral access | Segment or limit access |

---

# 6. Preconditions Before Containment

Containment must begin only after:
- initial investigation completed
- evidence preservation initiated
- HR/Legal review started (if required)
- containment approval received

---

## 6.1 Required Preconditions

| Requirement | Purpose |
|-------------|---------|
| Evidence preserved | Maintain legal integrity |
| Scope partially identified | Avoid incomplete containment |
| HR notified (if required) | Employee-impacting action review |
| Legal review initiated | Compliance protection |
| SOC Lead approval | Operational control |

---

## 6.2 Confidentiality Controls

Containment activities must remain confidential.

Do NOT:
- inform unrelated managers
- disclose containment publicly
- notify the subject without approval
- discuss the investigation outside approved channels

---

# 7. Containment Workflow Overview

| Phase | Focus Area |
|------|-------------|
| Phase 1 | Immediate risk reduction |
| Phase 2 | Identity and access restriction |
| Phase 3 | Endpoint and device containment |
| Phase 4 | Cloud and collaboration restriction |
| Phase 5 | Privileged access containment |
| Phase 6 | Validation and monitoring |

---

# 8. Phase 1 – Immediate Risk Reduction

The first objective is stopping ongoing malicious activity.

---

## 8.1 Active Exfiltration Containment

If exfiltration is actively occurring:
- block transfer paths immediately
- preserve evidence before disruption where possible
- coordinate with HR and Legal if user-facing actions are required

---

### Immediate Containment Actions

| Activity Detected | Recommended Action |
|------------------|-------------------|
| Large cloud upload | Disable sharing/upload temporarily |
| USB data transfer | Disable removable media access |
| Mass email forwarding | Disable forwarding rules |
| Unauthorized file sync | Pause sync service |
| Suspicious remote session | Restrict remote access |

---

## 8.2 Business Impact Assessment

Before high-impact containment:
- determine operational dependencies
- identify critical systems involved
- determine whether the user supports critical operations

---

### Critical Access Considerations

| User Type | Containment Caution |
|-----------|--------------------|
| Domain Admin | High-risk operational impact |
| Executive | HR and Legal coordination mandatory |
| Finance User | Payment operations impact |
| Developer/Admin | Potential production access impact |

---

# 9. Phase 2 – Identity and Access Restriction

Identity containment reduces insider access without unnecessarily disrupting business.

---

## 9.1 Account Restriction Options

| Action | Usage Scenario |
|--------|----------------|
| Force password reset | Suspected credential abuse |
| Session revocation | Active cloud sessions |
| MFA reset | Suspicious MFA changes |
| Temporary account disablement | High-risk activity |
| Remove privileged group membership | Privileged misuse |

---

## 9.2 Access Restriction Decision Matrix

| Scenario | Recommended Action |
|----------|-------------------|
| Suspicious but unconfirmed activity | Enhanced monitoring |
| Active exfiltration | Session revocation |
| Privileged misuse confirmed | Remove elevated access |
| Sabotage risk | Immediate access suspension |
| HR termination case | Coordinated disablement |

---

## 9.3 Session Revocation Guidance

Review:
- VPN sessions
- cloud sessions
- remote desktop sessions
- SaaS sessions

---

### Session Revocation Priority

| Session Type | Priority |
|--------------|----------|
| Privileged cloud sessions | Immediate |
| VPN access | Immediate |
| Admin RDP sessions | Immediate |
| SaaS collaboration sessions | High |

---

# 10. Phase 3 – Endpoint and Device Containment

Endpoint containment may be required when:
- local staging is detected
- USB abuse occurs
- sabotage is suspected
- evidence preservation is critical

---

## 10.1 Endpoint Restriction Options

| Action | Purpose |
|--------|---------|
| EDR isolate | Prevent external communication |
| Disable USB | Stop removable media use |
| Restrict network access | Limit movement |
| Preserve forensic image | Evidence preservation |
| Restrict local admin | Reduce sabotage risk |

---

## 10.2 Endpoint Isolation Guidance

Isolation should consider:
- operational impact
- evidence preservation
- user awareness risk

---

### Isolation Decision Matrix

| Scenario | Recommended Action |
|----------|-------------------|
| Data theft in progress | Isolate endpoint |
| Sabotage suspected | Immediate isolation |
| High-risk privileged misuse | Restrict network access |
| Monitoring-only investigation | No isolation initially |

---

## 10.3 USB and Removable Media Restriction

Actions:
- disable removable storage
- block unauthorized devices
- preserve USB logs
- monitor future insertion attempts

---

# 11. Phase 4 – Cloud and Collaboration Restriction

Cloud collaboration abuse is common in insider incidents.

---

## 11.1 Cloud Restriction Actions

| Action | Purpose |
|--------|---------|
| Disable external sharing | Prevent exfiltration |
| Revoke public links | Restrict exposure |
| Pause synchronization | Stop uploads |
| Restrict guest sharing | Reduce external access |
| Disable personal cloud apps | Prevent transfer |

---

## 11.2 Collaboration Platform Controls

| Platform | Restriction Type |
|----------|-----------------|
| OneDrive | Sharing restriction |
| SharePoint | Link revocation |
| Teams | External collaboration restriction |
| Slack | External workspace review |
| Email | Forwarding restriction |

---

## 11.3 Cloud Containment Indicators

| Indicator | Risk |
|-----------|------|
| Large uploads | Active exfiltration |
| External sharing links | Unauthorized exposure |
| Guest accounts added | Data sharing risk |
| Personal cloud storage use | Unapproved transfer |

---

# 12. Phase 5 – Privileged Access Containment

Privileged insider activity requires immediate attention.

---

## 12.1 Privileged Access Restriction

| Action | Purpose |
|--------|---------|
| Remove admin rights | Reduce risk |
| Disable privileged sessions | Stop misuse |
| Review privileged commands | Scope actions |
| Restrict production access | Prevent sabotage |

---

## 12.2 High-Risk Privileged Indicators

| Indicator | Required Action |
|-----------|----------------|
| Unauthorized admin account creation | Immediate review |
| Security tool disablement | IR escalation |
| Log deletion attempts | Preserve evidence immediately |
| Production system changes | Executive escalation |

---

# 13. Phase 6 – Validation and Monitoring

Containment is NOT complete until verified.

---

## 13.1 Validation Checklist

| Validation Item | Expected Result |
|----------------|----------------|
| Data transfer stopped | No active exfiltration |
| Sessions revoked | No active access |
| External sharing disabled | No unauthorized links |
| USB blocked | No further removable media activity |
| Privileged access removed | No elevated sessions |
| Monitoring active | Alerts configured |

---

## 13.2 Enhanced Monitoring Requirements

| Monitoring Area | Purpose |
|----------------|---------|
| Login activity | Detect re-access |
| Cloud uploads | Detect renewed exfiltration |
| Privileged commands | Detect misuse |
| DLP alerts | Detect transfers |
| Collaboration activity | Detect sharing |

---

## 13.3 Monitoring Duration Recommendations

| Severity | Monitoring Window |
|----------|------------------|
| P1 | Minimum 72 hours |
| P2 | Minimum 48 hours |
| P3 | Minimum 24 hours |

---

# 14. HR and Legal Coordination Requirements

Certain actions MUST NOT occur without coordination.

---

## 14.1 HR Coordination Required For

| Action | Reason |
|--------|--------|
| Employee interview | HR process |
| Access suspension | Employment impact |
| Termination-related containment | Legal/HR requirement |
| Device seizure | Employee rights considerations |

---

## 14.2 Legal Coordination Required For

| Action | Reason |
|--------|--------|
| Evidence preservation orders | Legal hold |
| Litigation support | Legal defense |
| Law enforcement involvement | Regulatory/legal process |
| Monitoring approvals | Privacy/legal review |

Reference:
`02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-HR-Legal-Coordination.md`

---

# 15. Documentation Requirements

The following must be documented:

| Documentation Item | Required |
|-------------------|----------|
| Containment actions taken | Yes |
| Approval records | Yes |
| HR/legal coordination status | Yes |
| Session revocations | Yes |
| Cloud sharing restrictions | Yes |
| Endpoint restrictions | Yes |
| Validation results | Yes |

---

# 16. Common Containment Mistakes

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Alerting employee too early | Evidence destruction |
| Disabling accounts without HR review | Legal risk |
| Failing to preserve evidence first | Investigation compromise |
| Ignoring cloud sharing | Ongoing exfiltration |
| Overly broad restrictions | Operational disruption |
| Failing to monitor after containment | Continued insider activity |

---

# 17. MSSP Client Handling Notes

For MSSP-managed environments:
- insider threat actions require client approval
- maintain strict confidentiality
- coordinate through client HR/legal teams
- document all approvals carefully
- avoid cross-client disclosure

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

# 18. Related Documents

| Document | Path |
|---------|------|
| Insider Threat Master | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-Master.md` |
| Insider Threat L1 Triage | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L1-Triage.md` |
| Insider Threat L2 Investigation | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L2-Investigation.md` |
| Insider Threat L3 Forensics | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L3-Forensics.md` |
| HR and Legal Coordination | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-HR-Legal-Coordination.md` |
| Insider Threat MITRE Mapping | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-MITRE-Mapping.md` |
| Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |

---

## 19. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 16-May-2026 | IR Team Lead / SOC Lead | Initial version |

---

## 20. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**