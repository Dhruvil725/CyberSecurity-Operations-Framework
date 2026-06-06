# TTP Intelligence Report Template

---

# 1. Document Control

| Field          | Value                                           |
| -------------- | ----------------------------------------------- |
| Document Name  | Template – TTP Intelligence Report              |
| Document ID    | TI-TTP-001                                      |
| Version        | 1.0                                             |
| Effective Date | 30-May-2026                                     |
| Owner          | Threat Intel Lead / SOC Manager                 |
| Approved By    | CISO                                            |
| Classification | Internal – Confidential (TLP varies per report) |
| Review Cycle   | Annually (template); per-report as needed       |

---

# 2. Purpose

This template provides the standardized **TTP (Tactics, Techniques, and Procedures) Intelligence Report** format used to document, analyze, and operationalize behavioral threat intelligence extracted from incidents, threat hunts, malware analysis, and external sources.

A formal TTP intelligence report is critical because:

- TTPs represent the highest-value indicators in the Pyramid of Pain (hardest for adversaries to change)
- behavioral detection is more durable than IoC-based detection
- NIST CSF Detect (DE.AE, DE.CM) and Identify (ID.RA) functions require TTP awareness
- ISO 27001 Annex A.5.7 requires threat intelligence as a control
- RBI Cyber Security Framework expects behavioral detection capability maturity
- MITRE ATT&CK is the de facto industry framework for TTP documentation
- TTP reports feed detection engineering, threat hunting, and adversary emulation
- audit trail required for behavioral intelligence program
- MSSP clients in regulated industries expect TTP-level briefings
- TTP intelligence supports proactive defense and detection coverage gap analysis
- TTPs inform tabletop scenarios, red team exercises, and purple team simulations

This template ensures:

- consistent structure across all TTP intelligence reports
- MITRE ATT&CK-aligned documentation
- evidence-based analysis with confidence ratings
- actionable detection and hunt recommendations
- TLP-classified content for appropriate sharing
- audit-ready evidence of behavioral intelligence capability
- linkage to incidents, IoCs, threat actor profiles, and detection improvements

Reference alignment:
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Platform-Usage-Guide.md`
`08_POST-INCIDENT/08.4_Threat-Intel-Output/IoC-Output-Register.md`
`08_POST-INCIDENT/08.4_Threat-Intel-Output/Threat-Actor-Profile-Template.md`

---

# 3. Scope

This template is used for reports covering:

| Report Focus                    | Examples                               |
| ------------------------------- | -------------------------------------- |
| **Single-Technique Deep Dive**  | T1078 Valid Accounts deep analysis     |
| **Technique Cluster**           | Initial Access techniques for BFSI     |
| **Campaign TTPs**               | TTPs from observed campaign            |
| **Actor TTP Update**            | New TTPs adopted by known actor        |
| **Industry TTP Trend**          | Top TTPs targeting financial sector    |
| **Emerging TTPs**               | New techniques observed in wild        |
| **Detection Coverage Analysis** | Mapping detections to MITRE techniques |
| **Threat Hunt TTP Findings**    | TTPs discovered through hunting        |
| **Red/Purple Team TTPs**        | Adversary emulation findings           |
| **Tabletop Scenario TTPs**      | TTPs for exercise design               |

Report triggers:

| Trigger              | Examples                           |
| -------------------- | ---------------------------------- |
| Significant incident | Post-incident TTP documentation    |
| Emerging threat      | New campaign/technique observed    |
| Vendor advisory      | Major TTP shift reported by vendor |
| Hunt findings        | Novel TTPs from threat hunting     |
| Quarterly trending   | Top TTPs in quarter                |
| Annual landscape     | Annual TTP landscape report        |
| Compliance request   | RBI/regulatory TTP briefing        |
| Strategic briefing   | Board/CISO request                 |

Out of scope:

- Single-actor profile reports (use Threat Actor Profile Template)
- IoC-only reports (use IoC Output Register)
- Incident-specific narratives (use Final Incident Report Template)
- Tactical incident response (use playbooks)

---

# 4. Definitions

| Term                 | Definition                                                             |
| -------------------- | ---------------------------------------------------------------------- |
| TTP                  | Tactics, Techniques, and Procedures – behavioral adversary descriptors |
| Tactic               | The adversary's tactical goal (e.g., Initial Access, Execution)        |
| Technique            | How the adversary achieves the goal (e.g., Phishing)                   |
| Sub-Technique        | Specific implementation (e.g., Spearphishing Attachment)               |
| Procedure            | Specific actor implementation (most granular)                          |
| MITRE ATT&CK         | Knowledge base of adversary tactics and techniques                     |
| Pyramid of Pain      | Hierarchy showing TTPs as highest-value indicators                     |
| Behavioral Detection | Detection based on activity patterns rather than static indicators     |
| Atomic Test          | Lightweight test to validate detection (Atomic Red Team)               |
| Detection Coverage   | Percentage of TTPs detected by security controls                       |
| Hunt Hypothesis      | Testable assumption about adversary behavior                           |
| ATT&CK Navigator     | MITRE tool to visualize technique coverage                             |
| Sigma Rule           | Open standard for behavioral SIEM rules                                |
| YARA Rule            | Pattern matching for file/memory artifacts                             |

---

# 5. Roles and Responsibilities

| Role                     | Responsibilities                                               |
| ------------------------ | -------------------------------------------------------------- |
| Threat Intel Lead        | Owns report quality; approves publication; coordinates sharing |
| Threat Intel Analyst     | Authors reports; conducts research; maps to ATT&CK             |
| L3 Analyst               | Provides incident-derived TTPs; technical depth                |
| Threat Hunter            | Provides hunt-derived TTPs; hypothesis validation              |
| Malware Analyst          | Provides malware-derived TTPs (static/dynamic)                 |
| Detection Engineer       | Operationalizes TTPs into detection rules                      |
| Red/Purple Team          | Validates detection coverage; provides emulation findings      |
| SOC Lead                 | Validates operational relevance                                |
| SOC Manager              | Approves strategic reports                                     |
| CISO                     | Approves external sharing; reviews strategic reports           |
| Compliance Lead          | Validates regulatory alignment                                 |
| MSSP SDM (if applicable) | Coordinates client-specific TTP reports                        |

---

# 6. TTP Intelligence Report Principles (Mandatory)

| Principle             | Description                                            |
| --------------------- | ------------------------------------------------------ |
| MITRE-aligned         | All TTPs mapped to ATT&CK techniques/sub-techniques    |
| Evidence-based        | Every TTP claim supported by evidence                  |
| Confidence-rated      | Use analytical confidence (High/Medium/Low)            |
| Actionable            | Must include detection/hunt/mitigation recommendations |
| Sourced               | Every claim must cite source                           |
| TLP-classified        | Report has TLP classification                          |
| Visual                | Use ATT&CK Navigator layers where applicable           |
| Procedural detail     | Include actor-specific procedures, not just techniques |
| Sanitized for sharing | External versions remove sensitive sources/methods     |
| Current               | Mapped to latest ATT&CK version                        |

---

# 7. MITRE ATT&CK Framework Quick Reference

The 14 ATT&CK Enterprise Tactics:

| ID     | Tactic               | Adversary Goal                       |
| ------ | -------------------- | ------------------------------------ |
| TA0043 | Reconnaissance       | Gather information about target      |
| TA0042 | Resource Development | Establish resources for operations   |
| TA0001 | Initial Access       | Gain entry into network              |
| TA0002 | Execution            | Run malicious code                   |
| TA0003 | Persistence          | Maintain foothold                    |
| TA0004 | Privilege Escalation | Gain higher permissions              |
| TA0005 | Defense Evasion      | Avoid detection                      |
| TA0006 | Credential Access    | Steal credentials                    |
| TA0007 | Discovery            | Learn about environment              |
| TA0008 | Lateral Movement     | Move through network                 |
| TA0009 | Collection           | Gather data of interest              |
| TA0011 | Command and Control  | Communicate with compromised systems |
| TA0010 | Exfiltration         | Steal data                           |
| TA0040 | Impact               | Manipulate, interrupt, destroy       |

Reference:
`https://attack.mitre.org/`
`10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md`

---

# 8. Confidence Rating Definitions (Mandatory)

| Confidence            | Definition                                                            |
| --------------------- | --------------------------------------------------------------------- |
| **High Confidence**   | Well-corroborated; observed in multiple sources; consistent over time |
| **Medium Confidence** | Credibly sourced; some information gaps; plausible                    |
| **Low Confidence**    | Limited sources; significant gaps; requires further validation        |

Use estimative language consistently throughout the report.

---

# 9. TTP Intelligence Report Template (Copy/Paste)

## 9.1 Report Metadata (Mandatory)

| Field                     | Value                                                                                      |
| ------------------------- | ------------------------------------------------------------------------------------------ |
| Report ID                 | `TTP-YYYY-####`                                                                            |
| Report Title              |                                                                                            |
| Report Type               | Single-Technique / Cluster / Campaign / Actor TTP / Industry / Emerging / Hunt / Quarterly |
| Date Published (UTC)      |                                                                                            |
| Reporting Period (UTC)    | Start – End                                                                                |
| Author / Analyst          |                                                                                            |
| Reviewed By               |                                                                                            |
| Approved By               |                                                                                            |
| TLP Classification        | RED / AMBER+STRICT / AMBER / GREEN / CLEAR                                                 |
| Distribution              | Internal SOC / MSSP / Client / External                                                    |
| Client/Tenant (MSSP only) | Client ID / Name (if client-specific)                                                      |
| MITRE ATT&CK Version      | e.g., v15.1                                                                                |
| Related Profiles          | TAP-YYYY-####                                                                              |
| Related IoC Sets          | IOC-YYYY-####                                                                              |
| Related Incidents         | INC-YYYY-####                                                                              |

---

## 9.2 Executive Summary (Mandatory)

> Provide a 3–5 sentence executive-level summary.

**Summary:**

`[Brief description of TTPs covered, observed actors, relevance to organization, key recommendations]`

**Key Findings:**

- `Finding 1`
- `Finding 2`
- `Finding 3`

**Bottom Line Up Front (BLUF):**

`[1-sentence assessment of impact and recommended action]`

---

## 9.3 Scope and Methodology (Mandatory)

### 9.3.1 Report Scope

| Aspect                | Details                            |
| --------------------- | ---------------------------------- |
| TTPs Covered          | Specific techniques/sub-techniques |
| Threat Actors Covered | Named actors or "Unknown"          |
| Industries Covered    | Target industries                  |
| Geographies Covered   | Target regions                     |
| Time Period           | Observation window                 |
| Detection Platforms   | Tools relevant to detection        |

### 9.3.2 Methodology

- **Sources analyzed:** `Internal incidents / Hunts / External feeds / Open-source / Vendor reports`
- **Analytical framework:** `MITRE ATT&CK / Diamond Model / Kill Chain`
- **Data sources:** `SIEM / EDR / TI Platform / External research`
- **Limitations:** `Data gaps, time constraints, source reliability`

---

## 9.4 TTP Analysis (Mandatory – Main Body)

> Document each TTP with the following structure.

### 9.4.1 TTP Entry Template

> Repeat this structure for each TTP covered.

#### TTP: `T#### – Technique Name`

**Metadata:**

| Field                  | Value                                        |
| ---------------------- | -------------------------------------------- |
| MITRE Tactic           | e.g., Initial Access (TA0001)                |
| MITRE Technique        | T####                                        |
| MITRE Sub-Technique    | T####.### (if applicable)                    |
| ATT&CK URL             | `https://attack.mitre.org/techniques/T####/` |
| Observed Threat Actors | APT##, FIN##, etc.                           |
| Confidence             | High / Medium / Low                          |
| Observed Frequency     | High / Medium / Low                          |

**Technique Description:**

`Brief description of the technique from MITRE ATT&CK perspective.`

**Observed Procedures:**

> Specific implementations observed (more granular than technique).

| #   | Procedure Description | Source | Date Observed |
| --- | --------------------- | ------ | ------------- |
| 1   |                       |        |               |
| 2   |                       |        |               |

**Example Command/Behavior (if applicable):**

```
[Sanitized example of commands, scripts, or behavior patterns observed]

Example:
powershell.exe -nop -w hidden -enc <base64_encoded_payload>
```

**Data Sources for Detection:**

| Data Source        | Required Telemetry              | Coverage in Environment |
| ------------------ | ------------------------------- | ----------------------- |
| Windows Event Logs | Event ID 4688, 4624             | Full / Partial / None   |
| Sysmon             | Event ID 1, 3, 7, 10            | Full / Partial / None   |
| EDR                | Process telemetry, command line | Full / Partial / None   |
| Network            | DNS, HTTP, TLS metadata         | Full / Partial / None   |
| Cloud Audit        | CloudTrail, Activity Log        | Full / Partial / None   |
| Email              | Headers, attachments            | Full / Partial / None   |

**Detection Approaches:**

| Approach        | Description | False Positive Risk |
| --------------- | ----------- | ------------------- |
| Signature-based |             | Low                 |
| Behavioral      |             | Medium              |
| Anomaly-based   |             | Medium-High         |
| Threshold-based |             | Medium              |

**Recommended Detection Logic:**

```
[Pseudo-code or detection rule logic]

Example (Sigma-style):
detection:
  selection:
    Image: '*\powershell.exe'
    CommandLine|contains:
      - '-EncodedCommand'
      - '-enc '
      - 'FromBase64String'
  condition: selection
```

**Existing Detection Coverage:**

| Detection Rule | Tool       | Status          | FP Rate |
| -------------- | ---------- | --------------- | ------- |
|                | SIEM / EDR | Active / Tuning | %       |

**Hunt Hypotheses:**

| Hypothesis | Data Sources | Approach |
| ---------- | ------------ | -------- |
|            |              |          |

**Mitigation Recommendations:**

| Mitigation | MITRE ID | Priority         |
| ---------- | -------- | ---------------- |
|            | M####    | High / Med / Low |

**Atomic Red Team Test:**

| Test ID | Description | Reference                                        |
| ------- | ----------- | ------------------------------------------------ |
| T####-X |             | `https://github.com/redcanaryco/atomic-red-team` |

**References:**

- MITRE ATT&CK: `https://attack.mitre.org/techniques/T####/`
- Vendor research: `[citation]`
- Internal incident: `INC-YYYY-####`

---

## 9.5 MITRE ATT&CK Coverage Heatmap (Mandatory)

### 9.5.1 Tactic-Level Coverage

> Summary of TTPs covered in this report across tactics.

| Tactic               | Techniques Covered in Report | Total Techniques in Tactic | Coverage % |
| -------------------- | ---------------------------- | -------------------------- | ---------- |
| Reconnaissance       |                              |                            |            |
| Resource Development |                              |                            |            |
| Initial Access       |                              |                            |            |
| Execution            |                              |                            |            |
| Persistence          |                              |                            |            |
| Privilege Escalation |                              |                            |            |
| Defense Evasion      |                              |                            |            |
| Credential Access    |                              |                            |            |
| Discovery            |                              |                            |            |
| Lateral Movement     |                              |                            |            |
| Collection           |                              |                            |            |
| Command and Control  |                              |                            |            |
| Exfiltration         |                              |                            |            |
| Impact               |                              |                            |            |

### 9.5.2 ATT&CK Navigator Layer

> Export an ATT&CK Navigator layer (JSON) and reference it here.

| Layer File                          | Purpose                     | Reference     |
| ----------------------------------- | --------------------------- | ------------- |
| `ttp-report-YYYY-####.json`         | Report TTPs visualization   | `[file path]` |
| `detection-coverage-YYYY-####.json` | Current detection coverage  | `[file path]` |
| `hunt-priorities-YYYY-####.json`    | Recommended hunt priorities | `[file path]` |

Reference:
`https://mitre-attack.github.io/attack-navigator/`

---

## 9.6 Detection Coverage Assessment (Mandatory)

### 9.6.1 Current Detection State

| TTP   | Detection Tool | Detection Rule | Status                  | Confidence |
| ----- | -------------- | -------------- | ----------------------- | ---------- |
| T#### |                |                | Active / Partial / None |            |

### 9.6.2 Detection Gaps Identified

| TTP   | Gap Description | Priority         | Proposed Solution |
| ----- | --------------- | ---------------- | ----------------- |
| T#### |                 | High / Med / Low |                   |

### 9.6.3 Recommended Detection Improvements

| Recommendation | Tool             | Priority         | Effort           | Owner |
| -------------- | ---------------- | ---------------- | ---------------- | ----- |
|                | SIEM / EDR / NDR | High / Med / Low | High / Med / Low |       |

Reference:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

---

## 9.7 Threat Hunting Recommendations (Mandatory)

### 9.7.1 Recommended Hunt Hypotheses

| #   | Hypothesis | Data Sources | Approach | Priority         |
| --- | ---------- | ------------ | -------- | ---------------- |
| 1   |            |              |          | High / Med / Low |
| 2   |            |              |          |                  |

### 9.7.2 Hunt Query Examples

```
[Tool-specific hunt query examples]

Example (Splunk SPL):
index=windows EventCode=4688
| where like(CommandLine, "%-EncodedCommand%")
| stats count by host, user, CommandLine
| where count > threshold
```

Reference:
`03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Threat-Hunting-Procedures.md`

---

## 9.8 Mitigation Recommendations (Mandatory)

| Mitigation Category | Specific Recommendation            | Priority | Effort |
| ------------------- | ---------------------------------- | -------- | ------ |
| Preventive          | Patching, hardening, segmentation  |          |        |
| Detective           | Logging, monitoring, alerting      |          |        |
| Responsive          | Playbook updates, automation       |          |        |
| Recovery            | Backup, restoration, BCP           |          |        |
| User Awareness      | Training, phishing simulation      |          |        |
| Policy              | Access controls, change management |          |        |

---

## 9.9 Threat Actor Mapping (If Applicable)

| Threat Actor | Aliases | TTPs Used (from this report) | Relevance        |
| ------------ | ------- | ---------------------------- | ---------------- |
| Actor 1      |         | T####, T####                 | High / Med / Low |
| Actor 2      |         |                              |                  |

Reference:
`08_POST-INCIDENT/08.4_Threat-Intel-Output/Threat-Actor-Profile-Template.md`

---

## 9.10 IoC Set Reference (If Applicable)

| IoC Set | TLP | Reference       |
| ------- | --- | --------------- |
|         |     | `IOC-YYYY-####` |

Reference:
`08_POST-INCIDENT/08.4_Threat-Intel-Output/IoC-Output-Register.md`

---

## 9.11 Industry/Geographic Relevance (Mandatory)

### 9.11.1 Industry Targeting

| Industry   | Confirmed / Suspected | Relevance to Organization |
| ---------- | --------------------- | ------------------------- |
| BFSI       |                       |                           |
| Government |                       |                           |
| Healthcare |                       |                           |
| Energy     |                       |                           |
| Telecom    |                       |                           |
| Other      |                       |                           |

### 9.11.2 Geographic Targeting

| Region        | Confirmed / Suspected | Relevance |
| ------------- | --------------------- | --------- |
| India         |                       |           |
| APAC          |                       |           |
| Europe        |                       |           |
| North America |                       |           |
| Other         |                       |           |

---

## 9.12 Trend Analysis (Mandatory for Quarterly/Annual Reports)

### 9.12.1 TTP Frequency Trend

| TTP   | Q1  | Q2  | Q3  | Q4  | Trend                            |
| ----- | --- | --- | --- | --- | -------------------------------- |
| T#### |     |     |     |     | Increasing / Stable / Decreasing |

### 9.12.2 Emerging TTPs

| TTP   | First Observed | Adoption Rate | Confidence |
| ----- | -------------- | ------------- | ---------- |
| T#### |                |               |            |

### 9.12.3 Retiring TTPs

| TTP   | Last Observed | Reason for Decline |
| ----- | ------------- | ------------------ |
| T#### |               |                    |

---

## 9.13 Strategic Recommendations (Mandatory for P1/Strategic Reports)

### 9.13.1 For Detection Engineering

| Recommendation | Priority         | Resource Required |
| -------------- | ---------------- | ----------------- |
|                | High / Med / Low |                   |

### 9.13.2 For Threat Hunting Program

| Recommendation | Priority | Resource Required |
| -------------- | -------- | ----------------- |
|                |          |                   |

### 9.13.3 For Security Architecture

| Recommendation | Priority | Resource Required |
| -------------- | -------- | ----------------- |
|                |          |                   |

### 9.13.4 For Training Program

| Recommendation | Audience             | Priority |
| -------------- | -------------------- | -------- |
|                | L1 / L2 / L3 / Users |          |

### 9.13.5 For Tabletop / Red Team Exercises

| Scenario Recommendation | Purpose                           | Priority |
| ----------------------- | --------------------------------- | -------- |
|                         | Validate detection / Test process |          |

Reference:
`10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`
`10_TRAINING-AND-EXERCISES/10.3_Drills/Purple-Team-Exercise-Guide.md`

---

## 9.14 Intelligence Gaps and Outstanding Questions

| Gap / Question | Priority         | Collection Plan |
| -------------- | ---------------- | --------------- |
|                | High / Med / Low |                 |

---

## 9.15 Source Material (Mandatory)

### 9.15.1 Internal Sources

| Source                    | Reference | Date | Confidence |
| ------------------------- | --------- | ---- | ---------- |
| Internal incident         |           |      |            |
| Internal hunt             |           |      |            |
| Internal malware analysis |           |      |            |
| Internal red/purple team  |           |      |            |

### 9.15.2 External Sources (Open-Source)

| Source                   | URL / Reference | Date | Confidence |
| ------------------------ | --------------- | ---- | ---------- |
| MITRE ATT&CK             |                 |      |            |
| Vendor reports           |                 |      |            |
| Government advisories    |                 |      |            |
| Academic research        |                 |      |            |
| Conference presentations |                 |      |            |
| Security blogs           |                 |      |            |

### 9.15.3 External Sources (Closed-Source / Subscription)

| Source             | Reference | TLP | Confidence |
| ------------------ | --------- | --- | ---------- |
| Commercial TI feed |           |     |            |
| ISAC sharing       |           |     |            |
| Trusted partner    |           |     |            |

---

## 9.16 Appendix (Optional)

- ATT&CK Navigator JSON files
- Atomic Red Team test references
- Sigma rule examples (full text)
- YARA rule examples (full text)
- Sample queries (SIEM-specific)
- Reference architecture diagrams

---

# 10. Visual Reference – Pyramid of Pain

TTPs are the highest-value intelligence indicators:

```
                  ▲
                 ╱ ╲           ← TTPs require adversary to
                ╱TTP╲          ← rebuild entire toolchain
               ╱─────╲         ← MAXIMUM DEFENSIVE VALUE
              ╱ TOOLS ╲
             ╱─────────╲
            ╱ARTIFACTS  ╲
           ╱─────────────╲
          ╱  DOMAINS      ╲
         ╱─────────────────╲
        ╱   IP ADDRESSES    ╲
       ╱─────────────────────╲
      ╱      HASH VALUES      ╲
     ─────────────────────────── ← Trivial to change
```

**Why TTP Intelligence Matters:**

- Adversaries can change hashes in seconds
- IPs/domains rotate frequently
- Tools are replaceable
- **TTPs require fundamental retraining and re-tooling**
- Detection at TTP level provides durable defense

---

# 11. Report Lifecycle (Mandatory)

| Phase                  | Activities                            | Owner                     | Frequency        |
| ---------------------- | ------------------------------------- | ------------------------- | ---------------- |
| **Trigger**            | Need identified (incident/hunt/intel) | Any stakeholder           | On trigger       |
| **Scoping**            | Report scope and methodology defined  | Threat Intel Analyst      | Per report       |
| **Research**           | Sources collected and analyzed        | Threat Intel Analyst      | Per report       |
| **Drafting**           | Report drafted per template           | Threat Intel Analyst      | Per report       |
| **Review**             | Technical and analytical review       | Threat Intel Lead         | Per report       |
| **Approval**           | TLP and distribution approved         | SOC Manager / CISO        | Per report       |
| **Publication**        | Report shared per TLP                 | Threat Intel Lead         | Per report       |
| **Operationalization** | Recommendations actioned              | Detection Eng / Hunt Team | Post-publication |
| **Update**             | New intel incorporated                | Threat Intel Analyst      | As needed        |
| **Archival**           | Report archived per retention         | Threat Intel Lead         | Per policy       |

---

# 12. Distribution and Sharing (Mandatory)

## 12.1 Internal Distribution

| Audience               | Format                        | Frequency       |
| ---------------------- | ----------------------------- | --------------- |
| SOC L2/L3              | Full report                   | Per publication |
| Detection Engineering  | Full report + Navigator layer | Per publication |
| Threat Hunters         | Full report + hunt hypotheses | Per publication |
| Incident Response Team | Full report                   | Per publication |
| Management             | Executive summary             | Per publication |
| CISO / Board           | Strategic briefing            | Quarterly       |

## 12.2 External Distribution (per TLP)

| Recipient                | TLP Limit   | Format        | Approval           |
| ------------------------ | ----------- | ------------- | ------------------ |
| MSSP Clients (relevant)  | AMBER       | Sanitized PDF | SOC Manager        |
| ISACs                    | GREEN/AMBER | STIX/MISP/PDF | SOC Manager        |
| CERT-In                  | GREEN       | PDF/Email     | SOC Manager + CISO |
| Trusted Partners         | AMBER       | PDF           | SOC Manager        |
| Public (blog/whitepaper) | CLEAR       | Markdown/PDF  | CISO               |

---

# 13. Report Types and Frequencies (Standard)

| Report Type                  | Frequency                                     | Audience                    |
| ---------------------------- | --------------------------------------------- | --------------------------- |
| **Tactical TTP Alert**       | As needed (within 24h of significant finding) | SOC, Detection Eng, Hunters |
| **Campaign TTP Report**      | Per campaign                                  | SOC, Detection Eng, IR      |
| **Actor TTP Update**         | As actor evolves                              | SOC, IR, Strategic          |
| **Industry TTP Trend**       | Quarterly                                     | Strategic, Compliance       |
| **Quarterly TTP Landscape**  | Quarterly                                     | Management, CISO, Board     |
| **Annual TTP Landscape**     | Annually                                      | CISO, Board                 |
| **Hunt-Driven TTP Report**   | Per significant hunt                          | SOC, Detection Eng          |
| **Compliance-Driven Report** | Per regulatory requirement                    | Compliance, CISO            |

---

# 14. Quality Checklist (Per Report)

Before publishing a TTP intelligence report:

- [ ] Report ID and metadata complete
- [ ] Executive summary written (3–5 sentences)
- [ ] Bottom Line Up Front (BLUF) statement included
- [ ] Scope and methodology documented
- [ ] Each TTP mapped to MITRE ATT&CK (current version)
- [ ] Procedures (actor-specific implementations) documented
- [ ] Detection approaches identified for each TTP
- [ ] Existing detection coverage assessed
- [ ] Detection gaps identified with recommendations
- [ ] Hunt hypotheses provided
- [ ] Mitigation recommendations included
- [ ] ATT&CK Navigator layer created (if applicable)
- [ ] Industry/geographic relevance assessed
- [ ] Threat actor mapping included (if applicable)
- [ ] IoC set references linked
- [ ] Source material cited with confidence
- [ ] Confidence ratings applied throughout
- [ ] Estimative language used consistently
- [ ] TLP classification assigned
- [ ] Intelligence gaps documented
- [ ] Strategic recommendations included (P1/strategic reports)
- [ ] Reviewed by Threat Intel Lead
- [ ] Approved per distribution requirements
- [ ] MSSP: tenant scoping verified (if applicable)
- [ ] Sanitized version prepared for external sharing

---

# 15. Review Process (Mandatory)

## 15.1 Per-Report Review

Each TTP intelligence report undergoes:

- Technical review by Threat Intel Lead
- Operational relevance review by SOC Lead
- Compliance review by Compliance Lead (if regulatory)
- Approval by SOC Manager (and CISO for external sharing)

## 15.2 Quarterly Review

Threat Intel Lead + SOC Manager review:

- TTP coverage across MITRE ATT&CK
- Detection coverage trend
- Hunt program alignment
- Report quality and timeliness
- Stakeholder feedback

## 15.3 Annual Review

CISO + Threat Intel Lead review:

- Strategic TTP intelligence priorities
- Coverage gaps (tactics/industries/actors)
- Detection maturity assessment
- Threat hunting program maturity
- Investment needs

---

# 16. MSSP Considerations (If Applicable)

For MSSP-managed clients:

- Master TTP reports maintained at MSSP level
- Client-specific TTP reports for high-relevance industries (BFSI, healthcare)
- Each client receives **relevant TTP reports** based on industry/geo
- Client-confidential TTPs (from client incidents) stay in tenant-scoped report
- Cross-client TTP observations sanitized before inclusion in master reports
- Client briefings on quarterly TTP trends per their industry
- Joint detection engineering sessions based on TTP reports
- Tabletop scenarios using client-relevant TTPs
- Compliance reporting (RBI, etc.) supported by TTP intelligence

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`
`07_REPORTING/07.3_MSSP-Client-Reports/MSSP-Executive-Briefing-Template.md`

---

# 17. Integration with Other Processes

| Process               | Integration Point                             |
| --------------------- | --------------------------------------------- |
| IoC Management        | TTPs contextualize IoCs                       |
| Threat Actor Profiles | TTPs documented in actor profiles             |
| Detection Engineering | TTPs drive detection rules                    |
| Threat Hunting        | TTPs drive hunt hypotheses                    |
| Incident Response     | TTPs identified during incidents feed reports |
| Red/Purple Team       | TTPs inform adversary emulation               |
| Tabletop Exercises    | TTPs drive realistic scenarios                |
| Executive Briefings   | TTPs support strategic communications         |
| Compliance            | TTP coverage demonstrates TI maturity         |
| Risk Assessment       | TTP relevance informs risk scoring            |
| Training              | TTPs inform analyst training curriculum       |

---

# 18. Common Pitfalls to Avoid

| Pitfall                      | Mitigation                           |
| ---------------------------- | ------------------------------------ |
| TTPs without ATT&CK mapping  | Always map to current ATT&CK version |
| Generic descriptions         | Include actor-specific procedures    |
| No detection recommendations | Always include actionable guidance   |
| No hunt hypotheses           | Include for each TTP                 |
| Outdated MITRE versions      | Re-map annually to latest ATT&CK     |
| Speculation as fact          | Use confidence language consistently |
| Single-source claims         | Require multi-source corroboration   |
| No data source mapping       | Always identify required telemetry   |
| Over-classification          | Use TLP appropriately                |
| Lack of visualization        | Include Navigator layers             |
| No strategic recommendations | Include for strategic-level reports  |
| Cross-tenant leakage (MSSP)  | Strict tenant scoping                |

---

# 19. Related Documents

| Document                         | Path                                                                            |
| -------------------------------- | ------------------------------------------------------------------------------- |
| IoC Output Register              | `08_POST-INCIDENT/08.4_Threat-Intel-Output/IoC-Output-Register.md`              |
| Threat Actor Profile Template    | `08_POST-INCIDENT/08.4_Threat-Intel-Output/Threat-Actor-Profile-Template.md`    |
| TI Feed Management               | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Feed-Management.md`        |
| TI Platform Usage Guide          | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Platform-Usage-Guide.md`   |
| TI IoC Handling SOP              | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md`       |
| TI Reporting Template            | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Reporting-Template.md`     |
| L3 Threat Intel Integration      | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Threat-Intel-Integration.md`      |
| L3 Attribution Analysis          | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Attribution-Analysis.md`          |
| L2 Threat Hunting Procedures     | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Threat-Hunting-Procedures.md`     |
| Detection Improvement Log        | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`       |
| Playbook Update Log              | `08_POST-INCIDENT/08.3_Improvement-Tracking/Playbook-Update-Log.md`             |
| APT Playbook (Master)            | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-Master.md`                              |
| APT MITRE Mapping                | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-MITRE-Mapping.md`                       |
| MITRE ATT&CK Quick Reference     | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md` |
| Attack Technique Reference       | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Attack-Technique-Reference.md`   |
| Common IoC Reference             | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Common-IoC-Reference.md`         |
| Tabletop Exercise Guide          | `10_TRAINING-AND-EXERCISES/10.2_Tabletop-Exercises/Tabletop-Exercise-Guide.md`  |
| Purple Team Exercise Guide       | `10_TRAINING-AND-EXERCISES/10.3_Drills/Purple-Team-Exercise-Guide.md`           |
| MSSP Executive Briefing Template | `07_REPORTING/07.3_MSSP-Client-Reports/MSSP-Executive-Briefing-Template.md`     |

---

# 20. Revision History

| Version | Date        | Author                          | Changes         |
| ------- | ----------- | ------------------------------- | --------------- |
| 1.0     | 30-May-2026 | Threat Intel Lead / SOC Manager | Initial version |

---

# 21. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**
