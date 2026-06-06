# Alert-to-Incident Qualification

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Alert-to-Incident Qualification |
| Document ID | IR-TRIAGE-002 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

## 2. Purpose

This document defines standardized rules for converting a security alert
into a formally tracked security incident.

It ensures that:
- true incidents are not missed due to inconsistent analyst judgment
- false positives are closed consistently and defensibly
- severity and SLA clocks are applied correctly
- incident reporting is accurate and audit-ready
- SOC operations are consistent across enterprise and MSSP environments

---

## 3. Scope

Applies to:
- SIEM alerts
- EDR alerts
- IDS/IPS/firewall/WAF alerts
- cloud and SaaS security alerts
- user-reported security events
- threat intelligence IOC matches
- MSSP multi-tenant alert streams

---

## 4. Definitions

| Term | Definition |
|------|------------|
| Alert | A detection produced by a tool or user report requiring validation |
| Incident | A confirmed or strongly suspected event that compromises confidentiality, integrity, or availability |
| Event | An observable occurrence in a system or network (may be benign) |
| False Positive (FP) | Alert triggered by non-malicious activity or detection error |
| Benign True Positive (BTP) | Alert triggered correctly but activity is authorized/expected |
| Qualification | The decision process to declare an alert as an incident or close it |

Reference: `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/`

---

## 5. Qualification Outcomes (Required)

Every alert must end as one of the following:

| Outcome | Description | Example |
|---------|-------------|---------|
| Incident – Confirmed | Malicious activity confirmed | malware executed; account takeover confirmed |
| Incident – Suspected | Strong evidence; investigation required | likely compromise; high-risk indicators present |
| Benign True Positive | Real activity but authorized | approved vulnerability scan; planned admin change |
| False Positive | Detection error or non-malicious | noisy rule, parsing issue, legitimate application |
| Informational | Not actionable but tracked | blocked scan with no impact |
| Duplicate | Already tracked in another ticket | same alert already under active incident |

---

## 6. Qualification Criteria (Decision Rules)

### 6.1 Declare an Incident Immediately When Any Condition Is True

Declare an incident (P1/P2/P3 as appropriate) if any are observed:

1. Unauthorized access is confirmed (successful login with suspicious context)
2. Malware execution is confirmed (EDR confirms execution or payload drop)
3. Persistence is detected (new scheduled task/service/autorun without authorization)
4. Privileged activity is suspicious or unauthorized (admin group change, privilege escalation)
5. Lateral movement is detected or strongly suspected (RDP/SMB/WMI spread)
6. Data access to sensitive repositories is unauthorized
7. Data exfiltration is confirmed or strongly suspected
8. Security tools or logs are tampered with (EDR disabled, logs cleared)
9. Public exposure of sensitive cloud storage is confirmed
10. Business-critical service availability is impacted by security-related activity

These conditions typically qualify as P2 or P1.

---

### 6.2 Declare a Suspected Incident When Evidence Is Strong But Incomplete

Declare a suspected incident when:

- attacker-like behavior exists but confirmation needs deeper analysis
- multiple weak signals correlate to form a high-confidence pattern
- initial alert source is reliable but additional confirmation is pending
- investigation is required to confirm scope and impact

Examples:
- suspicious sign-in + mailbox forwarding rule created
- suspicious process execution + suspicious outbound traffic
- web exploit attempts + server errors + new outbound connection

Suspected incidents must not be closed without L2 review.

---

### 6.3 Classify as Benign True Positive When Activity Is Authorized and Verified

An alert is Benign True Positive when:

- the detection is correct
- the underlying action is legitimate and authorized
- authorization can be verified by one of:
  - approved change ticket
  - penetration test approval document
  - vulnerability scan schedule
  - signed-off admin task request
  - known business workflow documentation

Benign True Positives should still be tracked for tuning and reporting.

---

### 6.4 Classify as False Positive When Detection Is Incorrect or Misleading

An alert is False Positive when:

- the activity is legitimate and not suspicious
- detection logic is wrong or misconfigured
- enrichment confirms the IOC is not malicious
- tool generated incorrect correlation due to parsing or data errors

False positives must include:
- reason for closure
- evidence supporting closure
- tuning recommendation if recurring

Reference: `01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/False-Positive-Handling.md`

---

### 6.5 Classify as Informational When No Action Is Required

An alert is Informational when:

- activity is blocked/prevented and no follow-on activity exists
- it is low risk and does not require containment actions
- it is useful for trend analysis but not for active response

Examples:
- blocked phishing with no click/open
- blocked port scan on perimeter with no exploit success
- routine policy violation without data exposure

---

## 7. Qualification Workflow (Operational Steps)

### Step 1: Validate Alert Data Quality
- confirm asset identity (hostname, IP, user)
- confirm timestamp accuracy and time synchronization concerns
- confirm log source is healthy and complete
- identify if the alert is part of a known noisy rule or outage

If data is incomplete, gather context before decision.

---

### Step 2: Enrichment (Minimum Standard)
Enrichment sources should include (as applicable):

- EDR details: process tree, hash, network connections
- identity logs: sign-in history, MFA, impossible travel
- proxy/firewall logs: outbound destinations, volume, frequency
- DNS logs: new domain queries, tunneling signs
- asset criticality: business impact and system role
- threat intel: IOC reputation and campaign context

---

### Step 3: Identify Authorization and Known Activities
Check whether the alert matches:
- scheduled vulnerability scans
- approved pentests
- change windows
- known admin tasks
- backup operations
- IT patching activities

If authorized and proven, disposition as BTP.

---

### Step 4: Evaluate Malicious Indicators
Evaluate indicators across:
- identity compromise
- endpoint execution
- persistence
- lateral movement
- data access/exfiltration
- defense evasion

If any strong malicious indicator exists, qualify as incident.

---

### Step 5: Determine Severity (P1–P4)
Use the Severity Classification Guide:

`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

Severity must be justified using:
- impact
- scope
- data sensitivity
- threat activity

---

### Step 6: Document Decision in Ticket
Ticket must contain:

- alert summary and evidence
- qualification outcome (incident/FP/BTP/etc.)
- severity (if incident)
- scope assessment and next steps
- escalations performed and timestamps

---

## 8. Mandatory Ticket Fields (Qualification Standard)

For all alerts (including closed):

- alert source and rule name
- affected asset(s) and user(s)
- time detected and time observed
- enrichment performed (what sources checked)
- decision outcome and justification
- evidence reference (log export, screenshot, query link)

For incidents:

- severity assigned (P1–P4)
- incident category (CAT-01 to CAT-14)
- escalation actions taken and timestamps
- containment recommendation (if applicable)

---

## 9. Escalation Triggers During Qualification

Escalate immediately to SOC Lead if any are observed:

- ransomware behavior indicators
- privileged account compromise suspected
- domain controller involved
- confirmed C2 beaconing from server assets
- confirmed or suspected exfiltration
- multiple systems affected rapidly
- security tool tampering
- business-critical outage suspected to be security-related

---

## 10. MSSP Qualification Notes (Multi-Tenant Considerations)

For MSSP operations:

- ensure alert belongs to correct tenant and client context
- enforce client data segregation and access controls
- apply client-specific severity rules if contracted
- maintain client-specific notification timelines and SLA requirements
- never cross-reference another client’s details in a different client ticket

Reference:
`01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/Multi-Client-Triage-MSSP.md`

---

## 11. Quality Assurance and Review Requirements

Quality checks should include:

- percentage of incidents incorrectly qualified
- percentage of P1/P2 incidents missing required evidence
- false positive rate per rule and per data source
- reclassification rate (P3 → P2, P2 → P1, etc.)
- trend analysis for repeated patterns

These metrics are tracked through SLO reporting.

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`

---

## 12. Related Documents

| Document | Path |
|---------|------|
| Master Triage Decision Tree | `01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/Master-Triage-Decision-Tree.md` |
| False Positive Handling | `01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/False-Positive-Handling.md` |
| Multi-Client Triage (MSSP) | `01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/Multi-Client-Triage-MSSP.md` |
| Severity Guide | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md` |
| Escalation Criteria | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Escalation-Criteria.md` |
| Ticket Standards | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md` |

---

## 13. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | SOC Manager | Initial version |

---

## 14. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

End of Document