# Role Definition – L3 SOC Analyst (Senior / Threat Specialist)

---

## 1. Document Control

| Field | Value |
|-------|--------|
| Role | L3 SOC Analyst |
| Document ID | IR-ROLE-003 |
| Version | 1.0 |
| Owner | SOC Manager / Head of SOC |
| Review Cycle | Annual |
| Classification | Confidential |

---

## 2. Role Purpose

The L3 SOC Analyst is responsible for advanced incident investigation, threat analysis, and technical leadership during high-severity incidents. L3 performs:

- Advanced endpoint and network forensics support
- Malware analysis and reverse engineering (as applicable)
- Root cause analysis and attack chain reconstruction
- Threat hunting and detection engineering recommendations
- Guidance to L2/L1 and support to IR Team

L3 acts as the **technical authority** within the SOC during complex incidents.

---

## 3. Reporting Structure

Reports To:
- SOC Manager / Head of SOC

Works Closely With:
- SOC Lead / Incident Commander
- Incident Response Team (IRT)
- Threat Intelligence Team
- IT Infrastructure / Cloud Teams

Escalates To:
- IR Team Lead / CISO (via SOC Lead) for crisis incidents

---

## 4. Key Responsibilities

---

### 4.1 Advanced Incident Investigation
- Analyze multi-stage attack behavior (intrusion → lateral movement → persistence → exfiltration)
- Perform deep SIEM correlations and custom hunting queries
- Validate attacker presence and persistence
- Identify impacted scope across enterprise / client environment

---

### 4.2 Forensics Support
- Guide forensic acquisition requirements (memory, disk, logs, network captures)
- Review forensic artifacts and extract key findings
- Support chain-of-custody compliance
- Ensure analysis is defensible for audits/legal needs

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

### 4.3 Malware Analysis (as applicable)
- Perform static/dynamic analysis of suspicious samples
- Extract Indicators of Compromise (hashes/domains/URLs/registry/processes)
- Recommend containment and detection signatures
- Support eradication recommendations

---

### 4.4 Threat Hunting & Detection Engineering
- Create proactive hunts based on IoCs and TTPs
- Identify detection gaps and propose new SIEM/EDR rules
- Validate alert tuning improvements
- Provide actionable recommendations to engineering teams

---

### 4.5 MITRE ATT&CK Mapping & TTP Analysis
- Map observed behaviors to MITRE techniques
- Identify likely adversary tradecraft
- Provide technical input for APT assessments
- Document attack chain / kill chain narrative

---

### 4.6 Technical Leadership & Mentorship
- Mentor L1/L2 analysts
- Provide investigation playbook enhancements
- Review quality of incident reports and timelines
- Support incident commander with technical decisions

---

### 4.7 Root Cause Analysis (RCA)
- Identify initial access vector
- Confirm exploitation method / misconfiguration / credential compromise
- Validate remediation actions to prevent recurrence
- Document RCA for post-incident review

---

## 5. Decision Authority

L3 MAY:
- Recommend high-impact containment actions (isolation, account-wide resets, blocking)
- Drive technical direction in P1/P2 incidents
- Approve/define advanced hunting and evidence collection steps
- Author technical deep-dive reports and RCA

L3 MAY NOT:
- Provide external regulatory submissions independently (done by compliance/CISO)
- Authorize ransom negotiation or financial/legal commitments
- Override business decisions without management approval

---

## 6. Required Skills

- Advanced incident investigation (Windows/Linux, cloud)
- Network forensics (PCAP analysis, proxy/DNS logs)
- EDR telemetry expertise
- Malware behavior analysis fundamentals
- Scripting and automation (PowerShell, Python, KQL/SPL)
- MITRE ATT&CK knowledge
- Strong technical report writing

---

## 7. Performance KPIs

- Quality of RCA and attack chain accuracy
- Reduction in recurrence through preventive actions
- Detection improvement contributions (new rules/use cases)
- Time to containment for major incidents
- Coaching effectiveness (team capability uplift)

---

## 8. Tools Used

- SIEM (advanced querying & correlation)
- EDR advanced telemetry and response
- Sandbox / detonation environment (if available)
- Network forensics tools (PCAP analysis)
- Forensic collection tools
- Threat intelligence platform
- Code/script repositories for hunts & detections

---

## 9. Compliance Responsibility

L3 ensures:
- Findings are evidence-based and repeatable
- Documentation supports audits (ISO/NIST/RBI)
- Evidence integrity and custody is maintained
- Recommendations include risk-based justification

---

## 10. Escalation to IR Team (Major Incident)

Escalate immediately when:
- Ransomware encryption confirmed
- Active data exfiltration confirmed
- Domain Controller compromise suspected
- Widespread credential compromise detected
- APT or supply-chain compromise suspected
- Business-critical service disruption occurs

---

## 11. Review & Update

Reviewed:
- Annually
- After major incidents / PIR outcomes
- Upon tool/platform changes or SOC restructure

---

**End of Document**