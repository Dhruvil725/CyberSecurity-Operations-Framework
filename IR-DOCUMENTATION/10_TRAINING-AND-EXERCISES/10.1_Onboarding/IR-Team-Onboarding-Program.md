# IR Team Onboarding Program

---

# 1. Document Control

| Field          | Value                                        |
| -------------- | -------------------------------------------- |
| Document Name  | IR Team Onboarding Program                   |
| Document ID    | MSSP-TRN-004                                 |
| Version        | 1.0                                          |
| Effective Date | 30-May-2026                                  |
| Owner          | MSSP IR Team Lead / SOC Manager              |
| Approved By    | MSSP CISO                                    |
| Classification | Confidential – MSSP Internal                 |
| Review Cycle   | Annually (or upon IR operating model change) |

---

# 2. Purpose

This document defines the standardized **Incident Response (IR) Team Onboarding Program** governing the structured induction, advanced specialization training, certification, and operational readiness of new IR Team members joining the MSSP — whether external senior IR hires, internal promotions from L3, or specialized transfers — ensuring incident command, crisis coordination, executive communication, regulatory engagement, and full-lifecycle incident handling competency required for the MSSP's most critical incidents and client engagements.

A formal IR Team onboarding program is critical because:

- IR Team members lead the most critical incidents (P1/major) across the MSSP client portfolio
- IR Team decisions determine containment authority, regulatory exposure, legal outcomes, and client trust
- inconsistent IR Team onboarding causes incident command failures, miscommunication, and mishandled escalations
- IR Team members coordinate across SOC tiers, executive stakeholders, clients, regulators, vendors, and legal counsel
- multi-tenant IR requires absolute tenant context discipline at the highest stakes
- onsite and remote IR response require defined procedures and operational readiness
- crisis communication under pressure requires formal training
- regulatory engagement (RBI, CERT-In, DPDP, sector regulators) requires specialized knowledge
- legal counsel coordination and evidence preservation for legal proceedings require formal training
- bridge call leadership during active incidents requires practiced skill
- executive briefings must translate technical complexity into business impact under time pressure
- vendor coordination (forensics retainers, vendor IR, supply chain) requires established protocols
- post-incident review leadership and lessons learned facilitation require formal training
- chain of custody for IR-led evidence collection has legal admissibility implications
- ISO 27001 A.5.24/A.5.26 and NIST CSF RS.MA/RS.CO require formal IR command capability
- RBI Cyber Security Framework and BFSI regulatory expectations require expert IR readiness
- audit and compliance reviews require evidence of IR Team expert competency
- this program is the foundation for IR Team quality and progression to IR Team Lead

This program ensures:

- consistent 12-week structured onboarding for new IR Team members
- 6-week accelerated program for L3-promoted members
- defined expert-level competency milestones with measurable assessments
- crisis coordination and incident command capability
- executive and client communication mastery
- regulatory engagement readiness
- legal counsel coordination capability
- onsite and remote IR response readiness
- multi-tenant IR discipline at executive stakes
- mentorship pairing with IR Team Lead for first 90 days
- formal certification before independent IR Team work
- audit-ready evidence of expert-level training completion
- linkage to IR Team role definition, IRT SOPs, escalation framework, and regulatory communication

**Reference alignment:**

- `00_GOVERNANCE/00.3_Roles-and-Responsibilities/IR-Team-Role-Definition.md`
- `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/`
- `10_TRAINING-AND-EXERCISES/10.1_Onboarding/L3-Onboarding-Program.md`
- `05_ESCALATION-AND-COMMUNICATION/`

---

# 3. Scope

This program applies to all IR Team members joining the MSSP:

| Scope Element                          | Coverage                                  |
| -------------------------------------- | ----------------------------------------- |
| New IR Team hires (external senior)    | Full 12-week program                      |
| L3-to-IR Team promotions (internal)    | Accelerated 6-week program                |
| IR Team transfers (specialist)         | Tailored 8-week program                   |
| IR Team returning (>12 months absence) | Refresher 4-week program                  |
| Per-client IR engagement training      | Per assigned client                       |
| IR command training                    | Bridge calls, war room, decision-making   |
| Crisis communication training          | Executive, client, regulator, press       |
| Legal/regulatory training              | RBI, CERT-In, DPDP, legal coordination    |
| Onsite IR response training            | Travel, equipment, deployment             |
| Remote IR response training            | Remote coordination, tooling              |
| Vendor coordination training           | Forensics retainers, vendor IR            |
| Mentorship                             | Mandatory for first 90 days               |
| Certification                          | Mandatory before independent IR Team work |

Out of scope:

- L1/L2/L3 onboarding (separate programs — L3 is prerequisite)
- IR Team Lead onboarding (separate program with additional leadership modules)
- SOC Manager/Director onboarding (separate program)
- Detection Engineering specialist onboarding (separate program)

---

# 4. Definitions

| Term                       | Definition                                                      |
| -------------------------- | --------------------------------------------------------------- |
| IR Team Member             | MSSP Incident Response Team member (advanced incident handling) |
| L3-Promoted                | L3 analyst promoted to IR Team                                  |
| Incident Commander (IC)    | Person in command during active incident                        |
| Bridge Call                | Active incident coordination call                               |
| War Room                   | Physical or virtual incident coordination space                 |
| Crisis Communication       | Communication during high-pressure incidents                    |
| Regulatory Engagement      | Formal communication with regulators                            |
| Legal Hold                 | Preservation of evidence for legal proceedings                  |
| Onsite IR                  | Physical deployment to client/incident location                 |
| Remote IR                  | Remote-led incident response                                    |
| Vendor IR Coordination     | Coordination with external forensics/IR vendors                 |
| Retainer                   | Pre-arranged third-party IR engagement                          |
| Post-Incident Review (PIR) | Structured lessons-learned session                              |
| Tabletop Exercise (TTX)    | Simulated incident scenario practice                            |
| CCIC                       | Cross-Client Incident Commander                                 |
| Containment Authority      | Decision authority for containment actions                      |

---

# 5. Roles and Responsibilities

| Role                               | Responsibilities                                      |
| ---------------------------------- | ----------------------------------------------------- |
| **MSSP IR Team Lead**              | Program ownership; mentor assignment; IR methodology  |
| **MSSP SOC Manager**               | Certification approval; performance oversight         |
| **MSSP CISO**                      | Final certification approval for IR Team              |
| **MSSP Senior IR Team Member**     | Mentor role for new IR Team                           |
| **MSSP Threat Intel Lead**         | TI integration in IR; attribution support             |
| **MSSP Compliance Lead**           | Regulatory engagement training                        |
| **MSSP Legal Counsel**             | Legal coordination training; legal hold               |
| **MSSP HR Lead**                   | Logistics; documentation; performance management      |
| **MSSP IT Lead**                   | IR tool access; onsite kit provisioning               |
| **MSSP SDM Leads**                 | Per-client briefing                                   |
| **External IR Trainer (optional)** | Specialized training (crisis management, IC)          |
| **New IR Team Member**             | Active participation; assessment completion; feedback |
| **Buddy IR Team Member**           | Peer support during first 90 days                     |

---

# 6. Onboarding Program Principles (Mandatory)

| Principle                        | Requirement                                                 |
| -------------------------------- | ----------------------------------------------------------- |
| **Builds on L3 Foundation**      | L3 knowledge prerequisite (internal) or verified (external) |
| **Incident Command Focus**       | Leadership and coordination as primary skill                |
| **Multi-Tenant IR Discipline**   | Strict tenant segregation at highest stakes                 |
| **Crisis Readiness**             | Composure and decision-making under pressure                |
| **Communication Excellence**     | Executive, client, regulator, legal mastery                 |
| **Mentorship Mandatory**         | Senior IR Team / IR Team Lead pairing first 90 days         |
| **Hands-On Heavy**               | Tabletop, simulation, supervised live IR                    |
| **Assessment-Based Progression** | Pass/fail at each milestone                                 |
| **Legal/Regulatory Awareness**   | Regulatory and legal standards mastered                     |
| **Documentation Excellence**     | All IR actions auditable                                    |
| **Audit-Ready Records**          | Complete training documentation                             |
| **24x7 Readiness**               | On-call IR Team rotation participation                      |

---

# 7. IR Team Onboarding Program Overview (12 Weeks Full / 6 Weeks Accelerated)

FULL PROGRAM (External IR Team Hire):

Week 1: FOUNDATION & ORIENTATION
├── HR + admin + NDAs
├── MSSP organization + multi-tenant (IR Team perspective)
├── L1/L2/L3 foundational verification
└── IR Team role expectations

Week 2: IR FRAMEWORK & GOVERNANCE
├── IR Policy Master + framework alignments
├── IR Team activation criteria
├── Incident severity matrix mastery
└── Cross-Client Incident Procedure (CCIC)

Week 3: INCIDENT COMMAND & COORDINATION
├── Incident Command (IC) methodology
├── Bridge call leadership
├── War room operations
├── Decision-making under pressure
└── Containment authority matrix

Week 4: CRISIS COMMUNICATION
├── Executive communication
├── Client communication
├── Regulatory communication
├── Legal counsel coordination
└── Press/external (with PR)

Week 5: REGULATORY ENGAGEMENT
├── RBI engagement protocols
├── CERT-In reporting
├── DPDP engagement
├── Sector-specific regulators
└── International regulators (where applicable)

Week 6: LEGAL & EVIDENCE COORDINATION
├── Legal hold procedures
├── Legal evidence preservation
├── Law enforcement coordination
├── Litigation support readiness
└── Privilege considerations

Week 7: ONSITE & REMOTE IR RESPONSE
├── IRT Onsite Response SOP
├── IRT Remote Response SOP
├── Onsite IR kit
├── Travel logistics
└── Remote war room setup

Week 8: VENDOR COORDINATION & RETAINERS
├── Forensics retainer engagement
├── Vendor IR coordination
├── Supply chain incident vendor coordination
├── Cloud provider escalations
└── Threat intel vendor engagement

Week 9: PLAYBOOK MASTERY (IR TEAM SECTIONS)
├── IR Team sections of all playbooks
├── Per-client IR procedures
├── APT/Zero-day IR command
└── Major incident coordination

Week 10: POST-INCIDENT EXCELLENCE
├── Post-Incident Review leadership
├── Lessons Learned facilitation
├── RCA leadership
├── Improvement tracking ownership
└── Threat intel output coordination

Week 11: SHADOWING & SUPERVISED IR
├── IR Team Lead shadowing
├── Reverse shadowing
├── Supervised live IR engagements
└── Tabletop leadership exercises

Week 12: CERTIFICATION & ON-CALL READINESS
├── Final IR Team certification
├── Tenant assignment confirmation
├── First on-call rotation
└── 90-day mentor pairing continues

ACCELERATED PROGRAM (L3-Promoted to IR Team):

Week 1: TRANSITION & IR FRAMEWORK
├── L3-to-IR Team transition briefing
├── IR Policy + framework alignment
├── IR Team activation criteria
└── CCIC / multi-tenant IR

Week 2: INCIDENT COMMAND & CRISIS COMMS
├── IC methodology + bridge calls
├── War room ops
├── Executive + client + regulator comms
└── Legal coordination

Week 3: REGULATORY + LEGAL + EVIDENCE
├── Regulatory engagement (compressed)
├── Legal hold + evidence preservation
└── Vendor coordination

Week 4: ONSITE/REMOTE IR + PLAYBOOKS
├── Onsite + remote response SOPs
├── IR Team playbook sections (all)
└── Per-client IR procedures

Week 5: SHADOWING & SUPERVISED IR
├── IR Team Lead shadowing
├── Reverse shadowing
├── Supervised live IR (2 cases)
└── Tabletop leadership

Week 6: CERTIFICATION & ON-CALL
├── Pre-certification assessment
├── Final IR Team certification
├── First on-call rotation
└── 90-day mentor pairing begins

---

# 8. Week 1: Foundation & Orientation (Mandatory)

## 8.1 Day 1 – Admin & Welcome

| Activity                               | Duration | Owner        |
| -------------------------------------- | -------- | ------------ |
| HR orientation (external hires only)   | 2 hours  | HR           |
| Equipment + IR-grade workstation setup | 2 hours  | IT           |
| MSSP organization (external hires)     | 1 hour   | SOC Manager  |
| IR Team role expectations briefing     | 2 hours  | IR Team Lead |
| Mentor introduction (Senior IR Team)   | 1 hour   | Mentor       |

## 8.2 Day 2 – Multi-Tenant IR Discipline

| Activity                                        | Duration | Owner           |
| ----------------------------------------------- | -------- | --------------- |
| Client Data Segregation Policy (IR perspective) | 2 hours  | Compliance Lead |
| Cross-tenant IR prohibitions and exceptions     | 2 hours  | Compliance Lead |
| CCIC role and coordination                      | 2 hours  | IR Team Lead    |
| **Multi-tenant IR quiz (must pass 100%)**       | 1 hour   | Compliance Lead |

**⚠️ Critical Gate:** Cannot proceed without 100% on multi-tenant IR quiz.

## 8.3 Day 3 – L1/L2/L3 Foundational Verification (External Hires)

| Activity                            | Duration  | Owner                      |
| ----------------------------------- | --------- | -------------------------- |
| L1+L2+L3 comprehensive verification | 4 hours   | SOC Manager + IR Team Lead |
| Tool proficiency verification       | 3 hours   | Detection Engineer         |
| Gap remediation plan                | As needed | Mentor                     |

*(L3-promoted members skip this day)*

## 8.4 Day 4 – IR Team Role Deep Dive

| Activity                          | Duration | Owner        |
| --------------------------------- | -------- | ------------ |
| IR Team Role Definition deep dive | 2 hours  | IR Team Lead |
| IR Team Activation Criteria       | 2 hours  | IR Team Lead |
| IR Team on-call rotation          | 1 hour   | IR Team Lead |
| IR Team escalation paths          | 1 hour   | IR Team Lead |

## 8.5 Day 5 – IR Tool & Process Landscape

| Activity               | Duration | Owner                 |
| ---------------------- | -------- | --------------------- |
| IR tooling overview    | 2 hours  | IT Lead               |
| Bridge call platforms  | 1 hour   | IR Team Lead          |
| War room setup         | 1 hour   | IR Team Lead          |
| Onsite IR kit overview | 1 hour   | IR Team Lead          |
| Week 1 retrospective   | 1 hour   | Mentor + IR Team Lead |

### Week 1 Completion Criteria

- [ ] All admin setup completed
- [ ] IR Team-specific NDAs signed
- [ ] Multi-tenant IR quiz passed (100%)
- [ ] L1/L2/L3 verification completed (external hires)
- [ ] IR Team role expectations understood
- [ ] Mentor pairing confirmed

---

# 9. Week 2: IR Framework & Governance (Mandatory)

## 9.1 IR Policy & Framework Alignments

| Topic                            | Duration | Owner           |
| -------------------------------- | -------- | --------------- |
| IR Policy Master                 | 2 hours  | IR Team Lead    |
| IR Policy NIST Alignment         | 1 hour   | Compliance Lead |
| IR Policy ISO27001 Alignment     | 1 hour   | Compliance Lead |
| IR Policy RBI Alignment          | 1 hour   | Compliance Lead |
| NIST SP 800-61 lifecycle mastery | 2 hours  | IR Team Lead    |

## 9.2 IR Team Activation

| Topic                                 | Duration | Owner        |
| ------------------------------------- | -------- | ------------ |
| IRT Activation Criteria               | 2 hours  | IR Team Lead |
| Activation triggers and decision tree | 1 hour   | IR Team Lead |
| Activation communication              | 1 hour   | IR Team Lead |
| **Hands-on: 5 activation scenarios**  | 4 hours  | Mentor       |

## 9.3 Incident Severity Mastery

| Topic                                              | Duration | Owner           |
| -------------------------------------------------- | -------- | --------------- |
| Severity Classification Guide                      | 2 hours  | SOC Manager     |
| P1/P2/P3/P4 definitions deep dive                  | 2 hours  | SOC Manager     |
| Severity escalation criteria                       | 1 hour   | SOC Manager     |
| Per-client severity overrides                      | 1 hour   | Compliance Lead |
| **Hands-on: 10 severity classification exercises** | 4 hours  | Mentor          |

## 9.4 Cross-Client Incident Procedure (CCIC)

| Topic                                     | Duration | Owner             |
| ----------------------------------------- | -------- | ----------------- |
| Cross-Client Incident Procedure deep dive | 3 hours  | IR Team Lead      |
| CCIC role responsibilities                | 2 hours  | IR Team Lead      |
| Portfolio assessment methodology          | 2 hours  | IR Team Lead      |
| Sanitized cross-client coordination       | 2 hours  | Threat Intel Lead |

### Week 2 Completion Criteria

- [ ] All IR framework documents reviewed
- [ ] IRT activation criteria mastered
- [ ] Severity classification demonstrated
- [ ] CCIC procedure understood
- [ ] Framework assessment passed (≥85%)

---

# 10. Week 3: Incident Command & Coordination (Mandatory)

## 10.1 Incident Command Methodology

| Topic                                  | Duration | Owner        |
| -------------------------------------- | -------- | ------------ |
| IC role and authority                  | 2 hours  | IR Team Lead |
| IC decision framework                  | 3 hours  | IR Team Lead |
| IC under pressure (composure training) | 2 hours  | IR Team Lead |
| IC handoff procedures                  | 1 hour   | IR Team Lead |
| ICS (Incident Command System) basics   | 2 hours  | IR Team Lead |

## 10.2 Bridge Call Leadership

| Topic                                  | Duration | Owner        |
| -------------------------------------- | -------- | ------------ |
| Bridge Call Agenda Template            | 1 hour   | SOC Lead     |
| SOC Lead P1/P2 Bridge Call SOP         | 2 hours  | SOC Lead     |
| Bridge call facilitation skills        | 2 hours  | IR Team Lead |
| Stakeholder management on bridges      | 2 hours  | IR Team Lead |
| **Hands-on: 3 simulated bridge calls** | 6 hours  | Mentor       |

## 10.3 War Room Operations

| Topic                             | Duration | Owner        |
| --------------------------------- | -------- | ------------ |
| War room physical/virtual setup   | 1 hour   | IR Team Lead |
| War room roles and assignments    | 1 hour   | IR Team Lead |
| War room information flow         | 1 hour   | IR Team Lead |
| War room documentation            | 1 hour   | IR Team Lead |
| **Hands-on: war room simulation** | 4 hours  | Mentor       |

## 10.4 Decision-Making Under Pressure

| Topic                                     | Duration | Owner        |
| ----------------------------------------- | -------- | ------------ |
| OODA loop methodology                     | 2 hours  | IR Team Lead |
| Time-boxed decision frameworks            | 2 hours  | IR Team Lead |
| Recognition-primed decision making        | 1 hour   | IR Team Lead |
| **Hands-on: decision-making simulations** | 3 hours  | Mentor       |

## 10.5 Containment Authority Matrix

| Topic                              | Duration | Owner           |
| ---------------------------------- | -------- | --------------- |
| IRT Containment Authority Matrix   | 2 hours  | IR Team Lead    |
| Per-client containment authority   | 2 hours  | Compliance Lead |
| Containment decision documentation | 1 hour   | IR Team Lead    |
| Containment escalation paths       | 1 hour   | IR Team Lead    |

### Week 3 Completion Criteria

- [ ] IC methodology demonstrated
- [ ] Bridge call simulations completed
- [ ] War room simulation completed
- [ ] Decision-making simulations completed
- [ ] Containment authority mastered
- [ ] IC assessment passed (≥85%)

---

# 11. Week 4: Crisis Communication (Mandatory)

## 11.1 Executive Communication

| Topic                               | Duration | Owner        |
| ----------------------------------- | -------- | ------------ |
| Management Notification Template    | 1 hour   | IR Team Lead |
| Executive briefing methodology      | 2 hours  | IR Team Lead |
| Translating technical → business    | 2 hours  | IR Team Lead |
| Risk articulation under pressure    | 2 hours  | IR Team Lead |
| **Hands-on: 3 executive briefings** | 4 hours  | Mentor       |

## 11.2 Client Communication

| Topic                                  | Duration | Owner        |
| -------------------------------------- | -------- | ------------ |
| MSSP Client Notification Template      | 1 hour   | SDM Lead     |
| Client escalation communication        | 2 hours  | IR Team Lead |
| Client trust preservation under crisis | 2 hours  | SDM Lead     |
| Per-client communication preferences   | 2 hours  | SDM Lead     |
| **Hands-on: 3 client communications**  | 4 hours  | Mentor       |

## 11.3 Regulatory Communication

| Topic                                     | Duration | Owner           |
| ----------------------------------------- | -------- | --------------- |
| Regulatory communication standards        | 2 hours  | Compliance Lead |
| Tone and content for regulators           | 1 hour   | Compliance Lead |
| Avoiding admissions/over-disclosure       | 2 hours  | Legal Counsel   |
| **Hands-on: 2 regulatory communications** | 3 hours  | Compliance Lead |

## 11.4 Legal Counsel Coordination

| Topic                               | Duration | Owner         |
| ----------------------------------- | -------- | ------------- |
| Legal Counsel Engagement SOP        | 2 hours  | Legal Counsel |
| Attorney-client privilege awareness | 2 hours  | Legal Counsel |
| Legal hold processes                | 2 hours  | Legal Counsel |
| When to involve legal counsel       | 1 hour   | Legal Counsel |

## 11.5 Press/External (with PR)

| Topic                                   | Duration | Owner                   |
| --------------------------------------- | -------- | ----------------------- |
| Public statement coordination           | 1 hour   | Legal/PR                |
| Social media monitoring during incident | 1 hour   | Threat Intel Lead       |
| Reputation management basics            | 1 hour   | PR Lead (if applicable) |

### Week 4 Completion Criteria

- [ ] Executive communication demonstrated
- [ ] Client communication demonstrated
- [ ] Regulatory communication demonstrated
- [ ] Legal coordination understood
- [ ] Communication assessment passed (≥85%)

---

# 12. Week 5: Regulatory Engagement (Mandatory)

## 12.1 RBI Engagement (BFSI Clients)

| Topic                            | Duration | Owner           |
| -------------------------------- | -------- | --------------- |
| RBI Cyber Security Framework     | 2 hours  | Compliance Lead |
| RBI Incident Reporting SOP       | 2 hours  | Compliance Lead |
| RBI Report Template usage        | 1 hour   | Compliance Lead |
| RBI reporting timelines          | 1 hour   | Compliance Lead |
| **Hands-on: write 1 RBI report** | 3 hours  | Compliance Lead |

## 12.2 CERT-In Reporting

| Topic                                | Duration | Owner           |
| ------------------------------------ | -------- | --------------- |
| CERT-In Reporting SOP                | 2 hours  | Compliance Lead |
| 6-hour reporting timeline            | 1 hour   | Compliance Lead |
| CERT-In log retention requirements   | 1 hour   | Compliance Lead |
| **Hands-on: write 1 CERT-In report** | 2 hours  | Compliance Lead |

## 12.3 DPDP Engagement

| Topic                                      | Duration | Owner         |
| ------------------------------------------ | -------- | ------------- |
| DPDP Act overview                          | 2 hours  | Legal Counsel |
| Data breach notification under DPDP        | 2 hours  | Legal Counsel |
| DPO coordination                           | 1 hour   | Legal Counsel |
| **Hands-on: 1 DPDP notification exercise** | 2 hours  | Legal Counsel |

## 12.4 Sector-Specific Regulators

| Topic                                     | Duration | Owner           |
| ----------------------------------------- | -------- | --------------- |
| SEBI engagement (capital markets clients) | 1 hour   | Compliance Lead |
| IRDAI engagement (insurance clients)      | 1 hour   | Compliance Lead |
| NCIIPC engagement (CII clients)           | 1 hour   | Compliance Lead |
| Sector-specific timelines                 | 1 hour   | Compliance Lead |

## 12.5 International Regulators (Where Applicable)

| Topic                              | Duration | Owner         |
| ---------------------------------- | -------- | ------------- |
| GDPR notification basics           | 1 hour   | Legal Counsel |
| Other privacy regimes (CCPA, etc.) | 1 hour   | Legal Counsel |

### Week 5 Completion Criteria

- [ ] RBI engagement demonstrated
- [ ] CERT-In reporting demonstrated
- [ ] DPDP notification demonstrated
- [ ] Sector-specific awareness confirmed
- [ ] Regulatory assessment passed (≥85%)

---

# 13. Week 6: Legal & Evidence Coordination (Mandatory)

## 13.1 Legal Hold Procedures

| Topic                           | Duration | Owner         |
| ------------------------------- | -------- | ------------- |
| Legal hold concept and triggers | 2 hours  | Legal Counsel |
| Issuing legal hold notices      | 2 hours  | Legal Counsel |
| Legal hold scope determination  | 2 hours  | Legal Counsel |
| Legal hold tracking             | 1 hour   | Legal Counsel |

## 13.2 Legal Evidence Preservation

| Topic                                | Duration | Owner                        |
| ------------------------------------ | -------- | ---------------------------- |
| Evidence preservation for litigation | 2 hours  | Legal Counsel + IR Team Lead |
| Spoliation risks                     | 1 hour   | Legal Counsel                |
| Forensic-grade preservation          | 2 hours  | IR Team Lead                 |
| Per-tenant evidence preservation     | 1 hour   | Compliance Lead              |

## 13.3 Law Enforcement Coordination

| Topic                               | Duration | Owner                |
| ----------------------------------- | -------- | -------------------- |
| Law enforcement engagement decision | 2 hours  | Legal Counsel + CISO |
| Law enforcement contact protocols   | 1 hour   | Legal Counsel        |
| Information sharing limits          | 1 hour   | Legal Counsel        |
| Law enforcement subpoena response   | 2 hours  | Legal Counsel        |

## 13.4 Litigation Support Readiness

| Topic                               | Duration | Owner         |
| ----------------------------------- | -------- | ------------- |
| Expert witness considerations       | 2 hours  | Legal Counsel |
| Deposition preparation basics       | 2 hours  | Legal Counsel |
| Court-admissible evidence standards | 2 hours  | Legal Counsel |
| Documentation for litigation        | 1 hour   | Legal Counsel |

## 13.5 Privilege Considerations

| Topic                                | Duration | Owner         |
| ------------------------------------ | -------- | ------------- |
| Attorney-client privilege protection | 2 hours  | Legal Counsel |
| Work product doctrine                | 1 hour   | Legal Counsel |
| Privileged communications during IR  | 2 hours  | Legal Counsel |

### Week 6 Completion Criteria

- [ ] Legal hold procedures mastered
- [ ] Evidence preservation demonstrated
- [ ] Law enforcement protocols understood
- [ ] Privilege considerations applied
- [ ] Legal assessment passed (≥85%)

---

# 14. Week 7: Onsite & Remote IR Response (Mandatory)

## 14.1 Onsite IR Response

| Topic                      | Duration | Owner        |
| -------------------------- | -------- | ------------ |
| IRT Onsite Response SOP    | 3 hours  | IR Team Lead |
| Onsite deployment criteria | 1 hour   | IR Team Lead |
| Onsite logistics planning  | 2 hours  | IR Team Lead |
| Onsite-client coordination | 2 hours  | SDM Lead     |

## 14.2 Onsite IR Kit

| Topic                          | Duration | Owner        |
| ------------------------------ | -------- | ------------ |
| Onsite kit inventory           | 1 hour   | IR Team Lead |
| Forensics equipment for travel | 2 hours  | IR Team Lead |
| Network/connectivity equipment | 1 hour   | IR Team Lead |
| Communication equipment        | 1 hour   | IR Team Lead |
| Kit deployment readiness       | 1 hour   | IR Team Lead |

## 14.3 Travel Logistics

| Topic                              | Duration | Owner             |
| ---------------------------------- | -------- | ----------------- |
| Travel approval process            | 1 hour   | HR + IR Team Lead |
| Visa/travel documentation          | 1 hour   | HR                |
| Per-diem and expense protocols     | 1 hour   | Finance           |
| Cross-border travel considerations | 1 hour   | Legal Counsel     |

## 14.4 Remote IR Response

| Topic                      | Duration | Owner              |
| -------------------------- | -------- | ------------------ |
| IRT Remote Response SOP    | 3 hours  | IR Team Lead       |
| Remote command capability  | 2 hours  | IR Team Lead       |
| Remote tool deployment     | 2 hours  | Detection Engineer |
| Remote-client coordination | 2 hours  | SDM Lead           |

## 14.5 Remote War Room Setup

| Topic                          | Duration | Owner        |
| ------------------------------ | -------- | ------------ |
| Virtual war room platforms     | 1 hour   | IR Team Lead |
| Remote evidence access         | 1 hour   | IR Team Lead |
| Remote bridge call hosting     | 1 hour   | IR Team Lead |
| Remote documentation workflows | 1 hour   | IR Team Lead |

### Week 7 Completion Criteria

- [ ] Onsite IR SOP demonstrated
- [ ] Onsite kit familiarity confirmed
- [ ] Remote IR SOP demonstrated
- [ ] Remote war room setup demonstrated
- [ ] Deployment assessment passed (≥85%)

---

# 15. Week 8: Vendor Coordination & Retainers (Mandatory)

## 15.1 Forensics Retainer Engagement

| Topic                                        | Duration | Owner                  |
| -------------------------------------------- | -------- | ---------------------- |
| Third-Party IR Retainer Contacts             | 1 hour   | IR Team Lead           |
| Retainer activation procedures               | 2 hours  | IR Team Lead           |
| Retainer scope and SLAs                      | 1 hour   | IR Team Lead           |
| Retainer cost authorization                  | 1 hour   | IR Team Lead + Finance |
| **Hands-on: retainer activation simulation** | 2 hours  | Mentor                 |

## 15.2 Vendor IR Coordination

| Topic                                   | Duration | Owner         |
| --------------------------------------- | -------- | ------------- |
| Vendor incident coordination            | 2 hours  | IR Team Lead  |
| Supply chain incident coordination      | 2 hours  | IR Team Lead  |
| Information sharing limits with vendors | 1 hour   | Legal Counsel |
| Joint investigation protocols           | 1 hour   | IR Team Lead  |

## 15.3 Supply Chain Incident Vendor Coordination

| Topic                                     | Duration | Owner         |
| ----------------------------------------- | -------- | ------------- |
| Supply chain attack response              | 2 hours  | IR Team Lead  |
| Vendor liability considerations           | 1 hour   | Legal Counsel |
| Cross-tenant supply chain impact          | 2 hours  | IR Team Lead  |
| Vendor engagement during portfolio impact | 1 hour   | IR Team Lead  |

## 15.4 Cloud Provider Escalations

| Topic                            | Duration | Owner            |
| -------------------------------- | -------- | ---------------- |
| AWS incident escalation          | 1 hour   | Cloud Specialist |
| Azure incident escalation        | 1 hour   | Cloud Specialist |
| GCP incident escalation          | 1 hour   | Cloud Specialist |
| Cloud provider evidence requests | 1 hour   | Legal Counsel    |

## 15.5 Threat Intel Vendor Engagement

| Topic                          | Duration | Owner             |
| ------------------------------ | -------- | ----------------- |
| TI vendor engagement during IR | 2 hours  | Threat Intel Lead |
| Premium TI request protocols   | 1 hour   | Threat Intel Lead |
| TI vendor confidentiality      | 1 hour   | Threat Intel Lead |

### Week 8 Completion Criteria

- [ ] Retainer activation simulated
- [ ] Vendor coordination procedures understood
- [ ] Cloud provider escalation paths known
- [ ] TI vendor engagement understood
- [ ] Vendor assessment passed (≥80%)

---

# 16. Week 9: Playbook Mastery (IR Team Sections) (Mandatory)

## 16.1 IR Team Sections of All Playbooks

| Playbook                                | Duration | Owner        |
| --------------------------------------- | -------- | ------------ |
| Ransomware Master Playbook (IR command) | 3 hours  | IR Team Lead |
| Phishing/BEC Master (IR command)        | 2 hours  | IR Team Lead |
| Malware Master (IR command)             | 2 hours  | IR Team Lead |
| DDoS Master + ISP coordination          | 2 hours  | IR Team Lead |
| Insider Threat + HR/Legal coordination  | 3 hours  | IR Team Lead |
| Data Breach + Legal/Regulatory          | 3 hours  | IR Team Lead |
| Credential Attack Master                | 2 hours  | IR Team Lead |
| Web Application Master                  | 2 hours  | IR Team Lead |
| Supply Chain Master                     | 3 hours  | IR Team Lead |
| Cloud Master                            | 3 hours  | IR Team Lead |
| Network Intrusion Master                | 2 hours  | IR Team Lead |
| Zero-Day Master                         | 3 hours  | IR Team Lead |
| APT Master                              | 4 hours  | IR Team Lead |
| Physical Security Master                | 2 hours  | IR Team Lead |

## 16.2 Per-Client IR Procedures

| Topic                                             | Duration | Owner           |
| ------------------------------------------------- | -------- | --------------- |
| Per-client IR policies (deep)                     | 3 hours  | SOC Manager     |
| Per-client escalation matrices                    | 2 hours  | SDM Lead        |
| Per-client custom playbooks (IR command sections) | 4 hours  | IR Team Lead    |
| Per-client legal/regulatory context               | 2 hours  | Compliance Lead |
| Per-client containment authority                  | 2 hours  | IR Team Lead    |

## 16.3 APT/Zero-Day IR Command

| Topic                               | Duration | Owner                            |
| ----------------------------------- | -------- | -------------------------------- |
| APT campaign IR command             | 3 hours  | IR Team Lead + Threat Intel Lead |
| Long-term monitoring coordination   | 2 hours  | Threat Intel Lead                |
| Zero-day IR command                 | 3 hours  | IR Team Lead                     |
| Vendor coordination during zero-day | 2 hours  | IR Team Lead                     |

## 16.4 Major Incident Coordination

| Topic                            | Duration | Owner        |
| -------------------------------- | -------- | ------------ |
| P1 incident command end-to-end   | 4 hours  | IR Team Lead |
| Multi-party coordination         | 2 hours  | IR Team Lead |
| Multi-client (CCIC) coordination | 2 hours  | IR Team Lead |
| Closure criteria management      | 1 hour   | IR Team Lead |

### Week 9 Completion Criteria

- [ ] All IR Team playbook sections reviewed
- [ ] Per-client IR procedures mastered
- [ ] APT/Zero-day IR command demonstrated
- [ ] Major incident coordination demonstrated
- [ ] Playbook practical assessment passed (≥85%)

---

# 17. Week 10: Post-Incident Excellence (Mandatory)

## 17.1 Post-Incident Review Leadership

| Topic                              | Duration | Owner        |
| ---------------------------------- | -------- | ------------ |
| PIR Meeting Agenda                 | 1 hour   | IR Team Lead |
| PIR facilitation skills            | 2 hours  | IR Team Lead |
| Blameless PIR principles           | 2 hours  | IR Team Lead |
| PIR documentation standards        | 1 hour   | IR Team Lead |
| **Hands-on: lead 1 simulated PIR** | 3 hours  | Mentor       |

## 17.2 Lessons Learned Facilitation

| Topic                                    | Duration | Owner        |
| ---------------------------------------- | -------- | ------------ |
| Lessons Learned Template usage           | 1 hour   | IR Team Lead |
| Lessons Learned Register                 | 1 hour   | IR Team Lead |
| Action Items Tracker                     | 1 hour   | IR Team Lead |
| Cross-client lessons learned (sanitized) | 2 hours  | IR Team Lead |

## 17.3 RCA Leadership

| Topic                          | Duration | Owner        |
| ------------------------------ | -------- | ------------ |
| RCA leadership vs L3 execution | 2 hours  | IR Team Lead |
| RCA report review and approval | 1 hour   | IR Team Lead |
| RCA-to-improvement conversion  | 1 hour   | IR Team Lead |

## 17.4 Improvement Tracking Ownership

| Topic                         | Duration | Owner              |
| ----------------------------- | -------- | ------------------ |
| Security Improvement Register | 1 hour   | Compliance Lead    |
| Control Gap Tracker           | 1 hour   | Compliance Lead    |
| Playbook Update Log           | 1 hour   | IR Team Lead       |
| Detection Improvement Log     | 1 hour   | Detection Engineer |

## 17.5 Threat Intel Output Coordination

| Topic                            | Duration | Owner             |
| -------------------------------- | -------- | ----------------- |
| IoC Output Register              | 1 hour   | Threat Intel Lead |
| TTP Intelligence Report          | 1 hour   | Threat Intel Lead |
| Threat Actor Profile             | 1 hour   | Threat Intel Lead |
| Sanitization for cross-client TI | 2 hours  | Threat Intel Lead |

### Week 10 Completion Criteria

- [ ] PIR leadership simulated
- [ ] Lessons learned process mastered
- [ ] RCA leadership understood
- [ ] Improvement tracking ownership accepted
- [ ] TI output coordination demonstrated
- [ ] Post-incident assessment passed (≥85%)

---

# 18. Week 11: Shadowing & Supervised IR (Mandatory)

## 18.1 Active IR Team Lead Shadowing

| Activity                          | Duration   | Owner                 |
| --------------------------------- | ---------- | --------------------- |
| Active shadowing of IR Team Lead  | 30 hours   | Mentor / IR Team Lead |
| Live IR engagement observation    | Continuous | Mentor                |
| Bridge call observation           | Continuous | Mentor                |
| Executive briefing observation    | Continuous | Mentor                |
| Regulatory engagement observation | Continuous | Mentor                |

## 18.2 Reverse Shadowing

| Activity                                   | Duration       | Owner  |
| ------------------------------------------ | -------------- | ------ |
| New IR Team member leads under observation | 25 hours       | Mentor |
| Real-time feedback                         | Continuous     | Mentor |
| End-of-engagement debrief                  | Per engagement | Mentor |

## 18.3 Supervised Live IR Engagements

| Activity                            | Duration     | Owner                 |
| ----------------------------------- | ------------ | --------------------- |
| Supervised live IR (2 engagements)  | 20 hours     | Mentor + IR Team Lead |
| Decision authority verification     | Per decision | Mentor                |
| Documentation review per engagement | Mandatory    | Mentor                |

## 18.4 Tabletop Leadership Exercises

| Exercise                | Duration | Owner        |
| ----------------------- | -------- | ------------ |
| Lead Ransomware TTX     | 3 hours  | IR Team Lead |
| Lead APT TTX            | 3 hours  | IR Team Lead |
| Lead Insider Threat TTX | 3 hours  | IR Team Lead |
| Lead Data Breach TTX    | 3 hours  | IR Team Lead |

### Week 11 Completion Criteria

- [ ] Minimum 30 hours active shadowing completed
- [ ] Minimum 25 hours reverse shadowing completed
- [ ] Minimum 2 supervised live IR engagements completed
- [ ] 4 tabletop leadership exercises completed
- [ ] Mentor positive evaluation

---

# 19. Week 12: Certification & On-Call Readiness (Mandatory)

## 19.1 Final IR Team Certification Assessment

| Component                                            | Pass Threshold        |
| ---------------------------------------------------- | --------------------- |
| Written exam (all IR Team SOPs/playbooks/procedures) | 85%                   |
| Multi-tenant IR exam                                 | 100% (must pass)      |
| Incident Command practical                           | 85%                   |
| Bridge call leadership practical                     | 85%                   |
| Executive briefing practical                         | 85%                   |
| Regulatory engagement assessment                     | 85%                   |
| Legal coordination assessment                        | 80%                   |
| Onsite/Remote IR deployment assessment               | 85%                   |
| Per-client IR knowledge assessment                   | 85%                   |
| Tabletop leadership assessment                       | Pass/Fail (must pass) |

## 19.2 Tenant Assignment Confirmation

| Activity                            | Owner                             |
| ----------------------------------- | --------------------------------- |
| Assigned client portfolio finalized | SOC Manager + IR Team Lead + CISO |
| IR-grade RBAC/ABAC verified         | IT Lead                           |
| Per-client IR access tested         | New IR + Mentor                   |
| On-call rotation slot confirmed     | IR Team Lead                      |

## 19.3 First On-Call Rotation

| Activity                               | Duration              | Owner        |
| -------------------------------------- | --------------------- | ------------ |
| First on-call shift (mentor on backup) | Full rotation         | New IR Team  |
| Mentor backup availability             | Throughout            | Mentor       |
| On-call shift review                   | 2 hours post-rotation | IR Team Lead |

## 19.4 90-Day Continued Mentorship

| Activity                   | Cadence               | Owner                             |
| -------------------------- | --------------------- | --------------------------------- |
| Daily mentor check-in      | Daily for 30 days     | Mentor                            |
| Weekly mentor check-in     | Weekly for days 31-90 | Mentor                            |
| Weekly IR Team Lead review | Weekly for 90 days    | IR Team Lead                      |
| Monthly SOC Manager review | Monthly for 90 days   | SOC Manager                       |
| 90-day formal review       | Day 90                | SOC Manager + IR Team Lead + CISO |

### Week 12 Completion Criteria

- [ ] Final IR Team certification passed (≥85%)
- [ ] Multi-tenant IR exam passed at 100%
- [ ] Tenant assignment confirmed
- [ ] First on-call rotation completed successfully
- [ ] 90-day mentorship plan documented
- [ ] CISO sign-off obtained

---

# 20. Accelerated Program for L3-Promoted (6 Weeks)

## 20.1 Week 1 (Accelerated): Transition & IR Framework

| Day     | Focus                                                |
| ------- | ---------------------------------------------------- |
| Day 1   | L3-to-IR Team transition + multi-tenant IR           |
| Day 2-3 | IR Policy + framework alignment + IR Team activation |
| Day 4-5 | CCIC + multi-tenant IR scenarios                     |

## 20.2 Week 2 (Accelerated): IC & Crisis Comms

| Day     | Focus                                    |
| ------- | ---------------------------------------- |
| Day 1-2 | IC methodology + bridge calls + war room |
| Day 3-4 | Executive + client communication         |
| Day 5   | Regulatory + legal coordination          |

## 20.3 Week 3 (Accelerated): Regulatory + Legal + Evidence

| Day     | Focus                              |
| ------- | ---------------------------------- |
| Day 1-2 | RBI + CERT-In + DPDP (compressed)  |
| Day 3   | Legal hold + evidence preservation |
| Day 4-5 | Vendor coordination + retainers    |

## 20.4 Week 4 (Accelerated): Onsite/Remote + Playbooks

| Day     | Focus                           |
| ------- | ------------------------------- |
| Day 1-2 | Onsite + remote response SOPs   |
| Day 3-5 | IR Team playbook sections (all) |

## 20.5 Week 5 (Accelerated): Shadowing & Supervised IR

| Day     | Focus                                                    |
| ------- | -------------------------------------------------------- |
| Day 1-3 | IR Team Lead shadowing                                   |
| Day 4-5 | Supervised live IR (2 engagements) + tabletop leadership |

## 20.6 Week 6 (Accelerated): Certification & On-Call

| Day     | Focus                                             |
| ------- | ------------------------------------------------- |
| Day 1-2 | Pre-certification preparation                     |
| Day 3   | Pre-certification assessment                      |
| Day 4   | Final IR Team certification                       |
| Day 5   | First on-call rotation + 90-day mentorship begins |

---

# 21. Mentor Program (Mandatory)

## 21.1 Mentor Selection Criteria for IR Team Onboarding

| Criterion                    | Requirement                                       |
| ---------------------------- | ------------------------------------------------- |
| Tenure                       | Minimum 2 years IR Team or IR Team Lead           |
| IR engagement experience     | 20+ documented major IR engagements               |
| Multi-tenant experience      | Multiple critical client tier experience          |
| Crisis management experience | Demonstrated under-pressure performance           |
| Communication skills         | Demonstrated executive/client coaching capability |
| Availability                 | Capacity to mentor including on-call backup       |

## 21.2 Mentor Responsibilities

- Daily check-ins during first 30 days
- Weekly check-ins days 31-90
- Active shadowing supervision week 11
- Reverse shadowing supervision week 11
- IC methodology coaching
- Crisis communication coaching
- Regulatory/legal coordination coaching
- Per-tenant IR discipline coaching
- On-call backup during first 30 days
- Weekly feedback to IR Team Lead

---

# 22. Assessment Framework (Mandatory)

## 22.1 Weekly Assessments

| Week    | Assessment                       | Pass Threshold |
| ------- | -------------------------------- | -------------- |
| Week 1  | Multi-tenant IR quiz             | 100%           |
| Week 1  | L1/L2/L3 verification (external) | 80%            |
| Week 2  | Framework assessment             | 85%            |
| Week 3  | IC assessment                    | 85%            |
| Week 4  | Communication assessment         | 85%            |
| Week 5  | Regulatory assessment            | 85%            |
| Week 6  | Legal assessment                 | 85%            |
| Week 7  | Deployment assessment            | 85%            |
| Week 8  | Vendor assessment                | 80%            |
| Week 9  | Playbook practical               | 85%            |
| Week 10 | Post-incident assessment         | 85%            |
| Week 11 | Mentor evaluation                | Positive       |
| Week 12 | Final IR Team certification      | 85% (100% MT)  |

## 22.2 Reassessment Policy

- 1 reassessment allowed per failed assessment
- Reassessment within 1 week
- 2nd failure → extended onboarding (additional 3 weeks)
- 3rd failure → role suitability review by IR Team Lead + SOC Manager + CISO + HR

---

# 23. Per-Client Assignment Strategy (Mandatory)

## 23.1 Initial IR Team Assignment

| Client Tier                     | New IR Team Eligibility                 |
| ------------------------------- | --------------------------------------- |
| **Tier 1 (Critical/Regulated)** | After 120 days IR Team + Tier 2 success |
| **Tier 2 (Standard)**           | After IR Team certification             |
| **Tier 3 (Monitoring-only)**    | After IR Team certification             |

## 23.2 Specialization Pathways (Post 120 Days)

| Specialization                            | Path                                |
| ----------------------------------------- | ----------------------------------- |
| Regulated Industry Lead (BFSI/Healthcare) | Industry-specific advanced training |
| Cloud IR Specialist                       | Cloud-focused IR engagements        |
| APT/Threat Hunting Lead                   | Long-term APT campaign leadership   |
| Onsite Deployment Lead                    | Onsite engagement leadership        |
| IR Team Lead Track                        | Leadership preparation program      |
| Crisis Management Specialist              | Executive crisis training           |

---

# 24. Documentation & Records (Mandatory)

## 24.1 Onboarding Records Maintained

- [ ] IR Team onboarding checklist (signed)
- [ ] IR Team-specific NDAs
- [ ] Multi-tenant IR quiz result
- [ ] All weekly assessment results
- [ ] Final IR Team certification result
- [ ] Shadowing hours log
- [ ] Mentor feedback reports
- [ ] 90-day review report
- [ ] Tenant assignment record
- [ ] IR-grade RBAC/ABAC provisioning
- [ ] On-call rotation enrollment
- [ ] Travel readiness confirmation

## 24.2 Records Retention

| Record                        | Retention                        |
| ----------------------------- | -------------------------------- |
| IR Team onboarding records    | Duration of employment + 7 years |
| Assessment results            | Duration of employment + 7 years |
| Mentor feedback               | Duration of employment + 3 years |
| On-call participation records | Duration of employment + 7 years |

---

# 25. Quality Checklist (Per New IR Team Onboarding)

Before declaring IR Team onboarding complete:

- [ ] Full or accelerated program completed
- [ ] All weekly assessments passed
- [ ] Multi-tenant IR quiz passed at 100%
- [ ] Final IR Team certification passed at ≥85%
- [ ] Minimum 30 hours shadowing (full) / 12 hours (accelerated)
- [ ] Minimum 25 hours reverse shadowing (full) / 12 hours (accelerated)
- [ ] Minimum 2 supervised live IR engagements completed
- [ ] 4 tabletop leadership exercises completed (full) / 2 (accelerated)
- [ ] First on-call rotation completed successfully
- [ ] 90-day mentorship plan active
- [ ] Tenant assignment confirmed
- [ ] IR-grade RBAC/ABAC verified
- [ ] Onsite deployment readiness confirmed
- [ ] All documentation captured
- [ ] HR record updated
- [ ] IR Team Lead + SOC Manager + CISO sign-off obtained

---

# 26. Continuous Post-Onboarding Development

| Activity                                      | Frequency     |
| --------------------------------------------- | ------------- |
| Daily mentor check-in                         | First 30 days |
| Weekly mentor check-in                        | Days 31-90    |
| Weekly IR Team Lead review                    | First 90 days |
| Monthly IR engagement review                  | Ongoing       |
| Quarterly tabletop leadership                 | Ongoing       |
| Annual recertification                        | Ongoing       |
| Annual multi-tenant policy refresher          | Ongoing       |
| Annual crisis simulation participation        | Ongoing       |
| Annual regulatory update training             | Ongoing       |
| Career progression review (IR Team Lead prep) | Annually      |

---

# 27. Integration with Other Processes

| Process                      | Integration                    |
| ---------------------------- | ------------------------------ |
| L3 Onboarding                | Prerequisite knowledge         |
| Multi-Tenant Policy Training | IR Team expert level mandatory |
| IR Framework                 | Week 2 mastery                 |
| Incident Command             | Week 3 core skill              |
| Crisis Communication         | Week 4 core skill              |
| Regulatory Communication     | Week 5 mastery                 |
| Legal Counsel Engagement     | Week 6 coordination            |
| Onsite/Remote IR             | Week 7 deployment              |
| Vendor Coordination          | Week 8 protocols               |
| Per-Client Playbooks         | Week 9 mastery                 |
| Post-Incident Review         | Week 10 leadership             |
| Tabletop Exercises           | Week 11 + ongoing              |
| On-Call Rotation             | Week 12 enrollment             |
| Mentorship Program           | 12 weeks + 90 days             |
| Certification                | Week 12                        |
| Performance Management       | Probation period               |
| IR Team Lead Career Path     | Post-120 days                  |

---

# 28. Related Documents

| Document                          | Path                                                                                                |
| --------------------------------- | --------------------------------------------------------------------------------------------------- |
| IR Team Role Definition           | `00_GOVERNANCE/00.3_Roles-and-Responsibilities/IR-Team-Role-Definition.md`                          |
| L3 Onboarding Program             | `10_TRAINING-AND-EXERCISES/10.1_Onboarding/L3-Onboarding-Program.md`                                |
| IR Policy Master                  | `00_GOVERNANCE/00.1_Policies/IR-Policy-Master.md`                                                   |
| IR Policy NIST Alignment          | `00_GOVERNANCE/00.1_Policies/IR-Policy-NIST-Alignment.md`                                           |
| IR Policy ISO27001 Alignment      | `00_GOVERNANCE/00.1_Policies/IR-Policy-ISO27001-Alignment.md`                                       |
| IR Policy RBI Alignment           | `00_GOVERNANCE/00.1_Policies/IR-Policy-RBI-Alignment.md`                                            |
| IRT Activation Criteria           | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Activation-Criteria.md`                         |
| IRT Onsite Response SOP           | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Onsite-Response-SOP.md`                         |
| IRT Remote Response SOP           | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Remote-Response-SOP.md`                         |
| IRT Evidence Chain of Custody     | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Evidence-Chain-of-Custody.md`                   |
| IRT Forensic Collection SOP       | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Forensic-Collection-SOP.md`                     |
| IRT Containment Authority Matrix  | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`                |
| IRT Closure Criteria              | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Closure-Criteria.md`                            |
| SOC Lead P1/P2 Bridge Call SOP    | `03_SOC-TIER-PROCEDURES/03.4_SOC-Lead-Procedures/SOCLead-P1-P2-Bridge-Call-SOP.md`                  |
| Severity Classification Guide     | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`                  |
| Escalation Matrix Master          | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/Escalation-Matrix-Master.md`                 |
| Bridge Call Agenda Template       | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Bridge-Call-Agenda-Template.md`       |
| Management Notification Template  | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/Management-Notification-Template.md`  |
| MSSP Client Notification Template | `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/MSSP-Client-Notification-Template.md` |
| RBI Incident Reporting SOP        | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md`       |
| CERT-In Reporting SOP             | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`            |
| Legal Counsel Engagement SOP      | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`     |
| Third-Party IR Retainer Contacts  | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Third-Party-IR-Retainer-Contacts.md`        |
| Cross-Client Incident Procedure   | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md`                  |
| Client Data Segregation Policy    | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`                   |
| All Master Playbooks              | `02_PLAYBOOKS/`                                                                                     |
| Lessons Learned Template          | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`                                 |
| PIR Meeting Agenda                | `08_POST-INCIDENT/08.1_Lessons-Learned/PIR-Meeting-Agenda.md`                                       |
| RCA Template                      | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`                                         |

---

# 29. Revision History

| Version | Date        | Author                          | Changes         |
| ------- | ----------- | ------------------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP IR Team Lead / SOC Manager | Initial version |

---

# 30. Approval

Approved by:

| Role              | Name | Signature | Date |
| ----------------- | ---- | --------- | ---- |
| MSSP IR Team Lead |      |           |      |
| MSSP SOC Manager  |      |           |      |
| MSSP HR Lead      |      |           |      |
| MSSP CISO         |      |           |      |

---

**End of Document**
