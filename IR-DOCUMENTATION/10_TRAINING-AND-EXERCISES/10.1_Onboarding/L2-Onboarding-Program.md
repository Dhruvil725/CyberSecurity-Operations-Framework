# L2 SOC Analyst Onboarding Program

---

# 1. Document Control

| Field          | Value                                         |
| -------------- | --------------------------------------------- |
| Document Name  | L2 SOC Analyst Onboarding Program             |
| Document ID    | MSSP-TRN-002                                  |
| Version        | 1.0                                           |
| Effective Date | 30-May-2026                                   |
| Owner          | MSSP SOC Manager / IR Team Lead               |
| Approved By    | MSSP CISO                                     |
| Classification | Confidential – MSSP Internal                  |
| Review Cycle   | Annually (or upon SOC operating model change) |

---

# 2. Purpose

This document defines the standardized **L2 SOC Analyst Onboarding Program** governing the structured induction, advanced training, certification, and operational readiness of Level 2 (L2) SOC analysts joining the MSSP — whether external hires, internal promotions from L1, or transfers — ensuring deep investigation competency, multi-tenant discipline, and incident handling excellence.

A formal L2 onboarding program is critical because:

- L2 analysts perform deeper investigations that determine incident classification accuracy
- L2 decisions directly affect containment timing, regulatory reporting, and client outcomes
- inconsistent L2 onboarding causes investigation gaps, missed indicators, and prolonged incidents
- L2 analysts coordinate across tools, tenants, and tiers requiring advanced skills
- multi-tenant investigation requires strict tenant context discipline at deeper investigation levels
- threat hunting, log analysis, and forensics integration require formal training
- ISO 27001 A.6.3 and NIST CSF PR.AT require structured advanced training
- RBI Cyber Security Framework requires competency for personnel handling regulated investigations
- evidence handling, chain of custody, and forensic readiness require formal training
- L2 escalation decisions to L3 must be calibrated to avoid under/over-escalation
- per-client investigation procedures must be mastered before independent handling
- threat intelligence integration into investigations requires specialized training
- audit and compliance reviews require evidence of structured advanced onboarding
- this program is the foundation for L2 analyst quality and career progression to L3

This program ensures:

- consistent 8-week structured onboarding for new L2 analysts
- 4-week accelerated program for L1-promoted analysts
- defined investigation competency milestones with measurable assessments
- advanced multi-tenant training building on L1 foundations
- tool proficiency for deeper investigation use cases
- per-client investigation procedure familiarity
- mentorship pairing with senior L2 or L3 for first 30 days
- formal certification before independent investigation handling
- audit-ready evidence of advanced training completion
- linkage to L2 role definition, SOC procedures, and incident response framework

**Reference alignment:**

- `00_GOVERNANCE/00.3_Roles-and-Responsibilities/L2-Analyst-Role-Definition.md`
- `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/`
- `10_TRAINING-AND-EXERCISES/10.1_Onboarding/L1-Onboarding-Program.md`
- `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 3. Scope

This program applies to all L2 SOC analysts joining the MSSP:

| Scope Element                       | Coverage                                    |
| ----------------------------------- | ------------------------------------------- |
| New L2 hires (external)             | Full 8-week program                         |
| L1-to-L2 promotions (internal)      | Accelerated 4-week program                  |
| L2 transfers (internal departments) | Tailored 5-week program                     |
| L2 returning (>6 months absence)    | Refresher 3-week program                    |
| Per-client investigation training   | Per assigned client                         |
| Advanced tool training              | SIEM deep, EDR deep, NDR, TI, SOAR advanced |
| Investigation procedures            | All L2 SOPs                                 |
| Threat hunting                      | Hypothesis-driven hunts                     |
| Network/log forensics               | Investigation-grade                         |
| Mentorship                          | Mandatory for first 30 days                 |
| Certification                       | Mandatory before independent L2 work        |

Out of scope:

- L1 onboarding (separate program)
- L3 advanced forensics (separate program)
- IR Team specialized onboarding (separate program)
- Management training (covered by HR)

---

# 4. Definitions

| Term                         | Definition                                         |
| ---------------------------- | -------------------------------------------------- |
| L2 Analyst                   | Level 2 SOC analyst (deep investigation)           |
| L1-Promoted                  | L1 analyst promoted to L2                          |
| Deep Investigation           | Multi-source, multi-step incident analysis         |
| Threat Hunting               | Hypothesis-driven proactive search                 |
| Investigation Pivoting       | Moving across data sources to expand investigation |
| Containment Decision         | Recommendation for containment actions             |
| Investigation Documentation  | Standardized investigation write-up                |
| Mentor                       | Senior L2 or L3 paired with new L2                 |
| Certification                | Formal L2 competency validation                    |
| Pre-Certification Assessment | Final readiness check                              |
| Reverse Shadowing            | New L2 performs work; mentor observes              |

---

# 5. Roles and Responsibilities

| Role                        | Responsibilities                                             |
| --------------------------- | ------------------------------------------------------------ |
| **MSSP SOC Manager**        | Program ownership; mentor assignment; certification approval |
| **MSSP IR Team Lead**       | Investigation methodology training; playbook coaching        |
| **MSSP SOC Lead**           | Operational integration; daily oversight                     |
| **MSSP L3 / Senior L2**     | Mentor role for new L2                                       |
| **MSSP Detection Engineer** | Advanced tool training; detection context                    |
| **MSSP Threat Intel Lead**  | TI integration; hunting hypothesis training                  |
| **MSSP Compliance Lead**    | Multi-tenant advanced training; evidence handling            |
| **MSSP HR Lead**            | Logistics; documentation; performance management             |
| **MSSP IT Lead**            | Advanced tool access provisioning                            |
| **New L2 Analyst**          | Active participation; assessment completion; feedback        |
| **Buddy Analyst**           | Daily peer support during first 30 days                      |

---

# 6. Onboarding Program Principles (Mandatory)

| Principle                        | Requirement                                                 |
| -------------------------------- | ----------------------------------------------------------- |
| **Builds on L1 Foundation**      | L1 knowledge prerequisite (internal) or verified (external) |
| **Investigation-Centric**        | Focus on deep investigation methodology                     |
| **Multi-Tenant Discipline**      | Strict tenant segregation at advanced level                 |
| **Tool Mastery Required**        | Advanced certification before independent work              |
| **Hands-On Heavy**               | Significant lab and live investigation time                 |
| **Mentorship Mandatory**         | Senior L2/L3 pairing first 30 days                          |
| **Assessment-Based Progression** | Pass/fail at each milestone                                 |
| **Per-Client Specialization**    | Specific to assigned client portfolio                       |
| **Documentation Excellence**     | Investigation write-up standards enforced                   |
| **Audit-Ready Records**          | Complete training documentation                             |

---

# 7. L2 Onboarding Program Overview (8 Weeks Full / 4 Weeks Accelerated)

FULL PROGRAM (External L2 Hire):

Week 1: FOUNDATION & ORIENTATION
├── HR + admin + NDAs
├── MSSP organization + multi-tenant policy
├── L1 foundational refresher (verified)
└── Initial tool exposure

Week 2: ADVANCED TOOL TRAINING
├── SIEM advanced queries (KQL/SPL deep)
├── EDR deep investigation
├── NDR / network forensics tools
├── SOAR playbook execution
└── TI platform integration

Week 3: L2 INVESTIGATION METHODOLOGY
├── L2 Investigation SOP
├── Threat hunting principles
├── Log analysis methodology
├── Network forensics basics
└── Evidence handling for investigations

Week 4: L2 SOPs & PROCEDURES
├── L2 SOPs deep dive
├── L2 escalation criteria (to L3)
├── L2 EDR/SIEM deep investigation
├── L2 evidence handling
└── L2 shift handover

Week 5: PLAYBOOK MASTERY
├── L2 sections of all 13+ playbooks
├── Per-client playbook deep dive
├── Containment recommendations
└── Investigation documentation standards

Week 6: SHADOWING & SUPERVISED INVESTIGATIONS
├── Active mentor shadowing
├── Reverse shadowing
├── Supervised live investigations
└── Per-client assignment briefing

Week 7: ADVANCED SCENARIOS & HUNTS
├── Threat hunting exercises
├── Multi-source pivoting exercises
├── Complex tabletop scenarios
└── Pre-certification assessment

Week 8: CERTIFICATION & SOLO READINESS
├── Final L2 certification
├── Tenant assignment confirmation
├── First independent shift
└── 30-day mentor pairing continues

**ACCELERATED PROGRAM (L1-Promoted to L2):**

Week 1: TRANSITION & ADVANCED TOOLS
├── L1-to-L2 transition briefing
├── Advanced SIEM/EDR/NDR training
├── SOAR advanced
└── TI integration

Week 2: L2 METHODOLOGY & SOPs
├── L2 Investigation SOP
├── Threat hunting basics
├── L2 SOPs deep dive
└── Evidence handling

Week 3: PLAYBOOK MASTERY & SHADOWING
├── L2 playbook sections
├── Mentor shadowing
├── Supervised investigations
└── Documentation standards

Week 4: CERTIFICATION & TRANSITION
├── Pre-certification assessment
├── Final L2 certification
├── Updated tenant assignment
└── 30-day mentor pairing

---

# 8. Week 1: Foundation & Orientation (Mandatory)

## 8.1 Day 1 – Admin & Welcome

| Activity                             | Duration | Owner       |
| ------------------------------------ | -------- | ----------- |
| HR orientation (external hires only) | 2 hours  | HR          |
| Equipment + workspace setup          | 1 hour   | IT          |
| MSSP organization (external hires)   | 1 hour   | SOC Manager |
| L2 role expectations briefing        | 1 hour   | SOC Manager |
| Mentor introduction                  | 1 hour   | Mentor      |
| NDAs + L2-specific agreements        | 1 hour   | Legal/HR    |

## 8.2 Day 2 – Multi-Tenant Advanced Policy

| Activity                                        | Duration | Owner             |
| ----------------------------------------------- | -------- | ----------------- |
| Client Data Segregation Policy (advanced)       | 2 hours  | Compliance Lead   |
| Cross-tenant investigation prohibitions         | 1 hour   | Compliance Lead   |
| Sanitization for L2 investigation outputs       | 1 hour   | Threat Intel Lead |
| Multi-Client Alert Handling (L2 perspective)    | 1 hour   | SOC Manager       |
| Cross-Client Incident Procedure overview        | 1 hour   | IR Team Lead      |
| **Multi-tenant advanced quiz (must pass 100%)** | 30 min   | Compliance Lead   |

**⚠️ Critical Gate:** Cannot proceed without 100% on multi-tenant advanced quiz.

## 8.3 Day 3 – L1 Foundational Verification (External Hires)

| Activity                              | Duration  | Owner              |
| ------------------------------------- | --------- | ------------------ |
| L1 policy/procedure verification quiz | 2 hours   | SOC Lead           |
| L1 tool proficiency verification      | 2 hours   | Detection Engineer |
| L1 SOP demonstration                  | 2 hours   | SOC Lead           |
| Gap remediation (if any)              | As needed | Mentor             |

*(L1-promoted analysts skip this day)*

## 8.4 Day 4 – Investigation Methodology Intro

| Activity                              | Duration | Owner             |
| ------------------------------------- | -------- | ----------------- |
| Investigation lifecycle overview      | 2 hours  | IR Team Lead      |
| Investigation documentation standards | 1 hour   | IR Team Lead      |
| Timeline construction principles      | 1 hour   | IR Team Lead      |
| IoC pivoting methodology              | 1 hour   | Threat Intel Lead |
| Investigation case studies            | 1 hour   | IR Team Lead      |

## 8.5 Day 5 – L2 Tool Preview

| Activity                        | Duration | Owner              |
| ------------------------------- | -------- | ------------------ |
| SIEM advanced features overview | 2 hours  | Detection Engineer |
| EDR deep investigation features | 1 hour   | Detection Engineer |
| NDR/network tools overview      | 1 hour   | Detection Engineer |
| TI platform advanced features   | 1 hour   | Threat Intel Lead  |
| Week 1 retrospective            | 1 hour   | Mentor + SOC Lead  |

### Week 1 Completion Criteria

- [ ] All admin setup completed
- [ ] L2-specific NDAs signed
- [ ] Multi-tenant advanced quiz passed (100%)
- [ ] L1 verification completed (external hires)
- [ ] Investigation methodology intro complete
- [ ] Mentor pairing confirmed

---

# 9. Week 2: Advanced Tool Training (Mandatory)

## 9.1 SIEM Advanced Training

| Topic                                      | Duration | Owner              |
| ------------------------------------------ | -------- | ------------------ |
| Advanced query language (KQL/SPL/etc.)     | 6 hours  | Detection Engineer |
| Multi-source correlation                   | 3 hours  | Detection Engineer |
| Custom dashboard creation                  | 2 hours  | Detection Engineer |
| Historical investigation queries           | 2 hours  | Detection Engineer |
| Threat hunting queries                     | 3 hours  | Threat Intel Lead  |
| **Hands-on lab: 20 investigation queries** | 6 hours  | Detection Engineer |

## 9.2 EDR Deep Investigation

| Topic                                        | Duration | Owner              |
| -------------------------------------------- | -------- | ------------------ |
| Endpoint timeline analysis                   | 2 hours  | Detection Engineer |
| Process tree deep analysis                   | 2 hours  | Detection Engineer |
| File/registry/network artifact analysis      | 3 hours  | Detection Engineer |
| Memory artifact examination                  | 2 hours  | Detection Engineer |
| Containment commands (full)                  | 1 hour   | Detection Engineer |
| **Hands-on lab: 10 endpoint investigations** | 6 hours  | Detection Engineer |

## 9.3 NDR / Network Forensics Tools

| Topic                                      | Duration | Owner              |
| ------------------------------------------ | -------- | ------------------ |
| NDR architecture overview                  | 1 hour   | Detection Engineer |
| Network flow analysis                      | 2 hours  | Detection Engineer |
| PCAP analysis basics                       | 3 hours  | Detection Engineer |
| C2 detection patterns                      | 2 hours  | Threat Intel Lead  |
| **Hands-on lab: 5 network investigations** | 4 hours  | Detection Engineer |

## 9.4 SOAR Advanced

| Topic                                      | Duration | Owner              |
| ------------------------------------------ | -------- | ------------------ |
| SOAR playbook design                       | 2 hours  | Detection Engineer |
| Manual playbook execution                  | 1 hour   | Detection Engineer |
| Playbook customization basics              | 1 hour   | Detection Engineer |
| **Hands-on lab: SOAR investigation flows** | 3 hours  | Detection Engineer |

## 9.5 Threat Intelligence Integration

| Topic                                        | Duration | Owner             |
| -------------------------------------------- | -------- | ----------------- |
| TI platform deep dive                        | 2 hours  | Threat Intel Lead |
| IoC enrichment in investigations             | 2 hours  | Threat Intel Lead |
| Threat actor profiles usage                  | 2 hours  | Threat Intel Lead |
| TTP-based hunting                            | 3 hours  | Threat Intel Lead |
| **Hands-on lab: TI-enriched investigations** | 3 hours  | Threat Intel Lead |

### Week 2 Completion Criteria

- [ ] SIEM advanced lab completed (20 queries)
- [ ] EDR deep investigation lab completed (10 investigations)
- [ ] Network forensics lab completed (5 investigations)
- [ ] SOAR investigation flow lab completed
- [ ] TI-enriched investigations completed
- [ ] Advanced tool quiz passed (≥85%)

---

# 10. Week 3: L2 Investigation Methodology (Mandatory)

## 10.1 L2 Investigation SOP

| Topic                                            | Duration | Owner        |
| ------------------------------------------------ | -------- | ------------ |
| L2 Investigation SOP walkthrough                 | 3 hours  | IR Team Lead |
| Investigation phases (initial, deep, conclusion) | 2 hours  | IR Team Lead |
| Hypothesis formation                             | 2 hours  | IR Team Lead |
| Evidence-driven analysis                         | 2 hours  | IR Team Lead |
| Investigation pivoting                           | 2 hours  | IR Team Lead |

## 10.2 Threat Hunting Principles

| Topic                                     | Duration | Owner             |
| ----------------------------------------- | -------- | ----------------- |
| L2 Threat Hunting Procedures              | 2 hours  | Threat Intel Lead |
| Hypothesis-driven hunting                 | 2 hours  | Threat Intel Lead |
| Hunt documentation standards              | 1 hour   | Threat Intel Lead |
| MITRE ATT&CK-driven hunts                 | 3 hours  | Threat Intel Lead |
| **Hands-on hunt exercise (1 hypothesis)** | 4 hours  | Threat Intel Lead |

## 10.3 Log Analysis Methodology

| Topic                         | Duration | Owner              |
| ----------------------------- | -------- | ------------------ |
| L2 Log Analysis SOP           | 2 hours  | Detection Engineer |
| Multi-source log correlation  | 3 hours  | Detection Engineer |
| Log parsing and normalization | 2 hours  | Detection Engineer |
| Anomaly identification        | 2 hours  | Detection Engineer |

## 10.4 Network Forensics Basics

| Topic                         | Duration | Owner              |
| ----------------------------- | -------- | ------------------ |
| L2 Network Forensics SOP      | 2 hours  | Detection Engineer |
| Flow vs packet analysis       | 1 hour   | Detection Engineer |
| Encrypted traffic analysis    | 2 hours  | Detection Engineer |
| Network timeline construction | 2 hours  | Detection Engineer |

## 10.5 Evidence Handling for Investigations

| Topic                                      | Duration | Owner           |
| ------------------------------------------ | -------- | --------------- |
| L2 Evidence Handling SOP                   | 2 hours  | Compliance Lead |
| Chain of Custody basics                    | 2 hours  | Compliance Lead |
| Evidence preservation during investigation | 1 hour   | Compliance Lead |
| Per-tenant evidence segregation            | 1 hour   | Compliance Lead |

### Week 3 Completion Criteria

- [ ] L2 Investigation SOP demonstrated
- [ ] Hunt exercise completed
- [ ] Log analysis demonstrated
- [ ] Network forensics basics demonstrated
- [ ] Evidence handling quiz passed (100%)
- [ ] Methodology assessment passed (≥80%)

---

# 11. Week 4: L2 SOPs & Procedures (Mandatory)

## 11.1 All L2 SOPs Deep Dive

| SOP                                  | Duration | Owner              |
| ------------------------------------ | -------- | ------------------ |
| L2 Investigation SOP (reinforcement) | 2 hours  | IR Team Lead       |
| L2 Escalation Criteria (to L3)       | 2 hours  | IR Team Lead       |
| L2 Evidence Handling SOP             | 1 hour   | Compliance Lead    |
| L2 Threat Hunting Procedures         | 1 hour   | Threat Intel Lead  |
| L2 SIEM Deep Investigation           | 2 hours  | Detection Engineer |
| L2 EDR Deep Investigation            | 2 hours  | Detection Engineer |
| L2 Network Forensics SOP             | 1 hour   | Detection Engineer |
| L2 Log Analysis SOP                  | 1 hour   | Detection Engineer |
| L2 Shift Handover Template           | 1 hour   | SOC Lead           |

## 11.2 Multi-Tenant L2 Considerations

| Topic                                     | Duration | Owner             |
| ----------------------------------------- | -------- | ----------------- |
| Cross-Client Incident Procedure (L2 role) | 2 hours  | IR Team Lead      |
| L2 investigation sanitization             | 1 hour   | Threat Intel Lead |
| Tenant-scoped investigation discipline    | 1 hour   | Compliance Lead   |
| Per-tenant ticket documentation           | 1 hour   | SOC Lead          |

## 11.3 Escalation Discipline

| Topic                              | Duration | Owner        |
| ---------------------------------- | -------- | ------------ |
| When to escalate to L3             | 2 hours  | IR Team Lead |
| When to escalate to IR Team        | 2 hours  | IR Team Lead |
| Escalation documentation standards | 1 hour   | IR Team Lead |
| Escalation case studies            | 2 hours  | IR Team Lead |

### Week 4 Completion Criteria

- [ ] All L2 SOPs reviewed and acknowledged
- [ ] Multi-tenant L2 considerations understood
- [ ] Escalation criteria mastered
- [ ] SOP quiz passed (≥85%)

---

# 12. Week 5: Playbook Mastery (Mandatory)

## 12.1 L2 Sections of All Playbooks

| Playbook                                                       | Duration | Owner        |
| -------------------------------------------------------------- | -------- | ------------ |
| Ransomware L2 Investigation                                    | 3 hours  | IR Team Lead |
| Phishing L2 Investigation                                      | 2 hours  | IR Team Lead |
| Malware L2 Investigation                                       | 3 hours  | IR Team Lead |
| DDoS L2 Investigation                                          | 1 hour   | IR Team Lead |
| Insider Threat L2 Investigation                                | 2 hours  | IR Team Lead |
| Data Breach L2 Investigation                                   | 2 hours  | IR Team Lead |
| Credential Attack L2 Investigation | 2 hours  | IR Team Lead |
| Web Application Attack L2 Investigation                        | 2 hours  | IR Team Lead |
| Cloud L2 Investigation                                         | 2 hours  | IR Team Lead |
| Network Intrusion L2 Investigation                             | 2 hours  | IR Team Lead |

## 12.2 Per-Client Playbook Deep Dive

| Topic                                  | Duration | Owner           |
| -------------------------------------- | -------- | --------------- |
| Per-client environment profiles (deep) | 3 hours  | SOC Manager     |
| Per-client IR policies (deep)          | 2 hours  | Compliance Lead |
| Per-client escalation matrices         | 2 hours  | SOC Lead        |
| Per-client custom playbooks            | 4 hours  | IR Team Lead    |
| Per-client containment authority       | 1 hour   | IR Team Lead    |

## 12.3 Containment Recommendations

| Topic                                    | Duration | Owner        |
| ---------------------------------------- | -------- | ------------ |
| Containment decision framework           | 2 hours  | IR Team Lead |
| Per-client containment authority matrix  | 1 hour   | IR Team Lead |
| Containment recommendation documentation | 1 hour   | IR Team Lead |

## 12.4 Investigation Documentation Standards

| Topic                            | Duration | Owner           |
| -------------------------------- | -------- | --------------- |
| Investigation report template    | 2 hours  | IR Team Lead    |
| Timeline construction in tickets | 1 hour   | IR Team Lead    |
| Evidence reference standards     | 1 hour   | Compliance Lead |
| Sanitization in documentation    | 1 hour   | Compliance Lead |

### Week 5 Completion Criteria

- [ ] All L2 playbook sections reviewed
- [ ] Per-client playbooks (assigned) mastered
- [ ] Containment recommendation framework understood
- [ ] Investigation documentation standards practiced
- [ ] Playbook practical assessment passed (≥85%)

---

# 13. Week 6: Shadowing & Supervised Investigations (Mandatory)

## 13.1 Active Mentor Shadowing

| Activity                                  | Duration   | Owner  |
| ----------------------------------------- | ---------- | ------ |
| Active shadowing of mentor L2 work        | 24 hours   | Mentor |
| Real-time investigation observation       | Continuous | Mentor |
| Per-tenant context discipline observation | Continuous | Mentor |
| Escalation decision observation           | Continuous | Mentor |
| Documentation observation                 | Continuous | Mentor |

## 13.2 Reverse Shadowing

| Activity                                                | Duration     | Owner  |
| ------------------------------------------------------- | ------------ | ------ |
| New L2 conducts investigations under mentor observation | 20 hours     | Mentor |
| Real-time feedback                                      | Continuous   | Mentor |
| End-of-shift debrief                                    | 1 hour daily | Mentor |

## 13.3 Supervised Live Investigations

| Activity                                        | Duration  | Owner            |
| ----------------------------------------------- | --------- | ---------------- |
| Supervised live investigations (low complexity) | 8 hours   | Mentor + IR Lead |
| Tenant verification every investigation         | Mandatory | New L2           |
| Documentation review per investigation          | Mandatory | Mentor           |

## 13.4 Per-Client Assignment Briefing

| Activity                                  | Duration | Owner          |
| ----------------------------------------- | -------- | -------------- |
| Specific assigned client briefings        | 4 hours  | Per-client SDM |
| Per-client investigation tools            | 2 hours  | SOC Lead       |
| Per-client investigation history overview | 2 hours  | Per-client SDM |

### Week 6 Completion Criteria

- [ ] Minimum 24 hours active shadowing completed
- [ ] Minimum 20 hours reverse shadowing completed
- [ ] Minimum 8 hours supervised live investigations
- [ ] All assigned client briefings completed
- [ ] Mentor positive evaluation

---

# 14. Week 7: Advanced Scenarios & Hunts (Mandatory)

## 14.1 Threat Hunting Exercises

| Exercise                                   | Duration | Owner             |
| ------------------------------------------ | -------- | ----------------- |
| Hypothesis-driven hunt (assigned scenario) | 6 hours  | Threat Intel Lead |
| MITRE ATT&CK technique hunt                | 4 hours  | Threat Intel Lead |
| Hunt documentation and presentation        | 2 hours  | Threat Intel Lead |

## 14.2 Multi-Source Pivoting Exercises

| Exercise                          | Duration | Owner              |
| --------------------------------- | -------- | ------------------ |
| SIEM-to-EDR pivot exercise        | 3 hours  | Detection Engineer |
| EDR-to-network pivot exercise     | 3 hours  | Detection Engineer |
| Cross-source correlation exercise | 4 hours  | Detection Engineer |

## 14.3 Complex Tabletop Scenarios

| Exercise                                    | Duration | Owner        |
| ------------------------------------------- | -------- | ------------ |
| Ransomware investigation tabletop (L2 lead) | 3 hours  | IR Team Lead |
| Insider threat investigation tabletop       | 3 hours  | IR Team Lead |
| Data breach investigation tabletop          | 3 hours  | IR Team Lead |

## 14.4 Pre-Certification Assessment

| Assessment                                | Duration | Owner              |
| ----------------------------------------- | -------- | ------------------ |
| Written assessment (all SOPs + playbooks) | 2 hours  | SOC Manager        |
| Tool advanced proficiency assessment      | 2 hours  | Detection Engineer |
| Live investigation assessment (3 cases)   | 4 hours  | IR Team Lead       |
| Hunt assessment                           | 2 hours  | Threat Intel Lead  |
| Multi-tenant scenario assessment          | 1 hour   | Compliance Lead    |

### Week 7 Completion Criteria

- [ ] Hunt exercises completed
- [ ] Pivoting exercises completed
- [ ] Tabletop scenarios completed
- [ ] Pre-certification assessment passed (≥80% overall)

---

# 15. Week 8: Certification & Solo Readiness (Mandatory)

## 15.1 Final L2 Certification Assessment

| Component                                     | Pass Threshold   |
| --------------------------------------------- | ---------------- |
| Written exam (all L2 policies/SOPs/playbooks) | 85%              |
| Multi-tenant scenario exam                    | 100% (must pass) |
| Tool advanced proficiency practical           | 85%              |
| Live investigation assessment (5 cases)       | 85% accuracy     |
| Hunt execution assessment                     | Pass/Fail        |
| Per-client investigation knowledge            | 85%              |
| Escalation decision assessment                | 90% accuracy     |

## 15.2 Tenant Assignment Confirmation

| Activity                               | Owner           |
| -------------------------------------- | --------------- |
| Assigned client portfolio finalized    | SOC Manager     |
| Advanced RBAC/ABAC verified            | IT Lead         |
| Per-client investigation access tested | New L2 + Mentor |
| Per-client SLA review                  | SOC Lead        |

## 15.3 First Independent L2 Shift

| Activity                                 | Duration                 | Owner             |
| ---------------------------------------- | ------------------------ | ----------------- |
| First independent shift (mentor on-call) | Full shift               | New L2            |
| Mentor 1-hour check-ins                  | Every hour first 4 hours | Mentor            |
| Shift debrief                            | 1 hour                   | Mentor + SOC Lead |

## 15.4 30-Day Continued Mentorship

| Activity                     | Cadence           | Owner            |
| ---------------------------- | ----------------- | ---------------- |
| Daily mentor check-in        | Daily for 30 days | Mentor           |
| Weekly IR Team Lead review   | Weekly            | IR Team Lead     |
| Bi-weekly SOC Manager review | Bi-weekly         | SOC Manager      |
| 30-day formal review         | Day 30            | SOC Manager + HR |

### Week 8 Completion Criteria

- [ ] Final L2 certification passed (≥85%)
- [ ] Multi-tenant exam passed at 100%
- [ ] Tenant assignment confirmed
- [ ] First independent L2 shift successful
- [ ] 30-day mentorship plan documented

---

# 16. Accelerated Program for L1-Promoted (4 Weeks)

## 16.1 Week 1 (Accelerated): Transition & Advanced Tools

| Day     | Focus                                                          |
| ------- | -------------------------------------------------------------- |
| Day 1   | L1-to-L2 transition briefing + multi-tenant advanced refresher |
| Day 2-3 | SIEM/EDR advanced training (compressed)                        |
| Day 4-5 | NDR/SOAR/TI advanced (compressed)                              |

## 16.2 Week 2 (Accelerated): L2 Methodology & SOPs

| Day     | Focus                                 |
| ------- | ------------------------------------- |
| Day 1-2 | L2 Investigation SOP + Threat Hunting |
| Day 3   | Log/Network/Evidence handling         |
| Day 4-5 | All L2 SOPs deep dive                 |

## 16.3 Week 3 (Accelerated): Playbook Mastery & Shadowing

| Day     | Focus                                        |
| ------- | -------------------------------------------- |
| Day 1-2 | L2 playbook sections (all)                   |
| Day 3-4 | Mentor shadowing                             |
| Day 5   | Reverse shadowing + supervised investigation |

## 16.4 Week 4 (Accelerated): Certification & Transition

| Day     | Focus                                          |
| ------- | ---------------------------------------------- |
| Day 1-2 | Pre-certification preparation                  |
| Day 3   | Pre-certification assessment                   |
| Day 4   | Final L2 certification                         |
| Day 5   | First independent L2 shift + mentorship begins |

---

# 17. Mentor Program (Mandatory)

## 17.1 Mentor Selection Criteria for L2 Onboarding

| Criterion                | Requirement                            |
| ------------------------ | -------------------------------------- |
| Tenure                   | Minimum 1 year L3 or 2 years senior L2 |
| Investigation experience | 50+ documented investigations          |
| Multi-tenant experience  | Multiple client tier experience        |
| Communication skills     | Demonstrated training capability       |
| Availability             | Capacity to mentor                     |

## 17.2 Mentor Responsibilities

- Daily check-ins during first 30 days
- Active shadowing supervision weeks 6
- Reverse shadowing supervision weeks 6
- Investigation methodology coaching
- Per-tenant context discipline coaching
- Documentation quality coaching
- Escalation decision coaching
- Weekly feedback to SOC Manager

---

# 18. Assessment Framework (Mandatory)

## 18.1 Weekly Assessments

| Week   | Assessment                       | Pass Threshold          |
| ------ | -------------------------------- | ----------------------- |
| Week 1 | Multi-tenant advanced quiz       | 100%                    |
| Week 1 | L1 verification (external hires) | 80%                     |
| Week 2 | Advanced tool quiz               | 85%                     |
| Week 3 | Methodology assessment           | 80%                     |
| Week 4 | SOP quiz                         | 85%                     |
| Week 5 | Playbook practical               | 85%                     |
| Week 6 | Mentor evaluation                | Positive                |
| Week 7 | Pre-certification assessment     | 80% overall             |
| Week 8 | Final certification              | 85% (100% multi-tenant) |

## 18.2 Reassessment Policy

- 1 reassessment allowed per failed assessment
- Reassessment within 1 week
- 2nd failure → extended onboarding (additional 2 weeks)
- 3rd failure → role suitability review

---

# 19. Per-Client Assignment Strategy (Mandatory)

## 19.1 Initial L2 Assignment

| Client Tier                     | New L2 Eligibility                |
| ------------------------------- | --------------------------------- |
| **Tier 1 (Critical/Regulated)** | After 90 days L2 + Tier 2 success |
| **Tier 2 (Standard)**           | After L2 certification            |
| **Tier 3 (Monitoring-only)**    | After L2 certification            |

## 19.2 Specialization Pathways (Post 90 Days)

| Specialization    | Path                                |
| ----------------- | ----------------------------------- |
| Network/Forensics | Additional NDR + forensics training |
| Cloud Security    | Cloud-specific deep training        |
| Threat Hunting    | Advanced hunting certification      |
| Incident Response | L3/IR Team prep program             |

---

# 20. Documentation & Records (Mandatory)

## 20.1 Onboarding Records Maintained

- [ ] L2 onboarding checklist (signed)
- [ ] L2-specific NDAs
- [ ] Multi-tenant advanced quiz result
- [ ] All weekly assessment results
- [ ] Final L2 certification result
- [ ] Shadowing hours log
- [ ] Mentor feedback reports
- [ ] 30-day review report
- [ ] Tenant assignment record
- [ ] Advanced RBAC/ABAC provisioning

## 20.2 Records Retention

| Record                | Retention                        |
| --------------------- | -------------------------------- |
| L2 onboarding records | Duration of employment + 7 years |
| Assessment results    | Duration of employment + 7 years |
| Mentor feedback       | Duration of employment + 3 years |

---

# 21. Quality Checklist (Per New L2 Onboarding)

Before declaring L2 onboarding complete:

- [ ] Full or accelerated program completed
- [ ] All weekly assessments passed
- [ ] Multi-tenant advanced quiz passed at 100%
- [ ] Final L2 certification passed at ≥85%
- [ ] Minimum 24 hours shadowing (full) / 8 hours (accelerated)
- [ ] Minimum 20 hours reverse shadowing (full) / 8 hours (accelerated)
- [ ] First independent L2 shift completed successfully
- [ ] 30-day mentorship plan active
- [ ] Tenant assignment confirmed
- [ ] Advanced RBAC/ABAC verified
- [ ] All documentation captured
- [ ] HR record updated
- [ ] SOC Manager sign-off obtained

---

# 22. Continuous Post-Onboarding Development

| Activity                                   | Frequency     |
| ------------------------------------------ | ------------- |
| Daily mentor check-in                      | First 30 days |
| Weekly performance review                  | First 90 days |
| Monthly investigation case review          | Ongoing       |
| Quarterly tabletop participation (L2 role) | Ongoing       |
| Annual recertification                     | Ongoing       |
| Annual multi-tenant policy refresher       | Ongoing       |
| Career progression review (L3 prep)        | Bi-annually   |

---

# 23. Integration with Other Processes

| Process                      | Integration              |
| ---------------------------- | ------------------------ |
| L1 Onboarding                | Prerequisite knowledge   |
| Multi-Tenant Policy Training | Advanced level mandatory |
| Tool Training                | Advanced features focus  |
| L2 SOPs                      | Week 4 deep dive         |
| Threat Hunting Program       | Week 3+7 training        |
| Per-Client Playbooks         | Week 5 mastery           |
| Tabletop Exercises           | Week 4+7 participation   |
| Mentorship Program           | 8 weeks + 30 days        |
| Certification                | Week 8                   |
| Performance Management       | Probation period         |
| L3 Career Path               | Post-90 days             |

---

# 24. Related Documents

| Document                        | Path                                                                               |
| ------------------------------- | ---------------------------------------------------------------------------------- |
| L2 Analyst Role Definition      | `00_GOVERNANCE/00.3_Roles-and-Responsibilities/L2-Analyst-Role-Definition.md`      |
| L1 Onboarding Program           | `10_TRAINING-AND-EXERCISES/10.1_Onboarding/L1-Onboarding-Program.md`               |
| L3 Onboarding Program           | `10_TRAINING-AND-EXERCISES/10.1_Onboarding/L3-Onboarding-Program.md`               |
| L2 Investigation SOP            | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Investigation-SOP.md`                |
| L2 Escalation Criteria          | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Escalation-Criteria.md`              |
| L2 Evidence Handling SOP        | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Evidence-Handling-SOP.md`            |
| L2 Threat Hunting Procedures    | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Threat-Hunting-Procedures.md`        |
| L2 SIEM Deep Investigation      | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-SIEM-Deep-Investigation.md`          |
| L2 EDR Deep Investigation       | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-EDR-Deep-Investigation.md`           |
| L2 Network Forensics SOP        | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Network-Forensics-SOP.md`            |
| L2 Log Analysis SOP             | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Log-Analysis-SOP.md`                 |
| L2 Shift Handover Template      | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Shift-Handover-Template.md`          |
| Client Data Segregation Policy  | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`  |
| Multi-Client Alert Handling     | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`     |
| Cross-Client Incident Procedure | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md` |
| All L2 Playbook Sections        | `02_PLAYBOOKS/`                                                                    |
| Tabletop Exercise Guide         | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`     |
| Attack Technique Reference      | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Attack-Technique-Reference.md`      |
| MITRE ATT&CK Quick Reference    | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md`    |
| Tool Command Reference          | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Tool-Command-Reference.md`          |
| Common IoC Reference            | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Common-IoC-Reference.md`            |

---

# 25. Revision History

| Version | Date        | Author                          | Changes         |
| ------- | ----------- | ------------------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP SOC Manager / IR Team Lead | Initial version |

---

# 26. Approval

Approved by:

| Role              | Name | Signature | Date |
| ----------------- | ---- | --------- | ---- |
| MSSP IR Team Lead |      |           |      |
| MSSP SOC Manager  |      |           |      |
| MSSP HR Lead      |      |           |      |
| MSSP CISO         |      |           |      |

---

**End of Document**
