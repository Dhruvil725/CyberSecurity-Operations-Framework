# Role Definition – Incident Response Team (IRT)

---

## 1. Document Control

| Field | Value |
|-------|--------|
| Role | Incident Response Team (IRT) |
| Document ID | IR-ROLE-005 |
| Version | 1.0 |
| Owner | Head of Cyber Security / SOC Manager |
| Approved By | CISO |
| Review Cycle | Annual |
| Classification | Confidential |

---

## 2. Role Purpose

The Incident Response Team (IRT) is responsible for leading and executing the organization’s response to high-impact security incidents (typically P1/P2), ensuring:

- Rapid containment and business risk reduction
- Evidence preservation and forensic readiness
- Coordination across technical, business, legal, and compliance stakeholders
- Recovery guidance and validation
- Post-incident reporting and improvements

IRT is activated when incidents exceed routine SOC handling or require coordinated containment/eradication/recovery actions.

---

## 3. When IRT is Activated (Triggers)

IRT activation is required when any of the following is suspected or confirmed:

- Ransomware execution/encryption or ransomware operator activity
- Confirmed data exfiltration / breach of sensitive data
- Domain Controller / IAM / privileged account compromise
- Enterprise-wide malware outbreak or worm-like activity
- APT / persistent foothold / repeated reinfection
- Supply-chain compromise affecting production environment
- Material disruption to critical services (availability impact)
- Regulatory notification likely required (RBI/CERT-In/contractual)

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Activation-Criteria.md`

---

## 4. Reporting & Command Structure

### 4.1 Incident Command
- **Incident Commander (IC):** Typically IR Team Lead or delegated senior responder.
- **SOC Lead:** Incident coordinator until IC assumes command; continues operational SOC coordination.
- **L3 Analyst:** Technical authority for deep investigation and threat analysis.

### 4.2 Primary Interfaces
- SOC (L1/L2/L3)
- IT Infrastructure / Network / Cloud Operations
- IAM / Active Directory Team
- Business Owners / Application Owners
- GRC / Compliance
- Legal Counsel (internal/external)
- MSSP Client contacts (if client environment impacted)
- Third-party vendors (EDR/SIEM/Cloud provider/ISP)

---

## 5. IRT Core Responsibilities (Lifecycle)

### 5.1 Preparation (Readiness)
- Maintain and update IR playbooks
- Ensure forensic collection capability and evidence storage readiness
- Validate contact lists and escalation paths
- Support tabletop exercises and drills

### 5.2 Detection & Analysis (During Incident)
- Validate incident scope and impact
- Establish attack timeline and kill chain
- Identify initial access vector and persistence mechanisms
- Perform/coordinate threat intel enrichment and MITRE mapping
- Confirm affected assets, users, and data at risk

### 5.3 Containment
- Define containment strategy (short-term and long-term)
- Coordinate endpoint isolation / network segmentation / firewall blocks
- Coordinate disabling of compromised accounts and session revocation
- Ensure containment actions are recorded and approved where required

### 5.4 Eradication
- Remove malicious artifacts and persistence
- Ensure patching / configuration fixes applied
- Coordinate credential resets (privileged and impacted user accounts)
- Validate threat removal through re-scans and monitoring

### 5.5 Recovery
- Guide restoration from clean backups (if needed)
- Validate integrity and return-to-service criteria
- Implement heightened monitoring post-recovery
- Confirm business services stability

### 5.6 Post-Incident
- Lead Post Incident Review (PIR)
- Produce RCA and final incident report inputs
- Identify control gaps and create remediation plan
- Drive improvements to detections and playbooks

Reference:
`08_POST-INCIDENT/`

---

## 6. Deliverables / Outputs

IRT produces or governs the following outputs:

- Incident timeline (authoritative)
- Evidence log and chain-of-custody records
- Containment/eradication action log
- Root Cause Analysis (RCA)
- Final Incident Report (technical + executive summary)
- Recommendations / action plan and tracking items
- Regulatory reporting inputs (via Compliance/CISO)

---

## 7. Decision Authority

IRT MAY:
- Direct technical response actions during P1/P2 incidents (within approved authority model)
- Require forensic acquisition and evidence preservation steps
- Recommend shutdown of services, segmentation, credential resets (approval per authority matrix)
- Engage external IR retainers (with management/CISO approval)
- Define incident closure criteria (in coordination with SOC Lead and business owners)

IRT MAY NOT (without required approvals):
- Make external public statements
- Provide regulatory submissions directly unless formally authorized
- Approve financial/legal actions (e.g., ransom payment, settlements)

Reference:
`03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`

---

## 8. Evidence Handling & Forensic Standards

IRT ensures:
- Evidence is collected using approved methods
- Chain-of-custody is maintained for all evidence
- Evidence retention and storage rules are followed
- Investigative actions are documented and reproducible

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 9. Communication Responsibilities

IRT supports communication by providing:
- Technical findings in plain language for management/client updates
- Risk and business impact assessments
- Recommended decisions and trade-offs

All external/client communications follow:
`05_ESCALATION-AND-COMMUNICATION/`

---

## 10. Required Skills / Competencies

- Incident command and coordination
- Endpoint, network, and cloud incident response
- Forensics fundamentals (memory/disk/logs)
- Threat actor TTP analysis and MITRE ATT&CK mapping
- Crisis communication support (technical input)
- Strong documentation and reporting skills

---

## 11. Performance Metrics (KPIs)

- Time to IRT activation (P1/P2)
- Time to containment
- Reoccurrence rate (post-recovery)
- Quality of RCA and completeness of evidence
- Timeliness and quality of executive/client updates
- Remediation completion rate after PIR

---

## 12. Review & Update

This role definition shall be reviewed:
- Annually
- After any major incident (PIR)
- Upon organizational/tooling changes
- Upon regulatory requirement updates (ISO/NIST/RBI/CERT-In)

---

**End of Document**