# Incident Response Policy (Master Policy)

---

## 1. Document Control

| Field | Value |
|-------|--------|
| Document Name | Incident Response Policy |
| Document ID | IR-POL-001 |
| Version | 1.0 |
| Effective Date | 14-May-2026 |
| Owner | SOC Manager |
| Approved By | CISO |
| Review Cycle | Annual |
| Classification | Internal / Confidential |

---

## 2. Purpose

The purpose of this policy is to establish a structured, consistent, and effective approach for identifying, responding to, managing, and recovering from cybersecurity incidents affecting the organization and its managed clients (MSSP environments).

This policy ensures:
- Rapid detection and containment of incidents
- Protection of organizational and client assets
- Regulatory compliance
- Business continuity
- Evidence preservation for legal and forensic purposes

---

## 3. Scope

This policy applies to:

- All employees
- SOC (L1/L2/L3)
- SOC Leads
- Incident Response Team (IRT)
- IT Teams
- Management
- MSSP Client environments
- All systems (on-prem, cloud, hybrid)
- All third-party managed infrastructure

---

## 4. Policy Statement

The organization shall:

1. Maintain a formal Incident Response Program aligned with:
   - ISO/IEC 27001
   - NIST Cybersecurity Framework
   - RBI Cyber Security Framework
2. Maintain documented incident classification criteria.
3. Ensure 24x7 monitoring through SOC operations.
4. Define escalation procedures across L1/L2/L3/IRT.
5. Preserve evidence following chain-of-custody procedures.
6. Notify regulatory authorities where required.
7. Conduct post-incident review and root cause analysis.
8. Continuously improve detection and response capabilities.

---

## 5. Incident Definition

A security incident is defined as:

> Any actual or suspected event that compromises the confidentiality, integrity, or availability (CIA) of information systems, data, or services.

Examples include:
- Ransomware
- Phishing
- Data exfiltration
- Unauthorized access
- DDoS
- Insider threats
- Zero-day exploitation

---

## 6. Incident Severity Levels

Incidents shall be classified into:

- P1 – Critical
- P2 – High
- P3 – Medium
- P4 – Low

Severity classification is defined in:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/`

---

## 7. Roles and Responsibilities

Defined in:
`00_GOVERNANCE/00.3_Roles-and-Responsibilities/`

Key roles:

- L1: Initial triage
- L2: Deep investigation
- L3: Advanced analysis / forensics
- SOC Lead: Coordination & escalation
- IR Team: Major incident handling
- Management: Oversight and approvals

---

## 8. Escalation Requirements

- P1 incidents require immediate SOC Lead notification.
- P1 and P2 incidents require management briefing.
- Regulatory reporting timelines must be followed (if applicable).
- Client notification must follow SLA agreements.

Detailed procedures available in:
`05_ESCALATION-AND-COMMUNICATION/`

---

## 9. Evidence Handling

All digital evidence must:

- Be collected using approved forensic tools
- Maintain chain-of-custody documentation
- Be stored securely
- Follow retention policies

Refer:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 10. Regulatory & Legal Compliance

The organization commits to compliance with:

- ISO/IEC 27001 (Annex A.5 & A.16)
- NIST CSF (Respond & Recover Functions)
- RBI Cyber Security Framework
- CERT-In reporting requirements (if applicable)

---

## 11. Training & Awareness

- Annual IR training mandatory
- Tabletop exercises conducted at least annually
- SOC personnel require role-based training
- IR simulations must be documented

---

## 12. Policy Violations

Failure to comply with this policy may result in:

- Disciplinary action
- Contractual penalties (MSSP context)
- Legal consequences

---

## 13. Review & Maintenance

This policy shall be:

- Reviewed annually
- Updated after major incidents
- Reviewed after regulatory changes

---

## 14. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**