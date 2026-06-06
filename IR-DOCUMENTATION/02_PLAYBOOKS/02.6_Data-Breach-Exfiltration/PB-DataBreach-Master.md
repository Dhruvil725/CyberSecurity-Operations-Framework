# Playbook: Data Breach and Data Exfiltration Response (Master)

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Data Breach and Data Exfiltration Response (Master) |
| Document ID | IR-PB-DBR-001 |
| Version | 1.0 |
| Effective Date | 16-May-2026 |
| Owner | IR Team Lead / SOC Manager |
| Approved By | CISO |
| Classification | Strictly Confidential |
| Review Cycle | Quarterly and after any P1/P2 data breach incident |

---

## 2. Purpose

This master playbook defines the end-to-end response procedures for:
- data breach incidents
- unauthorized data exposure
- sensitive data exfiltration
- cloud storage exposure
- insider or external data theft
- accidental data leakage
- regulatory-reportable breaches

The objectives are to:
- rapidly identify data exposure
- contain further leakage or exfiltration
- preserve evidence for legal and regulatory review
- determine impacted data and individuals
- coordinate legal, HR, compliance, and executive actions
- meet regulatory notification obligations
- minimize business, legal, and reputational impact

Data breach incidents are among the highest-risk security events because they may involve:
- regulatory penalties
- legal liability
- customer impact
- reputational damage
- contractual violations

---

## 3. Scope

Applies to:
- customer data breaches
- employee data exposure
- intellectual property theft
- cloud storage exposure
- unauthorized sharing
- accidental public exposure
- ransomware-related exfiltration
- insider data theft
- third-party data compromise

Includes:
- on-premises systems
- cloud environments
- SaaS platforms
- collaboration systems
- MSSP-managed client environments

Out of scope:
- non-sensitive data exposure without impact
- physical document exposure without digital impact
- privacy incidents unrelated to security compromise

---

## 4. Definitions

| Term | Definition |
|------|------------|
| Data Breach | Unauthorized access, exposure, or theft of data |
| Data Exfiltration | Unauthorized transfer of data outside controlled environment |
| Sensitive Data | PII, financial, healthcare, IP, regulated information |
| Regulatory Notification | Mandatory reporting to authorities |
| Data Subject | Individual whose information is impacted |
| Exposure Window | Time period data was accessible |
| Data Staging | Preparation of data before exfiltration |

---

## 5. Data Breach Categories

| Category | Description | Typical Impact |
|----------|-------------|----------------|
| Customer PII Breach | Exposure of personal data | Regulatory/legal |
| Financial Data Exposure | Banking/payment information | Critical |
| Intellectual Property Theft | Source code/trade secrets | Competitive/business |
| Cloud Exposure | Publicly accessible cloud storage | Large-scale exposure |
| Insider Data Theft | Employee or contractor exfiltration | Legal/compliance |
| Third-Party Breach | Vendor or partner compromise | Contractual/legal |

---

# 6. Severity Classification Guidance

Severity depends on:
- data sensitivity
- volume of records impacted
- exposure duration
- legal obligations
- business impact
- public exposure risk

---

## 6.1 Data Breach Severity Matrix

| Scenario | Recommended Severity |
|----------|----------------------|
| Confirmed exposure of regulated data | P1 |
| Large-scale customer data exfiltration | P1 |
| Public cloud storage exposure with sensitive data | P1 |
| Confirmed insider data theft | P1 |
| Unauthorized access without confirmed exfiltration | P2 |
| Limited internal-only exposure | P3 |
| Non-sensitive data exposure | P4 |

Reference:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

---

# 7. Activation Criteria

Activate this playbook when any of the following occur:

| Trigger | Example |
|---------|---------|
| DLP alert | Large outbound transfer |
| Cloud exposure alert | Public S3 bucket |
| Unauthorized sharing | External link sharing |
| Database export activity | Large data extraction |
| Ransomware exfiltration indicators | Data staging/upload |
| Customer notification | Reported exposure |
| Third-party notification | Vendor compromise |
| Insider theft indicators | USB/cloud exfiltration |

---

# 8. Roles and Responsibilities

| Role | Responsibilities |
|------|------------------|
| L1 SOC Analyst | Initial validation and escalation |
| L2 SOC Analyst | Scope analysis and evidence review |
| L3 Analyst | Advanced forensics and exfiltration analysis |
| SOC Lead | Incident coordination |
| IR Team | Major incident management |
| Legal Counsel | Regulatory and legal review |
| Compliance Team | Regulatory coordination |
| HR Team | Insider-related investigations |
| Executive Management | Risk and disclosure decisions |
| MSSP SDM | Client communication |

Reference:
`00_GOVERNANCE/00.3_Roles-and-Responsibilities/RACI-Matrix-IR.xlsx`

---

# 9. Data Breach Incident Lifecycle

| Phase | Description |
|------|-------------|
| Detection and Triage | Validate exposure indicators |
| Investigation | Determine scope and impact |
| Containment | Stop additional exposure |
| Legal and Regulatory Review | Determine obligations |
| Notification | Internal/external reporting |
| Recovery | Restore secure operations |
| Post-Incident Review | Lessons learned and controls improvement |

---

# 10. High-Level Response Workflow

---

## Phase A – Detection and Qualification

Activities:
- validate breach indicators
- identify data involved
- determine exposure scope
- classify severity

Reference:
`02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L1-Triage.md`

---

## Phase B – Investigation and Scoping

Activities:
- identify impacted systems
- identify impacted records
- determine exfiltration method
- review exposure duration
- assess attacker access

Reference:
`02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L2-Investigation.md`

---

## Phase C – Forensics and Evidence Preservation

Activities:
- preserve logs and evidence
- reconstruct attack timeline
- identify exfiltration methods
- determine scope of stolen data

Reference:
`02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L3-Forensics.md`

---

## Phase D – Containment and Remediation

Activities:
- stop active exfiltration
- revoke access
- secure exposed systems
- rotate credentials
- patch vulnerabilities

---

## Phase E – Legal and Regulatory Coordination

Activities:
- determine legal obligations
- coordinate notifications
- prepare regulator reports
- support law enforcement if required

References:
- `PB-DataBreach-Legal-Notification.md`
- `PB-DataBreach-Regulatory-Reporting.md`

---

## Phase F – Post-Incident Activities

Activities:
- lessons learned
- detection improvements
- policy updates
- control enhancements

Reference:
`08_POST-INCIDENT/`

---

# 11. Key Investigation Areas

| Investigation Area | Purpose |
|--------------------|---------|
| Data access logs | Identify exposure |
| Cloud audit logs | External sharing review |
| DLP telemetry | Exfiltration review |
| Email logs | Unauthorized transfers |
| Endpoint activity | Data staging review |
| Database logs | Large query/export detection |

---

# 12. Escalation Criteria

---

## 12.1 Escalate to Legal and Compliance if:

| Condition | Reason |
|-----------|--------|
| Regulated data exposed | Mandatory review |
| Public disclosure risk | Legal impact |
| Customer data involved | Notification obligations |
| Cross-border data exposure | Jurisdictional requirements |

---

## 12.2 Escalate to IR Team if:

| Condition | Reason |
|-----------|--------|
| Large-scale exfiltration | Major incident |
| Public exposure confirmed | Reputational risk |
| Multiple systems impacted | Enterprise-wide compromise |
| Insider theft confirmed | Coordinated response required |

---

# 13. Evidence Handling Requirements

Data breach evidence may become:
- legal evidence
- regulatory evidence
- litigation evidence

Preserve:
- DLP logs
- cloud audit logs
- database logs
- access records
- endpoint telemetry
- exfiltration evidence
- screenshots and exports

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

# 14. Common Data Breach Response Mistakes

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Delaying containment | Continued exposure |
| Failing to preserve logs quickly | Evidence loss |
| Underestimating exposed records | Regulatory issues |
| Public disclosure before validation | Reputational/legal risk |
| Delaying Legal involvement | Compliance exposure |
| Ignoring cloud audit logs | Missed exposure scope |

---

# 15. MSSP Considerations

For MSSP-managed environments:
- maintain client evidence segregation
- coordinate legal notifications through client-approved channels
- avoid cross-client disclosure
- follow contractual reporting obligations
- maintain strict confidentiality

Reference:
`09_MSSP-SPECIFIC/`

---

# 16. Related Documents

| Document | Path |
|---------|------|
| Data Breach L1 Triage | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L1-Triage.md` |
| Data Breach L2 Investigation | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L2-Investigation.md` |
| Data Breach L3 Forensics | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-L3-Forensics.md` |
| Legal Notification | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Legal-Notification.md` |
| Regulatory Reporting | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Regulatory-Reporting.md` |
| Data Breach MITRE Mapping | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-MITRE-Mapping.md` |
| Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |

---

## 17. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 16-May-2026 | IR Team Lead / SOC Manager | Initial version |

---

## 18. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**