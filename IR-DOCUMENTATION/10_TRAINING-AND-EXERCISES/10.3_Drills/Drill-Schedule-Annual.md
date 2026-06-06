# Annual Drill Schedule

---

# 1. Document Control

| Field          | Value                                      |
| -------------- | ------------------------------------------ |
| Document Name  | Annual Drill Schedule                      |
| Document ID    | MSSP-TRN-DRL-003                           |
| Version        | 1.0                                        |
| Effective Date | 30-May-2026                                |
| Owner          | MSSP IR Team Lead / SOC Manager            |
| Approved By    | MSSP CISO                                  |
| Classification | Confidential – MSSP Internal               |
| Review Cycle   | Annually (published Q4 for following year) |

---

# 2. Purpose

This document defines the standardized **Annual Drill Schedule** governing the planned cadence of all tabletop exercises, red team engagements, purple team exercises, BAS/CART operations, and operational drills across the MSSP — providing a single annual calendar that ensures continuous IR readiness validation, detection maturity improvement, personnel training, regulatory compliance, and client contractual fulfillment across multi-tenant operations.

A formal annual drill schedule is critical because:

- ad-hoc exercises produce inconsistent coverage and miss critical scenarios
- regulatory frameworks (RBI, ISO 27001 A.5.24, NIST CSF DE.DP) require periodic, documented testing
- client MSAs frequently require evidence of quarterly/annual exercises
- balanced coverage of all major incident types (ransomware, APT, insider, breach, cloud, etc.) requires planning
- red team, purple team, tabletop, and BAS each serve different purposes requiring coordinated scheduling
- new analyst onboarding requires scheduled exercise participation
- seasonal operational patterns (holidays, year-end, audit periods) affect drill timing
- resource allocation for exercises requires advance planning (red team, facilitators, evaluators, facilities)
- multi-tenant scheduling prevents conflict between client exercises
- annual schedule enables year-over-year maturity comparison
- ISO 27001 management reviews require demonstration of testing program execution
- NIST CSF maturity assessments use exercise frequency as maturity indicator
- without schedule, exercises cluster in Q4 (pre-audit) with gaps in Q1-Q3
- this schedule is the operational backbone for the MSSP exercise program

This schedule ensures:

- minimum annual exercise requirements met
- balanced scenario coverage across all major incident types
- balanced exercise type coverage (TTX, red team, purple team, BAS)
- balanced audience coverage (L1-L3, IR Team, executive, cross-functional, client)
- client exercise obligations tracked and scheduled
- regulatory and audit evidence planned in advance
- resource conflicts avoided through advance scheduling
- continuous detection improvement through quarterly purple team
- post-incident exercises triggered by real events
- calendar published and communicated to all stakeholders
- quarterly review and adjustment capability

**Reference alignment:**

- `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`
- `10_TRAINING-AND-EXERCISES/10.3_Drills/Red-Team-IR-Integration-SOP.md`
- `10_TRAINING-AND-EXERCISES/10.3_Drills/Purple-Team-Exercise-Guide.md`
- `10_TRAINING-AND-EXERCISES/10.3_Drills/Drill-After-Action-Report.md`

---

# 3. Scope

This schedule covers all MSSP exercise activities:

| Scope Element                          | Coverage                                  |
| -------------------------------------- | ----------------------------------------- |
| Tabletop exercises (TTX)               | All scenarios                             |
| Red team engagements                   | Internal + client                         |
| Purple team exercises                  | Internal + client                         |
| BAS / CART                             | Continuous automated                      |
| Operational drills                     | IR activation, shift handover, escalation |
| Client exercises (per MSA)             | Per client schedule                       |
| Onboarding exercises                   | Per cohort                                |
| Post-incident exercises                | Ad-hoc (triggered)                        |
| Regulatory exercises (RBI cyber drill) | Per regulatory requirement                |
| Executive exercises                    | Annual minimum                            |

Out of scope:

- BCP/DR exercises (covered by BCP/DR program — coordinated here)
- Physical security drills (covered by Facilities)
- General employee security awareness (covered by HR program)

---

# 4. Definitions

| Term                   | Definition                                           |
| ---------------------- | ---------------------------------------------------- |
| TTX                    | Tabletop Exercise (discussion-based)                 |
| Red Team               | Adversarial offensive testing                        |
| Purple Team            | Collaborative red+blue exercise                      |
| BAS                    | Breach and Attack Simulation (automated)             |
| CART                   | Continuous Automated Red Team                        |
| Operational Drill      | Live process test (e.g., IR activation, bridge call) |
| Client Exercise        | Exercise with/for specific client                    |
| Onboarding Exercise    | Exercise as part of analyst onboarding               |
| Post-Incident Exercise | Exercise triggered by real incident learnings        |
| Regulatory Drill       | Exercise mandated by regulator                       |
| Exercise Window        | Scheduled time period for exercise                   |

---

# 5. Roles and Responsibilities

| Role                                | Responsibilities                                           |
| ----------------------------------- | ---------------------------------------------------------- |
| **MSSP IR Team Lead**               | Annual schedule ownership; TTX/drill coordination          |
| **MSSP SOC Manager**                | Resource allocation; blue team availability                |
| **MSSP Detection Engineering Lead** | Purple team / red team coordination                        |
| **MSSP Compliance Lead**            | Regulatory exercise tracking; audit evidence               |
| **MSSP Training Lead**              | Schedule publication; tracking; records                    |
| **MSSP CISO**                       | Annual schedule approval; executive exercise participation |
| **Per-Client SDMs**                 | Client exercise coordination                               |
| **Red Team Lead**                   | Red team scheduling coordination                           |
| **All Participants**                | Calendar commitment; preparation; participation            |

---

# 6. Minimum Annual Exercise Requirements (Mandatory)

| Exercise Type                | Minimum Quantity | Cadence                   |
| ---------------------------- | ---------------- | ------------------------- |
| **Tabletop Exercises (TTX)** | 8                | Quarterly (2 per quarter) |
| **Red Team Engagements**     | 4                | Quarterly                 |
| **Purple Team Exercises**    | 4                | Quarterly                 |
| **BAS / CART**               | Continuous       | Daily/weekly automated    |
| **Operational Drills**       | 4                | Quarterly                 |
| **Executive TTX**            | 1                | Annual                    |
| **Multi-Tenant / CCIC TTX**  | 2                | Semi-annual               |
| **Client Exercises**         | Per MSA          | Per MSA                   |
| **Onboarding Exercises**     | Per cohort       | Per cohort                |
| **Post-Incident Exercises**  | As triggered     | Per major incident        |
| **Regulatory Drills**        | Per regulation   | Per regulation            |

---

# 7. Annual Calendar (Mandatory)

## 7.1 Q1 (January – March)

| Month | Week | Exercise Type      | Scenario / Focus                    | Audience                  | Owner              |
| ----- | ---- | ------------------ | ----------------------------------- | ------------------------- | ------------------ |
| Jan   | W2   | TTX                | Ransomware                          | L1+L2+L3+IR Team+SOC Lead | IR Team Lead       |
| Jan   | W3   | Purple Team        | Initial Access + Execution TTPs     | L2+L3+Detection Eng       | Detection Eng Lead |
| Jan   | W4   | Operational Drill  | IR Team activation drill            | IR Team                   | IR Team Lead       |
| Feb   | W1   | TTX                | Phishing/BEC                        | L1+L2+SOC Lead            | SOC Manager        |
| Feb   | W2   | Red Team           | Black Box internal SOC validation   | SOC (unaware)             | Red Team Lead      |
| Feb   | W4   | BAS Review         | Q4 BAS results review + gap closure | Detection Eng             | Detection Eng Lead |
| Mar   | W1   | Client TTX         | Per Tier-1 client MSA               | Per client + SDM          | Per-Client SDM     |
| Mar   | W3   | Onboarding TTX     | New analyst cohort exercise         | New L1/L2                 | Training Lead      |
| Mar   | W4   | Q1 Exercise Review | Review Q1 completion + gaps         | All leads                 | IR Team Lead       |

## 7.2 Q2 (April – June)

| Month | Week | Exercise Type      | Scenario / Focus                        | Audience                 | Owner              |
| ----- | ---- | ------------------ | --------------------------------------- | ------------------------ | ------------------ |
| Apr   | W1   | TTX                | APT Campaign                            | L3+IR Team+TI+Legal+CISO | IR Team Lead       |
| Apr   | W2   | Purple Team        | Defense Evasion + Credential Access     | L2+L3+Detection Eng      | Detection Eng Lead |
| Apr   | W3   | Operational Drill  | Escalation drill (L1→L2→L3→IR)          | All SOC tiers            | SOC Manager        |
| May   | W1   | TTX                | Insider Threat                          | L2+L3+IR+HR+Legal        | IR Team Lead       |
| May   | W2   | Red Team           | Grey Box per-client engagement (Tier 1) | Per client + SOC         | Red Team Lead      |
| May   | W4   | Multi-Tenant TTX   | CCIC coordination exercise              | IR Team+SDMs+TI          | IR Team Lead       |
| Jun   | W1   | Client TTX         | Per Tier-1 client MSA                   | Per client + SDM         | Per-Client SDM     |
| Jun   | W2   | BAS Review         | Q1 BAS results review + gap closure     | Detection Eng            | Detection Eng Lead |
| Jun   | W3   | Onboarding TTX     | New analyst cohort exercise             | New L1/L2                | Training Lead      |
| Jun   | W4   | Q2 Exercise Review | Review Q2 completion + gaps             | All leads                | IR Team Lead       |

## 7.3 Q3 (July – September)

| Month | Week | Exercise Type      | Scenario / Focus                      | Audience                  | Owner              |
| ----- | ---- | ------------------ | ------------------------------------- | ------------------------- | ------------------ |
| Jul   | W1   | TTX                | Data Breach / Exfiltration            | L2+L3+IR+Legal+DPO+CISO   | IR Team Lead       |
| Jul   | W2   | Purple Team        | Lateral Movement + Collection + C2    | L2+L3+Detection Eng       | Detection Eng Lead |
| Jul   | W3   | Operational Drill  | Shift handover drill                  | L1+L2+SOC Lead            | SOC Manager        |
| Aug   | W1   | TTX                | Cloud Security Incident               | L2+L3+IR+Cloud Specialist | IR Team Lead       |
| Aug   | W2   | Red Team           | White Box for new playbook validation | SOC + Detection Eng       | Red Team Lead      |
| Aug   | W4   | Regulatory Drill   | RBI cyber drill (if applicable)       | All + Compliance          | Compliance Lead    |
| Sep   | W1   | Client TTX         | Per Tier-1 client MSA                 | Per client + SDM          | Per-Client SDM     |
| Sep   | W2   | BAS Review         | Q2 BAS results review + gap closure   | Detection Eng             | Detection Eng Lead |
| Sep   | W3   | Onboarding TTX     | New analyst cohort exercise           | New L1/L2                 | Training Lead      |
| Sep   | W4   | Q3 Exercise Review | Review Q3 completion + gaps           | All leads                 | IR Team Lead       |

## 7.4 Q4 (October – December)

| Month | Week | Exercise Type                          | Scenario / Focus                                 | Audience                        | Owner              |
| ----- | ---- | -------------------------------------- | ------------------------------------------------ | ------------------------------- | ------------------ |
| Oct   | W1   | TTX                                    | Supply Chain Attack                              | L3+IR+TI+Vendor Mgmt            | IR Team Lead       |
| Oct   | W2   | Purple Team                            | Exfiltration + Impact + Full adversary emulation | All tiers + Detection Eng       | Detection Eng Lead |
| Oct   | W3   | Operational Drill                      | Communication drill (bridge call simulation)     | IR Team+SOC Lead                | IR Team Lead       |
| Nov   | W1   | Multi-Tenant TTX                       | Cross-client supply chain scenario               | IR Team+SDMs+TI+CISO            | IR Team Lead       |
| Nov   | W2   | Red Team                               | Black Box annual maturity assessment             | SOC (unaware)                   | Red Team Lead      |
| Nov   | W3   | Executive TTX                          | Strategic ransomware + breach (CISO+Exec)        | CISO+Executive+Legal+Compliance | IR Team Lead       |
| Dec   | W1   | Client TTX                             | Per Tier-1 client MSA                            | Per client + SDM                | Per-Client SDM     |
| Dec   | W2   | BAS Review | Q3 BAS results review + gap closure              | Detection Eng                   | Detection Eng Lead |
| Dec   | W3   | Annual Exercise Review                 | Full year review + next year planning            | All leads+CISO                  | IR Team Lead       |
| Dec   | W4   | Next Year Schedule Published           | Annual schedule for Y+1                          | All stakeholders                | IR Team Lead       |

---

# 8. Client Exercise Schedule Integration (Mandatory)

## 8.1 Per-Client Requirements

| Client Tier                 | Minimum Exercise per Year | Type                        |
| --------------------------- | ------------------------- | --------------------------- |
| Tier 1 (Critical/Regulated) | 4 (quarterly)             | TTX + per-client red/purple |
| Tier 2 (Standard)           | 2 (semi-annual)           | TTX                         |
| Tier 3 (Monitoring-only)    | 1 (annual)                | TTX                         |
| Custom per MSA              | Per MSA                   | Per MSA                     |

## 8.2 Client Exercise Coordination

| Step                                         | Owner               |
| -------------------------------------------- | ------------------- |
| Client exercise requirements documented      | SDM                 |
| Client exercise scheduled in annual calendar | Training Lead + SDM |
| Client participants confirmed                | SDM                 |
| Client exercise executed                     | IR Team Lead + SDM  |
| Client exercise AAR delivered                | IR Team Lead + SDM  |

---

# 9. Post-Incident Exercise Triggers (Mandatory)

| Trigger                            | Exercise Type                          | Timeline       |
| ---------------------------------- | -------------------------------------- | -------------- |
| P1 incident (any client)           | TTX based on real incident (sanitized) | Within 60 days |
| Major detection gap discovered     | Purple team for gap area               | Within 30 days |
| New playbook published             | TTX + purple validation                | Within 45 days |
| New tool deployed                  | Purple team for tool validation        | Within 30 days |
| Regulatory directive               | Per regulator requirement              | Per timeline   |
| Major industry incident (external) | TTX based on external incident         | Within 90 days |

---

# 10. Resource Planning (Mandatory)

## 10.1 Annual Resource Requirements

| Resource                             | Annual Estimate               |
| ------------------------------------ | ----------------------------- |
| Facilitator/evaluator hours          | ~200 hours                    |
| Red team operator hours              | ~160 hours                    |
| Purple team operator hours           | ~120 hours                    |
| Blue team participant hours          | ~400 hours (across all tiers) |
| Detection engineering (tuning) hours | ~120 hours                    |
| Training Lead (admin) hours          | ~100 hours                    |
| Venue/logistics budget               | Per organization              |

## 10.2 Scheduling Constraints

| Constraint                               | Mitigation                            |
| ---------------------------------------- | ------------------------------------- |
| Avoid during peak SOC workload months    | Schedule around holiday/audit periods |
| Red team not during real incident surge  | Hot stop protocol                     |
| Client exercises per client availability | SDM coordination                      |
| Executive availability                   | Calendar hold 6 months advance        |
| Multi-timezone coordination              | Follow-the-sun scheduling             |

---

# 11. Exercise Metrics (Mandatory)

| Metric                               | Target              |
| ------------------------------------ | ------------------- |
| Annual TTX count                     | ≥8                  |
| Annual red team count                | ≥4                  |
| Annual purple team count             | ≥4                  |
| Annual operational drill count       | ≥4                  |
| Client exercise obligations met      | 100%                |
| Regulatory exercise obligations met  | 100%                |
| AAR completion within 14 days        | 100%                |
| Action item closure (90 days)        | ≥80%                |
| Detection coverage improvement (YoY) | Measurable increase |
| Participant attendance rate          | ≥90%                |
| Executive exercise participation     | ≥1 annually         |

---

# 12. Quarterly Exercise Review (Mandatory)

| Review Element                  | Frequency | Owner              |
| ------------------------------- | --------- | ------------------ |
| Exercises completed vs planned  | Quarterly | Training Lead      |
| Exercises rescheduled/cancelled | Quarterly | Training Lead      |
| AAR completion status           | Quarterly | Training Lead      |
| Action item closure status      | Quarterly | Training Lead      |
| Detection improvement progress  | Quarterly | Detection Eng Lead |
| Client obligation status        | Quarterly | SDM Leads          |
| Next quarter readiness          | Quarterly | IR Team Lead       |

---

# 13. Annual Exercise Review (Mandatory)

| Review Element                      | Annual   | Owner              |
| ----------------------------------- | -------- | ------------------ |
| Full year exercise execution report | December | Training Lead      |
| Year-over-year coverage comparison  | December | Detection Eng Lead |
| Year-over-year maturity comparison  | December | IR Team Lead       |
| Client exercise completion report   | December | SDM Leads          |
| Regulatory obligation completion    | December | Compliance Lead    |
| Next year schedule draft            | December | IR Team Lead       |
| Next year schedule approval         | December | CISO               |
| Next year schedule publication      | December | Training Lead      |
| CISO sign-off                       | December | CISO               |

---

# 14. Quality Checklist (Annual Schedule Management)

- [ ] Annual schedule published before January 1
- [ ] All mandatory exercise types included
- [ ] All client obligations included
- [ ] All regulatory obligations included
- [ ] Executive exercise scheduled
- [ ] Multi-tenant exercises scheduled
- [ ] BAS/CART schedule confirmed
- [ ] Resource allocation confirmed
- [ ] Calendar holds placed for all exercises
- [ ] Quarterly reviews scheduled
- [ ] Annual review scheduled
- [ ] CISO approval obtained

---

# 15. Related Documents

| Document                       | Path                                                                               |
| ------------------------------ | ---------------------------------------------------------------------------------- |
| Tabletop Exercise Guide        | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`     |
| TTX Ransomware Scenario        | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Ransomware-Scenario.md`     |
| TTX APT Scenario               | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-APT-Scenario.md`            |
| TTX Insider Threat Scenario    | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Insider-Threat-Scenario.md` |
| TTX Data Breach Scenario       | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-DataBreach-Scenario.md`     |
| TTX Evaluation Scorecard       | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Evaluation-Scorecard.md`    |
| Red Team IR Integration SOP    | `10_TRAINING-AND-EXERCISES/10.3_Drills/Red-Team-IR-Integration-SOP.md`             |
| Purple Team Exercise Guide     | `10_TRAINING-AND-EXERCISES/10.3_Drills/Purple-Team-Exercise-Guide.md`              |
| Drill After-Action Report      | `10_TRAINING-AND-EXERCISES/10.3_Drills/Drill-After-Action-Report.md`               |
| Detection Improvement Log      | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`          |
| Playbook Update Log            | `08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`                |
| Action Items Tracker           | `08_POST-INCIDENT/08.1_Lessons-Learned/Action-Items-Tracker.xlsx`                  |
| MSSP Audit Readiness Checklist | `09_MSSP-SPECIFIC/09.4_MSSP-Compliance/MSSP-Audit-Readiness-Checklist.md`          |
| Client Data Segregation Policy | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`  |

---

# 16. Revision History

| Version | Date        | Author                          | Changes         |
| ------- | ----------- | ------------------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP IR Team Lead / SOC Manager | Initial version |

---

# 17. Approval

Approved by:

| Role               | Name | Signature | Date |
| ------------------ | ---- | --------- | ---- |
| MSSP IR Team Lead  |      |           |      |
| MSSP SOC Manager   |      |           |      |
| MSSP Training Lead |      |           |      |
| MSSP CISO          |      |           |      |

---

**End of Document**
