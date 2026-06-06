# SOP: L3 Attribution Analysis Procedures

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – L3 Attribution Analysis Procedures |
| Document ID | SOC-L3-SOP-007 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / Threat Intelligence Lead |
| Approved By | CISO |
| Classification | Internal – Restricted Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This Standard Operating Procedure (SOP) defines the methodology, analytical standards, workflows, intelligence handling requirements, and reporting procedures for Level 3 (L3) cyber threat attribution analysis.

Attribution analysis is the process of evaluating evidence to identify:

- Threat actor characteristics
- Campaign similarities
- Adversary tactics, techniques, and procedures (TTPs)
- Infrastructure reuse
- Malware family relationships
- Operational patterns
- Geographic indicators
- Motivations and targeting behavior

Attribution analysis supports:

- Incident response investigations
- Threat intelligence operations
- Strategic risk assessments
- Executive awareness
- Regulatory reporting
- Threat hunting prioritization
- Detection engineering
- Sector-wide intelligence sharing

The purpose of attribution analysis is to:

- Understand attacker behavior
- Correlate attacks to known campaigns
- Improve defensive posture
- Support intelligence-led defense
- Identify recurring adversary patterns
- Enhance threat hunting capability

Attribution analysis must be conducted carefully because incorrect attribution may result in:

- Misguided defensive actions
- False intelligence reporting
- Incorrect risk prioritization
- Legal or regulatory issues
- Executive misinformation
- Reputational risk

This SOP ensures:

- Structured attribution methodology
- Evidence-based analysis
- Confidence-based reporting
- Intelligence validation standards
- Controlled intelligence dissemination
- Audit-ready analytical documentation

---

# 3. Scope

This SOP applies to attribution analysis involving:

| Investigation Type | Example |
|---|---|
| APT investigations | Nation-state activity |
| Ransomware campaigns | Affiliate tracking |
| Malware investigations | Malware family attribution |
| Phishing campaigns | Infrastructure correlation |
| Credential theft campaigns | TTP analysis |
| Supply chain attacks | Infrastructure reuse |
| Insider threat investigations | Behavioral correlation |
| Cloud compromise campaigns | IAM abuse patterns |
| Financial fraud operations | Banking malware |
| Multi-stage attacks | Campaign reconstruction |

---

## 3.1 Attribution Data Sources

| Source Type | Examples |
|---|---|
| Malware analysis reports | Reverse engineering |
| Threat intelligence feeds | IOC/TTP correlation |
| SIEM telemetry | Attack timelines |
| EDR telemetry | Endpoint activity |
| DNS and network logs | Infrastructure analysis |
| Open-source intelligence (OSINT) | Public reporting |
| Government advisories | CERT intelligence |
| Internal investigations | Historical incidents |

---

# 4. Attribution Analysis Philosophy (IMPORTANT)

Attribution analysis is probabilistic, not absolute.

The objective is to assess evidence and determine the likelihood of adversary association.

Attribution should focus on:

- Evidence quality
- Infrastructure overlap
- Behavioral patterns
- TTP consistency
- Malware lineage
- Targeting patterns
- Operational similarities

L3 analysts must avoid:

| Poor Practice | Operational Risk |
|---|---|
| Declaring attribution without evidence | False attribution |
| Over-reliance on a single IOC | Weak intelligence |
| Ignoring false flag possibilities | Misleading conclusions |
| Using speculative language | Executive confusion |
| Overstating confidence levels | Strategic errors |

Attribution findings must always include:
- Confidence level
- Supporting evidence
- Analytical limitations
- Alternative explanations where relevant

---

# 5. L3 Attribution Analysis Responsibilities

| Responsibility | Description |
|---|---|
| Threat actor analysis | Adversary profiling |
| TTP correlation | ATT&CK mapping |
| Infrastructure analysis | C2 tracking |
| Malware family correlation | Campaign linkage |
| Intelligence validation | Evidence review |
| Confidence scoring | Analytical assessment |
| Strategic reporting | Executive intelligence |
| Escalation | Critical threat notification |

---

# 6. Attribution Analysis Workflow

| Phase | Objective | Primary Output |
|---|---|---|
| Phase 1 | Intelligence Collection | Attribution scope |
| Phase 2 | IOC and TTP Correlation | Threat linkage |
| Phase 3 | Infrastructure Analysis | Operational indicators |
| Phase 4 | Malware and Tooling Analysis | Capability analysis |
| Phase 5 | Behavioral Pattern Analysis | Adversary profiling |
| Phase 6 | Confidence Assessment | Attribution scoring |
| Phase 7 | Reporting and Escalation | Intelligence reporting |
| Phase 8 | Intelligence Archival | Long-term retention |

---

# 7. Phase 1 – Intelligence Collection

Collect all available evidence relevant to attribution.

---

## 7.1 Intelligence Collection Areas

| Area | Objective |
|---|---|
| IOC collection | Infrastructure analysis |
| Malware samples | Tooling analysis |
| TTP identification | Behavioral analysis |
| Victimology review | Targeting assessment |
| Timeline analysis | Campaign sequencing |

---

## 7.2 Collection Checklist

| Validation Item | Completed |
|---|---|
| Threat intelligence reviewed | ☐ |
| Malware analysis reports reviewed | ☐ |
| IOC correlations completed | ☐ |
| Historical incidents checked | ☐ |
| MITRE mapping initiated | ☐ |

---

## 7.3 Common Attribution Evidence Sources

| Evidence Type | Example |
|---|---|
| Infrastructure overlap | Shared IPs/domains |
| Malware reuse | Shared code |
| TTP reuse | Same attack methods |
| Operational timing | Consistent hours |
| Language artifacts | Embedded strings |

---

# 8. Phase 2 – IOC and TTP Correlation

Correlate observed indicators and behaviors with known adversary profiles.

---

## 8.1 IOC Correlation Areas

| IOC Type | Example |
|---|---|
| Domains | C2 infrastructure |
| IP addresses | Hosting providers |
| File hashes | Malware reuse |
| SSL certificates | Infrastructure overlap |
| Email addresses | Phishing campaigns |

---

## 8.2 TTP Mapping Areas

| MITRE ATT&CK Area | Example |
|---|---|
| Initial Access | Spearphishing |
| Execution | PowerShell abuse |
| Persistence | Scheduled tasks |
| Credential Access | LSASS dumping |
| Exfiltration | Cloud storage upload |

---

## 8.3 Correlation Validation Table

| IOC/TTP | Related Actor/Campaign | Confidence | Evidence |
|---|---|---|---|
| | | | |

---

# 9. Phase 3 – Infrastructure Analysis

Infrastructure analysis identifies adversary operational patterns.

---

## 9.1 Infrastructure Analysis Areas

| Area | Objective |
|---|---|
| Domain analysis | Campaign linkage |
| Hosting analysis | Infrastructure ownership |
| SSL certificate review | Infrastructure reuse |
| WHOIS analysis | Registration patterns |
| Passive DNS review | Historical infrastructure |

---

## 9.2 Infrastructure Risk Indicators

| Indicator | Meaning |
|---|---|
| Shared C2 infrastructure | Campaign overlap |
| Rapid domain rotation | Evasion |
| TOR/VPN hosting | Obfuscation |
| Bulletproof hosting | Malicious operations |

---

## 9.3 Infrastructure Tracking Table

| IOC | Infrastructure Type | Reputation | Linked Campaign |
|---|---|---|---|
| | | | |

---

# 10. Phase 4 – Malware and Tooling Analysis

Analyze malware families and attacker tooling.

---

## 10.1 Malware Analysis Objectives

| Objective | Purpose |
|---|---|
| Identify malware family | Campaign correlation |
| Analyze code reuse | Attribution support |
| Detect tooling overlap | Threat linkage |
| Identify anti-analysis methods | Capability assessment |

---

## 10.2 Tooling Categories

| Tool Type | Example |
|---|---|
| Remote access tools | RATs |
| Credential theft tools | Mimikatz |
| Lateral movement tools | PsExec |
| Persistence tools | Scheduled tasks |
| Exfiltration tools | Rclone |

---

## 10.3 Malware Correlation Indicators

| Indicator | Meaning |
|---|---|
| Shared code structure | Malware lineage |
| Shared encryption methods | Family similarity |
| Similar persistence | Campaign overlap |
| Common payload staging | Operational consistency |

---

# 11. Phase 5 – Behavioral Pattern Analysis

Analyze attacker operational behavior.

---

## 11.1 Behavioral Analysis Areas

| Area | Objective |
|---|---|
| Attack timing | Operational schedule |
| Target selection | Victimology |
| Persistence methods | Long-term strategy |
| Privilege escalation | Capability assessment |
| Exfiltration methods | Operational goals |

---

## 11.2 Behavioral Indicators

| Indicator | Possible Meaning |
|---|---|
| Financial targeting | Cybercrime |
| Government targeting | Nation-state |
| Long dwell time | APT behavior |
| Rapid encryption | Ransomware |
| Credential harvesting | Persistence preparation |

---

## 11.3 Victimology Review Table

| Target Type | Business Sector | Attack Objective |
|---|---|---|
| | | |

---

# 12. Phase 6 – Confidence Assessment

Attribution findings must include confidence scoring.

---

## 12.1 Confidence Levels

| Confidence Level | Meaning |
|---|---|
| High | Strong multi-source evidence |
| Medium | Partial evidence alignment |
| Low | Limited or weak evidence |

---

## 12.2 Confidence Assessment Factors

| Factor | Consideration |
|---|---|
| IOC overlap | Infrastructure reuse |
| TTP consistency | ATT&CK alignment |
| Malware similarity | Code overlap |
| Historical intelligence | Prior campaigns |
| False flag risk | Misleading indicators |

---

## 12.3 Attribution Confidence Table

| Attribution Finding | Confidence Level | Supporting Evidence |
|---|---|---|
| | | |

---

# 13. Phase 7 – Reporting and Escalation

Attribution findings must be documented carefully.

---

## 13.1 Reporting Requirements

| Requirement | Mandatory |
|---|---|
| Executive summary | Yes |
| Threat actor assessment | Yes |
| IOC/TTP mapping | Yes |
| Confidence assessment | Yes |
| Supporting evidence | Yes |
| Analytical limitations | Yes |
| Recommended actions | Yes |

---

## 13.2 Escalation Matrix

| Condition | Escalation Target |
|---|---|
| Nation-state indicators | CISO |
| Critical infrastructure targeting | Executive Management |
| Sector-wide campaign | Compliance / Risk |
| Multi-client MSSP threat | SOC Director |
| Regulatory reporting impact | Legal / Compliance |

---

## 13.3 Intelligence Dissemination Controls

| Distribution Type | Restriction |
|---|---|
| Internal SOC distribution | Authorized personnel only |
| Executive intelligence | Approved summary only |
| Client intelligence sharing | Client-specific only |
| External sharing | Legal approval required |

---

# 14. Phase 8 – Intelligence Archival

Attribution evidence and reports must be archived securely.

---

## 14.1 Archival Requirements

| Requirement | Standard |
|---|---|
| Secure storage | Mandatory |
| Access restricted | Mandatory |
| Retention schedule followed | Mandatory |
| Evidence references maintained | Mandatory |

---

## 14.2 Attribution Archive Table

| Case ID | Threat Actor | Confidence Level | Retention Period |
|---|---|---|---|
| | | | |

---

# 15. MITRE ATT&CK Integration

All attribution analysis should align with MITRE ATT&CK.

---

## 15.1 ATT&CK Mapping Objectives

| Objective | Purpose |
|---|---|
| Standardized threat language | Operational consistency |
| Behavioral correlation | Campaign comparison |
| Detection improvement | Defensive enhancement |
| Threat hunting alignment | Proactive operations |

---

## 15.2 ATT&CK Mapping Table

| ATT&CK Technique | Observed Activity | Related Threat Actor |
|---|---|---|
| | | |

Reference:
`10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md`

---

# 16. MSSP-Specific Attribution Considerations

For MSSP-managed environments:

| Requirement | Purpose |
|---|---|
| Maintain tenant segregation | Prevent intelligence leakage |
| Restrict cross-client attribution sharing | Confidentiality |
| Use client-approved intelligence distribution | Contract compliance |
| Protect client-sensitive findings | Regulatory alignment |
| Coordinate sector-wide threats carefully | Business risk management |

---

# 17. Common Attribution Analysis Mistakes

| Mistake | Operational Risk |
|---|---|
| Overstating attribution confidence | Strategic misdirection |
| Ignoring false flag possibilities | Incorrect attribution |
| Weak IOC validation | Intelligence contamination |
| No behavioral correlation | Incomplete analysis |
| Poor documentation | Executive confusion |

---

# 18. Related Documents

| Document | Path |
|---|---|
| L3 Threat Intel Integration | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Threat-Intel-Integration.md` |
| L3 Malware Analysis SOP | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Malware-Analysis-SOP.md` |
| Threat Actor Profile Template | `08_POST-INCIDENT/08.4_Threat-Intel-Output/Threat-Actor-Profile-Template.md` |
| TTP Intelligence Report | `08_POST-INCIDENT/08.4_Threat-Intel-Output/TTP-Intelligence-Report.md` |
| MITRE ATT&CK Reference | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md` |
| TI Platform Usage Guide | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Platform-Usage-Guide.md` |

---

# 19. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 22-May-2026 | SOC Manager / Threat Intelligence Lead | Initial version |

---

# 20. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**