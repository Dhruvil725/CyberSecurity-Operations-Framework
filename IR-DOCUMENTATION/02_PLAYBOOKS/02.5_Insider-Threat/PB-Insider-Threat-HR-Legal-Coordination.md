# Playbook: Insider Threat – HR and Legal Coordination

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Insider Threat (HR and Legal Coordination) |
| Document ID | IR-PB-INS-006 |
| Version | 1.0 |
| Effective Date | 16-May-2026 |
| Owner | IR Team Lead / HR Security Liaison |
| Approved By | CISO and Legal Counsel |
| Classification | Strictly Confidential |
| Review Cycle | Quarterly and after any P1/P2 insider threat incident |

---

## 2. Purpose

This document defines the coordination procedures between:
- Security Operations
- Incident Response
- Human Resources
- Legal Counsel
- Executive Management

during insider threat investigations.

Insider threat incidents frequently involve:
- employee misconduct
- policy violations
- legal risk
- privacy concerns
- disciplinary actions
- potential litigation

This document ensures:
- investigations remain legally defensible
- employee rights are respected
- evidence is preserved correctly
- HR and Legal are engaged appropriately
- confidentiality is maintained
- operational and legal risks are minimized

---

## 3. Scope

Applies to:
- malicious insider investigations
- employee misconduct investigations involving security
- privileged misuse investigations
- data theft or sabotage
- contractor/vendor misuse
- employee termination risk cases
- legal hold situations
- law enforcement escalation scenarios

Includes:
- employee interviews
- account restriction approvals
- legal evidence handling
- disciplinary coordination
- regulatory coordination

---

## 4. Coordination Principles

| Principle | Description |
|-----------|-------------|
| Confidentiality First | Limit exposure of investigation details |
| Need-to-Know Access | Only authorized personnel involved |
| Legal Defensibility | Preserve evidence integrity |
| HR Ownership of Personnel Actions | Security does not discipline employees |
| Minimize Business Risk | Balance investigation and operations |
| Preserve Employee Rights | Follow policy and legal requirements |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|------|------------------|
| SOC Team | Technical detection and investigation |
| IR Team | Coordination and evidence handling |
| HR Team | Employee management and disciplinary coordination |
| Legal Counsel | Legal guidance and evidence review |
| Executive Management | Business and risk decisions |
| IAM Team | Access restrictions and monitoring |
| MSSP SDM | Client communication (if applicable) |

---

# 6. HR Engagement Triggers

HR involvement is required when insider activity may involve:
- employee misconduct
- policy violations
- disciplinary action
- termination risk
- workplace conflict
- employee monitoring concerns

---

## 6.1 Mandatory HR Escalation Conditions

| Condition | HR Involvement Required |
|-----------|-------------------------|
| Employee suspected of data theft | Yes |
| Employee termination pending | Yes |
| Insider sabotage indicators | Yes |
| Privileged misuse by employee | Yes |
| Employee interview required | Yes |
| Access suspension impacts employment | Yes |

---

## 6.2 HR Coordination Objectives

| Objective | Purpose |
|-----------|---------|
| Protect employee rights | Compliance and fairness |
| Coordinate interviews | Reduce legal exposure |
| Manage disciplinary actions | HR governance |
| Support confidentiality | Prevent workplace disruption |

---

# 7. Legal Engagement Triggers

Legal Counsel must be engaged early when:
- litigation is possible
- sensitive data exposure occurred
- evidence may be used legally
- employee privacy concerns exist
- law enforcement involvement is possible

---

## 7.1 Mandatory Legal Escalation Conditions

| Condition | Legal Involvement Required |
|-----------|---------------------------|
| Data theft confirmed | Yes |
| Customer data exposure | Yes |
| Regulatory data involved | Yes |
| Employee litigation risk | Yes |
| Evidence seizure required | Yes |
| Law enforcement referral possible | Yes |

---

## 7.2 Legal Coordination Objectives

| Objective | Purpose |
|-----------|---------|
| Preserve legal defensibility | Evidence integrity |
| Reduce liability | Compliance |
| Guide employee actions | Legal protection |
| Review disclosure obligations | Regulatory alignment |

---

# 8. Confidentiality Requirements

Insider threat investigations are highly sensitive.

---

## 8.1 Information Classification Rules

| Information Type | Access Restriction |
|------------------|-------------------|
| Employee investigation details | Restricted |
| HR records | HR + Legal only |
| Evidence artifacts | Approved investigators only |
| Executive communications | Restricted |
| Disciplinary recommendations | HR + Legal only |

---

## 8.2 Prohibited Actions

| Prohibited Action | Risk |
|-------------------|------|
| Discussing case in open channels | Confidentiality breach |
| Informing unrelated managers | Investigation compromise |
| Sharing evidence broadly | Privacy/legal exposure |
| Discussing disciplinary outcomes | HR/legal violation |

---

# 9. Employee Monitoring Guidance

Monitoring employees may involve:
- legal requirements
- regional privacy laws
- policy limitations
- executive approvals

---

## 9.1 Monitoring Approval Requirements

| Monitoring Activity | Approval Required |
|---------------------|------------------|
| Enhanced endpoint monitoring | SOC Lead |
| Covert monitoring | Legal + Executive approval |
| Email review | HR + Legal |
| Cloud activity monitoring | Legal review |
| USB monitoring | Approved security monitoring policy |

---

## 9.2 Monitoring Principles

| Principle | Description |
|-----------|-------------|
| Least invasive first | Reduce privacy risk |
| Scope limitation | Monitor only relevant activity |
| Time limitation | Avoid indefinite monitoring |
| Documentation | Maintain legal defensibility |

---

# 10. Account Restriction and Suspension Procedures

Account restrictions may significantly impact employment and operations.

---

## 10.1 Account Restriction Types

| Restriction Type | Usage |
|------------------|------|
| Session revocation | Active threat containment |
| Password reset | Credential exposure |
| Privilege removal | Admin misuse |
| Full account suspension | High-risk insider activity |
| Cloud sharing disablement | Exfiltration prevention |

---

## 10.2 Approval Requirements

| Action | Required Approval |
|--------|-------------------|
| Session revocation | SOC Lead |
| Password reset | IAM + SOC Lead |
| Admin privilege removal | Management + HR |
| Full account disablement | HR + Legal + Management |
| Device seizure | Legal + HR |

---

## 10.3 High-Risk Scenarios

| Scenario | Required Action |
|-----------|----------------|
| Employee under termination review | Coordinate carefully with HR |
| Privileged administrator involved | Immediate escalation |
| Active sabotage risk | Emergency containment |
| Data theft in progress | Immediate restriction with legal review |

---

# 11. Employee Interview Coordination

Security personnel must NOT independently conduct disciplinary interviews.

---

## 11.1 Interview Coordination Principles

| Principle | Purpose |
|-----------|---------|
| HR-led process | Maintain compliance |
| Legal review before interview | Reduce liability |
| Preserve evidence first | Prevent evidence destruction |
| Controlled questioning | Avoid legal complications |

---

## 11.2 Pre-Interview Checklist

| Checklist Item | Required |
|----------------|----------|
| Evidence preserved | Yes |
| Timeline prepared | Yes |
| Legal review completed | Yes |
| HR representative assigned | Yes |
| Access status reviewed | Yes |

---

# 12. Legal Hold and Evidence Preservation

When litigation or legal review is possible:
- evidence must be preserved immediately
- deletion must stop
- retention periods may be extended

---

## 12.1 Legal Hold Triggers

| Trigger | Action |
|---------|--------|
| Litigation risk | Legal hold initiated |
| Regulatory review | Preserve evidence |
| Customer data theft | Extended retention |
| Employee dispute | Evidence preservation |

---

## 12.2 Evidence Preservation Requirements

| Evidence Type | Preservation Method |
|--------------|---------------------|
| Endpoint images | Forensic storage |
| Cloud logs | Export and hash |
| Email evidence | Immutable archive |
| DLP records | Secure export |
| HR communications | Restricted storage |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

# 13. Law Enforcement Coordination

Law enforcement involvement must be approved through Legal Counsel.

---

## 13.1 Law Enforcement Escalation Triggers

| Trigger | Escalation Requirement |
|----------|-----------------------|
| Criminal data theft | Legal review |
| Sabotage causing major impact | Executive escalation |
| Regulatory reporting requirement | Compliance + Legal |
| Financial fraud | Legal coordination |

---

## 13.2 Law Enforcement Evidence Requirements

| Requirement | Purpose |
|-------------|---------|
| Chain-of-custody complete | Legal admissibility |
| Evidence hashing | Integrity validation |
| Timeline reconstruction | Investigation support |
| Evidence access logging | Accountability |

---

# 14. Communication Guidance

Insider investigations require controlled communication.

---

## 14.1 Internal Communication Restrictions

| Audience | Allowed Information |
|----------|--------------------|
| SOC Analysts | Technical details only |
| HR | Employee-related findings |
| Legal | Full legal-impact information |
| Management | Business risk summary |
| General Employees | None |

---

## 14.2 Executive Briefing Requirements

Executive briefings should include:
- business impact
- legal risk
- operational risk
- status of investigation
- containment actions
- HR/legal coordination status

---

# 15. Documentation Requirements

The following must be documented:

| Documentation Item | Required |
|-------------------|----------|
| HR coordination timeline | Yes |
| Legal engagement timeline | Yes |
| Account restriction approvals | Yes |
| Monitoring approvals | Yes |
| Interview coordination notes | Yes |
| Legal hold documentation | Yes |

---

# 16. Common HR and Legal Coordination Mistakes

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Delaying Legal involvement | Increased liability |
| Security interviewing employees alone | HR/legal exposure |
| Broadly sharing investigation details | Confidentiality breach |
| Disabling accounts without approval | Employment/legal impact |
| Failing to preserve evidence early | Legal defensibility loss |
| Conducting covert monitoring without approval | Privacy/legal violation |

---

# 17. MSSP Client Handling Notes

For MSSP-managed environments:
- client HR and Legal teams own employee disciplinary actions
- MSSP personnel must not directly contact client employees unless authorized
- maintain strict client confidentiality
- document all approvals carefully
- insider investigations remain client-scoped

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
| Insider Threat Containment | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-Containment.md` |
| Insider Threat MITRE Mapping | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-MITRE-Mapping.md` |
| Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |
| Legal Counsel Engagement SOP | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |

---

## 19. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 16-May-2026 | IR Team Lead / HR Security Liaison | Initial version |

---

## 20. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**