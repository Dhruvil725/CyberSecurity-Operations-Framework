# MSSP – Client SLA Template (Incident Response)

---

## 1. Document Control

| Field | Value |
|-------|--------|
| Document Name | MSSP Client SLA Template – IR |
| Document ID | IR-SLA-002 |
| Version | 1.0 |
| Effective Date | 14-May-2026 |
| Owner | MSSP Service Delivery Manager |
| Approved By | CISO / Contract Owner |
| Classification | Confidential |
| Review Cycle | Quarterly / Contract Renewal |

---

## 2. Purpose

This template defines the Service Level Agreement (SLA) framework between the MSSP and its managed clients for Incident Response (IR) services.

This document must be:
- Customized per client engagement
- Signed by both MSSP and client authorized representatives
- Referenced in the Master Service Agreement (MSA) or Statement of Work (SOW)
- Reviewed quarterly and upon contract renewal

---

## 3. Client Information

| Field | Details |
|-------|---------|
| Client Name | |
| Client Industry | |
| Contract / SOW Reference | |
| Service Start Date | |
| Service End Date / Review Date | |
| MSSP Account Manager | |
| MSSP SDM (Service Delivery Manager) | |
| Client Primary Security Contact | |
| Client Escalation Contact | |
| Client After-Hours Contact | |

---

## 4. Scope of IR Services Covered Under This SLA

The following services are included under this SLA:

| Service | Included (Yes/No) | Notes |
|---------|-------------------|-------|
| 24x7 Security Monitoring (SIEM) | | |
| EDR Alert Monitoring & Response | | |
| Phishing Investigation | | |
| Malware/Ransomware Response | | |
| Threat Intelligence Integration | | |
| Incident Triage (L1/L2) | | |
| Advanced Investigation (L3) | | |
| IR Team Activation (P1/P2) | | |
| Forensic Evidence Collection | | |
| Regulatory Reporting Support | | |
| Post Incident Review (PIR) | | |
| Monthly Security Report | | |
| Quarterly SLA Review Call | | |

---

## 5. Incident Severity Definitions (Client-Agreed)

| Severity | Definition | Example |
|----------|------------|---------|
| P1 – Critical | Immediate threat to client business operations or data | Ransomware active encryption, confirmed breach |
| P2 – High | Significant threat requiring urgent response | Malware execution, privilege escalation |
| P3 – Medium | Suspicious activity requiring investigation | Repeated failed logins, anomalous behavior |
| P4 – Low | Informational / low-risk alert | Policy violation, minor configuration alert |

> Note: Client may request custom severity definitions – document below.

Client-specific severity notes:
_______________________________________________

---

## 6. SLA Timelines – Per Severity Level

---

### P1 – Critical

| SLA Metric | MSSP Commitment | Notes |
|------------|----------------|-------|
| Alert Detection to Triage | ≤ 5 minutes | |
| Initial Client Notification | ≤ 15 minutes from detection | Via agreed channel |
| L2 Escalation | ≤ 15 minutes | |
| IR Team Activation | ≤ 30 minutes | If included in scope |
| Status Update Cadence | Every 30 minutes | Until containment |
| Containment Action (where authorized) | ≤ 1 hour | Subject to client approval |
| Resolution Target | ≤ 4 hours (containment) | |
| Incident Report Delivery | ≤ 24 hours post closure | |

---

### P2 – High

| SLA Metric | MSSP Commitment | Notes |
|------------|----------------|-------|
| Alert Detection to Triage | ≤ 10 minutes | |
| Initial Client Notification | ≤ 30 minutes from detection | Via agreed channel |
| L2 Escalation | ≤ 30 minutes | |
| Status Update Cadence | Every 1 hour | |
| Containment Action (where authorized) | ≤ 2 hours | Subject to client approval |
| Resolution Target | ≤ 8 hours (containment) | |
| Incident Report Delivery | ≤ 48 hours post closure | |

---

### P3 – Medium

| SLA Metric | MSSP Commitment | Notes |
|------------|----------------|-------|
| Alert Detection to Triage | ≤ 15 minutes | |
| Initial Client Notification | ≤ 2 hours | |
| Investigation | ≤ 4 hours | |
| Status Update Cadence | Every 4 hours | |
| Resolution Target | ≤ 24 hours | |
| Incident Report Delivery | ≤ 5 business days | |

---

### P4 – Low

| SLA Metric | MSSP Commitment | Notes |
|------------|----------------|-------|
| Alert Detection to Triage | ≤ 30 minutes | |
| Initial Client Notification | Next business day | Unless upgraded |
| Investigation | ≤ 8 hours | |
| Resolution Target | ≤ 72 hours | |
| Incident Report Delivery | Monthly summary report | |

---

## 7. Client Notification Channels

| Channel | Details | Used For |
|---------|---------|---------|
| Primary Email | | P1/P2/P3 notifications |
| Secondary Email | | Backup contact |
| Phone / Mobile | | P1 only |
| Ticketing Portal | | All severities |
| Messaging Platform (Teams/Slack) | | As agreed |
| Bridge Call | | P1 bridge calls |

---

## 8. Client Response Obligations

For SLA timelines to be met, the client must:

| Obligation | SLA Impact if Not Met |
|------------|----------------------|
| Respond to P1 bridge call within 15 minutes | SLA clock paused pending client join |
| Provide containment approval within agreed time | SLA clock paused pending approval |
| Maintain up-to-date contact directory | MSSP not liable for missed notifications |
| Ensure log sources are active and integrated | Detection SLA paused if source unavailable |
| Provide access for investigation (if needed) | Investigation SLA paused pending access |

---

## 9. SLA Clock Rules

- SLA clock **starts**: Alert received in SIEM/EDR
- SLA clock **pauses** when:
  - Awaiting client approval for containment action
  - Awaiting client-provided access or information
  - Third-party dependency outside MSSP control
- SLA clock **resumes**: Upon client response/approval
- All pauses must be **documented** in incident ticket with timestamps

---

## 10. Reporting Commitments

| Report | Frequency | Delivery Method |
|--------|-----------|----------------|
| Incident Notification | Real-time (per severity) | Email / Portal / Bridge |
| Incident Summary Report | Per P1/P2 incident | Email (within 24-48 hrs) |
| Monthly Security Operations Report | Monthly | Email / Portal |
| SLA Compliance Report | Monthly | Email |
| Quarterly Business Review (QBR) | Quarterly | Meeting / Presentation |

---

## 11. SLA Exclusions

The following scenarios are excluded from SLA calculations:

- Client-initiated service outages
- Planned maintenance windows (agreed in advance)
- Log source failures outside MSSP control
- Force majeure events
- Delays caused by client non-response / approval delays
- Scope exclusions defined in MSA/SOW

---

## 12. SLA Breach & Remediation

| Breach Type | Remediation |
|------------|-------------|
| Notification SLA breach | Root cause documented; corrective action within 48 hours |
| Triage SLA breach | Operational review within 24 hours |
| Containment SLA breach | Bridge call + RCA within 24 hours |
| Repeated SLA breaches | Formal service improvement plan within 5 business days |

---

## 13. Service Credits (if applicable)

> Complete if contract includes service credit provisions.

| SLA Breach Threshold | Credit |
|----------------------|--------|
| 1 P1 SLA breach per month | % credit as per MSA |
| 2+ P1 SLA breaches per month | % credit as per MSA |
| Monthly SLA compliance < agreed % | Escalation to account review |

---

## 14. Review & Amendment

This SLA shall be reviewed:
- Quarterly
- Upon contract renewal
- After major incident affecting client
- Upon scope change

Amendments require written approval from both parties.

---

## 15. Sign-Off

**MSSP Authorized Representative**

Name: ____________________
Title: ____________________
Date: ____________________
Signature: ________________

**Client Authorized Representative**

Name: ____________________
Title: ____________________
Date: ____________________
Signature: ________________

---

**End of Document**