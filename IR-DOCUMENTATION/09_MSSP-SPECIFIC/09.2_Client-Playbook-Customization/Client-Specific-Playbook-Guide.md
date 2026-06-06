# Client-Specific Playbook Customization Guide (MSSP)

---

# 1. Document Control

| Field          | Value                                          |
| -------------- | ---------------------------------------------- |
| Document Name  | Guide – Client-Specific Playbook Customization |
| Document ID    | MSSP-PB-001                                    |
| Version        | 1.0                                            |
| Effective Date | 30-May-2026                                    |
| Owner          | MSSP SOC Manager / IR Team Lead                |
| Approved By    | CISO                                           |
| Classification | Confidential – MSSP Internal                   |
| Review Cycle   | Annually                                       |

---

# 2. Purpose

This guide provides the standardized **Client-Specific Playbook Customization** methodology used by the MSSP to develop, maintain, and govern client-tailored incident response playbooks built on top of the MSSP's master playbook library.

A formal client playbook customization guide is critical because:

- standard master playbooks cannot fully address each client's unique environment, regulatory obligations, and operational constraints
- client-specific playbooks ensure correct escalation, containment authority, and regulatory reporting per client
- NIST CSF Respond (RS.RP) function requires response planning aligned to specific environment
- ISO 27001 Annex A.5.24–A.5.27 require structured, contextualized incident management
- RBI Cyber Security Framework expects client-specific reporting timelines and escalation
- multi-tenant MSSP operations require strict tenant segregation in playbook design
- inconsistent customization leads to inconsistent service quality across clients
- audit trail required for client-specific playbook lifecycle
- analysts need clear guidance on when to use master vs client-specific playbooks
- regulatory differences (RBI vs CERT-In vs sector-specific) must be embedded per client
- containment authority varies significantly across clients
- detection rule tuning must align with playbook execution
- playbooks must reflect client-specific tools and integrations

This guide ensures:

- consistent methodology for creating client-specific playbooks
- clear distinction between master and client-specific content
- defined ownership for client playbook maintenance
- audit-ready evidence of client-specific customization
- tenant segregation throughout playbook design and storage
- linkage to client environment profile, IR contacts, and escalation matrix
- standardized folder structure across client playbook libraries
- governance for client review, approval, and version control

Reference alignment:
`02_PLAYBOOKS/02.0_Playbook-Index.md`
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-Environment-Profile-Template.md`
`08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`

---

# 3. Scope

This guide covers customization of:

| Playbook Category         | Customization Scope                       |
| ------------------------- | ----------------------------------------- |
| Attack-specific playbooks | Ransomware, Phishing, Malware, DDoS, etc. |
| Tier-specific playbooks   | L1 Triage, L2 Investigation, L3 Forensics |
| Sub-process playbooks     | Containment, Eradication, Recovery        |
| Regulatory playbooks      | RBI reporting, CERT-In, sector-specific   |
| Tool-specific playbooks   | Client's SIEM, EDR, cloud platforms       |
| Client-unique scenarios   | Custom scenarios per client business      |

Customization triggers:

| Trigger                            | Examples                                 |
| ---------------------------------- | ---------------------------------------- |
| Client onboarding                  | Initial playbook customization           |
| Client environment change          | New tool, new cloud platform, new region |
| Regulatory change affecting client | New RBI circular, sector regulation      |
| Post-incident lessons              | Client-specific learnings                |
| Client request                     | Specific scenarios or procedures         |
| Master playbook update             | Cascade to client playbooks              |
| Tabletop exercise findings         | Client-specific gaps                     |
| Quarterly review                   | Periodic refresh                         |

Out of scope:

- Master playbook content (maintained centrally in `02_PLAYBOOKS/`)
- Generic threat intelligence (covered in TI processes)
- Generic detection rules (covered in detection engineering)

---

# 4. Definitions

| Term                     | Definition                                                                           |
| ------------------------ | ------------------------------------------------------------------------------------ |
| Master Playbook          | MSSP-maintained generic playbook applicable across clients                           |
| Client-Specific Playbook | Customized playbook for specific client environment                                  |
| Customization Layer      | Client-specific overlay on master playbook (escalation, contacts, tools, regulatory) |
| Inheritance              | Client playbook inherits structure/content from master                               |
| Override                 | Client-specific content that supersedes master                                       |
| Extension                | Additional content unique to client (no master equivalent)                           |
| Tenant Folder            | Client-specific folder containing all client playbooks                               |
| Customization Map        | Document mapping master → client-specific deltas                                     |
| Approval Workflow        | Defined approvers for client playbook changes                                        |
| Sync Cadence             | Frequency of cascading master updates to client playbooks                            |

---

# 5. Roles and Responsibilities

| Role                      | Responsibilities                                    |
| ------------------------- | --------------------------------------------------- |
| MSSP SDM                  | Owns client playbook portfolio for assigned clients |
| IR Team Lead              | Validates technical accuracy of client playbooks    |
| SOC Manager               | Approves client playbook customizations             |
| L2/L3 Analysts            | Provide input on operational feasibility            |
| Detection Engineer        | Aligns client detection rules with playbooks        |
| Compliance Lead           | Validates regulatory alignment per client           |
| Threat Intel Analyst      | Provides client-relevant threat context             |
| Master Playbook Owner     | Notifies SDMs of master updates requiring cascade   |
| Client Primary Contact    | Reviews and approves client-specific playbooks      |
| Client Security Lead      | Validates technical accuracy of customizations      |
| Client Compliance Officer | Validates regulatory customizations                 |
| Documentation Custodian   | Maintains client playbook repository structure      |

---

# 6. Customization Principles (Mandatory)

| Principle              | Requirement                                                    |
| ---------------------- | -------------------------------------------------------------- |
| Inheritance first      | Always start from master playbook; never recreate from scratch |
| Delta-based            | Document only client-specific overrides and extensions         |
| Tenant segregation     | Client playbooks strictly isolated by tenant                   |
| Client validation      | Major customizations require client approval                   |
| Version-controlled     | All customizations tracked with version history                |
| Cascade-aware          | Master updates evaluated for cascade to client playbooks       |
| Operationally testable | Customizations validated via tabletop or test                  |
| Audit-ready            | Customization rationale documented                             |
| Confidential           | Client-specific playbooks are Client Restricted                |
| Cross-references valid | Links to client environment profile and contacts maintained    |

---

# 7. Standard Folder Structure (Mandatory)

Each client has a dedicated folder structure within `09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/`:

```
09.2_Client-Playbook-Customization/
├── Client-Specific-Playbook-Guide.md          ← This guide
│
├── [CLIENT-NAME-1]/
│   ├── Client-IR-Policy.md
│   ├── Client-Escalation-Matrix.md
│   └── Client-Custom-Playbooks/
│       ├── PB-Ransomware-[Client].md
│       ├── PB-Phishing-[Client].md
│       ├── PB-DataBreach-[Client].md
│       └── ...
│
├── [CLIENT-NAME-2]/
│   ├── Client-IR-Policy.md
│   ├── Client-Escalation-Matrix.md
│   └── Client-Custom-Playbooks/
│       └── ...
│
└── ...
```

### 7.1 Naming Conventions (Mandatory)

| Item                 | Convention                           | Example                     |
| -------------------- | ------------------------------------ | --------------------------- |
| Client folder        | `[CLIENT-NAME]/` (ALL CAPS, hyphens) | `ABC-BANK/`                 |
| Custom playbook file | `PB-[Type]-[Client].md`              | `PB-Ransomware-ABC-Bank.md` |
| Client IR policy     | `Client-IR-Policy.md`                | (standard)                  |
| Client escalation    | `Client-Escalation-Matrix.md`        | (standard)                  |

---

# 8. Customization Methodology (Mandatory)

## 8.1 Step-by-Step Customization Process

| Step | Activity                                 | Owner                   | Output              |
| ---- | ---------------------------------------- | ----------------------- | ------------------- |
| 1    | Identify master playbook(s) to customize | SDM                     | Customization scope |
| 2    | Review client environment profile        | SDM                     | Context document    |
| 3    | Identify customization areas             | SDM + IR Lead           | Customization map   |
| 4    | Draft client-specific playbook           | SDM                     | Draft playbook      |
| 5    | Internal review (IR Lead, SOC Lead)      | IR Team Lead            | Reviewed draft      |
| 6    | Client review                            | Client Primary Contact  | Client feedback     |
| 7    | Revisions                                | SDM                     | Revised draft       |
| 8    | Approval                                 | SOC Manager + Client    | Approved playbook   |
| 9    | Publication to client tenant folder      | Documentation Custodian | Published playbook  |
| 10   | Analyst briefing                         | SOC Lead                | Briefed team        |
| 11   | Validation via tabletop                  | SOC Lead                | Validation record   |
| 12   | Logging in Playbook Update Log           | SDM                     | Update logged       |

References:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`

---

## 8.2 Customization Areas (Mandatory)

For each client playbook, customize the following areas:

### 8.2.1 Escalation Paths

| Master Content                | Client-Specific Override             |
| ----------------------------- | ------------------------------------ |
| Generic escalation matrix     | Client-specific escalation contacts  |
| Standard severity levels      | Client-aligned severity (if differs) |
| Generic SLAs                  | Client-contracted SLAs               |
| Standard approval authorities | Client-specific approvers            |

### 8.2.2 Containment Authority

| Master Content                       | Client-Specific Override              |
| ------------------------------------ | ------------------------------------- |
| Generic containment authority matrix | Client-approved containment authority |
| Generic auto-response                | Client-approved auto-response rules   |
| Standard approval thresholds         | Client-specific thresholds            |
| Standard tool-based containment      | Client tool-specific commands         |

### 8.2.3 Communication Templates

| Master Content                 | Client-Specific Override           |
| ------------------------------ | ---------------------------------- |
| Generic notification templates | Client-branded/formatted templates |
| Standard distribution lists    | Client-specific stakeholders       |
| Generic bridge call format     | Client-preferred bridge format     |
| Standard status update cadence | Client-agreed cadence              |

### 8.2.4 Regulatory Reporting

| Master Content                | Client-Specific Override                     |
| ----------------------------- | -------------------------------------------- |
| Generic regulatory references | Client-applicable regulations                |
| Standard reporting timelines  | Client-specific timelines (RBI 2-6 hr, etc.) |
| Generic submission methods    | Client's specific regulatory portal/contacts |
| Standard report templates     | Client-specific report formats               |

### 8.2.5 Tool-Specific Procedures

| Master Content           | Client-Specific Override                |
| ------------------------ | --------------------------------------- |
| Generic SIEM queries     | Client SIEM-specific queries            |
| Generic EDR commands     | Client EDR-specific commands            |
| Generic cloud commands   | Client cloud platform-specific commands |
| Generic firewall actions | Client firewall-specific procedures     |

### 8.2.6 Asset and Application Context

| Master Content                 | Client-Specific Override          |
| ------------------------------ | --------------------------------- |
| Generic asset categories       | Client crown jewels               |
| Standard criticality tiers     | Client business impact tiers      |
| Generic application categories | Client critical applications      |
| Standard data classifications  | Client data classification scheme |

### 8.2.7 Operational Context

| Master Content                   | Client-Specific Override           |
| -------------------------------- | ---------------------------------- |
| Standard maintenance windows     | Client maintenance windows         |
| Generic change management        | Client change management process   |
| Standard false positive patterns | Client baseline FP patterns        |
| Generic operational hours        | Client business hours / time zones |

### 8.2.8 Business Continuity

| Master Content               | Client-Specific Override            |
| ---------------------------- | ----------------------------------- |
| Generic RTO/RPO              | Client-specific RTO/RPO             |
| Standard recovery procedures | Client-specific recovery procedures |
| Generic backup verification  | Client backup-specific procedures   |
| Standard DR coordination     | Client DR site coordination         |

---

## 8.3 Customization Map Template (Mandatory)

For each client playbook, document the customization map:

| Section               | Master Playbook                | Client Customization                        | Rationale                   |
| --------------------- | ------------------------------ | ------------------------------------------- | --------------------------- |
| Escalation Matrix     | Generic L1→L2→L3→Mgmt          | Client-specific contacts with phone numbers | Client SLA: 15 min P1 reach |
| Containment Authority | MSSP-decides for EDR isolation | Client approval required for >10 endpoints  | Per client SOW Section 4.2  |
| Regulatory Reporting  | NIST/ISO generic               | RBI 6-hour + CERT-In 6-hour                 | BFSI regulated entity       |
| Tool Commands         | Generic CrowdStrike commands   | Client's specific Falcon tenant URL         | Tenant-specific config      |
| ...                   | ...                            | ...                                         | ...                         |

---

# 9. Client-Specific Playbook Template (Standard Structure)

Each client-specific playbook should follow this structure:

```markdown
# [Playbook Type] – [Client Name]

## 1. Document Control
- Document Name, ID, Version, Owner, Client
- Classification: Client Restricted
- Approved By: SOC Manager + Client representative

## 2. Purpose
- Why this client-specific playbook exists
- Reference to master playbook it customizes

## 3. Scope
- When to use this playbook (client-specific triggers)

## 4. Master Playbook Reference
- Path to master playbook being customized
- Master playbook version this is based on

## 5. Client-Specific Customizations
### 5.1 Escalation Path (Client-Specific)
### 5.2 Containment Authority (Client-Specific)
### 5.3 Communication Templates (Client-Specific)
### 5.4 Regulatory Reporting (Client-Specific)
### 5.5 Tool-Specific Procedures (Client-Specific)
### 5.6 Asset/Application Context (Client-Specific)
### 5.7 Operational Considerations (Client-Specific)

## 6. Procedure
- Step-by-step procedure with client-specific overlays
- Reference master playbook for generic content

## 7. Client-Specific Decision Points
- Decisions requiring client approval
- Authority matrix for this client

## 8. Validation
- How this playbook is validated (tabletop, drill)
- Last validation date

## 9. Related Documents
- Client Environment Profile
- Client IR Contacts
- Client Escalation Matrix
- Master playbook reference
- Client IR Policy

## 10. Revision History
- Version control with client approvals

## 11. Approval
- MSSP approver
- Client approver
```

---

# 10. Master-to-Client Cascade Process (Mandatory)

When master playbooks are updated, evaluate cascade to client playbooks:

| Master Update Type            | Cascade Action                          | Timeline         |
| ----------------------------- | --------------------------------------- | ---------------- |
| **Patch (typo/format)**       | No cascade required                     | N/A              |
| **Minor (refinement)**        | Notify SDMs; selective cascade          | Within 30 days   |
| **Major (structural change)** | Full cascade evaluation per client      | Within 60 days   |
| **New playbook**              | Evaluate per client need                | Within 30 days   |
| **Retirement**                | Notify all SDMs; client playbook update | Within 30 days   |
| **Regulatory change**         | Mandatory cascade if applicable         | Within 7-30 days |
| **Critical incident-driven**  | Mandatory cascade                       | Within 7 days    |

### 10.1 Cascade Decision Tree

```
Master Playbook Updated
        |
        ▼
Is change relevant to client?
        |
   ┌────┴────┐
   ▼         ▼
   No        Yes
   |          |
   Skip      Does client have customization?
              |
         ┌────┴────┐
         ▼         ▼
         No        Yes
         |          |
   Apply directly  Evaluate conflict
                    |
              ┌─────┴─────┐
              ▼           ▼
          No conflict   Conflict exists
              |           |
         Apply update    Reconcile with client
                          |
                    Update client playbook
                          |
                    Get client approval
                          |
                    Publish and log
```

### 10.2 Cascade Tracking

For each master update, log cascade decisions per client:

| Client   | Master Update ID | Cascade Required?   | Cascade Status | Date Completed |
| -------- | ---------------- | ------------------- | -------------- | -------------- |
| Client A | PB-UPD-2026-0042 | Yes                 | Completed      | 2026-06-15     |
| Client B | PB-UPD-2026-0042 | No (not applicable) | N/A            | N/A            |
| Client C | PB-UPD-2026-0042 | Yes                 | In Progress    | -              |

References:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`

---

# 11. Approval Workflow (Mandatory)

| Customization Type                 | Reviewer                             | Approver                          |
| ---------------------------------- | ------------------------------------ | --------------------------------- |
| **Minor formatting/clarification** | SDM                                  | SDM                               |
| **Escalation contact update**      | SDM                                  | SOC Lead                          |
| **SLA/timeline adjustment**        | SDM + IR Lead                        | SOC Manager                       |
| **Containment authority change**   | IR Team Lead + Compliance            | SOC Manager + Client              |
| **Regulatory reporting change**    | Compliance Lead                      | SOC Manager + Client + Compliance |
| **New client-specific playbook**   | IR Team Lead + SOC Lead + Compliance | SOC Manager + CISO + Client       |
| **Master cascade application**     | SDM + IR Team Lead                   | SOC Manager                       |
| **Retirement of client playbook**  | SDM                                  | SOC Manager + Client              |

---

# 12. Versioning Standard (Mandatory)

Client-specific playbooks follow same versioning as master:

| Version Type  | When              | Example     |
| ------------- | ----------------- | ----------- |
| Major (X.0.0) | Structural change | 1.0 → 2.0   |
| Minor (X.Y.0) | Refinement        | 1.0 → 1.1   |
| Patch (X.Y.Z) | Typo/format       | 1.1 → 1.1.1 |

**Initial version:** `v1.0.0`

**Master reference tracking:** Each client playbook header must indicate:

- Based on Master Playbook: `[Path]`
- Master Version: `vX.Y.Z`
- Master Last Sync Date: `YYYY-MM-DD`

---

# 13. Client Validation Requirements (Mandatory)

## 13.1 Required Client Approvals

| Change Type                  | Client Approval Required? |
| ---------------------------- | ------------------------- |
| New client-specific playbook | Yes (written)             |
| Containment authority change | Yes (written)             |
| Escalation path change       | Yes (written)             |
| Regulatory reporting change  | Yes (written)             |
| Tool command updates         | No (notification only)    |
| Cascade of master updates    | Depends on change scope   |
| Asset context updates        | No (notification only)    |
| Minor formatting             | No                        |

## 13.2 Client Review Process

| Step | Action                    | Owner                   | Timeline                  |
| ---- | ------------------------- | ----------------------- | ------------------------- |
| 1    | SDM drafts customization  | SDM                     | Per change scope          |
| 2    | Internal MSSP review      | IR Lead / SOC Manager   | 3-5 days                  |
| 3    | Send to client for review | SDM                     | Day 1 of client review    |
| 4    | Client review period      | Client                  | 5-10 business days        |
| 5    | Client feedback received  | Client                  | Per review period         |
| 6    | Revisions                 | SDM                     | 2-5 days                  |
| 7    | Client final approval     | Client                  | 3-5 days                  |
| 8    | Publication               | Documentation Custodian | Within 2 days of approval |

---

# 14. Tabletop Validation (Mandatory)

All client-specific playbooks should be validated via tabletop exercises:

| Validation Trigger  | Frequency                          |
| ------------------- | ---------------------------------- |
| New client playbook | Within 60 days of publication      |
| Major customization | Within 90 days                     |
| Annual periodic     | All P1/P2 playbooks annually       |
| Post-incident       | Within 60 days of related incident |

References:
`10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`

---

# 15. Tenant Segregation Requirements (Mandatory)

| Requirement              | Implementation                                             |
| ------------------------ | ---------------------------------------------------------- |
| Storage segregation      | Each client in dedicated folder                            |
| Access control           | Per-client RBAC enforced                                   |
| No cross-references      | Client A playbooks must not reference Client B             |
| Sanitization for sharing | Generic learnings sanitized before master playbook updates |
| Repository isolation     | Client playbooks in MSSP secure repository                 |
| Backup segregation       | Tenant-scoped backups                                      |
| Audit logging            | All access to client playbooks logged                      |

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 16. Quality Checklist (Per Client Playbook)

Before publishing a client-specific playbook:

- [ ] Based on identified master playbook
- [ ] Master version referenced in header
- [ ] All mandatory customization areas addressed
- [ ] Customization map documented
- [ ] Client environment profile referenced
- [ ] Client IR contacts referenced
- [ ] Client escalation matrix referenced
- [ ] Client IR policy referenced
- [ ] Tool-specific procedures accurate to client tools
- [ ] Regulatory reporting accurate to client obligations
- [ ] Containment authority per client agreement
- [ ] Communication templates client-appropriate
- [ ] Decision points clearly marked
- [ ] Validation plan defined
- [ ] Reviewed by IR Team Lead
- [ ] Reviewed by Compliance Lead (if regulatory)
- [ ] Approved by SOC Manager
- [ ] Approved by client representative
- [ ] Versioned per standard
- [ ] Stored in correct client folder
- [ ] Access controls applied
- [ ] Logged in Playbook Update Log
- [ ] SOC team briefed
- [ ] Tabletop validation scheduled

---

# 17. Periodic Review (Mandatory)

| Review Type                         | Frequency                       | Owner              |
| ----------------------------------- | ------------------------------- | ------------------ |
| Per-playbook validation             | Annually                        | SDM                |
| Cascade review (post-master update) | Per master update               | SDM                |
| Client portfolio review             | Quarterly                       | SOC Manager + SDM  |
| Regulatory alignment review         | Annually + on regulation change | Compliance Lead    |
| Tool alignment review               | Quarterly                       | Detection Engineer |

---

# 18. MSSP Considerations (Mandatory)

| Aspect                 | Requirement                                                    |
| ---------------------- | -------------------------------------------------------------- |
| Tenant segregation     | Strict; no cross-client visibility for analysts                |
| Cross-client learnings | Sanitized aggregation only; no client identifiers              |
| Common improvements    | Apply to master playbooks for portfolio benefit                |
| Confidentiality        | Client playbooks are Client Restricted                         |
| IP considerations      | Custom playbook IP per contract (typically client-owned)       |
| Knowledge transfer     | Client playbooks transferred at offboarding                    |
| Audit access           | Auditors access only specific client's playbooks with approval |

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-Offboarding-Checklist.md`

---

# 19. Integration with Other Processes

| Process                    | Integration Point                       |
| -------------------------- | --------------------------------------- |
| Master Playbooks           | Source of inheritance                   |
| Client Onboarding          | Initial customization during onboarding |
| Client Offboarding         | Handover or destruction at offboarding  |
| Client Environment Profile | Provides context for customization      |
| Client IR Contacts         | Embedded in escalation customization    |
| Playbook Update Log        | All updates logged                      |
| Detection Engineering      | Detection rules aligned with playbooks  |
| Tabletop Exercises         | Validation mechanism                    |
| RCA / Lessons Learned      | Drive customization updates             |
| Compliance Management      | Regulatory updates drive customization  |

---

# 20. Related Documents

| Document                            | Path                                                                                 |
| ----------------------------------- | ------------------------------------------------------------------------------------ |
| Master Playbook Index               | `02_PLAYBOOKS/02.0_Playbook-Index.md`                                                |
| Client Environment Profile Template | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Environment-Profile-Template.md`     |
| Client IR Contacts                  | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`                      |
| Client Onboarding Checklist         | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Onboarding-Checklist.md`             |
| Client Offboarding Checklist        | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Offboarding-Checklist.md`            |
| Client Data Segregation Policy      | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`    |
| Multi-Client Alert Handling         | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`       |
| Playbook Update Log                 | `08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`                  |
| Detection Improvement Log           | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`            |
| MSSP-Client SLA Template            | `00_GOVERNANCE/00.4_SLA-and-SLO/MSSP-Client-SLA-Template.md`                         |
| MSSP-Client Responsibility Matrix   | `00_GOVERNANCE/00.3_Roles-and-Responsibilities/MSSP-Client-Responsibility-Matrix.md` |
| Tabletop Exercise Guide             | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`       |
| RBI Mandatory Report Template       | `07_REPORTING/07.4_Regulatory-Reports/RBI-Mandatory-Report-Template.md`              |

---

# 21. Revision History

| Version | Date        | Author                          | Changes         |
| ------- | ----------- | ------------------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP SOC Manager / IR Team Lead | Initial version |

---

# 22. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**
