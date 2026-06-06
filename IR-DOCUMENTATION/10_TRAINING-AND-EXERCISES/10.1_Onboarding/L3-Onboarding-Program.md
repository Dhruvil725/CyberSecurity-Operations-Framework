# L3 SOC Analyst Onboarding Program

---

# 1. Document Control

| Field          | Value                                         |
| -------------- | --------------------------------------------- |
| Document Name  | L3 SOC Analyst Onboarding Program             |
| Document ID    | MSSP-TRN-003                                  |
| Version        | 1.0                                           |
| Effective Date | 30-May-2026                                   |
| Owner          | MSSP IR Team Lead / SOC Manager               |
| Approved By    | MSSP CISO                                     |
| Classification | Confidential – MSSP Internal                  |
| Review Cycle   | Annually (or upon SOC operating model change) |

---

# 2. Purpose

This document defines the standardized **L3 SOC Analyst Onboarding Program** governing the structured induction, expert-level training, certification, and operational readiness of Level 3 (L3) SOC analysts joining the MSSP — whether external senior hires, internal promotions from L2, or specialized transfers — ensuring advanced forensics, malware analysis, threat intelligence integration, root cause analysis, and attribution competency required for the MSSP's most complex investigations.

A formal L3 onboarding program is critical because:

- L3 analysts handle the most complex investigations including APT, zero-day, and major breaches
- L3 forensic decisions determine attribution, regulatory exposure, and legal outcomes
- inconsistent L3 onboarding causes evidence handling errors, attribution gaps, and forensic deficiencies
- L3 analysts coordinate across L1/L2/IR Team/Threat Intel requiring expert-level skills
- multi-tenant forensics requires absolute tenant context discipline at expert investigation depth
- memory and disk forensics require specialized tooling and methodology training
- malware analysis (static and dynamic) requires safe lab environments and procedures
- threat actor attribution requires structured TI integration and analytical rigor
- ISO 27001 A.5.28 and NIST CSF RS.AN require formal evidence and analysis capability
- RBI Cyber Security Framework requires expert investigation capability for major incidents
- chain of custody during L3 forensics is the foundation for legal admissibility
- root cause analysis quality determines post-incident improvement effectiveness
- technical report writing for executive and regulatory audiences requires formal training
- audit and compliance reviews require evidence of L3 expert competency
- this program is the foundation for L3 quality and progression to IR Team / specialist roles

This program ensures:

- consistent 10-week structured onboarding for new L3 analysts
- 5-week accelerated program for L2-promoted analysts
- defined expert-level competency milestones with measurable assessments
- advanced multi-tenant forensics discipline
- malware analysis safe lab proficiency
- memory and disk forensics tool mastery
- threat intelligence and attribution integration capability
- root cause analysis and technical report writing excellence
- mentorship pairing with senior L3 or IR Team Lead for first 60 days
- formal certification before independent L3 work
- audit-ready evidence of expert-level training completion
- linkage to L3 role definition, forensics SOPs, and IR framework

**Reference alignment:**

- `00_GOVERNANCE/00.3_Roles-and-Responsibilities/L3-Analyst-Role-Definition.md`
- `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/`
- `10_TRAINING-AND-EXERCISES/10.1_Onboarding/L2-Onboarding-Program.md`
- `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/`

---

# 3. Scope

This program applies to all L3 SOC analysts joining the MSSP:

| Scope Element                     | Coverage                                    |
| --------------------------------- | ------------------------------------------- |
| New L3 hires (external senior)    | Full 10-week program                        |
| L2-to-L3 promotions (internal)    | Accelerated 5-week program                  |
| L3 transfers (specialist)         | Tailored 6-week program                     |
| L3 returning (>12 months absence) | Refresher 4-week program                    |
| Per-client forensics training     | Per assigned client                         |
| Forensics tool training           | EnCase, FTK, Volatility, Velociraptor, etc. |
| Malware analysis training         | Static + dynamic in safe lab                |
| Memory/disk forensics training    | Investigation-grade                         |
| Threat intel integration          | Attribution methodology                     |
| Root cause analysis               | RCA frameworks                              |
| Technical report writing          | Executive + regulatory + legal              |
| Mentorship                        | Mandatory for first 60 days                 |
| Certification                     | Mandatory before independent L3 work        |

Out of scope:

- L1/L2 onboarding (separate programs)
- IR Team onsite specialized onboarding (separate program — references L3 as prerequisite)
- SOC Lead/Manager training (separate program)
- Detection Engineering specialist onboarding (separate program)

---

# 4. Definitions

| Term                       | Definition                                                        |
| -------------------------- | ----------------------------------------------------------------- |
| L3 Analyst                 | Level 3 SOC analyst (advanced forensics and investigation expert) |
| L2-Promoted                | L2 analyst promoted to L3                                         |
| Memory Forensics           | Analysis of volatile memory artifacts                             |
| Disk Forensics             | Analysis of non-volatile storage artifacts                        |
| Malware Analysis (Static)  | Reverse engineering without execution                             |
| Malware Analysis (Dynamic) | Behavior analysis in sandbox/lab                                  |
| Attribution Analysis       | Linking activity to threat actors                                 |
| Root Cause Analysis (RCA)  | Identifying underlying cause of incident                          |
| Technical Report Writing   | Structured incident analysis documentation                        |
| Chain of Custody (CoC)     | Documented evidence handling trail                                |
| Sandbox                    | Isolated environment for malware execution                        |
| Mentor                     | Senior L3 or IR Team Lead paired with new L3                      |
| Certification              | Formal L3 competency validation                                   |
| Forensic Image             | Bit-by-bit copy of storage media                                  |
| Volatile Evidence          | Memory, network state, running processes                          |
| Non-Volatile Evidence      | Disk, registry, logs                                              |

---

# 5. Roles and Responsibilities

| Role                                      | Responsibilities                                            |
| ----------------------------------------- | ----------------------------------------------------------- |
| **MSSP IR Team Lead**                     | Program ownership; mentor assignment; forensics methodology |
| **MSSP SOC Manager**                      | Certification approval; performance oversight               |
| **MSSP Senior L3**                        | Mentor role for new L3; advanced coaching                   |
| **MSSP Threat Intel Lead**                | TI integration training; attribution methodology            |
| **MSSP Detection Engineer**               | Tool deep training; detection context                       |
| **MSSP Compliance Lead**                  | Multi-tenant expert training; CoC discipline                |
| **MSSP Legal Counsel**                    | Legal evidence requirements; regulatory standards           |
| **MSSP HR Lead**                          | Logistics; documentation; performance management            |
| **MSSP IT Lead**                          | Forensics tool access provisioning; lab access              |
| **New L3 Analyst**                        | Active participation; assessment completion; feedback       |
| **Buddy Analyst**                         | Peer support during first 60 days                           |
| **External Forensics Trainer (optional)** | Specialized training (memory/malware analysis)              |

---

# 6. Onboarding Program Principles (Mandatory)

| Principle                             | Requirement                                                 |
| ------------------------------------- | ----------------------------------------------------------- |
| **Builds on L2 Foundation**           | L2 knowledge prerequisite (internal) or verified (external) |
| **Expert-Level Methodology**          | Forensics, malware, attribution mastery                     |
| **Multi-Tenant Forensics Discipline** | Strict tenant segregation at expert level                   |
| **Safe Lab Practices**                | Mandatory before malware analysis                           |
| **Tool Mastery Required**             | Certification before forensics work                         |
| **Hands-On Heavy**                    | Significant lab time + real-world cases                     |
| **Mentorship Mandatory**              | Senior L3/IR Lead pairing first 60 days                     |
| **Assessment-Based Progression**      | Pass/fail at each milestone                                 |
| **Documentation Excellence**          | Technical report writing standards enforced                 |
| **Legal Awareness**                   | Evidence admissibility standards understood                 |
| **Audit-Ready Records**               | Complete training documentation                             |

---

# 7. L3 Onboarding Program Overview (10 Weeks Full / 5 Weeks Accelerated)

FULL PROGRAM (External L3 Hire):

Week 1: FOUNDATION & ORIENTATION
├── HR + admin + NDAs
├── MSSP organization + multi-tenant policy (expert)
├── L1/L2 foundational verification
└── L3 role expectations

Week 2: ADVANCED MULTI-TENANT & EVIDENCE HANDLING
├── Advanced segregation policy
├── Chain of Custody mastery
├── Evidence collection SOPs (deep)
└── Legal evidence standards

Week 3: FORENSICS TOOL TRAINING
├── Memory forensics tools (Volatility, etc.)
├── Disk forensics tools (FTK, EnCase, Autopsy)
├── Network forensics tools (Wireshark advanced, Zeek)
└── Log forensics tools

Week 4: MEMORY & DISK FORENSICS METHODOLOGY
├── Memory acquisition SOPs
├── Memory analysis methodology
├── Disk acquisition SOPs
└── Disk analysis methodology

Week 5: MALWARE ANALYSIS
├── Safe lab setup and procedures
├── Static analysis (PE/binary, strings, etc.)
├── Dynamic analysis (sandbox)
└── Reverse engineering basics

Week 6: THREAT INTELLIGENCE & ATTRIBUTION
├── TI integration in investigations
├── TTP mapping (MITRE ATT&CK)
├── Threat actor profiles
└── Attribution methodology

Week 7: ROOT CAUSE ANALYSIS & REPORTING
├── RCA frameworks (5 Whys, Fishbone, etc.)
├── Technical report writing
├── Executive summary writing
└── Regulatory/legal reporting

Week 8: PLAYBOOK MASTERY (L3 SECTIONS)
├── L3 sections of all playbooks
├── Per-client L3 procedures
├── APT/Zero-day specific procedures
└── Major incident L3 coordination

Week 9: SHADOWING & SUPERVISED CASES
├── Mentor shadowing
├── Reverse shadowing
├── Supervised live L3 investigations
└── Per-client briefing

Week 10: CERTIFICATION & SOLO READINESS
├── Final L3 certification
├── Tenant assignment confirmation
├── First independent L3 case
└── 60-day mentor pairing continues

**ACCELERATED PROGRAM (L2-Promoted to L3)**:

Week 1: TRANSITION & ADVANCED EVIDENCE/MT
├── L2-to-L3 transition briefing
├── Advanced multi-tenant + evidence handling
└── Legal evidence standards

Week 2: FORENSICS TOOLS & METHODOLOGY
├── Memory + disk forensics tools (compressed)
├── Memory + disk methodology (compressed)
└── Network/log forensics deep

Week 3: MALWARE ANALYSIS & TI/ATTRIBUTION
├── Safe lab + static + dynamic analysis
├── TI integration + attribution methodology
└── RCA + reporting

Week 4: L3 PLAYBOOK & SHADOWING
├── L3 playbook sections (all)
├── Mentor shadowing
└── Supervised L3 cases

Week 5: CERTIFICATION & TRANSITION
├── Pre-certification assessment
├── Final L3 certification
└── First independent L3 case + 60-day mentorship

---

# 8. Week 1: Foundation & Orientation (Mandatory)

## 8.1 Day 1 – Admin & Welcome

| Activity                                | Duration | Owner        |
| --------------------------------------- | -------- | ------------ |
| HR orientation (external hires only)    | 2 hours  | HR           |
| Equipment + forensics workstation setup | 2 hours  | IT           |
| MSSP organization (external hires)      | 1 hour   | SOC Manager  |
| L3 role expectations briefing           | 2 hours  | IR Team Lead |
| Mentor introduction (Senior L3)         | 1 hour   | Mentor       |

## 8.2 Day 2 – Multi-Tenant Expert Policy

| Activity                                      | Duration | Owner             |
| --------------------------------------------- | -------- | ----------------- |
| Client Data Segregation Policy (expert)       | 2 hours  | Compliance Lead   |
| Cross-tenant forensics prohibitions           | 2 hours  | Compliance Lead   |
| Sanitization for L3 forensic outputs          | 2 hours  | Threat Intel Lead |
| **Multi-tenant expert quiz (must pass 100%)** | 1 hour   | Compliance Lead   |

**⚠️ Critical Gate:** Cannot proceed without 100% on multi-tenant expert quiz.

## 8.3 Day 3 – L1/L2 Foundational Verification (External Hires)

| Activity                              | Duration  | Owner              |
| ------------------------------------- | --------- | ------------------ |
| L1 + L2 verification quiz             | 3 hours   | SOC Manager        |
| L1 + L2 tool proficiency verification | 3 hours   | Detection Engineer |
| Gap remediation (if any)              | As needed | Mentor             |

*(L2-promoted analysts skip this day)*

## 8.4 Day 4 – Legal/Regulatory Evidence Standards

| Activity                                              | Duration | Owner           |
| ----------------------------------------------------- | -------- | --------------- |
| Legal admissibility standards                         | 2 hours  | Legal Counsel   |
| Regulatory evidence requirements (RBI, CERT-In, DPDP) | 2 hours  | Compliance Lead |
| Cross-border evidence considerations                  | 1 hour   | Legal Counsel   |
| Privacy considerations in forensics                   | 1 hour   | Compliance Lead |

## 8.5 Day 5 – L3 Tool Landscape Preview

| Activity                        | Duration | Owner                 |
| ------------------------------- | -------- | --------------------- |
| Forensics toolkit overview      | 2 hours  | IR Team Lead          |
| Memory forensics tool landscape | 1 hour   | Detection Engineer    |
| Disk forensics tool landscape   | 1 hour   | Detection Engineer    |
| Malware analysis lab overview   | 2 hours  | IR Team Lead          |
| Week 1 retrospective            | 1 hour   | Mentor + IR Team Lead |

### Week 1 Completion Criteria

- [ ] All admin setup completed
- [ ] L3-specific NDAs signed
- [ ] Multi-tenant expert quiz passed (100%)
- [ ] L1/L2 verification completed (external hires)
- [ ] Legal/regulatory evidence standards understood
- [ ] Mentor pairing confirmed

---

# 9. Week 2: Advanced Multi-Tenant & Evidence Handling (Mandatory)

## 9.1 Advanced Multi-Tenant Procedures

| Topic                                            | Duration | Owner             |
| ------------------------------------------------ | -------- | ----------------- |
| Client Data Segregation Policy (reinforcement)   | 1 hour   | Compliance Lead   |
| Cross-Client Incident Procedure (L3 perspective) | 2 hours  | IR Team Lead      |
| Sanitization for cross-tenant intelligence       | 2 hours  | Threat Intel Lead |
| Per-tenant forensic evidence segregation         | 2 hours  | Compliance Lead   |
| MSSP-Client evidence handling                    | 1 hour   | Compliance Lead   |

## 9.2 Chain of Custody Mastery

| Topic                                    | Duration | Owner           |
| ---------------------------------------- | -------- | --------------- |
| CoC Master Form usage                    | 1 hour   | Compliance Lead |
| CoC for Digital Evidence                 | 2 hours  | Compliance Lead |
| CoC for Physical Evidence                | 1 hour   | Compliance Lead |
| CoC Transfer procedures                  | 1 hour   | Compliance Lead |
| **Hands-on CoC exercises (5 scenarios)** | 4 hours  | Compliance Lead |

## 9.3 Evidence Collection SOPs (Deep)

| Topic                     | Duration | Owner              |
| ------------------------- | -------- | ------------------ |
| Evidence Collection SOP   | 2 hours  | IR Team Lead       |
| Digital Evidence Handling | 2 hours  | IR Team Lead       |
| Log Evidence SOP          | 1 hour   | Detection Engineer |
| Memory Evidence SOP       | 2 hours  | IR Team Lead       |
| Network Evidence SOP      | 2 hours  | Detection Engineer |

## 9.4 Evidence Storage & Retention

| Topic                         | Duration | Owner           |
| ----------------------------- | -------- | --------------- |
| Evidence Storage Policy       | 1 hour   | Compliance Lead |
| Evidence Retention Schedule   | 1 hour   | Compliance Lead |
| Evidence Destruction SOP      | 1 hour   | Compliance Lead |
| Per-client evidence retention | 1 hour   | Compliance Lead |

### Week 2 Completion Criteria

- [ ] All evidence SOPs reviewed
- [ ] CoC exercises completed
- [ ] Evidence handling assessment passed (100%)
- [ ] Per-tenant evidence discipline demonstrated

---

# 10. Week 3: Forensics Tool Training (Mandatory)

## 10.1 Memory Forensics Tools

| Tool                                          | Duration | Owner              |
| --------------------------------------------- | -------- | ------------------ |
| Volatility framework basics                   | 4 hours  | Detection Engineer |
| Volatility plugins (deep)                     | 4 hours  | Detection Engineer |
| Memory acquisition tools (DumpIt, FTK Imager) | 2 hours  | Detection Engineer |
| Velociraptor / GRR for memory                 | 3 hours  | Detection Engineer |
| **Hands-on lab: 5 memory analysis cases**     | 6 hours  | Mentor             |

## 10.2 Disk Forensics Tools

| Tool                                    | Duration | Owner              |
| --------------------------------------- | -------- | ------------------ |
| Autopsy / Sleuth Kit                    | 4 hours  | Detection Engineer |
| FTK / EnCase (if licensed)              | 4 hours  | Detection Engineer |
| Disk imaging tools (dd, FTK Imager)     | 2 hours  | Detection Engineer |
| File system analysis (NTFS, ext4, APFS) | 3 hours  | Detection Engineer |
| **Hands-on lab: 3 disk analysis cases** | 6 hours  | Mentor             |

## 10.3 Network Forensics Tools (Advanced)

| Tool                                       | Duration | Owner              |
| ------------------------------------------ | -------- | ------------------ |
| Wireshark advanced                         | 3 hours  | Detection Engineer |
| Zeek (Bro) deep analysis                   | 3 hours  | Detection Engineer |
| Suricata for forensics                     | 2 hours  | Detection Engineer |
| **Hands-on lab: 3 network forensic cases** | 4 hours  | Detection Engineer |

## 10.4 Log Forensics Tools

| Tool                                   | Duration | Owner              |
| -------------------------------------- | -------- | ------------------ |
| Windows event log analysis (deep)      | 3 hours  | Detection Engineer |
| Linux/Unix log analysis (deep)         | 2 hours  | Detection Engineer |
| Cloud audit log analysis               | 3 hours  | Detection Engineer |
| **Hands-on lab: 3 log forensic cases** | 4 hours  | Detection Engineer |

### Week 3 Completion Criteria

- [ ] Memory forensics lab completed (5 cases)
- [ ] Disk forensics lab completed (3 cases)
- [ ] Network forensics lab completed (3 cases)
- [ ] Log forensics lab completed (3 cases)
- [ ] Tool proficiency assessment passed (≥85%)

---

# 11. Week 4: Memory & Disk Forensics Methodology (Mandatory)

## 11.1 Memory Acquisition SOPs

| Topic                           | Duration | Owner        |
| ------------------------------- | -------- | ------------ |
| L3 Memory Forensics SOP         | 2 hours  | IR Team Lead |
| Memory Acquisition SOP          | 2 hours  | IR Team Lead |
| Order of volatility             | 1 hour   | IR Team Lead |
| Live vs offline memory analysis | 2 hours  | IR Team Lead |

## 11.2 Memory Analysis Methodology

| Topic                                        | Duration | Owner        |
| -------------------------------------------- | -------- | ------------ |
| Process analysis                             | 3 hours  | IR Team Lead |
| Network artifact analysis (memory)           | 2 hours  | IR Team Lead |
| Code injection detection                     | 3 hours  | IR Team Lead |
| Rootkit detection                            | 2 hours  | IR Team Lead |
| Credential extraction                        | 2 hours  | IR Team Lead |
| **Hands-on case: full memory investigation** | 6 hours  | Mentor       |

## 11.3 Disk Acquisition SOPs

| Topic                 | Duration | Owner        |
| --------------------- | -------- | ------------ |
| L3 Disk Forensics SOP | 2 hours  | IR Team Lead |
| Disk Acquisition SOP  | 2 hours  | IR Team Lead |
| Write-blocker usage   | 1 hour   | IR Team Lead |
| Hash verification     | 1 hour   | IR Team Lead |

## 11.4 Disk Analysis Methodology

| Topic                                      | Duration | Owner        |
| ------------------------------------------ | -------- | ------------ |
| File system timeline analysis              | 3 hours  | IR Team Lead |
| Deleted file recovery                      | 2 hours  | IR Team Lead |
| Registry analysis                          | 3 hours  | IR Team Lead |
| Browser/email artifact analysis            | 2 hours  | IR Team Lead |
| **Hands-on case: full disk investigation** | 6 hours  | Mentor       |

### Week 4 Completion Criteria

- [ ] L3 Memory/Disk SOPs demonstrated
- [ ] Full memory investigation completed
- [ ] Full disk investigation completed
- [ ] Methodology assessment passed (≥85%)

---

# 12. Week 5: Malware Analysis (Mandatory)

## 12.1 Safe Lab Setup

| Topic                                 | Duration | Owner           |
| ------------------------------------- | -------- | --------------- |
| Isolated lab environment requirements | 1 hour   | IR Team Lead    |
| Network isolation procedures          | 1 hour   | IT Lead         |
| Snapshot management                   | 1 hour   | IR Team Lead    |
| Sample handling procedures            | 1 hour   | IR Team Lead    |
| Lab safety acknowledgment             | 30 min   | Compliance Lead |

## 12.2 Static Malware Analysis

| Topic                               | Duration | Owner        |
| ----------------------------------- | -------- | ------------ |
| L3 Malware Analysis SOP             | 2 hours  | IR Team Lead |
| PE/ELF/Mach-O structure             | 3 hours  | IR Team Lead |
| Strings/IoC extraction              | 2 hours  | IR Team Lead |
| YARA rule basics                    | 3 hours  | IR Team Lead |
| Disassembly basics (IDA/Ghidra)     | 4 hours  | IR Team Lead |
| **Hands-on lab: 3 static analyses** | 6 hours  | Mentor       |

## 12.3 Dynamic Malware Analysis

| Topic                                 | Duration | Owner        |
| ------------------------------------- | -------- | ------------ |
| Sandbox tools (Cuckoo, ANY.RUN, etc.) | 3 hours  | IR Team Lead |
| Behavior analysis                     | 3 hours  | IR Team Lead |
| Network behavior analysis             | 2 hours  | IR Team Lead |
| Persistence mechanism analysis        | 2 hours  | IR Team Lead |
| C2 extraction                         | 2 hours  | IR Team Lead |
| **Hands-on lab: 3 dynamic analyses**  | 6 hours  | Mentor       |

## 12.4 Reverse Engineering Basics

| Topic                           | Duration | Owner        |
| ------------------------------- | -------- | ------------ |
| Assembly basics (x86/x64)       | 4 hours  | IR Team Lead |
| Debugger usage (x64dbg/OllyDbg) | 3 hours  | IR Team Lead |
| Anti-analysis techniques        | 2 hours  | IR Team Lead |
| Unpacking basics                | 2 hours  | IR Team Lead |

### Week 5 Completion Criteria

- [ ] Lab safety acknowledged
- [ ] Static analysis lab completed (3 samples)
- [ ] Dynamic analysis lab completed (3 samples)
- [ ] Reverse engineering basics demonstrated
- [ ] Malware analysis assessment passed (≥80%)

---

# 13. Week 6: Threat Intelligence & Attribution (Mandatory)

## 13.1 TI Integration in Investigations

| Topic                                   | Duration | Owner             |
| --------------------------------------- | -------- | ----------------- |
| L3 Threat Intel Integration SOP         | 2 hours  | Threat Intel Lead |
| TI platform advanced usage              | 3 hours  | Threat Intel Lead |
| Pivoting on IoCs and TTPs               | 3 hours  | Threat Intel Lead |
| External TI sources (commercial, OSINT) | 2 hours  | Threat Intel Lead |
| Per-tenant TI enrichment                | 2 hours  | Threat Intel Lead |

## 13.2 TTP Mapping (MITRE ATT&CK)

| Topic                                  | Duration | Owner             |
| -------------------------------------- | -------- | ----------------- |
| MITRE ATT&CK framework deep            | 3 hours  | Threat Intel Lead |
| Tactic/Technique/Sub-technique mapping | 3 hours  | Threat Intel Lead |
| ATT&CK Navigator usage                 | 2 hours  | Threat Intel Lead |
| MITRE D3FEND integration               | 2 hours  | Threat Intel Lead |
| **Hands-on: TTP mapping exercise**     | 4 hours  | Threat Intel Lead |

## 13.3 Threat Actor Profiles

| Topic                            | Duration | Owner             |
| -------------------------------- | -------- | ----------------- |
| Threat actor taxonomy            | 2 hours  | Threat Intel Lead |
| Profile construction methodology | 2 hours  | Threat Intel Lead |
| Notable APT groups overview      | 4 hours  | Threat Intel Lead |
| Cybercrime ecosystem overview    | 2 hours  | Threat Intel Lead |

## 13.4 Attribution Methodology

| Topic                              | Duration | Owner             |
| ---------------------------------- | -------- | ----------------- |
| L3 Attribution Analysis SOP        | 2 hours  | Threat Intel Lead |
| Diamond Model usage                | 2 hours  | Threat Intel Lead |
| Attribution confidence levels      | 2 hours  | Threat Intel Lead |
| Limitations of attribution         | 1 hour   | Threat Intel Lead |
| **Hands-on: attribution exercise** | 4 hours  | Threat Intel Lead |

### Week 6 Completion Criteria

- [ ] TI integration demonstrated
- [ ] TTP mapping exercise completed
- [ ] Attribution exercise completed
- [ ] TI/Attribution assessment passed (≥80%)

---

# 14. Week 7: Root Cause Analysis & Reporting (Mandatory)

## 14.1 RCA Frameworks

| Topic                         | Duration | Owner        |
| ----------------------------- | -------- | ------------ |
| L3 Root Cause Analysis SOP    | 2 hours  | IR Team Lead |
| RCA Template usage            | 1 hour   | IR Team Lead |
| 5 Whys methodology            | 2 hours  | IR Team Lead |
| Fishbone/Ishikawa diagrams    | 2 hours  | IR Team Lead |
| Timeline-based RCA            | 2 hours  | IR Team Lead |
| **Hands-on: 2 RCA exercises** | 4 hours  | IR Team Lead |

## 14.2 Technical Report Writing

| Topic                                   | Duration | Owner           |
| --------------------------------------- | -------- | --------------- |
| L3 Technical Report Writing SOP         | 2 hours  | IR Team Lead    |
| Technical deep-dive structure           | 2 hours  | IR Team Lead    |
| Evidence reference standards            | 1 hour   | Compliance Lead |
| Multi-audience writing                  | 2 hours  | IR Team Lead    |
| **Hands-on: write 2 technical reports** | 6 hours  | Mentor          |

## 14.3 Executive Summary Writing

| Topic                                     | Duration | Owner        |
| ----------------------------------------- | -------- | ------------ |
| Executive Summary Template                | 1 hour   | IR Team Lead |
| Translating technical → business          | 2 hours  | IR Team Lead |
| Risk articulation                         | 2 hours  | IR Team Lead |
| **Hands-on: write 2 executive summaries** | 4 hours  | Mentor       |

## 14.4 Regulatory/Legal Reporting

| Topic                                   | Duration | Owner           |
| --------------------------------------- | -------- | --------------- |
| RBI report writing                      | 2 hours  | Compliance Lead |
| CERT-In report writing                  | 1 hour   | Compliance Lead |
| Legal evidence narrative                | 2 hours  | Legal Counsel   |
| **Hands-on: write 1 regulatory report** | 3 hours  | Compliance Lead |

### Week 7 Completion Criteria

- [ ] RCA exercises completed
- [ ] 2 technical reports written and reviewed
- [ ] 2 executive summaries written and reviewed
- [ ] 1 regulatory report written and reviewed
- [ ] Reporting assessment passed (≥85%)

---

# 15. Week 8: Playbook Mastery (L3 Sections) (Mandatory)

## 15.1 L3 Sections of All Playbooks

| Playbook                       | Duration | Owner        |
| ------------------------------ | -------- | ------------ |
| Ransomware L3 Forensics        | 3 hours  | IR Team Lead |
| Phishing L3 Forensics          | 2 hours  | IR Team Lead |
| Malware L3 Forensics           | 3 hours  | IR Team Lead |
| Insider Threat L3 Forensics    | 3 hours  | IR Team Lead |
| Data Breach L3 Forensics       | 3 hours  | IR Team Lead |
| Web Application L3 Forensics   | 2 hours  | IR Team Lead |
| Cloud L3 Forensics             | 3 hours  | IR Team Lead |
| Network Intrusion L3 Forensics | 2 hours  | IR Team Lead |
| Supply Chain L3 Forensics      | 3 hours  | IR Team Lead |
| Zero-Day L3 Forensics          | 3 hours  | IR Team Lead |
| APT L3 Forensics               | 4 hours  | IR Team Lead |

## 15.2 Per-Client L3 Procedures

| Topic                                              | Duration | Owner           |
| -------------------------------------------------- | -------- | --------------- |
| Per-client environment profiles (forensic context) | 3 hours  | SOC Manager     |
| Per-client legal/regulatory context                | 2 hours  | Compliance Lead |
| Per-client forensic constraints                    | 2 hours  | IR Team Lead    |
| Per-client evidence retention                      | 1 hour   | Compliance Lead |

## 15.3 APT/Zero-Day Specific Procedures

| Topic                           | Duration | Owner             |
| ------------------------------- | -------- | ----------------- |
| APT campaign analysis           | 3 hours  | Threat Intel Lead |
| Long-term monitoring strategy   | 2 hours  | Threat Intel Lead |
| Zero-day workaround development | 2 hours  | IR Team Lead      |
| Vendor coordination protocols   | 2 hours  | IR Team Lead      |

## 15.4 Major Incident L3 Coordination

| Topic                        | Duration | Owner        |
| ---------------------------- | -------- | ------------ |
| L3 role in P1/P2 incidents   | 2 hours  | IR Team Lead |
| L3 coordination with IR Team | 2 hours  | IR Team Lead |
| L3 bridge call participation | 1 hour   | SOC Lead     |
| L3 escalation to IR Team     | 1 hour   | IR Team Lead |

### Week 8 Completion Criteria

- [ ] All L3 playbook sections reviewed
- [ ] Per-client L3 procedures mastered
- [ ] APT/Zero-day procedures demonstrated
- [ ] Major incident L3 coordination understood
- [ ] Playbook practical assessment passed (≥85%)

---

# 16. Week 9: Shadowing & Supervised Cases (Mandatory)

## 16.1 Active Mentor Shadowing

| Activity                                   | Duration   | Owner  |
| ------------------------------------------ | ---------- | ------ |
| Active shadowing of mentor L3 work         | 30 hours   | Mentor |
| Forensic investigation observation         | Continuous | Mentor |
| Per-tenant forensic discipline observation | Continuous | Mentor |
| Documentation observation                  | Continuous | Mentor |
| Stakeholder communication observation      | Continuous | Mentor |

## 16.2 Reverse Shadowing

| Activity                                        | Duration   | Owner  |
| ----------------------------------------------- | ---------- | ------ |
| New L3 conducts forensic work under observation | 25 hours   | Mentor |
| Real-time feedback                              | Continuous | Mentor |
| End-of-case debrief                             | Per case   | Mentor |

## 16.3 Supervised Live L3 Investigations

| Activity                       | Duration  | Owner            |
| ------------------------------ | --------- | ---------------- |
| Supervised live L3 cases (2-3) | 16 hours  | Mentor + IR Lead |
| Tenant verification            | Mandatory | New L3           |
| Documentation review per case  | Mandatory | Mentor           |

## 16.4 Per-Client Briefing

| Activity                                | Duration | Owner            |
| --------------------------------------- | -------- | ---------------- |
| Per-client deep briefings               | 6 hours  | Per-client SDM   |
| Per-client forensic access verification | 2 hours  | IT Lead          |
| Per-client legal context briefing       | 2 hours  | Legal/Compliance |

### Week 9 Completion Criteria

- [ ] Minimum 30 hours active shadowing completed
- [ ] Minimum 25 hours reverse shadowing completed
- [ ] Minimum 2 supervised live L3 cases completed
- [ ] All assigned client briefings completed
- [ ] Mentor positive evaluation

---

# 17. Week 10: Certification & Solo Readiness (Mandatory)

## 17.1 Final L3 Certification Assessment

| Component                                        | Pass Threshold   |
| ------------------------------------------------ | ---------------- |
| Written exam (all L3 SOPs/playbooks/methodology) | 85%              |
| Multi-tenant expert exam                         | 100% (must pass) |
| Forensics tool proficiency practical             | 85%              |
| Live forensic case assessment                    | 85% accuracy     |
| Malware analysis assessment                      | 80%              |
| RCA + report writing assessment                  | 85%              |
| Attribution exercise assessment                  | 80%              |
| Per-client knowledge assessment                  | 85%              |

## 17.2 Tenant Assignment Confirmation

| Activity                            | Owner                      |
| ----------------------------------- | -------------------------- |
| Assigned client portfolio finalized | SOC Manager + IR Team Lead |
| Forensic RBAC/ABAC verified         | IT Lead                    |
| Per-client forensic access tested   | New L3 + Mentor            |
| Legal/regulatory context confirmed  | Compliance Lead            |

## 17.3 First Independent L3 Case

| Activity                                | Duration   | Owner        |
| --------------------------------------- | ---------- | ------------ |
| First independent case (mentor on-call) | Full case  | New L3       |
| Mentor periodic check-ins               | Throughout | Mentor       |
| Case completion review                  | 2 hours    | IR Team Lead |

## 17.4 60-Day Continued Mentorship

| Activity                     | Cadence               | Owner                      |
| ---------------------------- | --------------------- | -------------------------- |
| Daily mentor check-in        | Daily for 30 days     | Mentor                     |
| Weekly IR Team Lead review   | Weekly for 60 days    | IR Team Lead               |
| Bi-weekly SOC Manager review | Bi-weekly for 60 days | SOC Manager                |
| 60-day formal review         | Day 60                | SOC Manager + IR Team Lead |

### Week 10 Completion Criteria

- [ ] Final L3 certification passed (≥85%)
- [ ] Multi-tenant exam passed at 100%
- [ ] Tenant assignment confirmed
- [ ] First independent L3 case successful
- [ ] 60-day mentorship plan documented

---

# 18. Accelerated Program for L2-Promoted (5 Weeks)

## 18.1 Week 1 (Accelerated): Transition & Advanced Evidence/MT

| Day     | Focus                                     |
| ------- | ----------------------------------------- |
| Day 1   | L2-to-L3 transition + multi-tenant expert |
| Day 2-3 | Advanced evidence handling + CoC mastery  |
| Day 4-5 | Legal/regulatory evidence standards       |

## 18.2 Week 2 (Accelerated): Forensics Tools & Methodology

| Day     | Focus                         |
| ------- | ----------------------------- |
| Day 1-2 | Memory + disk forensics tools |
| Day 3-4 | Memory + disk methodology     |
| Day 5   | Network/log forensics deep    |

## 18.3 Week 3 (Accelerated): Malware Analysis & TI/Attribution

| Day     | Focus                                |
| ------- | ------------------------------------ |
| Day 1-2 | Safe lab + static + dynamic analysis |
| Day 3   | TI integration + attribution         |
| Day 4-5 | RCA + technical reporting            |

## 18.4 Week 4 (Accelerated): L3 Playbook & Shadowing

| Day     | Focus                               |
| ------- | ----------------------------------- |
| Day 1-2 | L3 playbook sections (all)          |
| Day 3-4 | Mentor shadowing + supervised cases |
| Day 5   | Per-client briefing                 |

## 18.5 Week 5 (Accelerated): Certification & Transition

| Day     | Focus                                                |
| ------- | ---------------------------------------------------- |
| Day 1-2 | Pre-certification preparation                        |
| Day 3   | Pre-certification assessment                         |
| Day 4   | Final L3 certification                               |
| Day 5   | First independent L3 case + 60-day mentorship begins |

---

# 19. Mentor Program (Mandatory)

## 19.1 Mentor Selection Criteria for L3 Onboarding

| Criterion               | Requirement                                  |
| ----------------------- | -------------------------------------------- |
| Tenure                  | Minimum 2 years L3 or IR Team experience     |
| Forensics experience    | 30+ documented L3 cases                      |
| Specialization          | Memory/disk/malware/network forensics expert |
| Multi-tenant experience | Multiple critical client tier experience     |
| Communication skills    | Demonstrated coaching capability             |
| Availability            | Capacity to mentor                           |

## 19.2 Mentor Responsibilities

- Daily check-ins during first 30 days
- Weekly check-ins days 31-60
- Active shadowing supervision week 9
- Reverse shadowing supervision week 9
- Forensic methodology coaching
- Per-tenant discipline coaching
- Documentation quality coaching
- Tool proficiency coaching
- Weekly feedback to IR Team Lead

---

# 20. Assessment Framework (Mandatory)

## 20.1 Weekly Assessments

| Week    | Assessment                    | Pass Threshold |
| ------- | ----------------------------- | -------------- |
| Week 1  | Multi-tenant expert quiz      | 100%           |
| Week 1  | L1/L2 verification (external) | 80%            |
| Week 2  | Evidence/CoC assessment       | 100%           |
| Week 3  | Tool proficiency assessment   | 85%            |
| Week 4  | Methodology assessment        | 85%            |
| Week 5  | Malware analysis assessment   | 80%            |
| Week 6  | TI/Attribution assessment     | 80%            |
| Week 7  | RCA + Reporting assessment    | 85%            |
| Week 8  | Playbook practical            | 85%            |
| Week 9  | Mentor evaluation             | Positive       |
| Week 10 | Final L3 certification        | 85% (100% MT)  |

## 20.2 Reassessment Policy

- 1 reassessment allowed per failed assessment
- Reassessment within 1 week
- 2nd failure → extended onboarding (additional 2 weeks)
- 3rd failure → role suitability review by IR Team Lead + SOC Manager + HR

---

# 21. Per-Client Assignment Strategy (Mandatory)

## 21.1 Initial L3 Assignment

| Client Tier                     | New L3 Eligibility                |
| ------------------------------- | --------------------------------- |
| **Tier 1 (Critical/Regulated)** | After 90 days L3 + Tier 2 success |
| **Tier 2 (Standard)**           | After L3 certification            |
| **Tier 3 (Monitoring-only)**    | After L3 certification            |

## 21.2 Specialization Pathways (Post 90 Days)

| Specialization              | Path                                 |
| --------------------------- | ------------------------------------ |
| Memory Forensics Specialist | Advanced training + cert (GCFA/GREM) |
| Malware Reverse Engineer    | Advanced RE training + cert (GREM)   |
| Cloud Forensics Specialist  | Cloud forensics certification        |
| Threat Intel Specialist     | TI certification (CTIA)              |
| IR Team Lead Track          | IR Team prep program                 |

---

# 22. Documentation & Records (Mandatory)

## 22.1 Onboarding Records Maintained

- [ ] L3 onboarding checklist (signed)
- [ ] L3-specific NDAs
- [ ] Multi-tenant expert quiz result
- [ ] All weekly assessment results
- [ ] Final L3 certification result
- [ ] Shadowing hours log
- [ ] Mentor feedback reports
- [ ] 60-day review report
- [ ] Tenant assignment record
- [ ] Forensic RBAC/ABAC provisioning
- [ ] Lab safety acknowledgment

## 22.2 Records Retention

| Record                | Retention                        |
| --------------------- | -------------------------------- |
| L3 onboarding records | Duration of employment + 7 years |
| Assessment results    | Duration of employment + 7 years |
| Mentor feedback       | Duration of employment + 3 years |
| Lab safety records    | Duration of employment + 7 years |

---

# 23. Quality Checklist (Per New L3 Onboarding)

Before declaring L3 onboarding complete:

- [ ] Full or accelerated program completed
- [ ] All weekly assessments passed
- [ ] Multi-tenant expert quiz passed at 100%
- [ ] Final L3 certification passed at ≥85%
- [ ] Minimum 30 hours shadowing (full) / 8 hours (accelerated)
- [ ] Minimum 25 hours reverse shadowing (full) / 8 hours (accelerated)
- [ ] Minimum 2 supervised L3 cases completed
- [ ] Malware lab safety acknowledged
- [ ] First independent L3 case completed successfully
- [ ] 60-day mentorship plan active
- [ ] Tenant assignment confirmed
- [ ] Forensic RBAC/ABAC verified
- [ ] All documentation captured
- [ ] HR record updated
- [ ] IR Team Lead + SOC Manager sign-off obtained

---

# 24. Continuous Post-Onboarding Development

| Activity                                   | Frequency     |
| ------------------------------------------ | ------------- |
| Daily mentor check-in                      | First 30 days |
| Weekly mentor check-in                     | Days 31-60    |
| Weekly performance review                  | First 90 days |
| Monthly case review                        | Ongoing       |
| Quarterly tabletop participation (L3 role) | Ongoing       |
| Annual recertification                     | Ongoing       |
| Annual multi-tenant policy refresher       | Ongoing       |
| Annual specialized certification renewal   | Per cert      |
| Career progression review (IR Team prep)   | Bi-annually   |

---

# 25. Integration with Other Processes

| Process                      | Integration            |
| ---------------------------- | ---------------------- |
| L2 Onboarding                | Prerequisite knowledge |
| Multi-Tenant Policy Training | Expert level mandatory |
| Forensics Tool Training      | Weeks 3-4 deep focus   |
| Malware Analysis Lab         | Week 5 hands-on        |
| TI/Attribution Program       | Week 6                 |
| RCA/Reporting Standards      | Week 7                 |
| Per-Client Playbooks         | Week 8 mastery         |
| Tabletop Exercises           | Week 9 + ongoing       |
| Mentorship Program           | 10 weeks + 60 days     |
| Certification                | Week 10                |
| Performance Management       | Probation period       |
| IR Team Career Path          | Post-90 days           |

---

# 26. Related Documents

| Document                       | Path                                                                                     |
| ------------------------------ | ---------------------------------------------------------------------------------------- |
| L3 Analyst Role Definition     | `00_GOVERNANCE/00.3_Roles-and-Responsibilities/L3-Analyst-Role-Definition.md`            |
| L2 Onboarding Program          | `10_TRAINING-AND-EXERCISES/10.1_Onboarding/L2-Onboarding-Program.md`                     |
| IR Team Onboarding Program     | `10_TRAINING-AND-EXERCISES/10.1_Onboarding/IR-Team-Onboarding-Program.md`                |
| L3 Advanced Forensics SOP      | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Advanced-Forensics-SOP.md`                 |
| L3 Malware Analysis SOP        | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Malware-Analysis-SOP.md`                   |
| L3 Memory Forensics SOP        | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Memory-Forensics-SOP.md`                   |
| L3 Disk Forensics SOP          | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Disk-Forensics-SOP.md`                     |
| L3 Threat Intel Integration    | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Threat-Intel-Integration.md`               |
| L3 Root Cause Analysis         | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Root-Cause-Analysis.md`                    |
| L3 Attribution Analysis        | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Attribution-Analysis.md`                   |
| L3 Technical Report Writing    | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Technical-Report-Writing.md`               |
| Forensics Toolkit Reference    | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Forensics-Toolkit-Reference.md`            |
| Memory Acquisition SOP         | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Memory-Acquisition-SOP.md`                 |
| Disk Acquisition SOP           | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Disk-Acquisition-SOP.md`                   |
| Log Collection SOP             | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Log-Collection-SOP.md`                     |
| Tool Chain of Custody          | `04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Tool-Chain-of-Custody.md`                  |
| Evidence Collection SOP        | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md`   |
| Digital Evidence Handling      | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Digital-Evidence-Handling.md` |
| CoC Master Form                | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Master-Form.md`              |
| Client Data Segregation Policy | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`        |
| All L3 Playbook Sections       | `02_PLAYBOOKS/`                                                                          |
| RCA Template                   | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`                              |
| MITRE ATT&CK Quick Reference   | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md`          |
| Attack Technique Reference     | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Attack-Technique-Reference.md`            |

---

# 27. Revision History

| Version | Date        | Author                          | Changes         |
| ------- | ----------- | ------------------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP IR Team Lead / SOC Manager | Initial version |

---

# 28. Approval

Approved by:

| Role              | Name | Signature | Date |
| ----------------- | ---- | --------- | ---- |
| MSSP IR Team Lead |      |           |      |
| MSSP SOC Manager  |      |           |      |
| MSSP HR Lead      |      |           |      |
| MSSP CISO         |      |           |      |

---

**End of Document**
