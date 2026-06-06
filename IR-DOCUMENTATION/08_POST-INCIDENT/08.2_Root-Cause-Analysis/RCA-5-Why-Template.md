# RCA 5-Why Analysis Template

---

# 1. Document Control

| Field          | Value                         |
| -------------- | ----------------------------- |
| Document Name  | Template – RCA 5-Why Analysis |
| Document ID    | RCA-5W-001                    |
| Version        | 1.0                           |
| Effective Date | 30-May-2026                   |
| Owner          | IR Team Lead / SOC Manager    |
| Approved By    | CISO                          |
| Classification | Internal – Confidential       |
| Review Cycle   | Annually                      |

---

# 2. Purpose

This template provides the **5-Why Analysis** method as a focused root cause identification technique used during incident RCA, post-incident reviews, and recurring problem analysis.

The 5-Why method is critical because:

- it provides a simple, structured approach to drill from symptoms to root cause
- it forces analysts to challenge assumptions and seek deeper understanding
- it is fast and lightweight, suitable for quick RCA on P3/P4 incidents
- it complements deeper methodologies (Fishbone, Fault Tree) for P1/P2 incidents
- it helps SOC teams avoid stopping at proximate causes
- it builds analytical discipline across L1/L2/L3 analysts
- it is widely accepted in NIST, ISO, ITIL, and Six Sigma frameworks

This template ensures:

- consistent 5-Why application across all incidents
- evidence-based reasoning at every step
- documented rationale that can be challenged and validated
- clear distinction between symptom, proximate cause, and root cause
- linkage to corrective and preventive actions
- audit-ready documentation

Reference alignment:
`08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`
`08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`

---

# 3. Scope

The 5-Why method is used for:

| Scenario                  | Application                           |
| ------------------------- | ------------------------------------- |
| P3/P4 incidents (TP)      | Primary RCA method                    |
| P1/P2 incidents           | Used as part of combined RCA approach |
| Recurring incidents       | Identify systemic root cause          |
| Near-miss events          | Lightweight analysis                  |
| Tabletop / Drill findings | Quick root cause identification       |
| Process/Procedure gaps    | Identify procedural root cause        |
| Detection gaps            | Identify detection failure root cause |
| Tool/Technology failures  | Identify technical root cause         |

Out of scope:

- false positive closures
- complex incidents requiring deeper methodologies as standalone (use combined RCA)

---

# 4. Definitions

| Term            | Definition                                                                 |
| --------------- | -------------------------------------------------------------------------- |
| 5 Whys          | Iterative interrogative technique to drill down from problem to root cause |
| Symptom         | Observable manifestation of a problem (not the cause)                      |
| Proximate Cause | Immediate cause that directly triggered the issue                          |
| Root Cause      | Fundamental underlying cause; removal prevents recurrence                  |
| Branching       | When a "why" has multiple valid answers requiring parallel analysis        |
| Validation      | Testing if reversing the cause prevents the problem                        |

---

# 5. Roles and Responsibilities

| Role               | Responsibilities                                              |
| ------------------ | ------------------------------------------------------------- |
| 5-Why Owner        | Conducts analysis; documents reasoning; validates conclusions |
| Incident Responder | Provides factual incident details and evidence                |
| L2/L3 Analyst      | Supports technical depth in analysis                          |
| SOC Lead           | Reviews 5-Why outcome; validates root cause                   |
| SOC Manager        | Approves analysis; ensures actions are tracked                |
| Action Owner       | Executes corrective and preventive actions                    |

---

# 6. 5-Why Methodology Principles (Mandatory)

| Principle                | Description                                            |
| ------------------------ | ------------------------------------------------------ |
| Start with clear problem | Define the problem in factual, observable terms        |
| Ask "why" iteratively    | Each answer becomes the basis for next "why"           |
| Evidence-based answers   | Every answer must be supported by evidence             |
| Avoid assumptions        | If unsure, mark as "assumption – needs validation"     |
| Stop at actionable cause | Root cause must enable corrective action               |
| Don't stop too early     | If cause still has a deeper "why", continue            |
| Don't go too deep        | Stop when answers become philosophical or out of scope |
| Branch when needed       | Multiple causes may require parallel 5-Why chains      |
| Validate by reversal     | "If we fix this, would the problem be prevented?"      |
| Blameless                | Focus on systems/processes, not individuals            |

---

# 7. When to Stop Asking "Why"

Stop drilling deeper when:

- ✅ The cause is within your organization's control to address
- ✅ Reversing the cause would prevent the problem
- ✅ Further "why" leads to philosophical or external factors
- ✅ The cause is a process, system, or design weakness (root cause)
- ❌ **Do NOT stop at:** "Human error", "Lack of attention", or any individual blame

---

# 8. 5-Why Template (Copy/Paste)

## 8.1 Analysis Metadata (Mandatory)

| Field                         | Value                   |
| ----------------------------- | ----------------------- |
| 5-Why Analysis ID             | `5W-YYYY-####`          |
| Incident ID / Ticket ID       | `INC-YYYY-####`         |
| Linked RCA ID (if applicable) | `RCA-YYYY-####`         |
| Incident Category             | `...`                   |
| Incident Severity             | P1 / P2 / P3 / P4       |
| Analysis Date (UTC)           | `YYYY-MM-DD HH:MM`      |
| Analysis Owner                | `Name / Role`           |
| Contributors                  | `Name, Name`            |
| Reviewed By                   | `Name / Role`           |
| Approved By                   | `Name / Role`           |
| Client/Tenant (MSSP only)     | `Client ID / Name`      |
| Classification                | Internal – Confidential |

---

## 8.2 Problem Statement (Mandatory)

Define the problem clearly and factually:

> *Example: "On [date], a phishing email bypassed email security controls and was delivered to 50 users. 5 users clicked the link, and 2 entered credentials on a fake login page. Credentials were used to access internal email accounts before detection 18 hours later."*

**Your Problem Statement:**

`[Write 2–3 sentence factual problem statement here]`

**Evidence Reference:** `[Ticket ID / Evidence vault reference]`

---

## 8.3 5-Why Analysis Chain (Mandatory)

### Why #1

**Question:** Why did `[problem]` occur?

**Answer:**
`[Factual answer supported by evidence]`

**Evidence Reference:**
`[Log / Artifact / Document reference]`

**Confidence:** High / Medium / Low

---

### Why #2

**Question:** Why did `[answer from Why #1]` happen?

**Answer:**
`[Factual answer supported by evidence]`

**Evidence Reference:**
`[Log / Artifact / Document reference]`

**Confidence:** High / Medium / Low

---

### Why #3

**Question:** Why did `[answer from Why #2]` happen?

**Answer:**
`[Factual answer supported by evidence]`

**Evidence Reference:**
`[Log / Artifact / Document reference]`

**Confidence:** High / Medium / Low

---

### Why #4

**Question:** Why did `[answer from Why #3]` happen?

**Answer:**
`[Factual answer supported by evidence]`

**Evidence Reference:**
`[Log / Artifact / Document reference]`

**Confidence:** High / Medium / Low

---

### Why #5

**Question:** Why did `[answer from Why #4]` happen?

**Answer:**
`[Factual answer supported by evidence]`

**Evidence Reference:**
`[Log / Artifact / Document reference]`

**Confidence:** High / Medium / Low

---

### Additional Whys (if needed)

> Continue with Why #6, Why #7, etc., if root cause not yet reached.
> Limit to 7–10 maximum; if deeper analysis needed, switch to Fault Tree Analysis.

---

## 8.4 Root Cause Statement (Mandatory)

**Identified Root Cause:**

`[Single, clear statement of the root cause identified at the end of the chain]`

**Evidence Supporting Root Cause:**

- `Evidence reference 1`
- `Evidence reference 2`

**Validation Test:**

- *"If we fix this root cause, would the problem be prevented in the future?"*
- **Answer:** Yes / No / Partially
- **Rationale:** `...`

---

## 8.5 Branching Analysis (If Applicable)

If any "Why" had multiple valid answers, document parallel chains:

### Branch A: `[Description]`

| Level      | Question | Answer | Evidence Ref |
| ---------- | -------- | ------ | ------------ |
| Why #1     |          |        |              |
| Why #2     |          |        |              |
| Why #3     |          |        |              |
| Root Cause |          |        |              |

### Branch B: `[Description]`

| Level      | Question | Answer | Evidence Ref |
| ---------- | -------- | ------ | ------------ |
| Why #1     |          |        |              |
| Why #2     |          |        |              |
| Why #3     |          |        |              |
| Root Cause |          |        |              |

---

## 8.6 Visual Representation (Copy/Paste Format)

```
PROBLEM: [State the problem]
   |
   ↓ Why?
WHY #1: [Answer]
   |
   ↓ Why?
WHY #2: [Answer]
   |
   ↓ Why?
WHY #3: [Answer]
   |
   ↓ Why?
WHY #4: [Answer]
   |
   ↓ Why?
WHY #5: [Answer]
   |
   ↓
ROOT CAUSE: [Identified root cause]
   |
   ↓
CORRECTIVE ACTION: [What will be done]
```

---

## 8.7 Assumptions Made (Mandatory)

Document any assumptions in the analysis:

| #   | Assumption | Validation Required? | Validation Plan |
| --- | ---------- | -------------------- | --------------- |
| 1   |            | Yes / No             |                 |
| 2   |            |                      |                 |

---

## 8.8 Corrective and Preventive Actions (Mandatory)

Based on identified root cause:

| Action ID | Action | Type (CA/PA) | Owner | Due Date (UTC) | Priority         | Tracking Ref |
| --------- | ------ | ------------ | ----- | -------------- | ---------------- | ------------ |
| CA-001    |        | CA / PA      |       |                | High / Med / Low |              |
| CA-002    |        |              |       |                |                  |              |

References:
`08_POST-INCIDENT/08.1_Lessons-Learned/Action-Items-Tracker.xlsx`
`08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx`

---

## 8.9 Validation Plan (Mandatory)

How will the corrective action be validated?

| Action ID | Validation Method                              | Success Criteria | Validation Date |
| --------- | ---------------------------------------------- | ---------------- | --------------- |
| CA-001    | Detection test / Audit / Drill / Metric review |                  |                 |

---

# 9. Worked Example (Reference)

> Example for training and reference purposes.

**Problem:** A ransomware attack encrypted 50 servers before detection.

| Level  | Question                                                                       | Answer                                                                                 |
| ------ | ------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------- |
| Why #1 | Why was ransomware not detected before encryption? | EDR did not generate an alert for the ransomware binary                                |
| Why #2 | Why did EDR not alert?                                                         | The binary was not in the EDR signature database and behavioral detection was disabled |
| Why #3 | Why was behavioral detection disabled?                                         | It was disabled during a performance tuning exercise 6 months ago                      |
| Why #4 | Why was it not re-enabled after tuning?                                        | There was no documented change request or re-enablement checklist                      |
| Why #5 | Why was there no change management for security tool configuration?            | Security tool changes were not included in the formal change management process        |

**Root Cause:** Security tool configuration changes were excluded from formal change management, allowing critical detection features to be disabled without review or rollback plan.

**Corrective Action:**

- Include all security tool configuration changes in formal change management process
- Implement quarterly review of EDR configuration baseline
- Enable behavioral detection with optimized rules

**Preventive Action:**

- Establish configuration baseline for all security tools
- Automated configuration drift detection
- Mandatory peer review for security tool changes

---

# 10. Common 5-Why Mistakes to Avoid

| Mistake                     | Why It's Wrong                    | Correct Approach                      |
| --------------------------- | --------------------------------- | ------------------------------------- |
| Stopping at "human error"   | Blames individual; not actionable | Ask why the system allowed the error  |
| Stopping at proximate cause | Misses root cause                 | Continue asking "why"                 |
| Skipping evidence           | Conclusions unsupported           | Reference evidence at every step      |
| Single-path thinking        | Misses multiple causes            | Use branching when applicable         |
| Too shallow (1–2 whys)      | Symptom-level fix                 | Aim for 4–5 whys minimum              |
| Too deep (10+ whys)         | Becomes philosophical             | Stop at actionable root cause         |
| Blame-focused answers       | Toxic culture; ineffective        | Reframe to system/process focus       |
| Vague answers               | Unactionable                      | Be specific and factual               |
| Rushing                     | Misses key insights               | Take time to think through each level |
| Not validating              | False root cause                  | Apply reversal test                   |

---

# 11. 5-Why Quality Checklist (Mandatory)

Before finalizing the analysis:

- [ ] Problem statement is factual and clear
- [ ] Each "Why" has an evidence-based answer
- [ ] No "human error" or individual-blame conclusions
- [ ] Branching used where multiple causes exist
- [ ] Assumptions documented and flagged for validation
- [ ] Root cause is within organizational control
- [ ] Root cause passes reversal test
- [ ] Corrective actions linked to root cause
- [ ] Preventive actions defined
- [ ] Validation plan included
- [ ] Actions logged in tracker
- [ ] Reviewed by SOC Lead / IR Team Lead
- [ ] Approved by SOC Manager
- [ ] MSSP: tenant scoping verified

---

# 12. MSSP Considerations (If Applicable)

For MSSP-managed clients:

- 5-Why analysis must be **tenant-scoped**; no cross-client data
- Client-facing version must be **sanitized** of internal MSSP details
- Client review may be required per SLA
- Client-specific actions tracked separately in client folder
- MSSP-internal 5-Why for service-related issues kept separate
- Cross-client trend analysis only in anonymized aggregate form

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 13. Integration with Other RCA Methodologies

| Methodology             | When to Combine with 5-Why                                                  |
| ----------------------- | --------------------------------------------------------------------------- |
| **Fishbone (Ishikawa)** | Use Fishbone first to identify possible causes, then 5-Why on top candidate |
| **Fault Tree Analysis** | Use 5-Why to explore individual fault paths in detail                       |
| **Timeline Analysis**   | Use Timeline to establish sequence, then 5-Why on key failure points        |
| **Pareto Analysis**     | Use Pareto to identify top issue, then 5-Why on root cause                  |

References:
`08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`
`08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Timeline-Builder.md`

---

# 14. Related Documents

| Document                      | Path                                                                            |
| ----------------------------- | ------------------------------------------------------------------------------- |
| RCA Template (Master)         | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Template.md`                     |
| RCA Timeline Builder          | `08_POST-INCIDENT/08.2_Root-Cause-Analysis/RCA-Timeline-Builder.md`             |
| Lessons Learned Template      | `08_POST-INCIDENT/08.1_Lessons-Learned/Lessons-Learned-Template.md`             |
| PIR Meeting Agenda            | `08_POST-INCIDENT/08.1_Lessons-Learned/PIR-Meeting-Agenda.md`                   |
| Action Items Tracker          | `08_POST-INCIDENT/08.1_Lessons-Learned/Action-Items-Tracker.xlsx`               |
| Security Improvement Register | `08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx` |
| Detection Improvement Log     | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`       |
| L3 Root Cause Analysis SOP    | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Root-Cause-Analysis.md`           |

---

# 15. Revision History

| Version | Date        | Author                     | Changes         |
| ------- | ----------- | -------------------------- | --------------- |
| 1.0     | 30-May-2026 | IR Team Lead / SOC Manager | Initial version |

---

# 16. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**
