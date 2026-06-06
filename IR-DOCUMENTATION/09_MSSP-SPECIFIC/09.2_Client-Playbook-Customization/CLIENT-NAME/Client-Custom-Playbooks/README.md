# Client Custom Playbooks – README

---

# 1. Document Control

| Field                | Value                                                     |
| -------------------- | --------------------------------------------------------- |
| Document Name        | README – Client Custom Playbooks                          |
| Document ID          | MSSP-CL-PB-README-[CLIENT-ID]                             |
| Version              | 1.0                                                       |
| Effective Date       | `[YYYY-MM-DD]`                                            |
| Client Name          | `[CLIENT-NAME]`                                           |
| Client ID            | `CL-####`                                                 |
| Owner (MSSP)         | MSSP SDM / IR Team Lead                                   |
| Owner (Client)       | Client CISO / Security Lead                               |
| Approved By (MSSP)   | MSSP SOC Manager                                          |
| Approved By (Client) | Client CISO                                               |
| Classification       | Confidential – Client Restricted                          |
| Review Cycle         | Annually (or upon playbook addition / significant change) |

---

# 2. Purpose

This **README** document defines the structure, naming standards, contents, and governance of the `Client-Custom-Playbooks/` folder for `[CLIENT-NAME]`. It serves as the authoritative index and operational guide for all client-specific playbooks customized from the MSSP's master playbook library.

A formal README for client custom playbooks is critical because:

- multiple client-specific playbooks must be discoverable and consistently structured
- SOC analysts need a single entry point to locate the correct playbook during incident response
- audit and compliance reviews require evidence of organized, governed playbook libraries
- NIST CSF Respond (RS.RP) function requires planned response with discoverable artifacts
- ISO 27001 Annex A.5.24 requires structured response planning
- RBI Cyber Security Framework expects mature, current incident handling procedures
- inconsistent organization across clients increases analyst onboarding time and error risk
- new playbook additions must follow standardized creation, review, and approval workflow
- versioning, master-cascade tracking, and validation records must be visible
- multi-tenant MSSP operations require strict tenant segregation evidence
- post-incident reviews and lessons learned drive new playbook additions
- regulatory and threat landscape changes drive playbook lifecycle activity

This README ensures:

- consistent folder organization across all client custom playbook libraries
- standardized naming for all playbook files
- discoverable index of all playbooks with status and version
- defined ownership for each playbook
- audit-ready evidence of playbook governance
- linkage to Client IR Policy, Escalation Matrix, and Client-Specific Playbook Guide
- governance for adding, updating, and retiring playbooks
- tenant segregation maintained throughout

Reference alignment:
`09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/Client-Specific-Playbook-Guide.md`
`09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/[CLIENT-NAME]/Client-IR-Policy.md`
`09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/[CLIENT-NAME]/Client-Escalation-Matrix.md`
`02_PLAYBOOKS/02.0_Playbook-Index.md`

---

# 3. Scope

This README covers:

| Scope Element           | Coverage                                       |
| ----------------------- | ---------------------------------------------- |
| Folder structure        | Standard structure for client custom playbooks |
| Naming conventions      | File naming standards                          |
| Playbook inventory      | Index of all client custom playbooks           |
| Master playbook mapping | Each custom playbook mapped to source master   |
| Versioning              | Version tracking per playbook                  |
| Status tracking         | Lifecycle status per playbook                  |
| Approval workflow       | Review and approval per playbook               |
| Cascade tracking        | Master update cascade status                   |
| Access control          | Per-client RBAC enforcement                    |
| Audit evidence          | Documentation of governance activities         |

Out of scope:

- Individual playbook content (in each respective playbook file)
- Master playbook content (in `02_PLAYBOOKS/`)
- Generic customization methodology (in `Client-Specific-Playbook-Guide.md`)

---

# 4. Folder Structure (Standard – Mandatory)

```
[CLIENT-NAME]/
└── Client-Custom-Playbooks/
    ├── README.md                                    ← This file
    │
    ├── 01_Attack-Specific/                          ← Per-attack playbooks
    │   ├── PB-Ransomware-[CLIENT].md
    │   ├── PB-Phishing-[CLIENT].md
    │   ├── PB-Malware-[CLIENT].md
    │   ├── PB-DDoS-[CLIENT].md
    │   ├── PB-Insider-Threat-[CLIENT].md
    │   ├── PB-DataBreach-[CLIENT].md
    │   ├── PB-Credential-Attack-[CLIENT].md
    │   ├── PB-WebApp-[CLIENT].md
    │   ├── PB-Supply-Chain-[CLIENT].md
    │   ├── PB-Cloud-[CLIENT].md
    │   ├── PB-Network-Intrusion-[CLIENT].md
    │   ├── PB-Zero-Day-[CLIENT].md
    │   └── PB-APT-[CLIENT].md
    │
    ├── 02_Tier-Specific/                            ← L1/L2/L3 customizations (if needed)
    │   ├── PB-L1-Triage-[CLIENT].md
    │   ├── PB-L2-Investigation-[CLIENT].md
    │   └── PB-L3-Forensics-[CLIENT].md
    │
    ├── 03_Sub-Process/                              ← Containment, Eradication, Recovery
    │   ├── PB-Containment-[CLIENT].md
    │   ├── PB-Eradication-[CLIENT].md
    │   └── PB-Recovery-[CLIENT].md
    │
    ├── 04_Regulatory/                               ← Client regulatory playbooks
    │   ├── PB-RBI-Reporting-[CLIENT].md
    │   ├── PB-CERTIn-Reporting-[CLIENT].md
    │   ├── PB-DPDP-Breach-Notification-[CLIENT].md
    │   └── PB-Sector-Specific-[CLIENT].md
    │
    ├── 05_Tool-Specific/                            ← Client tool-specific procedures
    │   ├── PB-SIEM-[ClientSIEM]-[CLIENT].md
    │   ├── PB-EDR-[ClientEDR]-[CLIENT].md
    │   ├── PB-Cloud-AWS-[CLIENT].md
    │   ├── PB-Cloud-Azure-[CLIENT].md
    │   └── PB-Cloud-GCP-[CLIENT].md
    │
    ├── 06_Client-Unique/                            ← Custom scenarios unique to client
    │   ├── PB-[ClientUniqueScenario1]-[CLIENT].md
    │   └── PB-[ClientUniqueScenario2]-[CLIENT].md
    │
    └── 99_Archive/                                  ← Retired playbooks
        └── [Retired playbooks with retirement date]
```

### 4.1 Subfolder Purpose

| Subfolder             | Purpose                                                  |
| --------------------- | -------------------------------------------------------- |
| `01_Attack-Specific/` | Per-attack-type playbooks (most common)                  |
| `02_Tier-Specific/`   | Client-specific tier procedures (if differs from master) |
| `03_Sub-Process/`     | Containment/Eradication/Recovery procedures              |
| `04_Regulatory/`      | Regulatory reporting procedures per client obligations   |
| `05_Tool-Specific/`   | Client tool-specific procedures                          |
| `06_Client-Unique/`   | Scenarios with no master playbook equivalent             |
| `99_Archive/`         | Retired/superseded playbooks (retained for audit)        |

---

# 5. Naming Conventions (Mandatory)

| Item                     | Convention                              | Example                                      |
| ------------------------ | --------------------------------------- | -------------------------------------------- |
| Standard custom playbook | `PB-[Type]-[CLIENT].md`                 | `PB-Ransomware-ABC-Bank.md`                  |
| Tier-specific            | `PB-[Tier]-[Type]-[CLIENT].md`          | `PB-L2-Investigation-ABC-Bank.md`            |
| Tool-specific            | `PB-[Tool]-[CLIENT].md`                 | `PB-SIEM-Splunk-ABC-Bank.md`                 |
| Regulatory               | `PB-[Regulation]-[CLIENT].md`           | `PB-RBI-Reporting-ABC-Bank.md`               |
| Client-unique            | `PB-[ScenarioName]-[CLIENT].md`         | `PB-CoreBanking-Outage-ABC-Bank.md`          |
| Retired                  | `[Original Name]_RETIRED_[YYYYMMDD].md` | `PB-Ransomware-ABC-Bank_RETIRED_20260101.md` |

### 5.1 CLIENT Identifier Standard

- Use **client short name** (no spaces, hyphens allowed)
- Use **ALL CAPS** or **PascalCase** consistently
- Match the folder name: `[CLIENT-NAME]`
- Example: `ABC-Bank`, `XYZ-Healthcare`, `Acme-Corp`

---

# 6. Standard Playbook Header (Mandatory)

Every client custom playbook must begin with this standardized header:

```markdown
# [Playbook Type] – [CLIENT-NAME]

## Document Control

| Field | Value |
| --- | --- |
| Document Name | [Playbook Type] – [CLIENT-NAME] |
| Document ID | MSSP-CL-PB-[CLIENT-ID]-[####] |
| Version | v1.0.0 |
| Effective Date | YYYY-MM-DD |
| Based on Master Playbook | [Path to master] |
| Master Version | vX.Y.Z |
| Master Last Sync Date | YYYY-MM-DD |
| Client Name | [CLIENT-NAME] |
| Client ID | CL-#### |
| Owner (MSSP) | MSSP SDM |
| Owner (Client) | Client Security Lead |
| Approved By (MSSP) | MSSP SOC Manager |
| Approved By (Client) | Client CISO |
| Classification | Confidential – Client Restricted |
| Review Cycle | Annually |
```

---

# 7. Playbook Inventory (Mandatory – Update on Add/Remove/Update)

> Maintain this table as the authoritative index for `[CLIENT-NAME]`.

## 7.1 Attack-Specific Playbooks

| #   | Playbook File                      | Master Playbook Source                                               | Custom Version | Master Version | Status | Last Updated | Last Validated | Owner |
| --- | ---------------------------------- | -------------------------------------------------------------------- | -------------- | -------------- | ------ | ------------ | -------------- | ----- |
| 1   | `PB-Ransomware-[CLIENT].md`        | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Master.md`               | v1.0.0         | vX.Y.Z         | Active |              |                |       |
| 2   | `PB-Phishing-[CLIENT].md`          | `02_PLAYBOOKS/02.2_Phishing-BEC/PB-Phishing-Master.md`               |                |                |        |              |                |       |
| 3   | `PB-Malware-[CLIENT].md`           | `02_PLAYBOOKS/02.3_Malware-Trojan/PB-Malware-Master.md`              |                |                |        |              |                |       |
| 4   | `PB-DDoS-[CLIENT].md`              | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-Master.md`                           |                |                |        |              |                |       |
| 5   | `PB-Insider-Threat-[CLIENT].md`    | `02_PLAYBOOKS/02.5_Insider-Threat/PB-Insider-Threat-Master.md`       |                |                |        |              |                |       |
| 6   | `PB-DataBreach-[CLIENT].md`        | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Master.md` |                |                |        |              |                |       |
| 7   | `PB-Credential-Attack-[CLIENT].md` | `02_PLAYBOOKS/02.7_Credential-Attack/PB-CredentialAttack-Master.md`  |                |                |        |              |                |       |
| 8   | `PB-WebApp-[CLIENT].md`            | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-Master.md`       |                |                |        |              |                |       |
| 9   | `PB-Supply-Chain-[CLIENT].md`      | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-Master.md`     |                |                |        |              |                |       |
| 10  | `PB-Cloud-[CLIENT].md`             | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/PB-Cloud-Master.md`      |                |                |        |              |                |       |
| 11  | `PB-Network-Intrusion-[CLIENT].md` | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-Master.md` |                |                |        |              |                |       |
| 12  | `PB-Zero-Day-[CLIENT].md`          | `02_PLAYBOOKS/02.12_Zero-Day-Exploit/PB-ZeroDay-Master.md`           |                |                |        |              |                |       |
| 13  | `PB-APT-[CLIENT].md`               | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-Master.md`                   |                |                |        |              |                |       |

## 7.2 Tier-Specific Playbooks (Only if Differs from Master)

| #   | Playbook File                     | Master Source                                                            | Status | Owner |
| --- | --------------------------------- | ------------------------------------------------------------------------ | ------ | ----- |
| 1   | `PB-L1-Triage-[CLIENT].md`        | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Alert-Handling-SOP.md`     |        |       |
| 2   | `PB-L2-Investigation-[CLIENT].md` | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Investigation-SOP.md`      |        |       |
| 3   | `PB-L3-Forensics-[CLIENT].md`     | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Advanced-Forensics-SOP.md` |        |       |

## 7.3 Sub-Process Playbooks

| #   | Playbook File                | Master Source                                   | Status | Owner |
| --- | ---------------------------- | ----------------------------------------------- | ------ | ----- |
| 1   | `PB-Containment-[CLIENT].md` | Per attack-specific master containment sections |        |       |
| 2   | `PB-Eradication-[CLIENT].md` | Per attack-specific master eradication sections |        |       |
| 3   | `PB-Recovery-[CLIENT].md`    | Per attack-specific master recovery sections    |        |       |

## 7.4 Regulatory Playbooks

| #   | Playbook File                             | Master Source                                                                            | Status | Owner |
| --- | ----------------------------------------- | ---------------------------------------------------------------------------------------- | ------ | ----- |
| 1   | `PB-RBI-Reporting-[CLIENT].md`            | `07_REPORTING/07.4_Regulatory-Reports/RBI-Mandatory-Report-Template.md`                  |        |       |
| 2   | `PB-CERTIn-Reporting-[CLIENT].md`         | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md` |        |       |
| 3   | `PB-DPDP-Breach-Notification-[CLIENT].md` | N/A (client-specific)                                                                    |        |       |
| 4   | `PB-Sector-Specific-[CLIENT].md`          | Per applicable sector (SEBI/IRDAI/etc.)                                                  |        |       |

## 7.5 Tool-Specific Playbooks

| #   | Playbook File                      | Tool        | Status | Owner |
| --- | ---------------------------------- | ----------- | ------ | ----- |
| 1   | `PB-SIEM-[ClientSIEM]-[CLIENT].md` | Client SIEM |        |       |
| 2   | `PB-EDR-[ClientEDR]-[CLIENT].md`   | Client EDR  |        |       |
| 3   | `PB-Cloud-AWS-[CLIENT].md`         | AWS         |        |       |
| 4   | `PB-Cloud-Azure-[CLIENT].md`       | Azure       |        |       |
| 5   | `PB-Cloud-GCP-[CLIENT].md`         | GCP         |        |       |

## 7.6 Client-Unique Playbooks (No Master Equivalent)

| #   | Playbook File               | Scenario        | Status | Owner |
| --- | --------------------------- | --------------- | ------ | ----- |
| 1   | `PB-[Scenario]-[CLIENT].md` | `[Description]` |        |       |

## 7.7 Archived Playbooks

| #   | Playbook File | Retirement Date | Replaced By | Reason |
| --- | ------------- | --------------- | ----------- | ------ |
|     |               |                 |             |        |

---

# 8. Status Definitions (Standard)

| Status              | Definition                                             |
| ------------------- | ------------------------------------------------------ |
| **Draft**           | Under development, not yet reviewed                    |
| **In Review**       | Under internal MSSP review                             |
| **Client Review**   | Sent to client for review/approval                     |
| **Approved**        | Approved by both MSSP and client; awaiting publication |
| **Active**          | Live and in use                                        |
| **Tuning**          | Active but undergoing refinement                       |
| **Cascade Pending** | Awaiting cascade of master playbook update             |
| **Under Revision**  | Active version exists but update in progress           |
| **Retired**         | No longer in use; archived                             |

---

# 9. Playbook Lifecycle (Mandatory)

| Phase                   | Activities                                               | Owner                         | Timeline           |
| ----------------------- | -------------------------------------------------------- | ----------------------------- | ------------------ |
| **1. Identification**   | Need identified (onboarding/incident/regulation/request) | SDM / IR Lead                 | On trigger         |
| **2. Scoping**          | Customization scope defined                              | SDM                           | Within 7 days      |
| **3. Drafting**         | Playbook drafted from master                             | SDM / Detection Eng           | Per complexity     |
| **4. Internal Review**  | MSSP review (IR Lead, SOC Lead, Compliance)              | IR Team Lead                  | 3-5 days           |
| **5. Client Review**    | Sent to client for review                                | SDM                           | 5-10 business days |
| **6. Revision**         | Updates per feedback                                     | SDM                           | 2-5 days           |
| **7. Client Approval**  | Final client sign-off                                    | Client CISO                   | 3-5 days           |
| **8. MSSP Approval**    | Final MSSP sign-off                                      | SOC Manager                   | 1-2 days           |
| **9. Publication**      | Published to client folder                               | Documentation Custodian       | 1-2 days           |
| **10. Briefing**        | SOC team briefed                                         | SOC Lead                      | Within 7 days      |
| **11. Validation**      | Tabletop / drill validation                              | SOC Lead                      | Within 60-90 days  |
| **12. Logging**         | Logged in Playbook Update Log                            | SDM                           | At publication     |
| **13. Periodic Review** | Annual review                                            | SDM                           | Annually           |
| **14. Retirement**      | Archive when superseded                                  | SDM + Documentation Custodian | On retirement      |

References:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`

---

# 10. Approval Workflow (Mandatory)

| Change Type                   | MSSP Reviewer                        | MSSP Approver      | Client Approver             |
| ----------------------------- | ------------------------------------ | ------------------ | --------------------------- |
| **New playbook**              | IR Team Lead + SOC Lead + Compliance | SOC Manager + CISO | Client CISO                 |
| **Major update (structural)** | IR Team Lead + SOC Lead              | SOC Manager        | Client Security Lead + CISO |
| **Minor update (refinement)** | IR Team Lead                         | SOC Lead           | Client Primary Contact      |
| **Patch (typo/format)**       | SDM                                  | SDM                | Notification only           |
| **Cascade from master**       | IR Team Lead                         | SOC Manager        | Per change scope            |
| **Retirement**                | IR Team Lead + SOC Lead              | SOC Manager        | Client CISO                 |

References:
`09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/Client-Specific-Playbook-Guide.md`

---

# 11. Versioning Standard (Mandatory)

| Version Type      | When to Use                         | Example       |
| ----------------- | ----------------------------------- | ------------- |
| **Major (X.0.0)** | Structural change, complete rewrite | 1.0.0 → 2.0.0 |
| **Minor (X.Y.0)** | New section, refinement             | 1.0.0 → 1.1.0 |
| **Patch (X.Y.Z)** | Typo, format, link fix              | 1.1.0 → 1.1.1 |

**Initial Version:** `v1.0.0`

**Master Reference Tracking:** Every playbook header must indicate:

- Based on Master Playbook (path)
- Master Version
- Master Last Sync Date

---

# 12. Cascade Tracking (Mandatory)

When master playbooks are updated, evaluate cascade per playbook:

| Master Playbook Updated | Date Master Updated | Client Playbooks Affected | Cascade Decision         | Cascade Completed Date |
| ----------------------- | ------------------- | ------------------------- | ------------------------ | ---------------------- |
|                         |                     |                           | Apply / Skip / Reconcile |                        |

References:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`

---

# 13. Validation Tracking (Mandatory)

Each playbook must be validated periodically:

| Playbook | Last Validation | Validation Method                | Outcome               | Next Validation Due |
| -------- | --------------- | -------------------------------- | --------------------- | ------------------- |
|          |                 | Tabletop / Drill / Real Incident | Pass / Partial / Fail |                     |

Validation requirements:

| Playbook Category    | Validation Frequency | Method                            |
| -------------------- | -------------------- | --------------------------------- |
| P1 attack playbooks  | Annually             | Tabletop                          |
| P2 attack playbooks  | Annually             | Tabletop or drill                 |
| Regulatory playbooks | Annually             | Tabletop with regulatory scenario |
| Tool-specific        | On tool upgrade      | Drill                             |
| Client-unique        | Annually             | Tabletop                          |

References:
`10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`

---

# 14. Access Control (Mandatory)

| Audience                            | Access Level                        |
| ----------------------------------- | ----------------------------------- |
| Assigned SDM                        | Full read/write                     |
| Assigned SOC team (per client)      | Full read                           |
| IR Team Lead                        | Full read                           |
| SOC Manager                         | Full read/write                     |
| Detection Engineer (assigned)       | Read for alignment                  |
| MSSP CISO                           | Full read                           |
| Other clients                       | NO ACCESS                           |
| Other MSSP SOC teams (not assigned) | NO ACCESS                           |
| Third parties                       | NO ACCESS (without client approval) |
| Client SOC (if co-managed)          | Full read for their playbooks       |
| Auditors                            | Read with client approval           |

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 15. Quick Reference – How to Use This Folder (For Analysts)

## 15.1 During an Incident

1. **Identify incident type** → Triage and severity
2. **Open this README** → Locate relevant playbook in inventory (Section 7)
3. **Open the specific playbook** → Follow client-specific procedures
4. **Cross-reference**:
   - `Client-IR-Policy.md` for governance
   - `Client-Escalation-Matrix.md` for escalation
   - `Client-Environment-Profile-Template.md` for context
   - `Client-IR-Contacts.md` for contacts
5. **Log all actions** in the ticket
6. **Escalate per matrix** when criteria met

## 15.2 When Adding a New Playbook

1. Identify the master playbook source
2. Follow process in `Client-Specific-Playbook-Guide.md`
3. Use standard header template (Section 6)
4. Follow naming convention (Section 5)
5. Place in appropriate subfolder (Section 4)
6. Update this README inventory (Section 7)
7. Log in Playbook Update Log
8. Brief SOC team
9. Schedule validation

## 15.3 When Updating a Playbook

1. Increment version per standard (Section 11)
2. Update master sync date in header
3. Update this README inventory (Section 7)
4. Document changes in playbook revision history
5. Get appropriate approval per workflow (Section 10)
6. Notify SOC team
7. Log in Playbook Update Log

## 15.4 When Retiring a Playbook

1. Identify replacement (if any)
2. Get retirement approval
3. Move file to `99_Archive/` with retirement-date suffix
4. Update this README inventory (move to Section 7.7)
5. Notify SOC team
6. Log in Playbook Update Log

---

# 16. Quality Checklist (Per Playbook Added)

Before adding a new playbook to the inventory:

- [ ] Follows standard naming convention
- [ ] Placed in correct subfolder
- [ ] Uses standard header template
- [ ] Master playbook source identified
- [ ] Master version referenced
- [ ] Customization map documented
- [ ] Escalation aligned with `Client-Escalation-Matrix.md`
- [ ] Containment authority aligned with `Client-IR-Policy.md`
- [ ] Tool commands accurate to client tools
- [ ] Regulatory steps accurate per client obligations
- [ ] Contact references valid
- [ ] Reviewed by IR Team Lead
- [ ] Reviewed by Compliance (if regulatory)
- [ ] Approved by SOC Manager
- [ ] Approved by client
- [ ] Versioned per standard
- [ ] Added to README inventory (Section 7)
- [ ] Logged in Playbook Update Log
- [ ] SOC team briefed
- [ ] Validation scheduled
- [ ] Tenant segregation verified

---

# 17. MSSP Considerations (Mandatory)

| Aspect                 | Requirement                                              |
| ---------------------- | -------------------------------------------------------- |
| Tenant segregation     | Strict; no cross-client references                       |
| Cross-client learnings | Sanitized only; applied to master playbooks              |
| Confidentiality        | Client Restricted classification                         |
| Storage                | MSSP secure repository, tenant-scoped                    |
| Backups                | Tenant-scoped backups                                    |
| Access logging         | All access logged for audit                              |
| IP considerations      | Per contract (typically client-owned for custom content) |
| Offboarding            | All playbooks handover per offboarding plan              |

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-Offboarding-Checklist.md`

---

# 18. Integration with Other Processes

| Process                 | Integration                                   |
| ----------------------- | --------------------------------------------- |
| Client Onboarding       | Initial playbook creation during onboarding   |
| Client Offboarding      | Playbooks transferred/archived at offboarding |
| Incident Response       | Playbooks used during all incidents           |
| RCA / Lessons Learned   | Drives playbook updates                       |
| Master Playbook Updates | Cascade evaluation per playbook               |
| Detection Engineering   | Detections aligned with playbooks             |
| Tabletop Exercises      | Validates playbooks                           |
| Audit / Compliance      | Evidence of governed playbook library         |
| Steering Committee      | Playbook portfolio reviewed quarterly         |

---

# 19. Periodic Review (Mandatory)

| Review Type                  | Frequency             | Owner                      |
| ---------------------------- | --------------------- | -------------------------- |
| Inventory accuracy review    | Monthly               | SDM                        |
| Per-playbook annual review   | Annually per playbook | SDM + IR Lead              |
| Cascade backlog review       | Per master update     | SDM                        |
| Validation compliance review | Quarterly             | SOC Manager + SDM          |
| Quarterly portfolio review   | Quarterly             | SOC Manager + SDM + Client |
| Annual strategic review      | Annually              | CISO + Client CISO         |

---

# 20. Related Documents

| Document                       | Path                                                                                            |
| ------------------------------ | ----------------------------------------------------------------------------------------------- |
| Client-Specific Playbook Guide | `09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/Client-Specific-Playbook-Guide.md`         |
| Client IR Policy               | `09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/[CLIENT-NAME]/Client-IR-Policy.md`         |
| Client Escalation Matrix       | `09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/[CLIENT-NAME]/Client-Escalation-Matrix.md` |
| Client Environment Profile     | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Environment-Profile-Template.md`                |
| Client IR Contacts             | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`                                 |
| Client Onboarding Checklist    | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Onboarding-Checklist.md`                        |
| Client Offboarding Checklist   | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Offboarding-Checklist.md`                       |
| Client Data Segregation Policy | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`               |
| Master Playbook Index          | `02_PLAYBOOKS/02.0_Playbook-Index.md`                                                           |
| Playbook Update Log            | `08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`                             |
| Detection Improvement Log      | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`                       |
| Tabletop Exercise Guide        | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`                  |
| MSSP-Client SLA Template       | `00_GOVERNANCE/00.4_SLA-and-SLO/MSSP-Client-SLA-Template.md`                                    |
| RBI Mandatory Report Template  | `07_REPORTING/07.4_Regulatory-Reports/RBI-Mandatory-Report-Template.md`                         |
| CERT-In Reporting SOP          | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`        |

---

# 21. Revision History

| Version | Date           | Author                  | Changes         |
| ------- | -------------- | ----------------------- | --------------- |
| 1.0     | `[YYYY-MM-DD]` | MSSP SDM / IR Team Lead | Initial version |

---

# 22. Approval

**Approved by (MSSP):**

| Role             | Name | Signature | Date |
| ---------------- | ---- | --------- | ---- |
| MSSP SDM         |      |           |      |
| MSSP SOC Manager |      |           |      |

**Approved by (Client):**

| Role                   | Name | Signature | Date |
| ---------------------- | ---- | --------- | ---- |
| Client Primary Contact |      |           |      |
| Client CISO            |      |           |      |

---

**End of Document**
