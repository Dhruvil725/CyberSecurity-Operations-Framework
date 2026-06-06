# Threat Intelligence (TI) Reporting Template

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | Template – Threat Intelligence Reporting |
| Document ID | TOOL-TI-006 |
| Version | 1.0 |
| Effective Date | 25-May-2026 |
| Owner | SOC Manager / Threat Intelligence Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

# 2. Purpose

This document provides a standardized, audit-ready template for producing Threat Intelligence (TI) reports used by the SOC for:

- Operational awareness
- Detection engineering improvements (SIEM/EDR)
- Incident response support
- MSSP client communications (where contractually required)
- Management briefings
- Compliance and audit evidence

This template ensures:

- Consistent structure and completeness across all TI reports
- Clear separation of facts vs assumptions vs assessments
- Proper handling of sharing restrictions (TLP/licensing)
- Traceable sources and evidence references
- Actionable recommendations with ownership and timelines

---

# 3. Scope

Use this template for the following report types:

| Report Type | Examples | Typical Audience |
|---|---|---|
| Flash Alert | New ransomware campaign; active exploitation | SOC / IR / Management |
| Weekly TI Summary | Trending threats, key IOCs, notable incidents | SOC / SOC Lead |
| Monthly Threat Landscape | Sector trends, top TTPs, risk themes | Management / Clients |
| Campaign Report | APT or coordinated phishing/BEC campaign | IR / Detection Eng |
| Client-Specific Advisory (MSSP) | Client environment exposure to new threat | Client Security Team |

---

# 4. Report Metadata (Mandatory)

> Fill all applicable fields.

| Field | Value |
|---|---|
| Report Title | `[TI REPORT TYPE] – [TOPIC] – [YYYY-MM-DD]` |
| Report ID | `TI-RPT-[YYYY]-[####]` |
| Report Type | Flash / Weekly / Monthly / Campaign / Client Advisory |
| TLP Classification | TLP:CLEAR / TLP:GREEN / TLP:AMBER / TLP:RED |
| Date Published (UTC) | `YYYY-MM-DD HH:MM` |
| Prepared By | `Name / Role` |
| Reviewed By | `Name / Role` |
| Approved By | `Name / Role` (if required) |
| Validity Window | `Start date → End date` |
| Related Tickets / Incidents | `INC-xxxx`, `PIR-xxxx` |
| Related Campaign / Actor | `If known` |
| Distribution List | `Teams / Clients / Mailing list` |
| MSSP Client Scope | `Client IDs` (if applicable) |
| Sharing Restrictions | Licensing / contractual / regulatory constraints |

---

# 5. Executive Summary (Mandatory)

## 5.1 Summary (Non-Technical)

- **What is happening:**  
  `…`

- **Why it matters:**  
  `…`

- **Who is impacted (internal / clients):**  
  `…`

- **Expected impact:**  
  `Service disruption / credential theft / data theft / ransomware risk / fraud risk`

- **Recommended immediate actions (Top 3):**  
  1. `…`  
  2. `…`  
  3. `…`

---

# 6. Intelligence Assessment

## 6.1 Confidence Statement (Mandatory)

> Choose one and justify.

- **Confidence Level:** High / Medium / Low  
- **Justification:**  
  `Source reliability, corroboration, recency, internal sightings, known FP history…`

## 6.2 Sources (Mandatory)

> List sources with sufficient detail for traceability. Do not include restricted details if TLP/contract forbids.

| Source Type | Source Name / Reference | Date Accessed (UTC) | Notes |
|---|---|---:|---|
| Commercial Feed | `…` | `…` | `…` |
| OSINT | `…` | `…` | `…` |
| Vendor Advisory | `…` | `…` | `…` |
| Internal Telemetry | `SIEM/EDR` | `…` | `Sighting summary` |
| Client Provided (MSSP) | `Client ID` | `…` | `…` |

## 6.3 Key Judgments (Optional but Recommended)

- `Judgment 1…`
- `Judgment 2…`
- `Judgment 3…`

---

# 7. Threat Overview

## 7.1 Threat Description (Mandatory)

- **Threat Type:** `Ransomware / Phishing / BEC / Malware / APT / Exploit / DDoS / Insider`  
- **Observed Objectives:** `Credential theft / persistence / lateral movement / data theft / disruption`  
- **Initial Access Methods:** `…`  
- **Notable Behaviors:** `…`

## 7.2 Targets and Sector Relevance (Recommended)

- **Sector relevance (BFSI/MSSP):** `…`
- **Likely targets:** `…`
- **Geographies impacted:** `…`

---

# 8. TTPs (MITRE ATT&CK Mapping)

> Include confirmed and suspected techniques.

| Tactic | Technique ID | Technique Name | Confidence | Evidence / Notes |
|---|---|---|---|---|
| `…` | `Txxxx` | `…` | High/Med/Low | `…` |
| `…` | `Txxxx` | `…` | High/Med/Low | `…` |

Reference:
`10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md`

---

# 9. Indicators of Compromise (IoCs)

## 9.1 IoC Handling Notes (Mandatory)

- **IoCs are time-bound:** TTL/expiry must be applied before dissemination.
- **Do not block without validation/approval:** Follow IoC handling and integration SOPs.
- **MSSP segregation:** IoCs must be scoped to tenant/client where applicable.

References:  
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md`  
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Integration-with-SIEM.md`  
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Integration-with-EDR.md`

## 9.2 IoC Table (Mandatory if IoCs exist)

> Add rows as needed.

| IoC Type | Indicator | Confidence | TTL/Expiry (UTC) | Source | Notes / Context |
|---|---|---|---|---|---|
| IP | `x.x.x.x` | High/Med/Low | `YYYY-MM-DD` | `…` | `C2 / staging / scan infra` |
| Domain | `example.com` | High/Med/Low | `YYYY-MM-DD` | `…` | `Phishing landing page` |
| URL | `https://…` | High/Med/Low | `YYYY-MM-DD` | `…` | `Credential harvest path` |
| Hash (SHA256) | `…` | High/Med/Low | `YYYY-MM-DD` | `…` | `Malware payload` |
| Cert Fingerprint | `…` | High/Med/Low | `YYYY-MM-DD` | `…` | `If supported` |

## 9.3 Suggested Detection Content (Recommended)

> Provide ready-to-use ideas; do not include vendor-proprietary query language unless permitted.

- **SIEM ideas:**  
  - `DNS queries to listed domains + suspicious parent processes`  
  - `Proxy connections to URLs + file download + execution chain`  
  - `Outbound firewall connections to IOCs from privileged servers`

- **EDR ideas:**  
  - `Alert on hash execution`  
  - `Watchlist suspicious command-lines`  
  - `Detect persistence mechanisms (scheduled tasks, registry run keys)`

---

# 10. Internal Exposure / Sightings

## 10.1 Summary (Mandatory if checked)

- **Sighting status:** Confirmed / None observed / Not assessed  
- **Time range searched (UTC):** `Start → End`  
- **Data sources searched:** `SIEM indexes, EDR telemetry, DNS logs, proxy logs…`

## 10.2 Sighting Table (Recommended)

| Entity | Type | Evidence Source | Time (UTC) | Match Details | Disposition |
|---|---|---|---:|---|---|
| `FIN-WS-12` | Host | EDR | `…` | `Hash executed…` | TP/FP/Unknown |
| `jsmith` | User | IAM | `…` | `Login anomalies…` | TP/FP/Unknown |
| `10.10.1.10` | IP | Firewall | `…` | `Outbound to IOC IP…` | TP/FP/Unknown |

---

# 11. Risk Assessment

## 11.1 Impact and Likelihood (Recommended)

| Dimension | Rating | Rationale |
|---|---|---|
| Impact | Low / Medium / High | `Business/system/data impact rationale` |
| Likelihood | Low / Medium / High | `Exposure, prevalence, ease of exploitation` |
| Overall Risk | Low / Medium / High | `Summary` |

## 11.2 Affected Assets / Services (If Known)

- **Critical systems potentially impacted:** `…`
- **Accounts/roles at risk:** `…`
- **Client environments at risk (MSSP):** `Client IDs…`

---

# 12. Recommended Actions (Mandatory)

## 12.1 Immediate Actions (0–24 hours)

| Action | Owner | Priority | Due (UTC) | Evidence / Tracking |
|---|---|---|---:|---|
| `Add SIEM lookup + correlation rule` | Detection Eng | High | `…` | `TKT-…` |
| `Enable EDR watchlist` | EDR Admin | High | `…` | `TKT-…` |
| `Client advisory sent` | MSSP SDM | Medium | `…` | `TKT-…` |

## 12.2 Short-Term Actions (1–7 days)

| Action | Owner | Priority | Due (UTC) | Evidence / Tracking |
|---|---|---|---:|---|
| `Patch/update…` | IT Ops | High | `…` | `CHG-…` |
| `Hunt for TTP…` | L2/L3 | Medium | `…` | `HUNT-…` |

## 12.3 Long-Term Actions (7–30 days)

| Action | Owner | Priority | Due (UTC) | Evidence / Tracking |
|---|---|---|---:|---|
| `Improve baseline detections` | Detection Eng | Medium | `…` | `DET-IMP-…` |
| `Tabletop exercise scenario update` | SOC Lead | Low | `…` | `TTX-…` |

---

# 13. Communication Guidance (Optional)

## 13.1 Internal Communication (SOC/IT/Management)

- **Who should be notified:** `…`
- **Message summary:** `…`
- **Update frequency:** `…`

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/`

## 13.2 MSSP Client Communication (If Applicable)

- **Client(s):** `Client IDs / names`  
- **Notification timeline (per SLA):** `…`  
- **Client actions requested:** `…`

---

# 14. Limitations and Assumptions (Recommended)

- **Assumptions:** `…`
- **Gaps in visibility:** `…`
- **Potential false positive areas:** `…`
- **Data freshness constraints:** `…`

---

# 15. Appendix (Optional)

## 15.1 Reference Links

- `…`
- `…`

## 15.2 Attachments / Artifacts

| Artifact | Location / Reference | Notes |
|---|---|---|
| IoC export | `…` | `Tenant-scoped if MSSP` |
| Screenshots | `…` | `Sanitized as required` |
| Query outputs | `…` | `Evidence references` |

---

# 16. Related Documents

| Document | Path |
|---|---|
| TI Feed Management | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Feed-Management.md` |
| TI IoC Handling SOP | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md` |
| TI Integration with SIEM | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Integration-with-SIEM.md` |
| TI Integration with EDR | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Integration-with-EDR.md` |
| TI Platform Usage Guide | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Platform-Usage-Guide.md` |
| Ticket Fields Standards | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Fields-Standards.md` |
| SLO Metrics Definition | `00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md` |

---

# 17. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 25-May-2026 | SOC Manager / Threat Intelligence Lead | Initial version |

---

# 18. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**
