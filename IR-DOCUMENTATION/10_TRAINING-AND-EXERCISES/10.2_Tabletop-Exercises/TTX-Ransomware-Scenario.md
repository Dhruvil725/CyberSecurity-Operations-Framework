# Tabletop Exercise – Ransomware Scenario

---

# 1. Document Control

| Field                | Value                                                               |
| -------------------- | ------------------------------------------------------------------- |
| Document Name        | TTX – Ransomware Scenario                                           |
| Document ID          | MSSP-TRN-TTX-005                                                    |
| Version              | 1.0                                                                 |
| Effective Date       | 30-May-2026                                                         |
| Owner                | MSSP IR Team Lead / SOC Manager                                     |
| Approved By          | MSSP CISO                                                           |
| Classification       | Confidential – MSSP Internal                                        |
| Review Cycle         | Annually (or upon major ransomware campaign update)                 |
| Scenario Difficulty  | High                                                                |
| Recommended Audience | L1 + L2 + L3 + IR Team + SOC Lead + Compliance + Legal + CISO + SDM |

---

# 2. Purpose

This document defines a standardized **Ransomware Tabletop Exercise Scenario** designed to test the MSSP's ability to detect, investigate, contain, eradicate, and recover from a major ransomware incident with double-extortion (encryption + data exfiltration) across multi-tenant environments — validating SOC tier coordination from L1 to IR Team, containment authority decision-making, ransom-payment policy application, regulatory engagement, legal coordination, executive communication, client recovery support, BCP/DR coordination, and post-incident program improvement.

A formal Ransomware TTX is critical because:

- ransomware is the most common high-severity incident type for MSSP clients
- modern ransomware is double-extortion (encryption + data theft) requiring breach response in parallel
- containment timing under ransomware is critical — minutes affect business impact
- ransom-payment policy decisions involve Legal, CISO, executive leadership, sometimes regulators
- BCP/DR coordination during ransomware is rarely practiced end-to-end live
- multi-tenant MSSPs face ransomware affecting multiple clients in same campaign
- CCIC coordination for cross-client ransomware campaigns must be rehearsed
- regulatory engagement (RBI, CERT-In, DPDP, sector-specific) is mandatory for major ransomware
- executive communication under ransomware pressure must be practiced
- client recovery support spans days/weeks — coordination patterns matter
- forensic preservation while restoring operations requires expert balance
- ISO 27001 A.5.24/A.5.29/A.5.30 and NIST CSF RS.MA, RS.MI, RC.RP require validated ransomware readiness
- RBI Cyber Security Framework requires demonstrated ransomware preparedness for BFSI
- without structured TTX, ransomware response gaps lead to extended downtime and regulatory exposure
- this scenario is the foundation for annual mandatory ransomware exercise

This scenario ensures:

- structured ransomware simulation across detection, containment, eradication, recovery
- end-to-end SOC tier coordination (L1 → L2 → L3 → IR Team)
- double-extortion handling (encryption + exfiltration in parallel)
- ransom-payment policy decision-making
- BCP/DR coordination
- multi-tenant CCIC handling (if campaign-style)
- regulatory engagement workflow validation
- legal coordination practice
- executive and client communication under pressure
- forensic preservation during recovery
- post-incident threat intelligence output for portfolio defense
- audit-ready exercise documentation

**Reference alignment:**

- `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`
- `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Master.md`
- `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Containment.md`
- `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Recovery.md`

---

# 3. Scenario Overview

| Field                               | Value                                                                             |
| ----------------------------------- | --------------------------------------------------------------------------------- |
| **Scenario Name**                   | "Operation Frozen Vault"                                                          |
| **Scenario Type**                   | Discussion-Based Tabletop Exercise                                                |
| **Difficulty**                      | High                                                                              |
| **Estimated Duration**              | 4-6 hours (full day with breaks recommended)                                      |
| **Threat Category**                 | Ransomware (Double-Extortion)                                                     |
| **Threat Actor (fictional)**        | "BlackTide" ransomware-as-a-service (RaaS) affiliate                              |
| **Targeted Industry (in scenario)** | Manufacturing / Logistics (single MSSP client primary; portfolio echoes optional) |
| **Affected Client (in scenario)**   | "AutoLogix" — fictional automotive parts manufacturer & distributor               |
| **Initial Access Vector**           | Phishing → MFA bypass → VPN credential theft → lateral movement                   |
| **Detection Method**                | EDR mass-encryption alerts + SIEM correlation                                     |
| **Encryption Scope**                | ~3,500 servers + 8,000 endpoints across 4 sites                                   |
| **Exfiltration Scope**              | ~1.2 TB of business data including customer/supplier records                      |
| **Ransom Demand**                   | $15M USD in cryptocurrency                                                        |
| **Primary Objective**               | Test full ransomware lifecycle including double-extortion + recovery              |

---

# 4. TTX Objectives (Mandatory)

| ID         | Objective                                               | Success Criteria                                                |
| ---------- | ------------------------------------------------------- | --------------------------------------------------------------- |
| **OBJ-1**  | Validate L1 ransomware detection and escalation         | L1 escalates to L2 within 15 min of first mass-encryption alert |
| **OBJ-2**  | Test L2/L3 investigation under pressure                 | L2/L3 produce initial scope within 60 min                       |
| **OBJ-3**  | Validate IR Team activation for P1 ransomware           | IR Team Lead assumes IC within 30 min                           |
| **OBJ-4**  | Test containment authority decision (network isolation) | Containment decision per authority matrix within 45 min         |
| **OBJ-5**  | Validate double-extortion handling (encryption + exfil) | Data theft confirmed; breach response triggered in parallel     |
| **OBJ-6**  | Test BCP/DR coordination                                | DR plans activated; recovery priorities set within 90 min       |
| **OBJ-7**  | Validate ransom-payment policy application              | Payment decision discussion per policy with Legal + CISO + Exec |
| **OBJ-8**  | Test regulatory engagement (RBI + CERT-In + DPDP)       | All reports drafted within respective timelines                 |
| **OBJ-9**  | Validate legal coordination                             | Legal hold issued; law enforcement decision per Legal           |
| **OBJ-10** | Test executive + client communication                   | CISO + Client CISO briefed; cadence maintained                  |
| **OBJ-11** | Validate forensic preservation during recovery          | CoC maintained while restoring operations                       |
| **OBJ-12** | Test multi-tenant discipline                            | No cross-client information leakage                             |
| **OBJ-13** | Validate sanitized cross-portfolio TI brief             | Sanitized IoC/TTP brief for other MSSP clients                  |

---

# 5. Participants and Roles (Mandatory)

## 5.1 Required Participants

| Role                       | Played By             | Active in Scenario       |
| -------------------------- | --------------------- | ------------------------ |
| L1 Analyst                 | L1 Analyst            | Yes (initial detection)  |
| L2 Lead Analyst            | Senior L2             | Yes                      |
| L3 Forensics Lead          | Senior L3             | Yes                      |
| Threat Intel Lead          | Threat Intel Lead     | Yes                      |
| SOC Lead                   | SOC Lead              | Yes                      |
| IR Team Lead               | Senior IR Team member | Yes (Incident Commander) |
| Per-Client SDM (AutoLogix) | SDM                   | Yes                      |
| Compliance Lead            | Compliance Lead       | Yes                      |
| Legal Counsel              | Legal Counsel         | Yes                      |
| MSSP CISO                  | CISO                  | Yes (executive role)     |
| Detection Engineer         | Detection Eng         | Yes                      |

## 5.2 Optional / Observer Participants

| Role                                | Played By          |
| ----------------------------------- | ------------------ |
| Junior L1/L2/L3 (learning)          | Observer           |
| New IR Team member (learning)       | Observer           |
| Internal Auditor                    | Observer           |
| BCP/DR Lead (if separate)           | Observer or Active |
| HR Lead                             | Observer           |
| Insurance / Cyber Insurance Liaison | Observer           |
| Negotiation Specialist (3rd party)  | Observer           |

## 5.3 White Team (Facilitators + Evaluators)

| Role                                | Person                              |
| ----------------------------------- | ----------------------------------- |
| Lead Facilitator                    | IR Team Lead (or designated senior) |
| Co-Facilitator                      | SOC Manager                         |
| Evaluator – SOC Tier Coordination   | SOC Manager                         |
| Evaluator – IR Command              | IR Team Lead                        |
| Evaluator – Containment Authority   | IR Team Lead                        |
| Evaluator – BCP/DR                  | BCP/DR Lead                         |
| Evaluator – Ransom Policy           | Legal Counsel + CISO                |
| Evaluator – Regulatory              | Compliance Lead                     |
| Evaluator – Multi-Tenant Discipline | Compliance Lead                     |
| Evaluator – Communication           | CISO or designate                   |
| Timekeeper                          | Training Lead                       |
| Scribe / Note-Taker                 | Training Lead                       |

---

# 6. Threat Actor Profile (Fictional – for Realism)

| Attribute                     | Detail                                                                         |
| ----------------------------- | ------------------------------------------------------------------------------ |
| **Actor Name (fictional)**    | BlackTide (RaaS)                                                               |
| **Affiliate**                 | "Crimson-Wave" (fictional)                                                     |
| **Motivation**                | Financial — double-extortion model                                             |
| **Sophistication**            | High — modern RaaS with affiliate program                                      |
| **Known TTPs (MITRE ATT&CK)** | T1566.001, T1078, T1133, T1110.003, T1059.001, T1486, T1490, T1567.002, T1041  |
| **Tooling**                   | Custom encryptor; Cobalt Strike; Mimikatz; Rclone for exfil; PsExec for spread |
| **Infrastructure**            | TOR-hosted negotiation portal; leak site for non-payers                        |
| **Encryption**                | AES-256 + RSA-4096; fast multi-threaded encryption                             |
| **Exfiltration**              | Rclone to cloud storage prior to encryption                                    |
| **Negotiation**               | TOR portal with auto-generated victim ID; tiered demands                       |
| **Public Profile**            | Active leak site; published 200+ victims in past year                          |

---

# 7. Scenario Background

## 7.1 MSSP Context

The MSSP provides 24x7 MDR services to AutoLogix:

- **AutoLogix** – Mid-size automotive parts manufacturer + distributor; ~12,000 employees; 4 sites (HQ + 3 plants)
- ~11,500 endpoints + ~3,500 servers (mix of Windows + Linux)
- Customer base: 800+ B2B customers (auto OEMs, dealerships, repair networks)
- Critical operations: ERP, manufacturing control systems (limited segmentation), warehouse mgmt
- Subject to DPDP Act, sector-specific data protection, contractual obligations to OEM customers

## 7.2 Initial Situation (Day 0 — Detection Day)

The MSSP SOC begins receiving alerts at 02:17 AM local time:

| Time           | Event                                                                         | Source           |
| -------------- | ----------------------------------------------------------------------------- | ---------------- |
| T+0 (02:17 AM) | EDR alert: 50+ endpoints showing rapid file modification (encryption pattern) | EDR              |
| T+5 min        | EDR alert: file extensions changing to ".blacktide" on multiple servers       | EDR              |
| T+10 min       | SIEM: ransom note files ("README_BLACKTIDE.txt") being created across network | SIEM             |
| T+15 min       | EDR: domain controller showing encryption activity                            | EDR              |
| T+20 min       | Network: unusual outbound traffic 6 hours earlier to cloud storage (~1.2 TB)  | NDR (historical) |

**Hidden background (revealed via injects):**

- Initial access via spear-phishing 12 days ago (HR person clicked invoice attachment)
- MFA bypassed via session token theft
- Threat actor moved laterally over 8 days; harvested credentials
- Cobalt Strike beacons deployed on 47 systems
- Data exfiltration via Rclone to actor cloud storage (6 hours before encryption)
- Encryption launched simultaneously across 4 sites at 02:00 AM
- ~1.2 TB exfiltrated includes:
  - Customer master records (~400 GB)
  - Supplier contracts + pricing (~200 GB)
  - HR records (~150 GB)
  - R&D blueprints (~250 GB)
  - Financial data (~200 GB)
- Ransom demand: $15M USD; deadline 7 days; leak site countdown active

---

# 8. Master Scenario Events List (MSEL) — FACILITATOR ONLY

⚠️ **CONFIDENTIAL — DO NOT SHARE WITH PARTICIPANTS BEFORE EXERCISE**

## 8.1 Phase 1: Detection & Initial Escalation (T+0 to T+30 min)

| #   | T+     | Method  | Content                                                                                  | Expected Response                                                      | Evaluator Notes              |
| --- | ------ | ------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------- | ---------------------------- |
| 1   | 0 min  | Verbal  | "EDR alert: 50+ endpoints showing rapid file modification — encryption pattern detected" | L1 acknowledges; immediate escalation to L2                            | TTA < 5 min                  |
| 2   | 5 min  | Verbal  | "EDR alert: file extensions changing to '.blacktide' on multiple servers"                | L1 escalates to L2 + SOC Lead                                          | Escalation < 10 min          |
| 3   | 10 min | Written | "SIEM: ransom note files ('README_BLACKTIDE.txt') across network"                        | L2 confirms ransomware; SOC Lead notifies IR Team Lead                 | Confirmation rapid           |
| 4   | 15 min | Verbal  | "EDR: domain controller showing encryption activity"                                     | Severity P1 declared; IR Team activation triggered                     | Severity correct             |
| 5   | 20 min | Verbal  | "Network: ~1.2 TB outbound to unknown cloud 6 hours earlier"                             | **Double-extortion recognized**; breach response triggered in parallel | Double-extortion recognition |
| 6   | 25 min | Verbal  | "IR Team Lead activates — assumes IC"                                                    | IR Team Lead assumes command; war room opens                           | IC assumption < 30 min       |

## 8.2 Phase 2: Containment Decision & Authority (T+30 to T+60 min)

| #   | T+     | Method | Content                                                                            | Expected Response                             | Evaluator Notes     |
| --- | ------ | ------ | ---------------------------------------------------------------------------------- | --------------------------------------------- | ------------------- |
| 7   | 35 min | Verbal | "Question: full network isolation (kill switch) or surgical containment?"          | Decision per containment authority matrix     | Authority applied   |
| 8   | 40 min | Verbal | "Per-Client SDM: AutoLogix CIO on phone — wants immediate guidance"                | SDM coordinates per-client decision           | Client coordination |
| 9   | 45 min | Verbal | "AutoLogix CIO authorizes network isolation at all 4 sites"                        | Per-client authority respected; MSSP executes | Authority respected |
| 10  | 50 min | Verbal | "Containment action: VPN + internet gateways disabled; site interconnects severed" | Containment executed; documented              | Execution timing    |
| 11  | 55 min | Verbal | "Question: also disable encryption-active hosts immediately?"                      | Containment vs evidence balance               | Balance discussed   |

## 8.3 Phase 3: Forensic Scoping + BCP/DR Activation (T+60 to T+120 min)

| #   | T+      | Method  | Content                                                                     | Expected Response                                     | Evaluator Notes          |
| --- | ------- | ------- | --------------------------------------------------------------------------- | ----------------------------------------------------- | ------------------------ |
| 12  | 65 min  | Verbal  | "L3 begins forensic scoping while containment holds"                        | L3 deep investigation begins                          | L3 methodology           |
| 13  | 75 min  | Written | "Initial scope: ~3,500 servers + ~8,000 endpoints encrypted across 4 sites" | Scope quantified                                      | Scoping rigor            |
| 14  | 85 min  | Verbal  | "AutoLogix CIO: BCP/DR needs to activate — which systems priority?"         | DR priorities discussed; per-client decision          | DR coordination          |
| 15  | 95 min  | Verbal  | "Priority systems: ERP, customer order portal, manufacturing control"       | Recovery prioritization framework applied             | Prioritization framework |
| 16  | 105 min | Verbal  | "DR site activation: hot standby for ERP; warm for others"                  | DR activation coordinated                             | DR activation timing     |
| 17  | 115 min | Verbal  | "L3 identifies Cobalt Strike beacons on 47 systems — actor presence"        | Actor presence confirmed; eradication scope expanding | Actor identification     |

## 8.4 Phase 4: Double-Extortion & Ransom Decision (T+120 to T+180 min)

| #   | T+      | Method | Content                                                                                       | Expected Response                                                  | Evaluator Notes     |
| --- | ------- | ------ | --------------------------------------------------------------------------------------------- | ------------------------------------------------------------------ | ------------------- |
| 18  | 125 min | Verbal | "Ransom note demands $15M USD; 7-day deadline; data leak threat"                              | Ransom intel triaged                                               | Ransom triage       |
| 19  | 135 min | Verbal | "Question: AutoLogix asks MSSP — should we pay?"                                              | **Per policy**: MSSP advises; client decides; Legal + Exec engaged | Policy applied      |
| 20  | 145 min | Verbal | "Legal Counsel weighs in: sanctions screening on actor required before payment consideration" | Sanctions screening initiated                                      | Legal compliance    |
| 21  | 155 min | Verbal | "Cyber insurance carrier joins call — wants status"                                           | Insurance coordination                                             | Insurance liaison   |
| 22  | 165 min | Verbal | "Question: engage professional ransomware negotiator?"                                        | 3rd-party negotiator decision per client                           | Negotiator decision |
| 23  | 175 min | Verbal | "AutoLogix Board convening emergency meeting — needs MSSP brief"                              | Executive brief prepared; CISO + IR Team Lead deliver              | Exec brief quality  |

## 8.5 Phase 5: Regulatory + Legal + Customer Notification (T+180 to T+240 min)

| #   | T+      | Method | Content                                                                                     | Expected Response                           | Evaluator Notes         |
| --- | ------- | ------ | ------------------------------------------------------------------------------------------- | ------------------------------------------- | ----------------------- |
| 24  | 185 min | Verbal | "CERT-In 6-hour reporting clock — must file"                                                | Compliance drafts CERT-In report            | CERT-In timing          |
| 25  | 195 min | Verbal | "DPDP — 1.2 TB exfil includes customer records — breach notification triggers"              | DPDP timeline applied; DPO/Legal coordinate | DPDP awareness          |
| 26  | 205 min | Verbal | "Sector regulator: automotive OEM customers may have contractual notification requirements" | Contractual notification reviewed           | Contractual awareness   |
| 27  | 215 min | Verbal | "AutoLogix B2B customers (OEMs) demanding to know if their data was exfiltrated"            | Customer notification strategy via Legal    | Customer comms strategy |
| 28  | 225 min | Verbal | "Press leak: cybersecurity news outlet has BlackTide leak site link"                        | Press response via Legal + Client PR        | Press coordination      |
| 29  | 235 min | Verbal | "Law enforcement engagement decision?"                                                      | Legal-led decision per protocol             | LE decision             |

## 8.6 Phase 6: Eradication + Recovery + Post-Incident (T+240 to T+360 min)

| #   | T+      | Method | Content                                                                                | Expected Response                                            | Evaluator Notes          |
| --- | ------- | ------ | -------------------------------------------------------------------------------------- | ------------------------------------------------------------ | ------------------------ |
| 30  | 245 min | Verbal | "Eradication plan: rebuild compromised systems; rotate ALL credentials; remove all C2" | Eradication plan articulated                                 | Plan comprehensive       |
| 31  | 260 min | Verbal | "Recovery sequencing: ERP first; then customer-facing; then internal"                  | Recovery sequence per business priority                      | Sequence rationale       |
| 32  | 275 min | Verbal | "Question: restore from backups (clean state) or decrypt (risky)?"                     | Backup restoration preferred; decryption only as last resort | Restoration strategy     |
| 33  | 290 min | Verbal | "Backup integrity check: last clean backup 48 hours old; manageable data loss"         | Backup integrity validated                                   | Backup discipline        |
| 34  | 305 min | Verbal | "Forensic preservation: which evidence captured before rebuild?"                       | Forensic-grade preservation; CoC maintained                  | Forensic balance         |
| 35  | 320 min | Verbal | "AutoLogix CISO asks: 'Any lessons applicable to other MSSP clients?' (sanitized)"     | Sanitized cross-portfolio brief planned                      | Sanitization process     |
| 36  | 335 min | Verbal | "Long-term monitoring: 90-day intensified monitoring for residual actor presence"      | Long-term plan articulated                                   | Long-term plan           |
| 37  | 350 min | Verbal | "Lessons learned + Playbook updates queued"                                            | Post-incident process triggered                              | Post-incident discipline |
| 38  | 360 min | Verbal | "Scenario freeze — move to hot wash"                                                   | Hot wash begins                                              | —                        |

---

# 9. Pre-Read for Participants (NON-CONFIDENTIAL)

## 9.1 Scenario Brief (Share with Participants Pre-TTX)

### Background

You will participate in a 4-6 hour tabletop exercise simulating a major double-extortion ransomware incident at an MSSP client — an automotive parts manufacturer with 3,500 servers and 8,000 endpoints encrypted across 4 sites, plus 1.2 TB of data exfiltrated before encryption. The scenario involves end-to-end SOC tier coordination (L1 → IR Team), containment authority decisions, BCP/DR activation, ransom-payment policy application, regulatory engagement (CERT-In, DPDP, sector), legal coordination, executive briefings, customer notifications, and forensic preservation during recovery.

### Your Preparation

Before the TTX, please:

1. Review your role-specific playbooks (Ransomware Master, Containment, Recovery)
2. Review your role-specific SOPs
3. Review the Client Data Segregation Policy
4. Review the IRT Containment Authority Matrix
5. Review the Legal Counsel Engagement SOP
6. Be ready to engage as your actual role under realistic pressure

### What You Will NOT Have

- The Master Scenario Events List (MSEL) — facilitator only
- Specific inject timing
- Resolution path — to be determined by your decisions

### Ground Rules

- This is a safe, no-blame learning environment
- Engage authentically as your role
- Make decisions using actual playbooks and SOPs
- Maintain multi-tenant discipline
- Per-client authority is critical — MSSP advises; client decides
- Legal-first sequencing for breach + ransom decisions
- All decisions will be documented and discussed in hot wash
- Hot wash will follow immediately; AAR within 14 days

---

# 10. Evaluation Framework (Mandatory)

## 10.1 Per-Objective Scoring

Use `TTX-Evaluation-Scorecard.md` for detailed scoring. Summary:

| Objective                            | Evaluator               | Pass Threshold      |
| ------------------------------------ | ----------------------- | ------------------- |
| OBJ-1: L1 Detection & Escalation     | SOC Tier Evaluator      | Score ≥3            |
| OBJ-2: L2/L3 Investigation           | Forensic Evaluator      | Score ≥3            |
| OBJ-3: IR Team Activation            | IR Command Evaluator    | Score ≥3            |
| OBJ-4: Containment Authority         | Containment Evaluator   | Score ≥4 (critical) |
| OBJ-5: Double-Extortion Handling     | IR Command Evaluator    | Score ≥4 (critical) |
| OBJ-6: BCP/DR Coordination           | BCP/DR Evaluator        | Score ≥3            |
| OBJ-7: Ransom-Payment Policy         | Ransom Policy Evaluator | Score ≥4 (critical) |
| OBJ-8: Regulatory Engagement         | Compliance Evaluator    | Score ≥3            |
| OBJ-9: Legal Coordination            | Legal Evaluator         | Score ≥3            |
| OBJ-10: Executive + Client Comms     | Communication Evaluator | Score ≥3            |
| OBJ-11: Forensic Preservation        | L3 Evaluator            | Score ≥3            |
| OBJ-12: Multi-Tenant Discipline      | Multi-Tenant Evaluator  | Score ≥4 (critical) |
| OBJ-13: Sanitized Cross-Portfolio TI | Multi-Tenant Evaluator  | Score ≥3            |

## 10.2 Critical Failure Triggers

The TTX is marked **FAIL** if any of:

- Containment action without per-client authorization (where required)
- Double-extortion missed (only encryption treated; data theft ignored)
- Ransom-payment decision made unilaterally by MSSP
- Sanctions screening skipped before payment consideration
- CERT-In 6-hour reporting timeline missed
- DPDP notification timeline ignored
- Legal hold not issued before forensic activities
- Backup restoration skipped in favor of decryption without justification
- Cross-client information leakage
- Public statement without legal + client approval
- Forensic evidence destroyed during rebuild

---

# 11. Hot Wash Agenda (Mandatory)

| Time      | Activity                            |
| --------- | ----------------------------------- |
| 0-10 min  | What went well — round robin        |
| 10-25 min | What did not go well — round robin  |
| 25-40 min | Specific gaps identified            |
| 40-50 min | Quick wins (immediate improvements) |
| 50-60 min | Next steps + AAR timeline           |

---

# 12. Expected Findings Areas (For Facilitator Preparation)

Based on prior Ransomware TTX patterns, expect findings in:

| Area                          | Common Gaps                                         |
| ----------------------------- | --------------------------------------------------- |
| Double-extortion recognition  | Treating only encryption; missing data exfiltration |
| Containment authority         | MSSP overstepping client authority                  |
| Ransom-payment policy         | Unclear who decides; sanctions screening missed     |
| BCP/DR coordination           | Underestimating coordination complexity             |
| Backup integrity              | Assuming backups clean without validation           |
| Regulatory parallel reporting | Multiple regulators with different timelines        |
| Customer notification         | B2B customer notification obligations missed        |
| Insurance coordination        | Carrier requirements unclear                        |
| Forensic preservation         | Evidence destroyed during rebuild                   |
| Long-term monitoring          | Underestimating post-incident vigilance             |

---

# 13. Improvement Areas to Probe (Facilitator Prompts)

If participants miss these, prompt with:

| Prompt                                                | Tests                        |
| ----------------------------------------------------- | ---------------------------- |
| "Is this double-extortion?"                           | Double-extortion recognition |
| "Who has containment authority for this client?"      | Authority matrix             |
| "What's the policy on ransom payment?"                | Ransom policy                |
| "Has sanctions screening been done?"                  | Legal compliance             |
| "Are backups clean and recent enough?"                | Backup discipline            |
| "What's the CERT-In timeline status?"                 | Regulatory timing            |
| "B2B customers — do we have contractual obligations?" | Contractual awareness        |
| "Is the cyber insurance carrier engaged?"             | Insurance coordination       |
| "Are we preserving evidence during rebuild?"          | Forensic balance             |
| "Other MSSP clients — sanitized brief planned?"       | Portfolio defense            |

---

# 14. Multi-Tenant Considerations (Mandatory)

Although the primary scenario is single-client, multi-tenant discipline is tested:

| Test                            | Inject           |
| ------------------------------- | ---------------- |
| Cross-client mention temptation | Throughout       |
| Sanitized portfolio TI brief    | Inject 35        |
| Per-client authority            | Inject 9, 14, 19 |
| Per-client communication        | Inject 23, 27    |

### Optional Multi-Client Variant

Facilitator may add injects making the scenario cross-client:

| Extension Inject                                             | Tests                        |
| ------------------------------------------------------------ | ---------------------------- |
| "Similar BlackTide pattern detected at 2nd MSSP client"      | CCIC activation              |
| "BlackTide affiliate appears to target manufacturing sector" | Portfolio risk               |
| "3rd MSSP client reports IoC matches in last 24 hours"       | Multi-client TTP correlation |

**Reference:**

- `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md`

---

# 15. Logistics Checklist (Mandatory)

## 15.1 T-30 Days

- [ ] TTX scheduled
- [ ] Calendar invites sent
- [ ] Venue confirmed (in-person/virtual/hybrid)
- [ ] Scenario reviewed and approved by IR Team Lead + Legal + Compliance

## 15.2 T-7 Days

- [ ] Pre-read distributed to participants
- [ ] Role assignments confirmed
- [ ] Facilitator MSEL final
- [ ] Evaluator scorecards prepared
- [ ] Equipment tested

## 15.3 T-1 Day

- [ ] Reminder sent
- [ ] Materials printed
- [ ] Backup facilitator confirmed
- [ ] Catering arranged

## 15.4 Day of TTX

- [ ] Sign-in sheet
- [ ] Ground rules briefing
- [ ] Per-client authority emphasized
- [ ] Double-extortion recognition emphasized
- [ ] Timekeeping started
- [ ] Recording (if applicable, with consent)
- [ ] Hot wash facilitation
- [ ] AAR timeline communicated

---

# 16. Required Materials (Mandatory)

| Material                                    | Source                                                                                          |
| ------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| Scenario brief (pre-read)                   | Section 9 of this document                                                                      |
| MSEL (facilitator only)                     | Section 8 of this document                                                                      |
| Evaluation scorecards                       | `TTX-Evaluation-Scorecard.md`                                                                   |
| Reference: Ransomware Master Playbook       | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Master.md`                                          |
| Reference: Ransomware Containment Playbook  | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Containment.md`                                     |
| Reference: Ransomware Eradication Playbook  | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Eradication.md`                                     |
| Reference: Ransomware Recovery Playbook     | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Recovery.md`                                        |
| Reference: IRT Containment Authority Matrix | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`            |
| Reference: Legal Counsel Engagement SOP     | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |
| Reference: RBI Incident Reporting SOP       | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md`   |
| Reference: CERT-In Reporting SOP            | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`        |
| Sign-in sheet                               | Template                                                                                        |
| Timekeeping (visible clock)                 | Mandatory                                                                                       |
| Whiteboard / virtual whiteboard             | Mandatory                                                                                       |

---

# 17. AAR Template (Post-TTX)

After-action report will document per `Tabletop-Exercise-Guide.md` Section 15:

| Section           | Content                          |
| ----------------- | -------------------------------- |
| Executive summary | TTX overview + headline findings |
| Objectives status | Pass/fail per objective          |
| Participant list  | By role                          |
| Scenario summary  | What was simulated               |
| Timeline          | Major scenario milestones        |
| Strengths         | What went well                   |
| Gaps              | What did not go well             |
| Recommendations   | Specific actionable improvements |
| Action items      | Owner + due date                 |
| Lessons learned   | Generalized takeaways            |
| Appendix          | Scorecards + decisions + quotes  |

---

# 18. Quality Checklist (Per Ransomware TTX Execution)

Before declaring this TTX complete:

- [ ] All 13 objectives evaluated
- [ ] Scorecards collected from all evaluators
- [ ] Hot wash conducted immediately post-TTX
- [ ] Critical failure triggers reviewed
- [ ] AAR drafted within 7 days
- [ ] AAR distributed within 14 days
- [ ] Action items entered in tracker
- [ ] Double-extortion handling observations documented
- [ ] Containment authority observations documented
- [ ] Ransom-payment policy observations documented
- [ ] BCP/DR coordination observations documented
- [ ] Multi-tenant discipline observations documented
- [ ] Records archived per retention policy

---

# 19. Records Retention

| Record                       | Retention               |
| ---------------------------- | ----------------------- |
| TTX scenario (this document) | 7 years                 |
| MSEL (facilitator copy)      | 3 years                 |
| Sign-in sheet                | 3 years                 |
| Evaluator scorecards         | 3 years                 |
| Hot wash notes               | 3 years                 |
| AAR                          | 7 years                 |
| Action items records         | Until closure + 3 years |

---

# 20. Integration with Other Processes

| Process                          | Integration                   |
| -------------------------------- | ----------------------------- |
| Tabletop Exercise Guide          | Master methodology            |
| Ransomware Master Playbook       | Validated by this TTX         |
| Ransomware Containment Playbook  | Validated by this TTX         |
| Ransomware Recovery Playbook     | Validated by this TTX         |
| IRT Containment Authority Matrix | Tested by this TTX            |
| BCP/DR Plans                     | Coordinated in this TTX       |
| Legal Counsel Engagement SOP     | Tested by this TTX            |
| RBI Incident Reporting SOP       | Tested by this TTX            |
| CERT-In Reporting SOP            | Tested by this TTX            |
| Client Data Segregation Policy   | Tested by this TTX            |
| Cross-Client Incident Procedure  | Optional in this TTX          |
| L1/L2/L3/IR Team Onboarding      | TTX participation requirement |
| Lessons Learned Register         | AAR feeds register            |
| Playbook Update Log              | Playbook gaps tracked         |
| Detection Improvement Log        | Detection gaps tracked        |
| Control Gap Tracker              | Control gaps tracked          |
| Threat Actor Profile             | Refined post-TTX              |

---

# 21. Related Documents

| Document                         | Path                                                                                            |
| -------------------------------- | ----------------------------------------------------------------------------------------------- |
| Tabletop Exercise Guide          | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`                  |
| TTX Evaluation Scorecard         | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Evaluation-Scorecard.md`                 |
| TTX APT Scenario                 | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-APT-Scenario.md`                         |
| TTX Insider Threat Scenario      | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-Insider-Threat-Scenario.md`              |
| TTX Data Breach Scenario         | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/TTX-DataBreach-Scenario.md`                  |
| Ransomware Master Playbook       | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Master.md`                                          |
| Ransomware L1 Triage             | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-L1-Triage.md`                                       |
| Ransomware L2 Investigation      | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-L2-Investigation.md`                                |
| Ransomware L3 Forensics          | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-L3-Forensics.md`                                    |
| Ransomware Containment           | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Containment.md`                                     |
| Ransomware Eradication           | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Eradication.md`                                     |
| Ransomware Recovery              | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-Recovery.md`                                        |
| Ransomware MITRE Mapping         | `02_PLAYBOOKS/02.1_Ransomware/PB-Ransomware-MITRE-Mapping.md`                                   |
| Data Breach Master Playbook      | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Master.md`                            |
| IRT Containment Authority Matrix | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md`            |
| IRT Activation Criteria          | `03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Activation-Criteria.md`                     |
| Legal Counsel Engagement SOP     | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |
| RBI Incident Reporting SOP       | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md`   |
| CERT-In Reporting SOP            | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md`        |
| Client Data Segregation Policy   | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`               |
| Cross-Client Incident Procedure  | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md`              |
| Lessons Learned Template         | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`                             |
| Playbook Update Log              | `08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`                             |
| Detection Improvement Log        | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`                       |

---

# 22. Revision History

| Version | Date        | Author                          | Changes         |
| ------- | ----------- | ------------------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP IR Team Lead / SOC Manager | Initial version |

---

# 23. Approval

Approved by:

| Role                 | Name | Signature | Date |
| -------------------- | ---- | --------- | ---- |
| MSSP IR Team Lead    |      |           |      |
| MSSP SOC Manager     |      |           |      |
| MSSP Compliance Lead |      |           |      |
| MSSP CISO            |      |           |      |

---

**End of Document**
