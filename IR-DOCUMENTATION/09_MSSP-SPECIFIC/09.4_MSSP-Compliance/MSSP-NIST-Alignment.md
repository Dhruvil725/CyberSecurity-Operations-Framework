# MSSP NIST Cybersecurity Framework 2.0 Alignment

---

# 1. Document Control

| Field          | Value                                    |
| -------------- | ---------------------------------------- |
| Document Name  | MSSP – NIST CSF 2.0 Alignment            |
| Document ID    | MSSP-CMP-002                             |
| Version        | 1.0                                      |
| Effective Date | 30-May-2026                              |
| Owner          | MSSP Compliance Lead / CISO              |
| Approved By    | MSSP CISO                                |
| Classification | Confidential – MSSP Internal             |
| Review Cycle   | Annually (or upon NIST framework update) |

---

# 2. Purpose

This document defines how the MSSP's Incident Response (IR) program and Security Operations Center (SOC) operations align with the **NIST Cybersecurity Framework (CSF) 2.0**, **NIST SP 800-61 Rev.2/Rev.3 (Computer Security Incident Handling Guide)**, and **NIST SP 800-53 Rev.5 (Security and Privacy Controls)** — providing structured, standards-based evidence of cybersecurity program maturity across the MSSP multi-tenant environment.

A formal NIST alignment document is critical because:

- NIST CSF 2.0 is the de facto global cybersecurity framework adopted by enterprises and regulators
- the MSSP serves clients who require NIST-aligned service providers (especially US-based, BFSI, critical infrastructure)
- NIST CSF 2.0 introduces the new **GOVERN** function which is foundational for MSSP service delivery
- client vendor risk assessments increasingly require NIST CSF self-assessments
- US Federal clients (FedRAMP, FISMA, DoD) require NIST SP 800-53 control alignment
- NIST SP 800-61 defines the global standard for incident handling lifecycle
- the MSSP multi-tenant architecture creates unique NIST control implementation considerations
- NIST profiles allow tiered maturity demonstration (Partial → Risk Informed → Repeatable → Adaptive)
- continuous improvement of NIST function maturity drives MSSP service excellence
- NIST mapping is widely cross-referenced to ISO 27001, SOC 2, CIS Controls, RBI, and other frameworks
- threat intelligence sharing, detection engineering, and response require NIST-aligned governance
- client procurement and audits demand demonstrable NIST function coverage
- MSSP personnel must understand which NIST functions/categories govern their daily operations
- detection engineering, playbook updates, and lessons learned must feed NIST function improvement
- this alignment is the single source of truth for NIST audit and assessment evidence
- without structured alignment, MSSP cannot demonstrate maturity progression to clients/regulators

This alignment ensures:

- complete mapping of NIST CSF 2.0 functions, categories, and subcategories to MSSP implementations
- alignment with NIST SP 800-61 incident handling lifecycle phases
- mapping to NIST SP 800-53 control families for federal/regulated clients
- defined maturity tier per function (current state + target state)
- per-function ownership and review cycles
- multi-tenant specific NIST implementation considerations documented
- audit-ready evidence for internal and external assessments
- continuous improvement loop tied to function maturity progression
- linkage to ISO 27001, RBI, SOC 2, DPDP, and other framework mappings

**Reference alignment:**

- `00_GOVERNANCE/00.1_Policies/IR-Policy-NIST-Alignment.md`
- `00_GOVERNANCE/00.2_Frameworks-Mapping/NIST-CSF-Control-Mapping.xlsx`
- `09_MSSP-SPECIFIC/09.4_MSSP-Compliance/MSSP-ISO27001-Controls.md`
- `09_MSSP-SPECIFIC/09.4_MSSP-Compliance/MSSP-Audit-Readiness-Checklist.md`

---

# 3. Scope

This document covers NIST framework alignment across all MSSP operations:

| Scope Element                    | Coverage                                                                                        |
| -------------------------------- | ----------------------------------------------------------------------------------------------- |
| NIST CSF 2.0 functions           | All 6 functions (GOVERN, IDENTIFY, PROTECT, DETECT, RESPOND, RECOVER)                           |
| NIST CSF 2.0 categories          | All categories under each function                                                              |
| NIST CSF 2.0 subcategories       | All subcategories with implementation evidence                                                  |
| NIST SP 800-61 lifecycle         | All 4 phases (Preparation, Detection/Analysis, Containment/Eradication/Recovery, Post-Incident) |
| NIST SP 800-53 control families  | All applicable families (especially IR, AU, SI, CP, RA)                                         |
| MSSP SOC operations              | 24x7 monitoring, IR, threat hunting                                                             |
| MSSP multi-tenant infrastructure | All client environments                                                                         |
| MSSP personnel                   | All SOC, IR, compliance, support staff                                                          |
| MSSP technology stack            | SIEM, EDR, SOAR, TI, ticketing, forensics                                                       |
| Maturity tiers                   | Current + target per function                                                                   |
| Client-facing services           | All MSSP service tiers                                                                          |

Out of scope:

- Client-internal NIST compliance (client's responsibility)
- NIST SP 800-171 (CUI handling) detailed mapping (separate document if applicable)
- NIST AI RMF detailed mapping (separate document)
- NIST Privacy Framework detailed mapping (separate document)
- Detailed federal compliance (FedRAMP/FISMA) procedures (covered by separate program docs)

---

# 4. Definitions

| Term                     | Definition                                                    |
| ------------------------ | ------------------------------------------------------------- |
| NIST CSF                 | NIST Cybersecurity Framework                                  |
| CSF 2.0                  | Version 2.0 released 2024 with new GOVERN function            |
| Function                 | Top-level CSF organizing structure (GV, ID, PR, DE, RS, RC)   |
| Category                 | Subdivision of a function                                     |
| Subcategory              | Specific cybersecurity outcomes                               |
| Profile                  | Selection of subcategories representing current/target state  |
| Implementation Tier      | Maturity level (Partial, Risk Informed, Repeatable, Adaptive) |
| Informative References   | Mappings to other standards (ISO, SP 800-53, etc.)            |
| SP 800-61                | Incident handling guide                                       |
| SP 800-53                | Security and privacy controls catalog                         |
| Current Profile          | As-is implementation state                                    |
| Target Profile           | To-be desired implementation state                            |
| Gap                      | Difference between current and target profile                 |
| Multi-Tenant Subcategory | Subcategory with specific multi-tenant implementation         |

---

# 5. Roles and Responsibilities

| Role                         | Responsibilities                                                      |
| ---------------------------- | --------------------------------------------------------------------- |
| **MSSP CISO**                | NIST program owner; maturity tier targets; profile approval           |
| **MSSP Compliance Lead**     | NIST program management; assessment coordination; mapping maintenance |
| **MSSP SOC Manager**         | Operational NIST functions (DE, RS); SOC evidence                     |
| **MSSP IR Team Lead**        | Incident response NIST function (RS, RC); IR evidence                 |
| **MSSP Detection Engineer**  | Detection NIST function (DE); detection evidence                      |
| **MSSP Threat Intel Lead**   | Identify/Detect support (TI categories); intel evidence               |
| **MSSP IT/Platform Lead**    | Protect NIST function (PR); technical evidence                        |
| **MSSP HR Lead**             | People-related subcategories; training evidence                       |
| **MSSP Legal Counsel**       | Govern function; legal/regulatory alignment                           |
| **Function Owners**          | Per-function accountability                                           |
| **Subcategory Implementers** | Daily subcategory execution                                           |
| **External Assessors**       | NIST CSF maturity assessments                                         |

---

# 6. NIST CSF 2.0 Structure Overview (Mandatory)

NIST CSF 2.0 consists of **6 Functions**:

| Function     | Code | Purpose                                                                                              |
| ------------ | ---- | ---------------------------------------------------------------------------------------------------- |
| **GOVERN**   | GV   | Establish, communicate, and monitor cybersecurity risk management strategy, expectations, and policy |
| **IDENTIFY** | ID   | Understand cybersecurity risks to assets, capabilities, and data                                     |
| **PROTECT**  | PR   | Use safeguards to manage cybersecurity risks                                                         |
| **DETECT**   | DE   | Find and analyze possible cybersecurity attacks and compromises                                      |
| **RESPOND**  | RS   | Take action regarding a detected cybersecurity incident                                              |
| **RECOVER**  | RC   | Restore assets and operations affected by a cybersecurity incident                                   |

### NIST CSF 2.0 Implementation Tiers

| Tier                      | Description                                |
| ------------------------- | ------------------------------------------ |
| **Tier 1: Partial**       | Ad-hoc, reactive cybersecurity practices   |
| **Tier 2: Risk Informed** | Risk-informed but not organization-wide    |
| **Tier 3: Repeatable**    | Formalized, organization-wide policies     |
| **Tier 4: Adaptive**      | Continuously improving, adaptive practices |

**MSSP Target Tier:** Tier 3-4 (Repeatable to Adaptive) across all functions

---

# 7. NIST CSF 2.0 Function Alignment (Mandatory)

## 7.1 GOVERN (GV) – Cybersecurity Governance

| Category                                           | Subcategory Examples                | MSSP Implementation                                            | Evidence                          | Current Tier | Target Tier |
| -------------------------------------------------- | ----------------------------------- | -------------------------------------------------------------- | --------------------------------- | ------------ | ----------- |
| GV.OC – Organizational Context                     | Mission, stakeholders, dependencies | MSSP context documented; client/regulator stakeholder register | Context Doc; Stakeholder Register | 3            | 4           |
| GV.RM – Risk Management Strategy                   | Risk tolerance, strategy            | Documented MSSP risk management strategy                       | Risk Strategy Doc                 | 3            | 4           |
| GV.RR – Roles, Responsibilities, Authorities       | RACI, accountability                | RACI Matrix; role definitions                                  | RACI-Matrix-IR.xlsx               | 3            | 4           |
| GV.PO – Policy                                     | Policies established                | Comprehensive policy library                                   | All policies in `00_GOVERNANCE/`  | 3            | 4           |
| GV.OV – Oversight                                  | Governance committee, reporting     | Steering committee; executive reporting                        | Committee Minutes; KPI Reports    | 3            | 4           |
| GV.SC – Cybersecurity Supply Chain Risk Management | Supplier risk, agreements           | Supplier risk program; contract clauses                        | Supplier Register; Contracts      | 3            | 3           |

## 7.2 IDENTIFY (ID) – Asset and Risk Understanding

| Category                 | Subcategory Examples                     | MSSP Implementation                      | Evidence                      | Current Tier | Target Tier |
| ------------------------ | ---------------------------------------- | ---------------------------------------- | ----------------------------- | ------------ | ----------- |
| ID.AM – Asset Management | Asset inventory                          | Asset register (MSSP + per-client)       | Asset Register                | 3            | 4           |
| ID.RA – Risk Assessment  | Threats, vulnerabilities identified      | Risk assessment program; vuln management | Risk Register; Vuln Reports   | 3            | 4           |
| ID.IM – Improvement      | Improvements identified from assessments | Improvement register                     | Security Improvement Register | 3            | 4           |

## 7.3 PROTECT (PR) – Safeguards

| Category                                                    | Subcategory Examples     | MSSP Implementation                  | Evidence            | Current Tier | Target Tier |
| ----------------------------------------------------------- | ------------------------ | ------------------------------------ | ------------------- | ------------ | ----------- |
| PR.AA – Identity Management, Authentication, Access Control | IAM, MFA, RBAC           | IAM program; MFA mandate; RBAC/ABAC  | IAM Procedures      | 3            | 4           |
| PR.AT – Awareness and Training                              | Security training        | Annual + role-based training         | Training Records    | 3            | 4           |
| PR.DS – Data Security                                       | Data protection          | Data classification; encryption; DLP | Data Policies       | 3            | 4           |
| PR.PS – Platform Security                                   | Platform hardening       | Endpoint/server/cloud hardening      | Hardening Standards | 3            | 4           |
| PR.IR – Technology Infrastructure Resilience                | Network/infra resilience | Network design; redundancy           | Architecture Docs   | 3            | 4           |

## 7.4 DETECT (DE) – Detection

| Category                       | Subcategory Examples | MSSP Implementation              | Evidence            | Current Tier | Target Tier |
| ------------------------------ | -------------------- | -------------------------------- | ------------------- | ------------ | ----------- |
| DE.CM – Continuous Monitoring  | 24x7 monitoring      | SOC 24x7 operations; SIEM; EDR   | SOC Reports         | 4            | 4           |
| DE.AE – Adverse Event Analysis | Event analysis       | L1/L2/L3 tier model; correlation | Alert Handling SOPs | 4            | 4           |

## 7.5 RESPOND (RS) – Response

| Category                                              | Subcategory Examples     | MSSP Implementation             | Evidence                           | Current Tier | Target Tier |
| ----------------------------------------------------- | ------------------------ | ------------------------------- | ---------------------------------- | ------------ | ----------- |
| RS.MA – Incident Management                           | IR planning, execution   | IR Policy + Playbooks + IR Team | IR-Policy-Master.md; All Playbooks | 4            | 4           |
| RS.AN – Incident Analysis                             | Investigation, forensics | L3 forensics; threat hunting    | L3 SOPs                            | 3            | 4           |
| RS.CO – Incident Response Reporting and Communication | Internal/external comms  | Escalation matrix; templates    | Communication Templates            | 4            | 4           |
| RS.MI – Incident Mitigation                           | Containment, eradication | Containment playbooks           | Containment SOPs                   | 4            | 4           |

## 7.6 RECOVER (RC) – Recovery

| Category                                 | Subcategory Examples | MSSP Implementation                     | Evidence       | Current Tier | Target Tier |
| ---------------------------------------- | -------------------- | --------------------------------------- | -------------- | ------------ | ----------- |
| RC.RP – Incident Recovery Plan Execution | Recovery execution   | Recovery playbooks; client coordination | Recovery SOPs  | 3            | 4           |
| RC.CO – Incident Recovery Communication  | Recovery comms       | Closure templates; status updates       | Comm Templates | 3            | 4           |

---

# 8. Multi-Tenant NIST Implementation Considerations (Mandatory)

| Function     | Multi-Tenant Considerations                                                                                  |
| ------------ | ------------------------------------------------------------------------------------------------------------ |
| **GOVERN**   | Per-client governance via DPA/MSA; tenant-aware policies; client governance committees                       |
| **IDENTIFY** | Per-tenant asset register; per-client risk assessments; tenant-scoped vulnerability scans                    |
| **PROTECT**  | Tenant-scoped RBAC; per-client encryption; tenant data segregation; per-client training requirements         |
| **DETECT**   | Per-tenant SIEM indexes; tenant-scoped EDR; per-client detection rules; cross-tenant correlation (sanitized) |
| **RESPOND**  | Per-client playbooks; tenant-scoped IR; cross-client incident coordination via CCIC                          |
| **RECOVER**  | Per-client recovery; per-client regulatory reporting; per-client lessons learned                             |

---

# 9. NIST SP 800-61 Incident Handling Lifecycle Alignment (Mandatory)

The MSSP follows the NIST four-phase lifecycle:

## 9.1 Phase 1 – Preparation

| Activity                       | MSSP Implementation                  | Reference                                            |
| ------------------------------ | ------------------------------------ | ---------------------------------------------------- |
| Incident Response Policy       | Documented and approved              | `IR-Policy-Master.md`                                |
| IR Team established            | SOC + IR Team defined                | `IR-Team-Role-Definition.md`                         |
| Playbooks developed            | 13+ incident-type playbooks          | `02_PLAYBOOKS/`                                      |
| Tools configured               | SIEM, EDR, SOAR, TI, ticketing       | `04_TOOLS-AND-TECHNOLOGY/`                           |
| Training conducted             | L1/L2/L3/IR Team onboarding + annual | `10_TRAINING-AND-EXERCISES/`                         |
| Threat intelligence integrated | TI platform; per-client feeds        | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/`  |
| Communication plans            | Escalation matrix; templates         | `05_ESCALATION-AND-COMMUNICATION/`                   |
| Evidence procedures            | CoC; collection SOPs                 | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`                  |
| Tabletop exercises             | Annual + quarterly                   | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/` |

## 9.2 Phase 2 – Detection & Analysis

| Activity                       | MSSP Implementation                             | Reference                                    |
| ------------------------------ | ----------------------------------------------- | -------------------------------------------- |
| Alert monitoring               | 24x7 SOC; SIEM/EDR alerts                       | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/` |
| Alert triage                   | L1 alert handling SOP                           | `L1-Alert-Handling-SOP.md`                   |
| Investigation                  | L2/L3 investigation SOPs                        | `L2-Investigation-SOP.md`                    |
| Threat intelligence enrichment | Auto-enrichment in SOAR                         | `TI-Integration-with-SIEM.md`                |
| Severity classification        | Standard severity matrix + per-client overrides | `Severity-Classification-Guide.md`           |
| Incident declaration           | Formal declaration process                      | `Alert-to-Incident-Qualification.md`         |
| Documentation                  | All actions in ticketing system                 | `Ticket-Lifecycle-SOP.md`                    |

## 9.3 Phase 3 – Containment, Eradication & Recovery

| Activity               | MSSP Implementation                                    | Reference                             |
| ---------------------- | ------------------------------------------------------ | ------------------------------------- |
| Short-term containment | Network isolation; account disable; per playbook       | Per-playbook containment sections     |
| Long-term containment  | System rebuild; controlled access                      | Per-playbook                          |
| Evidence preservation  | CoC during containment                                 | `CoC-Master-Form.md`                  |
| Eradication            | Malware removal; vuln patching; threat actor removal   | Per-playbook eradication sections     |
| Recovery               | System restoration; integrity verification; monitoring | Per-playbook recovery sections        |
| Authorization          | Per-client containment authority matrix                | `IRT-Containment-Authority-Matrix.md` |

## 9.4 Phase 4 – Post-Incident Activity

| Activity                                | MSSP Implementation             | Reference                                                        |
| --------------------------------------- | ------------------------------- | ---------------------------------------------------------------- |
| Lessons learned meeting                 | Per-incident LL session         | `Lessons-Learned-Template.md`                                    |
| Root cause analysis                     | RCA per major incident          | `RCA-Template.md`                                                |
| Control gap identification              | Tracked in improvement register | `Control-Gap-Tracker.xlsx`                                       |
| Detection improvement                   | Detection engineering feedback  | `Detection-Improvement-Log.md`                                   |
| Playbook updates                        | Playbook improvement log        | `Playbook-Update-Log.md`                                         |
| Threat intelligence output              | IoCs/TTPs/Actor profiles        | `08_POST-INCIDENT/08.4_Threat-Intel-Output/`                     |
| Reporting to management                 | Executive reports               | `Executive-Summary-Template.md`                                  |
| Regulatory reporting (where applicable) | Per regulation                  | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/` |

---

# 10. NIST SP 800-53 Rev.5 Control Family Alignment (Mandatory)

The MSSP aligns with the following NIST SP 800-53 control families:

| Family                                    | Code | MSSP Implementation                  | Evidence                 |
| ----------------------------------------- | ---- | ------------------------------------ | ------------------------ |
| Access Control                            | AC   | RBAC/ABAC; MFA; PAM                  | Access Control Policy    |
| Awareness and Training                    | AT   | Annual + role-based training         | Training Records         |
| Audit and Accountability                  | AU   | Centralized logging; SIEM            | SIEM Logs                |
| Assessment, Authorization, and Monitoring | CA   | Continuous monitoring                | SOC Reports              |
| Configuration Management                  | CM   | Configuration baselines              | Baseline Docs            |
| Contingency Planning                      | CP   | BC/DR plans                          | BCP/DRP Docs             |
| Identification and Authentication         | IA   | IAM program                          | IAM Procedures           |
| Incident Response                         | IR   | Full IR program (this documentation) | All IR Docs              |
| Maintenance                               | MA   | Maintenance procedures               | Maintenance Records      |
| Media Protection                          | MP   | Media handling policy                | Media Policy             |
| Physical and Environmental Protection     | PE   | Physical security                    | Physical Standards       |
| Planning                                  | PL   | Security planning                    | Plan Docs                |
| Personnel Security                        | PS   | Background checks; NDA               | HR Records               |
| PII Processing and Transparency           | PT   | Privacy controls                     | Privacy Policy           |
| Risk Assessment                           | RA   | Risk program                         | Risk Register            |
| System and Services Acquisition           | SA   | Procurement security                 | Procurement Policy       |
| System and Communications Protection      | SC   | Network/comms security               | Network Design           |
| System and Information Integrity          | SI   | Malware protection; monitoring       | EDR Reports; SOC Reports |
| Supply Chain Risk Management              | SR   | Supply chain risk                    | Supply Chain Register    |
| Program Management                        | PM   | Cybersecurity program                | Program Charter          |

## 10.1 Detailed IR Control Family (Primary for IR Documentation)

| Control | Title                         | MSSP Implementation     |
| ------- | ----------------------------- | ----------------------- |
| IR-1    | Policy and Procedures         | IR Policy + SOPs        |
| IR-2    | Incident Response Training    | Training program        |
| IR-3    | Incident Response Testing     | Tabletop + drills       |
| IR-4    | Incident Handling             | IR lifecycle            |
| IR-5    | Incident Monitoring           | SOC monitoring          |
| IR-6    | Incident Reporting            | Reporting templates     |
| IR-7    | Incident Response Assistance  | IR Team + retainer      |
| IR-8    | Incident Response Plan        | IR Plan documented      |
| IR-9    | Information Spillage Response | Data leakage procedures |

---

# 11. NIST CSF 2.0 Implementation Tier Assessment (Mandatory)

## 11.1 Current State Profile (MSSP Self-Assessment)

| Function | Current Tier | Notes                                          |
| -------- | ------------ | ---------------------------------------------- |
| GOVERN   | 3            | Formalized policies; quarterly oversight       |
| IDENTIFY | 3            | Asset register; annual risk assessment         |
| PROTECT  | 3            | Multi-layered controls deployed                |
| DETECT   | 4            | 24x7 SOC with continuous improvement           |
| RESPOND  | 4            | Mature IR program with playbooks               |
| RECOVER  | 3            | Recovery plans documented; client coordination |

## 11.2 Target State Profile

| Function | Target Tier | Gap                     | Initiatives                                      |
| -------- | ----------- | ----------------------- | ------------------------------------------------ |
| GOVERN   | 4           | Adaptive governance     | Real-time governance metrics; AI-driven risk     |
| IDENTIFY | 4           | Adaptive identification | Continuous asset discovery; dynamic risk scoring |
| PROTECT  | 4           | Adaptive protection     | Zero-trust maturity; automated hardening         |
| DETECT   | 4           | Maintain                | Continuous detection engineering                 |
| RESPOND  | 4           | Maintain                | SOAR maturity expansion                          |
| RECOVER  | 4           | Adaptive recovery       | Automated recovery validation                    |

## 11.3 Maturity Roadmap

| Function | 2026 Q3 | 2026 Q4 | 2027 Q1 | 2027 Q2 |
| -------- | ------- | ------- | ------- | ------- |
| GOVERN   | 3       | 3       | 3.5     | 4       |
| IDENTIFY | 3       | 3       | 3.5     | 4       |
| PROTECT  | 3       | 3       | 3.5     | 4       |
| DETECT   | 4       | 4       | 4       | 4       |
| RESPOND  | 4       | 4       | 4       | 4       |
| RECOVER  | 3       | 3.5     | 4       | 4       |

---

# 12. Multi-Tenant NIST Architecture (Mandatory)

┌──────────────────────────────────────────────────────────────┐
│ GOVERN (GV): Multi-Tenant Adaptations │
│ • Per-client DPA/MSA governance │
│ • Tenant-aware policies │
│ • Per-client risk acceptance │
├──────────────────────────────────────────────────────────────┤
│ IDENTIFY (ID): Multi-Tenant Adaptations │
│ • Per-tenant asset register │
│ • Per-client risk assessments │
│ • Tenant-scoped vulnerability mgmt │
├──────────────────────────────────────────────────────────────┤
│ PROTECT (PR): Multi-Tenant Adaptations │
│ • Tenant-scoped IAM │
│ • Per-tenant encryption │
│ • Data segregation enforcement │
├──────────────────────────────────────────────────────────────┤
│ DETECT (DE): Multi-Tenant Adaptations │
│ • Per-tenant SIEM indexes │
│ • Per-tenant EDR consoles │
│ • Sanitized cross-tenant correlation │
├──────────────────────────────────────────────────────────────┤
│ RESPOND (RS): Multi-Tenant Adaptations │
│ • Per-client playbooks │
│ • Tenant-scoped response │
│ • Cross-client coordination via CCIC │
├──────────────────────────────────────────────────────────────┤
│ RECOVER (RC): Multi-Tenant Adaptations │
│ • Per-client recovery plans │
│ • Per-client regulatory reporting │
│ • Per-client lessons learned │
└──────────────────────────────────────────────────────────────┘

---

# 13. NIST Assessment Program (Mandatory)

## 13.1 Assessment Schedule

| Assessment Type                  | Frequency          | Scope                            |
| -------------------------------- | ------------------ | -------------------------------- |
| Self-assessment                  | Quarterly          | All functions, focused           |
| Full NIST CSF assessment         | Annually           | All functions, all subcategories |
| Third-party assessment           | Biennially         | External validation              |
| Pre-client onboarding assessment | Per client         | Per client requirements          |
| Post-incident NIST review        | Per major incident | RESPOND + RECOVER focused        |

## 13.2 Assessment Methodology

| Step | Action                          | Owner           |
| ---- | ------------------------------- | --------------- |
| 1    | Assessment scope confirmation   | Compliance Lead |
| 2    | Subcategory evidence collection | Function Owners |
| 3    | Tier rating per subcategory     | Compliance Lead |
| 4    | Gap analysis                    | Compliance Lead |
| 5    | Improvement plan                | Function Owners |
| 6    | Management review               | CISO            |
| 7    | Action tracking                 | Compliance Lead |
| 8    | Re-assessment                   | Per schedule    |

---

# 14. NIST Profile Management (Mandatory)

## 14.1 MSSP Master Profile

The MSSP maintains a master CSF profile covering all functions/subcategories applicable to its multi-tenant SOC service.

## 14.2 Per-Client Sub-Profiles

For clients requiring NIST alignment, sub-profiles document:

- Client-specific subcategory implementations
- Client tier targets
- Client gap analysis
- Client improvement roadmap

**Reference:**

- `09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/[CLIENT-NAME]/`

---

# 15. NIST Subcategory Evidence Management (Mandatory)

## 15.1 Evidence Standards

| Standard                 | Requirement                          |
| ------------------------ | ------------------------------------ |
| Per-subcategory evidence | Mandatory for assessed subcategories |
| Evidence currency        | Within 12 months                     |
| Evidence attribution     | Documented owner/date                |
| Cross-reference          | Linked to subcategory ID             |
| Multi-tenant tagging     | Where applicable                     |

## 15.2 Evidence Repository

NIST-Evidence-Repository/
├── GOVERN/
│ ├── GV.OC/
│ ├── GV.RM/
│ ├── GV.RR/
│ ├── GV.PO/
│ ├── GV.OV/
│ └── GV.SC/
├── IDENTIFY/
│ ├── ID.AM/
│ ├── ID.RA/
│ └── ID.IM/
├── PROTECT/
│ ├── PR.AA/
│ ├── PR.AT/
│ ├── PR.DS/
│ ├── PR.PS/
│ └── PR.IR/
├── DETECT/
│ ├── DE.CM/
│ └── DE.AE/
├── RESPOND/
│ ├── RS.MA/
│ ├── RS.AN/
│ ├── RS.CO/
│ └── RS.MI/
└── RECOVER/
├── RC.RP/
└── RC.CO/

---

# 16. Continuous Improvement (Mandatory)

## 16.1 Improvement Inputs

| Source                   | Examples                      |
| ------------------------ | ----------------------------- |
| Self-assessments         | Tier gaps                     |
| Third-party assessments  | External findings             |
| Client feedback          | Client maturity expectations  |
| Incident lessons learned | Response/recover improvements |
| Threat landscape changes | New protection requirements   |
| NIST framework updates   | New subcategories             |
| Regulatory changes       | New governance requirements   |

## 16.2 Improvement Tracking

All NIST-related improvements tracked in:

- `08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx`
- `08_POST-INCIDENT/08.3_Improvement-Tracking/Control-Gap-Tracker.xlsx`

---

# 17. Federal/Regulated Client Considerations (Mandatory)

## 17.1 FedRAMP Considerations

For clients requiring FedRAMP-aligned services:

- NIST SP 800-53 Rev.5 control baselines (Low/Moderate/High)
- Continuous monitoring per FedRAMP requirements
- Annual assessments
- POA&M management
- Authorization boundary documentation

## 17.2 FISMA Considerations

For US Federal clients:

- NIST RMF (Risk Management Framework) alignment
- System Security Plans
- Authorization to Operate (ATO) support

## 17.3 CMMC Considerations

For DoD supply chain clients:

- CMMC Level alignment per client requirement
- Practice and process maturity demonstration

---

# 18. Client NIST Assessment Support (Mandatory)

## 18.1 Client Assessment Support Activities

| Activity                                       | MSSP Role                  |
| ---------------------------------------------- | -------------------------- |
| Provide NIST CSF self-assessment               | On client request          |
| Support client NIST audits                     | Provide evidence per scope |
| Map MSSP services to client NIST subcategories | Per client onboarding      |
| Quarterly NIST metrics reporting               | Per client request         |
| Annual maturity progression report             | Per client request         |

## 18.2 Multi-Tenant Assessment Constraints

| Constraint                          | Requirement |
| ----------------------------------- | ----------- |
| Other clients' identifiers redacted | Mandatory   |
| Tenant-scoped evidence only         | Mandatory   |
| Sanitized policies shareable        | Mandatory   |
| Cross-tenant correlation excluded   | Mandatory   |

---

# 19. Integration with Other Frameworks

| Framework                    | Mapping                               |
| ---------------------------- | ------------------------------------- |
| ISO 27001:2022               | `MSSP-ISO27001-Controls.md`           |
| SOC 2                        | Trust Service Criteria mapping        |
| RBI Cyber Security Framework | `IR-Policy-RBI-Alignment.md`          |
| DPDP Act                     | Privacy controls overlay              |
| CIS Controls v8              | Direct mapping in NIST CSF references |
| PCI DSS (if applicable)      | Per client                            |
| HIPAA (if applicable)        | Per client                            |
| HITRUST (if applicable)      | Per client                            |
| FedRAMP                      | Direct via SP 800-53                  |
| CMMC                         | Direct via SP 800-171                 |

**Reference:**

- `00_GOVERNANCE/00.2_Frameworks-Mapping/Multi-Framework-Gap-Analysis.xlsx`

---

# 20. Quality Checklist (Annual NIST Validation)

Before annual NIST assessment:

- [ ] All 6 CSF functions evidenced
- [ ] All applicable categories evidenced
- [ ] All applicable subcategories evidenced
- [ ] Current state tiers assessed per function
- [ ] Target state tiers documented
- [ ] Gap analysis completed
- [ ] Improvement roadmap current
- [ ] NIST SP 800-61 lifecycle alignment evidenced
- [ ] NIST SP 800-53 control families mapped
- [ ] Master MSSP profile current
- [ ] Per-client sub-profiles current (where required)
- [ ] Multi-tenant adaptations documented
- [ ] Evidence repository organized
- [ ] All previous assessment actions closed
- [ ] Self-assessment completed
- [ ] Third-party assessment scheduled (if year due)
- [ ] CISO sign-off obtained

---

# 21. Related Documents

| Document                        | Path                                                                                    |
| ------------------------------- | --------------------------------------------------------------------------------------- |
| IR Policy Master                | `00_GOVERNANCE/00.1_Policies/IR-Policy-Master.md`                                       |
| IR Policy NIST Alignment        | `00_GOVERNANCE/00.1_Policies/IR-Policy-NIST-Alignment.md`                               |
| IR Policy ISO27001 Alignment    | `00_GOVERNANCE/00.1_Policies/IR-Policy-ISO27001-Alignment.md`                           |
| IR Policy RBI Alignment         | `00_GOVERNANCE/00.1_Policies/IR-Policy-RBI-Alignment.md`                                |
| NIST CSF Control Mapping        | `00_GOVERNANCE/00.2_Frameworks-Mapping/NIST-CSF-Control-Mapping.xlsx`                   |
| ISO27001 Annex A Mapping        | `00_GOVERNANCE/00.2_Frameworks-Mapping/ISO27001-Annex-A-Mapping.xlsx`                   |
| Multi-Framework Gap Analysis    | `00_GOVERNANCE/00.2_Frameworks-Mapping/Multi-Framework-Gap-Analysis.xlsx`               |
| RACI Matrix IR                  | `00_GOVERNANCE/00.3_Roles-and-Responsibilities/RACI-Matrix-IR.xlsx`                     |
| MSSP ISO27001 Controls          | `09_MSSP-SPECIFIC/09.4_MSSP-Compliance/MSSP-ISO27001-Controls.md`                       |
| MSSP Audit Readiness Checklist  | `09_MSSP-SPECIFIC/09.4_MSSP-Compliance/MSSP-Audit-Readiness-Checklist.md`               |
| Client Data Segregation Policy  | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`       |
| Cross-Client Incident Procedure | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md`      |
| Multi-Client Alert Handling     | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`          |
| Severity Classification Guide   | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`      |
| L1 Alert Handling SOP           | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Alert-Handling-SOP.md`                    |
| L2 Investigation SOP            | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Investigation-SOP.md`                     |
| L3 Advanced Forensics SOP       | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Advanced-Forensics-SOP.md`                |
| All Playbooks                   | `02_PLAYBOOKS/`                                                                         |
| Lessons Learned Register        | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Register.xlsx`                   |
| Security Improvement Register   | `08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx`         |
| Control Gap Tracker             | `08_POST-INCIDENT/08.3_Improvement-Tracking/Control-Gap-Tracker.xlsx`                   |
| Detection Improvement Log       | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`               |
| Playbook Update Log             | `08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`                     |
| Evidence Retention Schedule     | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Retention-Schedule.md` |
| Tabletop Exercise Guide         | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`          |

---

# 22. Revision History

| Version | Date        | Author                      | Changes                                 |
| ------- | ----------- | --------------------------- | --------------------------------------- |
| 1.0     | 30-May-2026 | MSSP Compliance Lead / CISO | Initial version aligned to NIST CSF 2.0 |

---

# 23. Approval

Approved by:

| Role                 | Name | Signature | Date |
| -------------------- | ---- | --------- | ---- |
| MSSP Compliance Lead |      |           |      |
| MSSP SOC Manager     |      |           |      |
| MSSP IR Team Lead    |      |           |      |
| MSSP CISO            |      |           |      |

---

**End of Document**
