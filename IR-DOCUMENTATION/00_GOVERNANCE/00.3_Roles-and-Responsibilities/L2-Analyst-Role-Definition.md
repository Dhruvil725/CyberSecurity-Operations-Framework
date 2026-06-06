# Role Definition – L2 SOC Analyst

---

## 1. Document Control

| Field | Value |
|-------|--------|
| Role | L2 SOC Analyst |
| Document ID | IR-ROLE-002 |
| Version | 1.0 |
| Owner | SOC Manager |
| Review Cycle | Annual |
| Classification | Internal |

---

## 2. Role Purpose

The L2 SOC Analyst is responsible for:

- In-depth investigation of escalated alerts
- Confirming security incidents
- Performing detailed log and endpoint analysis
- Coordinating containment actions
- Supporting regulatory and audit documentation

L2 acts as the **investigation and validation authority** within the SOC.

---

## 3. Reporting Structure

Reports To:
- SOC Lead / SOC Manager

Escalates To:
- L3 Analyst
- IR Team
- SOC Lead (for P1/P2 updates)

---

## 4. Key Responsibilities

---

### 4.1 Deep Investigation

- Perform detailed SIEM queries
- Correlate multi-source logs
- Investigate endpoint telemetry
- Analyze user behavior anomalies
- Identify attack patterns and TTPs

---

### 4.2 Incident Confirmation

- Confirm whether activity is:
  - True Positive
  - False Positive
  - Suspicious (needs monitoring)
- Assign severity level
- Declare incident if criteria met

---

### 4.3 Containment Coordination

- Recommend isolation of endpoint
- Recommend credential resets
- Recommend IP/domain blocking
- Coordinate with IT/Network teams

Note: Critical containment requires SOC Lead approval.

---

### 4.4 Evidence Handling

- Preserve logs
- Export relevant artifacts
- Maintain forensic integrity
- Document evidence chain

Follow:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

### 4.5 Client & Internal Communication

- Provide technical updates to SOC Lead
- Participate in bridge calls (P1/P2)
- Support MSSP client communication (technical input)

---

### 4.6 Threat Intelligence Enrichment

- Enrich indicators with TI feeds
- Map activity to MITRE ATT&CK
- Identify threat actor patterns
- Recommend detection improvements

---

### 4.7 Documentation

- Maintain detailed investigation notes
- Document timeline of events
- Provide technical summary
- Attach relevant evidence
- Ensure ticket completeness

---

## 5. Decision Authority

L2 MAY:
- Confirm incidents
- Recommend containment
- Escalate to IR Team
- Close validated false positives

L2 MAY NOT:
- Authorize regulatory reporting
- Declare crisis mode independently
- Approve high-risk business-impacting containment

---

## 6. Required Skills

- Advanced log analysis
- Network traffic analysis
- Endpoint telemetry analysis
- Understanding of attacker TTPs
- Familiarity with MITRE ATT&CK
- Knowledge of malware behavior
- Basic scripting (PowerShell/Python preferred)

---

## 7. Performance KPIs

- Mean Time to Respond (MTTR)
- Investigation accuracy
- Escalation quality
- Documentation completeness
- Containment coordination time
- Detection improvement suggestions

---

## 8. Tools Used

- SIEM (Advanced Querying)
- EDR Deep Investigation Console
- Network Analysis Tools
- Threat Intelligence Platform
- Sandbox (if available)
- Firewall Management Console

---

## 9. Compliance Responsibility

L2 ensures:

- Proper incident classification
- Regulatory impact identification
- SLA adherence
- Audit-ready documentation
- Evidence preservation

---

## 10. Training Requirements

- Advanced investigation training
- Threat hunting training
- MITRE ATT&CK mapping
- Malware behavior fundamentals
- Tabletop exercise participation
- Regulatory awareness (ISO/NIST/RBI)

---

## 11. Escalation Criteria to L3 / IR Team

Escalate when:

- Advanced persistent threat suspected
- Lateral movement detected
- Data exfiltration confirmed
- Ransomware activity detected
- Zero-day exploitation suspected
- Enterprise-wide compromise suspected

---

## 12. Review & Update

Reviewed:
- Annually
- After major incidents
- Upon SOC process changes

---

**End of Document**