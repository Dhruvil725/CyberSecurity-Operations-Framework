# Playbook: Insider Threat Response (Master)

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Insider Threat Response (Master) |
| Document ID | IR-PB-INS-001 |
| Version | 1.0 |
| Effective Date | 16-May-2026 |
| Owner | IR Team Lead / SOC Manager |
| Approved By | CISO |
| Classification | Strictly Confidential |
| Review Cycle | Quarterly and after any major insider threat incident |

---

## 2. Purpose

This master playbook defines the end-to-end response procedures for
insider threat incidents across enterprise and MSSP-managed environments.

Insider threats differ from traditional cyberattacks because:
- the actor already has legitimate access
- activity may initially appear normal
- incidents often involve HR, Legal, and executive management
- evidence handling requirements are significantly more sensitive
- legal and privacy considerations are critical

This playbook standardizes:
- insider threat identification
- investigation and escalation
- HR and Legal coordination
- evidence preservation
- containment and access restriction
- employee monitoring procedures
- privileged misuse investigations
- data exfiltration investigations
- post-incident review and reporting

---

## 3. Scope

Applies to:
- malicious insider activity
- negligent insider actions
- employee data theft
- unauthorized privileged access
- sabotage attempts
- insider-assisted breaches
- intellectual property theft
- policy violations with security impact
- contractor or vendor misuse
- privileged account abuse

Includes:
- employees
- contractors
- vendors
- temporary staff
- privileged administrators
- MSSP internal users (where applicable)

Out of scope unless specifically escalated:
- HR-only disciplinary matters
- non-security workplace misconduct
- physical violence or safety incidents

---

## 4. Definitions

| Term | Definition |
|------|------------|
| Insider Threat | Threat originating from trusted internal access |
| Malicious Insider | Insider intentionally causing harm |
| Negligent Insider | Insider unintentionally causing risk |
| Privileged Misuse | Abuse of elevated access rights |
| Data Exfiltration | Unauthorized transfer of sensitive data |
| Need-to-Know Principle | Restricting information access to essential personnel only |
| Covert Monitoring | Monitoring performed without subject awareness |
| Evidence Integrity | Preservation of evidence without alteration |

---

## 5. Insider Threat Categories

| Category | Description | Typical Risk |
|----------|-------------|--------------|
| Malicious Insider | Intentional harm or theft | Critical |
| Negligent Insider | Unsafe behavior causing risk | Medium |
| Compromised Insider Account | Insider account used by attacker | High |
| Privileged Abuse | Unauthorized admin activity | Critical |
| Data Theft | Exfiltration of sensitive data | Critical |
| Sabotage | Intentional disruption | Critical |

---

# 6. Severity Classification Guidance

Severity depends on:
- sensitivity of impacted data
- privilege level involved
- business impact
- legal implications
- regulatory exposure
- intent indicators

---

## 6.1 Insider Threat Severity Matrix

| Scenario | Recommended Severity |
|----------|----------------------|
| Executive or admin data theft | P1 |
| Confirmed sabotage or destructive activity | P1 |
| Large-scale sensitive data exfiltration | P1 |
| Privileged misuse without exfiltration | P2 |
| Unauthorized access to restricted data | P2 |
| Suspicious insider behavior under investigation | P3 |
| Policy violation without security impact | P4 |

Reference:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

---

# 7. Activation Criteria

Activate this playbook when any of the following occur:

| Trigger | Example |
|---------|---------|
| Unusual privileged activity | Admin access outside normal hours |
| Large data transfer | Massive file copy or upload |
| Unauthorized cloud storage usage | Upload to personal drive |
| USB mass copy activity | Sensitive files copied externally |
| HR termination notification | Elevated insider risk |
| Suspicious email forwarding | Internal data forwarding |
| Access outside normal role | Unauthorized database access |
| Data deletion or sabotage indicators | Intentional destruction |

---

# 8. Roles and Responsibilities

| Role | Responsibilities |
|------|------------------|
| L1 SOC Analyst | Initial alert validation and escalation |
| L2 SOC Analyst | Activity analysis and scoping |
| L3 Analyst | Advanced forensics and timeline reconstruction |
| SOC Lead | Incident coordination |
| IR Team | Major incident response |
| HR Team | Employee coordination and policy review |
| Legal Counsel | Legal guidance and evidence handling |
| Management | Business decisions and risk acceptance |
| IAM Team | Account restriction and access review |
| MSSP SDM | Client communication (if applicable) |

Reference:
`00_GOVERNANCE/00.3_Roles-and-Responsibilities/RACI-Matrix-IR.xlsx`

---

# 9. Insider Threat Investigation Principles

Insider threat investigations require strict operational discipline.

---

## 9.1 Key Principles

| Principle | Description |
|-----------|-------------|
| Need-to-Know Only | Limit awareness to approved personnel |
| Preserve Evidence | Do not alter activity records |
| Avoid Premature Confrontation | Prevent evidence destruction |
| Coordinate with HR/Legal | Mandatory for employee-related actions |
| Maintain Confidentiality | Reduce legal and reputational risk |
| Use Least Disruptive Measures First | Minimize operational impact |

---

## 9.2 Confidentiality Requirements

Information regarding insider investigations must NOT be shared with:
- unrelated employees
- unauthorized managers
- external parties
- other clients (MSSP)

Only approved personnel may access:
- investigation notes
- HR communications
- legal guidance
- evidence repositories

---

# 10. Insider Threat Incident Lifecycle

| Phase | Description |
|------|-------------|
| Detection and Triage | Validate suspicious activity |
| Investigation | Scope actions and intent |
| Containment | Restrict access and stop activity |
| Coordination | HR and Legal engagement |
| Forensics | Evidence preservation and timeline |
| Remediation | Remove unauthorized access |
| Post-Incident Review | Lessons learned and controls improvement |

---

# 11. High-Level Response Workflow

---

## Phase A – Detection and Qualification

Performed by:
- SOC
- DLP tools
- IAM monitoring
- UEBA systems
- HR referrals

Activities:
- validate suspicious behavior
- identify impacted assets/data
- assess privilege level
- determine escalation requirements

Reference:
`02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L1-Triage.md`

---

## Phase B – Investigation and Scoping

Performed by:
- L2/L3 SOC
- IR Team
- HR and Legal (where required)

Activities:
- review access history
- review data transfer activity
- identify policy violations
- determine malicious intent indicators
- reconstruct timeline

Reference:
`02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L2-Investigation.md`

---

## Phase C – Containment

Activities:
- restrict account access
- disable privileged sessions
- preserve evidence
- prevent exfiltration continuation
- coordinate HR/legal actions

Reference:
`02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-Containment.md`

---

## Phase D – Advanced Forensics

Activities:
- endpoint forensics
- log correlation
- data transfer analysis
- timeline reconstruction
- cloud activity review

Reference:
`02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L3-Forensics.md`

---

## Phase E – HR and Legal Coordination

Activities:
- disciplinary coordination
- legal review
- evidence handling guidance
- employee interview coordination

Reference:
`02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-HR-Legal-Coordination.md`

---

## Phase F – Post-Incident Activities

Activities:
- lessons learned
- control improvement
- DLP tuning
- access review improvements
- monitoring enhancements

Reference:
`08_POST-INCIDENT/`

---

# 12. Key Investigation Areas

| Investigation Area | Purpose |
|--------------------|---------|
| File access activity | Detect sensitive data access |
| USB activity | Detect removable media usage |
| Cloud uploads | Detect exfiltration |
| Email forwarding | Detect unauthorized sharing |
| Privileged access logs | Detect admin misuse |
| Login patterns | Detect unusual behavior |
| Endpoint activity | Detect local data staging |

---

# 13. Escalation Criteria

---

## 13.1 Escalate to HR and Legal if:

| Condition | Reason |
|-----------|--------|
| Employee misconduct suspected | HR involvement required |
| Data theft suspected | Legal risk |
| Termination-related activity | Elevated insider risk |
| Sabotage indicators present | Legal and executive involvement |

---

## 13.2 Escalate to IR Team if:

| Condition | Reason |
|-----------|--------|
| Large-scale data theft | Major incident |
| Privileged misuse confirmed | Critical risk |
| Multiple insiders involved | Coordinated activity |
| Destructive activity detected | Business impact |

---

# 14. Evidence Handling Requirements

Insider threat investigations require strict evidence handling controls.

Preserve:
- endpoint logs
- DLP logs
- access logs
- email records
- cloud audit logs
- USB activity
- screenshots and exports
- HR/legal communications (restricted access)

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

# 15. Common Insider Threat Investigation Mistakes

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Alerting employee too early | Evidence destruction |
| Broad internal disclosure | Confidentiality breach |
| Failing to involve Legal | Legal exposure |
| Not preserving logs quickly | Evidence loss |
| Ignoring HR coordination | Process failure |
| Assuming malicious intent too early | Incorrect escalation |

---

# 16. MSSP Considerations

For MSSP-managed environments:
- insider investigations must remain client-scoped
- strict confidentiality required
- client HR/legal teams must approve employee-impacting actions
- maintain evidence segregation
- avoid cross-client intelligence sharing

Reference:
`09_MSSP-SPECIFIC/`

---

# 17. Related Documents

| Document | Path |
|---------|------|
| Insider Threat L1 Triage | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L1-Triage.md` |
| Insider Threat L2 Investigation | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L2-Investigation.md` |
| Insider Threat L3 Forensics | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-L3-Forensics.md` |
| Insider Threat Containment | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-Containment.md` |
| HR and Legal Coordination | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-HR-Legal-Coordination.md` |
| Insider Threat MITRE Mapping | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-MITRE-Mapping.md` |
| Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |

---

## 18. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 16-May-2026 | IR Team Lead / SOC Manager | Initial version |

---

## 19. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**