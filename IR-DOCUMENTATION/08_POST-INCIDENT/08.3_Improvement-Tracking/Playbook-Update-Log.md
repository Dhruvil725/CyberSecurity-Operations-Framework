# Playbook Update Log

---

# 1. Document Control

| Field          | Value                          |
| -------------- | ------------------------------ |
| Document Name  | Register – Playbook Update Log |
| Document ID    | IMP-PB-001                     |
| Version        | 1.0                            |
| Effective Date | 30-May-2026                    |
| Owner          | IR Team Lead / SOC Manager     |
| Approved By    | CISO                           |
| Classification | Internal – Confidential        |
| Review Cycle   | Quarterly                      |

---

# 2. Purpose

This document provides the standardized **Playbook Update Log** register to track all updates, revisions, additions, and retirements of incident response playbooks across the IR documentation library.

A formal playbook update log is critical because:

- playbooks are living documents that must evolve with the threat landscape
- post-incident lessons must translate into playbook improvements
- NIST SP 800-61 emphasizes continuous improvement of response capability
- ISO 27001 Annex A.5.27 mandates learning from incidents
- RBI Cyber Security Framework expects mature, current incident handling procedures
- outdated playbooks lead to ineffective response and increased dwell time
- audit trail required for playbook lifecycle (creation, update, retirement)
- MSSP clients expect documented playbook maintenance evidence
- multiple stakeholders must be aware of playbook changes
- compliance audits require version control evidence

This register ensures:

- consistent tracking of all playbook changes
- version control across the playbook library
- traceability from trigger (incident/intel/exercise) to playbook update
- approval workflow for playbook changes
- notification tracking to relevant SOC/IR personnel
- audit-ready evidence of playbook maintenance
- linkage to RCA, Lessons Learned, and detection improvements

Reference alignment:
`02_PLAYBOOKS/02.0_Playbook-Index.md`
`08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`
`08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`

---

# 3. Scope

This log tracks updates to playbooks across:

| Category                         | Coverage                                               |
| -------------------------------- | ------------------------------------------------------ |
| Attack-specific playbooks        | Ransomware, Phishing, Malware, DDoS, etc. (02.1–02.13) |
| Tier-specific playbooks          | L1 Triage, L2 Investigation, L3 Forensics              |
| Sub-process playbooks            | Containment, Eradication, Recovery                     |
| Tool-specific playbooks          | SIEM, EDR, Firewall, Cloud-specific                    |
| MITRE-mapping playbooks          | Per-attack ATT&CK mappings                             |
| Client-specific playbooks (MSSP) | Custom client playbooks                                |
| Sub-procedure SOPs               | Within playbook context                                |

Triggers for playbook updates:

| Trigger             | Examples                                           |
| ------------------- | -------------------------------------------------- |
| Incident-driven     | New TTPs observed, response gap identified         |
| RCA/LL-driven       | Post-incident improvement action                   |
| Threat intel-driven | New threat actor TTPs                              |
| Exercise-driven     | Tabletop or red/purple team finding                |
| Tool change-driven  | New tool deployment or capability change           |
| Compliance-driven   | Regulatory requirement change                      |
| Periodic review     | Scheduled annual/quarterly review                  |
| Vendor advisory     | Critical vulnerability response procedure          |
| Cloud/SaaS update   | Provider feature change requiring procedure update |

Out of scope:

- minor typo corrections (version increment only)
- formatting-only changes (no functional impact)
- changes tracked separately in other registers (e.g., detection rules)

---

# 4. Definitions

| Term                | Definition                                                                        |
| ------------------- | --------------------------------------------------------------------------------- |
| Playbook            | Documented step-by-step response procedure for specific incident type or activity |
| Master Playbook     | Top-level playbook for an attack category (e.g., PB-Ransomware-Master.md)         |
| Sub-Playbook        | Tier or phase-specific playbook (e.g., PB-Ransomware-L1-Triage.md)                |
| Version             | Semantic version of playbook (Major.Minor.Patch)                                  |
| Major Update        | Significant structural or content change; new procedures added                    |
| Minor Update        | Refinement of existing procedures; clarifications                                 |
| Patch Update        | Typo fixes, formatting, link corrections                                          |
| Retired Playbook    | Playbook no longer in active use; archived                                        |
| Approval Workflow   | Defined approvers for playbook changes based on impact                            |
| Change Notification | Communication to stakeholders about playbook changes                              |

---

# 5. Roles and Responsibilities

| Role                     | Responsibilities                                              |
| ------------------------ | ------------------------------------------------------------- |
| Playbook Owner           | Owns specific playbook(s); drives updates; maintains accuracy |
| IR Team Lead             | Reviews technical accuracy of major updates                   |
| SOC Lead                 | Validates operational feasibility of playbook procedures      |
| L1/L2/L3 Analysts        | Provide feedback on playbook usability; identify gaps         |
| Threat Intel Analyst     | Provides intel-driven update requirements                     |
| Detection Engineer       | Aligns playbook with detection capability                     |
| SOC Manager              | Approves major updates; reviews log quarterly                 |
| CISO                     | Approves strategic playbook changes; reviews quarterly        |
| Compliance Lead          | Validates compliance alignment of playbook changes            |
| Training Lead            | Coordinates training on updated playbooks                     |
| MSSP SDM (if applicable) | Coordinates client-specific playbook updates                  |
| Documentation Custodian  | Maintains version control and archive                         |

---

# 6. Playbook Update Lifecycle (Mandatory)

| Phase               | Activities                         | Owner                     | Output                 |
| ------------------- | ---------------------------------- | ------------------------- | ---------------------- |
| **1. Trigger**      | Update need identified             | Any stakeholder           | Update request created |
| **2. Logging**      | Entry created in update log        | Playbook Owner            | Log entry              |
| **3. Assessment**   | Impact assessment, scope defined   | Playbook Owner            | Update scope document  |
| **4. Drafting**     | Updates drafted                    | Playbook Owner            | Draft playbook         |
| **5. Review**       | Technical and operational review   | IR Team Lead / SOC Lead   | Review comments        |
| **6. Approval**     | Approval per workflow              | SOC Manager / CISO        | Approval record        |
| **7. Versioning**   | Version incremented                | Playbook Owner            | Versioned playbook     |
| **8. Publication**  | Published to documentation library | Documentation Custodian   | Published version      |
| **9. Notification** | Stakeholders notified              | Playbook Owner / SOC Lead | Notification log       |
| **10. Training**    | Training delivered if needed       | Training Lead             | Training record        |
| **11. Validation**  | Validation via drill/exercise      | SOC Lead                  | Validation record      |
| **12. Archive**     | Previous version archived          | Documentation Custodian   | Archived version       |

---

# 7. Versioning Standard (Mandatory)

| Version Type      | When to Use                                               | Example     |
| ----------------- | --------------------------------------------------------- | ----------- |
| **Major (X.0.0)** | Structural change, new procedures added, complete rewrite | 1.0 → 2.0   |
| **Minor (X.Y.0)** | New section, refinement of procedures, expanded content   | 1.0 → 1.1   |
| **Patch (X.Y.Z)** | Typo fix, link correction, formatting                     | 1.1 → 1.1.1 |

**Format:** `vMajor.Minor.Patch` (e.g., `v2.3.1`)

**Initial Version:** All new playbooks start at `v1.0.0`

---

# 8. Approval Workflow (Mandatory)

| Update Type                | Reviewer                             | Approver             |
| -------------------------- | ------------------------------------ | -------------------- |
| **Patch (typo/format)**    | Playbook Owner                       | Playbook Owner       |
| **Minor (refinement)**     | IR Team Lead                         | SOC Lead             |
| **Major (structural)**     | IR Team Lead + SOC Lead              | SOC Manager          |
| **New Playbook**           | IR Team Lead + SOC Lead + Compliance | SOC Manager + CISO   |
| **Retirement**             | IR Team Lead + SOC Lead              | SOC Manager + CISO   |
| **Client-specific (MSSP)** | MSSP SDM + IR Team Lead              | SOC Manager + Client |

---

# 9. Notification Requirements (Mandatory)

| Update Type     | Notification Audience        | Method                                      |
| --------------- | ---------------------------- | ------------------------------------------- |
| Patch           | Playbook Owner only          | Internal note                               |
| Minor           | SOC team (L1/L2/L3/Lead)     | Email + Team channel                        |
| Major           | All SOC + IR + Management    | Email + Team meeting + Documentation portal |
| New Playbook    | All SOC + IR + Training Team | Email + Training session                    |
| Retirement      | All SOC + IR                 | Email + Documentation portal                |
| Client-specific | Internal SOC + Client SOC    | Email + Client portal                       |

---

# 10. Playbook Update Register Template (Copy/Paste)

## 10.1 Register Schema (Mandatory Fields)

| Field                        | Description                                                                           |
| ---------------------------- | ------------------------------------------------------------------------------------- |
| Update ID                    | Unique identifier (`PB-UPD-YYYY-####`)                                                |
| Date Identified (UTC)        | When update need was identified                                                       |
| Date Completed (UTC)         | When update was published                                                             |
| Trigger Type                 | Incident / RCA / LL / Intel / Exercise / Periodic / Compliance / Tool Change / Vendor |
| Trigger Reference            | INC-####, RCA-####, LL-####, EX-####, etc.                                            |
| Playbook Affected            | Path / Name of playbook                                                               |
| Playbook Category            | Attack Type / Tier / Tool / Client / Sub-process                                      |
| Update Type                  | Major / Minor / Patch / New / Retired                                                 |
| Version (Before)             | Previous version                                                                      |
| Version (After)              | New version                                                                           |
| Summary of Change            | Brief summary of update                                                               |
| Detailed Change              | Detailed description of changes                                                       |
| Owner                        | Playbook Owner                                                                        |
| Reviewer(s)                  | Reviewers per workflow                                                                |
| Approver                     | Approver per workflow                                                                 |
| Approval Date (UTC)          | Date of approval                                                                      |
| Publication Date (UTC)       | Date published                                                                        |
| Notification Sent (Y/N)      | Whether stakeholders notified                                                         |
| Training Required (Y/N)      | Whether training is required                                                          |
| Training Date                | If training delivered                                                                 |
| Validation Method            | Drill / Exercise / Next incident                                                      |
| Validation Date              | When validated                                                                        |
| Linked RCA                   | RCA-YYYY-####                                                                         |
| Linked LL                    | LL-YYYY-####                                                                          |
| Linked Detection Improvement | DET-IMP-YYYY-####                                                                     |
| Status                       | Open / In Review / Approved / Published / Validated / Closed                          |
| Notes                        | Additional context                                                                    |

---

## 10.2 Register Table (Copy/Paste)

| Update ID        | Date Identified | Date Completed | Trigger         | Trigger Ref | Playbook                     | Category  | Update Type | Version Before | Version After | Summary | Owner | Approver | Status    | Linked RCA | Notes |
| ---------------- | --------------- | -------------- | --------------- | ----------- | ---------------------------- | --------- | ----------- | -------------- | ------------- | ------- | ----- | -------- | --------- | ---------- | ----- |
| PB-UPD-YYYY-0001 |                 |                | Incident        | INC-####    | `PB-Ransomware-L1-Triage.md` | L1 Triage | Minor       | v1.2.0         | v1.3.0        |         |       |          | Published |            |       |
| PB-UPD-YYYY-0002 |                 |                | RCA             | RCA-####    |                              |           |             |                |               |         |       |          |           |            |       |
| PB-UPD-YYYY-0003 |                 |                | Periodic Review | N/A         |                              |           |             |                |               |         |       |          |           |            |       |

---

## 10.3 Detailed Entry Template (Per Update)

> Use this format for each significant playbook update.

### Update: `PB-UPD-YYYY-####`

**Metadata:**

| Field                 | Value                                 |
| --------------------- | ------------------------------------- |
| Playbook              |                                       |
| Date Identified (UTC) |                                       |
| Trigger Type          |                                       |
| Trigger Reference     |                                       |
| Update Type           | Major / Minor / Patch / New / Retired |
| Priority              | Critical / High / Medium / Low        |
| Status                |                                       |
| Owner                 |                                       |
| Reviewer(s)           |                                       |
| Approver              |                                       |
| Target Completion     |                                       |
| Actual Completion     |                                       |

**Trigger Context:**

`Describe what triggered the update need. Reference the source (incident, RCA, exercise, etc.).`

**Current State (Before Update):**

`Describe the current playbook content/approach that requires change.`

**Proposed Change:**

`Detailed description of what will be changed and why.`

**Impact Assessment:**

| Aspect                             | Impact                 |
| ---------------------------------- | ---------------------- |
| Affected SOC tiers                 | L1 / L2 / L3 / IR Team |
| Affected processes                 |                        |
| Tool/configuration changes needed  |                        |
| Training required                  |                        |
| Other playbooks affected (cascade) |                        |
| Detection rules affected           |                        |
| MSSP client impact (if applicable) |                        |

**Version Change:**

| Aspect       | Before | After |
| ------------ | ------ | ----- |
| Version      |        |       |
| Last Updated |        |       |
| Owner        |        |       |
| Approver     |        |       |

**Detailed Change Log:**

| Section                         | Change Description                    |
| ------------------------------- | ------------------------------------- |
| Section 1 (e.g., Triage)        | Added new alert validation step       |
| Section 3 (e.g., Containment)   | Updated EDR isolation procedure       |
| Section 5 (e.g., Communication) | Added regulatory notification trigger |

**Review Comments:**

| Reviewer | Comment | Resolution |
| -------- | ------- | ---------- |
|          |         |            |

**Approval:**

| Role                | Name | Date | Signature/Approval Ref |
| ------------------- | ---- | ---- | ---------------------- |
| Playbook Owner      |      |      |                        |
| IR Team Lead        |      |      |                        |
| SOC Manager         |      |      |                        |
| CISO (if Major/New) |      |      |                        |

**Notification Log:**

| Audience                    | Method               | Date Sent | Confirmation |
| --------------------------- | -------------------- | --------- | ------------ |
| SOC L1/L2/L3                | Email + Team channel |           |              |
| IR Team                     | Email                |           |              |
| Management                  | Email                |           |              |
| MSSP Client (if applicable) | Client portal        |           |              |

**Training Record:**

| Training Type               | Audience | Date | Trainer | Attendance |
| --------------------------- | -------- | ---- | ------- | ---------- |
| Briefing / Workshop / Drill |          |      |         |            |

**Validation:**

| Validation Method | Date | Result                | Notes |
| ----------------- | ---- | --------------------- | ----- |
| Tabletop exercise |      | Pass / Fail / Partial |       |
| Drill             |      |                       |       |
| Real incident     |      |                       |       |

---

# 11. Status Definitions (Standard)

| Status                 | Definition                                      |
| ---------------------- | ----------------------------------------------- |
| **Identified**         | Update need identified, logged                  |
| **Assessed**           | Impact assessed, scope defined                  |
| **In Drafting**        | Update being drafted                            |
| **In Review**          | Under review by designated reviewers            |
| **Pending Approval**   | Awaiting approval per workflow                  |
| **Approved**           | Approved, awaiting publication                  |
| **Published**          | Published to documentation library              |
| **Notified**           | Stakeholders notified                           |
| **Training Delivered** | Training completed (if required)                |
| **Validated**          | Validated via drill/exercise/incident           |
| **Closed**             | Update lifecycle complete                       |
| **Blocked**            | Cannot proceed (dependency, resource, etc.)     |
| **Rejected**           | Update not approved |

---

# 12. Priority Definitions (Standard)

| Priority     | Definition                                             | Target Completion SLA |
| ------------ | ------------------------------------------------------ | --------------------- |
| **Critical** | Active gap exposed during incident; regulatory mandate | 7 days                |
| **High**     | Significant operational gap; major new threat          | 30 days               |
| **Medium**   | Refinement based on lessons learned                    | 60 days               |
| **Low**      | Periodic review, minor clarifications                  | 90 days               |

---

# 13. Periodic Review Schedule (Mandatory)

In addition to trigger-based updates, all playbooks must undergo periodic review:

| Playbook Type                             | Review Frequency                    | Owner                           |
| ----------------------------------------- | ----------------------------------- | ------------------------------- |
| Master playbooks (per attack type)        | Annually                            | Playbook Owner + IR Team Lead   |
| Tier-specific playbooks (L1/L2/L3)        | Annually                            | SOC Lead + Tier Lead            |
| Sub-process playbooks (Containment, etc.) | Annually                            | IR Team Lead                    |
| Tool-specific playbooks                   | Annually + on tool upgrade          | Detection Engineer + Tool Owner |
| MITRE mapping playbooks                   | Semi-annually                       | Threat Intel Analyst            |
| Client-specific (MSSP)                    | Per client SLA (typically annually) | MSSP SDM + Client               |

**Periodic review must verify:**

- Current tool versions and procedures reflected
- Threat landscape changes incorporated
- Regulatory requirements current
- Contact information updated
- Links and references valid
- Recent incidents reflected in playbook lessons

---

# 14. Performance Metrics (Mandatory – Quarterly Report)

Track these metrics quarterly:

| Metric                      | Calculation                         | Target |
| --------------------------- | ----------------------------------- | ------ |
| Updates identified          | Count this quarter                  |        |
| Updates completed           | Count completed this quarter        |        |
| Average time-to-completion  | Days from identified to published   |        |
| Overdue updates             | Count past target date              |        |
| Major updates               | Count of major version increments   |        |
| New playbooks created       | Count this quarter                  |        |
| Playbooks retired           | Count retired this quarter          |        |
| Playbooks pending review    | Count overdue for periodic review   |        |
| Training sessions delivered | Count of update-driven training     |        |
| Validation success rate     | % of updates validated successfully |        |

---

# 15. Quality Checklist (Per Update Entry)

Before marking an update as "Closed":

- [ ] Update logged with unique ID
- [ ] Trigger source documented and referenced
- [ ] Impact assessment completed
- [ ] Update reviewed by designated reviewers
- [ ] Approval obtained per workflow
- [ ] Version incremented per standard
- [ ] Previous version archived
- [ ] Updated playbook published to documentation library
- [ ] Stakeholders notified per requirements
- [ ] Training delivered (if required)
- [ ] Training attendance recorded
- [ ] Cascade impact addressed (other playbooks updated)
- [ ] Detection rule alignment verified
- [ ] Linked to source (incident/RCA/LL)
- [ ] Validation planned or completed
- [ ] MSSP: tenant scoping verified (if applicable)

---

# 16. Review Process (Mandatory)

## 16.1 Monthly Review

Playbook Owners review:

- New updates identified
- Status of in-progress updates
- Blocked items requiring escalation
- Overdue items

## 16.2 Quarterly Review

IR Team Lead + SOC Manager review:

- Update completion metrics
- Periodic review compliance
- Training compliance
- Playbook library health
- Strategic gaps identified across multiple incidents

## 16.3 Annual Review

CISO + SOC Manager review:

- Strategic playbook portfolio assessment
- Coverage across attack types and MITRE techniques
- MSSP client playbook portfolio
- Resource needs for playbook maintenance
- Technology investment needs

---

# 17. MSSP Considerations (If Applicable)

For MSSP-managed clients:

- Client-specific playbook updates logged in **tenant-scoped registers**
- Master playbook updates may apply across clients with customization
- Client must approve client-specific playbook changes per SLA
- Client receives quarterly **playbook update summary**
- Client-specific playbooks maintained in client folder
- Cross-client lessons applied to master playbooks (sanitized)
- Notifications to client SOC team coordinated via MSSP SDM
- Training on updated playbooks may be joint MSSP-client sessions

References:
`09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/Client-Specific-Playbook-Guide.md`
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 18. Integration with Other Processes

| Process               | Integration Point                           |
| --------------------- | ------------------------------------------- |
| RCA                   | RCA findings create playbook update entries |
| Lessons Learned       | LL actions for playbooks create entries     |
| Detection Engineering | New detections may require playbook updates |
| Threat Intel          | New TTPs create playbook update entries     |
| Red/Purple Team       | Exercise findings create entries            |
| Tabletop Exercises    | TTX findings create entries                 |
| Tool Upgrades         | New tool features require playbook updates  |
| Compliance Changes    | Regulatory updates create playbook entries  |
| Training Program      | Updated playbooks drive training updates    |

---

# 19. Playbook Library Structure (Reference)

For context, the playbook library is organized as:

```
02_PLAYBOOKS/
├── 02.0_Playbook-Index.md
├── 02.1_Ransomware/
├── 02.2_Phishing-BEC/
├── 02.3_Malware-Trojan/
├── 02.4_DDoS/
├── 02.5_Insider-Threat/
├── 02.6_Data-Breach-Exfiltration/
├── 02.7_Credential-Attack/
├── 02.8_Web-Application-Attack/
├── 02.9_Supply-Chain-Attack/
├── 02.10_Cloud-Security-Incident/
├── 02.11_Network-Intrusion/
├── 02.12_Zero-Day-Exploit/
└── 02.13_APT-Campaign/
```

Reference:
`02_PLAYBOOKS/02.0_Playbook-Index.md`

---

# 20. Related Documents

| Document                       | Path                                                                                    |
| ------------------------------ | --------------------------------------------------------------------------------------- |
| Playbook Index                 | `02_PLAYBOOKS/02.0_Playbook-Index.md`                                                   |
| Detection Improvement Log      | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`               |
| Security Improvement Register  | `08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx`         |
| Control Gap Tracker            | `08_POST-INCIDENT/08.3_Improvement-Tracking/Control-Gap-Tracker.xlsx`                   |
| RCA Template                   | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`                             |
| Lessons Learned Template       | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`                     |
| PIR Meeting Agenda             | `08_POST-INCIDENT/08.1_Lessons-Learned/PIR-Meeting-Agenda.md`                           |
| Action Items Tracker           | `08_POST-INCIDENT/08.1_Lessons-Learned/Action-Items-Tracker.xlsx`                       |
| Client-Specific Playbook Guide | `09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/Client-Specific-Playbook-Guide.md` |
| Tabletop Exercise Guide        | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`          |
| Purple Team Exercise Guide     | `10_TRAINING-AND-EXERCISES/10.3_Drills/Purple-Team-Exercise-Guide.md`                   |
| L1/L2/L3 Onboarding Programs   | `10_TRAINING-AND-EXERCISES/10.1_Onboarding/`                                            |

---

# 21. Revision History

| Version | Date        | Author                     | Changes         |
| ------- | ----------- | -------------------------- | --------------- |
| 1.0     | 30-May-2026 | IR Team Lead / SOC Manager | Initial version |

---

# 22. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**
