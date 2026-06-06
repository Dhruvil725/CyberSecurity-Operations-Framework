# Multi-Client Alert Handling Procedure (MSSP Multi-Tenant)

---

# 1. Document Control

| Field          | Value                                         |
| -------------- | --------------------------------------------- |
| Document Name  | Procedure – Multi-Client Alert Handling       |
| Document ID    | MSSP-MT-003                                   |
| Version        | 1.0                                           |
| Effective Date | 30-May-2026                                   |
| Owner          | MSSP SOC Manager / SOC Lead                   |
| Approved By    | MSSP CISO                                     |
| Classification | Confidential – MSSP Internal                  |
| Review Cycle   | Annually (or upon SOC operating model change) |

---

# 2. Purpose

This document defines the standardized **Multi-Client Alert Handling Procedure** governing how the MSSP SOC receives, prioritizes, triages, assigns, and tracks security alerts originating from multiple client environments simultaneously — while maintaining strict tenant segregation, contractual SLAs, and analyst efficiency.

A formal multi-client alert handling procedure is critical because:

- the MSSP SOC processes alerts from many clients concurrently across shared queues and analyst pools
- inconsistent alert handling leads to SLA breaches, missed incidents, and client dissatisfaction
- multi-tenant alert queues are the primary operational risk surface for tenant segregation violations
- NIST CSF Detect (DE.AE, DE.CM) requires structured alert correlation and continuous monitoring
- ISO 27001 Annex A.5.24, A.8.16 require structured alert response and monitoring
- RBI Cyber Security Framework and contractual SLAs require client-specific response timelines
- analyst overload and alert fatigue directly cause missed P1/P2 detections
- inconsistent tenant context switching by analysts causes errors and segregation issues
- client-specific severity definitions, escalation rules, and contacts must be applied per alert
- after-hours and 24x7 coverage require structured handoff and assignment
- detection rule alert volume must be balanced against analyst capacity
- alert auto-enrichment and SOAR automation reduce manual handling errors
- shift changes risk dropped alerts without structured handover
- correlation across clients (cross-client trigger) must be enabled while preserving segregation
- audit and SLA compliance reporting require complete alert audit trail
- false positive feedback loop drives detection improvement

This procedure ensures:

- consistent alert reception, queuing, prioritization, and routing across all clients
- enforced tenant context awareness throughout analyst workflow
- adherence to per-client SLAs and severity definitions
- balanced analyst workload across the multi-client portfolio
- structured shift management and handover preventing dropped alerts
- correlation hooks for cross-client incident detection
- audit-ready evidence of alert lifecycle and SLA performance
- linkage to Client Data Segregation Policy, Cross-Client Incident Procedure, and per-client playbooks

Reference alignment:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md`
`03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Alert-Handling-SOP.md`
`04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`

---

# 3. Scope

This procedure covers:

| Scope Element        | Coverage                                                          |
| -------------------- | ----------------------------------------------------------------- |
| Alert sources        | SIEM, EDR, NDR, Email Sec, Cloud, Identity, DLP, etc.             |
| Alert volumes        | All tier (high to low volume)                                     |
| Coverage hours       | 24x7 / business hours / hybrid per client                         |
| Analyst tiers        | L1 (triage), L2 (investigation), L3 (deep)                        |
| Client tiers         | All MSSP service tiers (Monitoring / MDR / Co-Managed / Full SOC) |
| Auto-response alerts | SOAR-automated handling                                           |
| Manual handling      | Analyst-triage required                                           |
| Correlation alerts   | Cross-tenant correlation hooks                                    |
| Shift management     | Handover between shifts/regions                                   |

Out of scope:

- Single-client alert handling within a dedicated team (covered by per-client playbooks)
- Internal MSSP monitoring (covered by MSSP IT operations)
- Detailed L2/L3 investigation procedures (covered by tier-specific SOPs)
- Cross-client incident coordination beyond initial correlation (covered by `Cross-Client-Incident-Procedure.md`)

---

# 4. Definitions

| Term                      | Definition                                                            |
| ------------------------- | --------------------------------------------------------------------- |
| Alert                     | Notification from a security tool indicating potential security event |
| Multi-Tenant Queue        | Shared alert queue containing alerts from multiple clients            |
| Tenant Context            | The specific client an alert belongs to                               |
| Tenant Routing            | Assignment of alerts to analysts based on tenant assignment           |
| Alert Triage              | Initial assessment to classify alert as TP/FP/Info                    |
| Auto-Triage               | SOAR-automated initial classification                                 |
| Manual Triage             | Analyst-performed classification                                      |
| Severity Mapping          | Tool-native severity translated to client-specific severity           |
| SLA Clock                 | Timer measuring time elapsed for SLA compliance                       |
| Acknowledgement           | Analyst formally claiming an alert                                    |
| Time to Acknowledge (TTA) | Elapsed time from alert generation to analyst acknowledgement         |
| Time to Triage (TTT)      | Elapsed time from acknowledgement to triage completion                |
| Alert Suppression         | Temporary muting of alerts (with approval)                            |
| Alert Storm               | Sudden surge of alerts (legitimate or otherwise)                      |
| Shift Handover            | Structured transfer of in-flight alerts at shift change               |

---

# 5. Roles and Responsibilities

| Role                     | Responsibilities                                                   |
| ------------------------ | ------------------------------------------------------------------ |
| **SOC Lead (on-shift)**  | Queue oversight; analyst assignment; escalation; SLA monitoring    |
| **L1 Analyst**           | Initial alert triage; escalation per criteria                      |
| **L2 Analyst**           | Investigation of escalated alerts                                  |
| **L3 Analyst**           | Deep investigation; forensics support                              |
| **IR Team Lead**         | Incident-level coordination                                        |
| **SOC Manager**          | Queue capacity planning; analyst assignment; performance oversight |
| **Detection Engineer**   | Alert rule tuning; FP reduction                                    |
| **Threat Intel Analyst** | Enrichment; correlation indicators                                 |
| **Per-Client SDM**       | Per-client SLA accountability; client communication                |
| **Shift Lead**           | Shift-specific oversight and handover                              |
| **MSSP CISO**            | Strategic oversight; escalation point                              |

---

# 6. Multi-Client Alert Handling Principles (Mandatory)

| Principle                          | Requirement                                                       |
| ---------------------------------- | ----------------------------------------------------------------- |
| **Tenant Context First**           | Every alert clearly tagged with tenant ID before reaching analyst |
| **Per-Client SLA Adherence**       | Each alert handled per its client's SLA                           |
| **Severity-Based Prioritization**  | P1 always precedes P2 precedes P3 precedes P4                     |
| **Analyst Assignment Respected**   | Alerts routed only to assigned analysts                           |
| **No Cross-Tenant Context**        | Analyst handles one tenant at a time per session                  |
| **Auto-Enrichment Before Manual**  | SOAR enrichment runs before analyst triage                        |
| **Structured Triage Output**       | Standard classifications across clients                           |
| **Documented Handover**            | All shift transitions documented                                  |
| **Continuous Tuning**              | False positives drive detection improvement                       |
| **Audit Logging**                  | All alert lifecycle events logged                                 |
| **Auto-Response Where Authorized** | Pre-approved SOAR actions executed automatically                  |

---

# 7. Alert Lifecycle Overview (Mandatory)

```
┌──────────────────────────────────────────────────────────┐
│  1. ALERT GENERATION                                     │
│  Security tool generates alert (per-client tenant)       │
└──────────────────────────────────────────────────────────┘
                          │
                          ▼
┌──────────────────────────────────────────────────────────┐
│  2. ALERT INGESTION & ENRICHMENT                         │
│  SOAR ingests; auto-enrichment; tenant tagging           │
└──────────────────────────────────────────────────────────┘
                          │
                          ▼
┌──────────────────────────────────────────────────────────┐
│  3. AUTO-TRIAGE (SOAR)                                   │
│  Automated classification; auto-response (if authorized) │
└──────────────────────────────────────────────────────────┘
                          │
              ┌───────────┴───────────┐
              ▼                       ▼
         Auto-Resolved          Manual Triage Required
              │                       │
              ▼                       ▼
        Log & Close          ┌──────────────────────┐
                             │  4. QUEUE ROUTING    │
                             │  Tenant-aware routing│
                             └──────────────────────┘
                                       │
                                       ▼
                             ┌──────────────────────┐
                             │  5. L1 TRIAGE        │
                             │  Acknowledge + Triage│
                             └──────────────────────┘
                                       │
                               ┌───────┴───────┐
                               ▼               ▼
                            FP/Info        TP/Suspicious
                               │               │
                               ▼               ▼
                          Close + Tune   ┌─────────────┐
                                         │ 6. ESCALATE │
                                         │ to L2/L3    │
                                         └─────────────┘
                                                │
                                                ▼
                                         Incident Lifecycle
                                         (per client playbook)
```

---

# 8. Stage 1: Alert Generation (Mandatory)

## 8.1 Alert Sources and Tenant Tagging

| Source                     | Tenant Tagging Method                               |
| -------------------------- | --------------------------------------------------- |
| SIEM                       | Per-tenant index/namespace; tenant ID embedded      |
| EDR                        | Per-tenant console/group; endpoint tenant attribute |
| NDR                        | Tenant-tagged sensors                               |
| Email Security             | Tenant-tagged inbound rules                         |
| Cloud Security (CSPM/CWPP) | Per-account/subscription tenant mapping             |
| Identity (UEBA/ITDR)       | Per-IdP-tenant tagging                              |
| DLP                        | Tenant-tagged policies                              |
| Vulnerability Mgmt         | Tenant-scoped scans                                 |
| Threat Intel Platform      | Per-tenant feeds                                    |

## 8.2 Tenant Tagging Validation

Every alert must contain (before reaching analyst):

- Client / Tenant ID
- Source tool
- Detection rule ID
- Tool-native severity
- Timestamp (UTC)
- Affected entity (host/user/IP)
- Raw event data

If tenant tagging missing → **alert quarantined** for SOC Lead review.

References:
`04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Integration-Map.md`
`04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Alert-Handling-Guide.md`

---

# 9. Stage 2: Alert Ingestion & Enrichment (Mandatory)

## 9.1 SOAR Ingestion

| Activity                | Detail                                            |
| ----------------------- | ------------------------------------------------- |
| Centralized ingestion   | All alerts flow into SOAR/SIEM correlation engine |
| Deduplication           | Duplicate alerts within window suppressed         |
| Tenant context attached | Tenant ID + client SLA tier                       |
| Source enrichment       | Tool source + rule ID + native severity           |

## 9.2 Standard Auto-Enrichment (Pre-Triage)

| Enrichment            | Source                                        | Purpose                                     |
| --------------------- | --------------------------------------------- | ------------------------------------------- |
| Asset context         | Client asset register                         | Criticality / owner / business function     |
| User context          | Client IdP                                    | Role / privileges / OOO status              |
| Geo-location          | GeoIP service                                 | Source / destination location               |
| Threat intel          | TI platform (tenant + sanitized cross-tenant) | IoC reputation                              |
| Vulnerability context | Vuln scanner                                  | Known vulnerabilities on affected asset     |
| Historical context    | SIEM                                          | Prior alerts on same entity (tenant-scoped) |
| MITRE ATT&CK mapping  | Rule metadata                                 | Tactic/technique mapping                    |

## 9.3 Severity Translation (Mandatory)

Tool-native severity is translated to client-specific severity:

| Tool Native   | Standard MSSP Severity | Per-Client Override        |
| ------------- | ---------------------- | -------------------------- |
| Critical      | P1                     | Per client severity matrix |
| High          | P2                     | Per client severity matrix |
| Medium        | P3                     | Per client severity matrix |
| Low           | P4                     | Per client severity matrix |
| Informational | Info (logged only)     | Per client severity matrix |

References:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`
`09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/[CLIENT-NAME]/Client-IR-Policy.md`

---

# 10. Stage 3: Auto-Triage and Auto-Response (Mandatory)

## 10.1 Auto-Triage Classification

SOAR auto-classifies alerts when possible:

| Classification                     | Trigger                                     | Action                      |
| ---------------------------------- | ------------------------------------------- | --------------------------- |
| **Auto-FP**                        | Matches known FP pattern (per client)       | Auto-close with audit log   |
| **Auto-Info**                      | Informational only                          | Auto-close with summary log |
| **Auto-Suppressed**                | Within active suppression window (approved) | Suppress with log           |
| **Auto-Enriched / Pending Triage** | Cannot auto-classify                        | Route to analyst queue      |
| **Auto-Escalated**                 | High-confidence TP signature                | Direct escalation to L2     |

## 10.2 Auto-Response (Pre-Authorized Only)

Auto-response actions require per-client pre-authorization:

| Auto-Response                     | Per-Client Authorization Required       |
| --------------------------------- | --------------------------------------- |
| Generic IoC blocking at perimeter | Per client config                       |
| Endpoint isolation (single host)  | Per client containment authority matrix |
| Email auto-quarantine             | Per client config                       |
| Account auto-disable (low-risk)   | Per client config                       |
| Process termination (malware)     | Per client config                       |

References:
`09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/[CLIENT-NAME]/Client-IR-Policy.md` (Section 9 – Containment Authority Matrix)

## 10.3 Auto-Response Audit

All auto-responses logged with:

- Tenant ID
- Alert ID
- Action taken
- Authorization reference (per-client policy)
- Timestamp
- Result (success/failure)

---

# 11. Stage 4: Queue Routing (Mandatory)

## 11.1 Routing Logic

| Routing Attribute  | Logic                                                                  |
| ------------------ | ---------------------------------------------------------------------- |
| **Tenant**         | Route to analysts assigned to that tenant                              |
| **Severity**       | P1 alerts get highest priority queue                                   |
| **Coverage hours** | Route to currently on-shift team in client's time zone (if applicable) |
| **Specialization** | Route specialized alerts (cloud/identity) to specialists               |
| **Workload**       | Distribute across available assigned analysts                          |
| **Skill match**    | Route by analyst skill level (L1/L2/L3)                                |

## 11.2 Queue Structure (Standard)

```
SOC Alert Queues:
├── P1-Critical (highest priority; SLA-driven)
│   ├── Per-tenant sub-queues (if dedicated team)
│   └── Shared queue (if pool/follow-the-sun)
├── P2-High
├── P3-Medium
├── P4-Low
├── Auto-Resolved (logging only)
├── Suppressed (audit only)
└── Quarantine (tenant-tag missing / errors)
```

## 11.3 Tenant Awareness in Queue

| UI Requirement                                       | Standard                                            |
| ---------------------------------------------------- | --------------------------------------------------- |
| Tenant clearly visible in alert summary              | Mandatory (color-coded or tenant name/ID prominent) |
| Tenant logo (where appropriate)                      | Recommended                                         |
| Tenant context switch warning                        | Mandatory if analyst changes tenant context         |
| Cross-tenant alerts visible only to authorized roles | Mandatory                                           |

---

# 12. Stage 5: L1 Triage (Mandatory)

## 12.1 L1 Acknowledgement

| Activity                   | Standard                       |
| -------------------------- | ------------------------------ |
| Acknowledge within SLA TTA | Per-client SLA                 |
| Verify tenant context      | Mandatory before any action    |
| Lock alert (assignment)    | Auto-locked on acknowledgement |
| Begin investigation timer  | Triggers TTT clock             |

## 12.2 L1 Triage Process

| Step | Action                                   | Reference              |
| ---- | ---------------------------------------- | ---------------------- |
| 1    | Verify tenant context                    | Match assigned tenant  |
| 2    | Review auto-enrichment                   | All enrichment fields  |
| 3    | Validate alert legitimacy                | Per-client playbook    |
| 4    | Check for known FP patterns (per client) | Per-client FP register |
| 5    | Apply detection rule context             | Rule documentation     |
| 6    | Classify (TP / FP / Info / Escalate)     | Mandatory              |
| 7    | Document triage notes                    | Mandatory              |
| 8    | Apply classification action              | Per classification     |

References:
`03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Alert-Handling-SOP.md`
`03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-False-Positive-Handling.md`

## 12.3 Standard Triage Output

| Classification             | Action                                        |
| -------------------------- | --------------------------------------------- |
| **True Positive (TP)**     | Escalate to L2 + create incident ticket       |
| **Suspicious / Uncertain** | Escalate to L2 for deeper investigation       |
| **False Positive (FP)**    | Close with FP justification + tuning feedback |
| **Informational**          | Close with summary log                        |
| **Duplicate**              | Close referencing original alert              |
| **Suppress Request**       | Submit suppression request for approval       |

## 12.4 Per-Client Triage Considerations

| Consideration                            | Source                     |
| ---------------------------------------- | -------------------------- |
| Per-client severity overrides            | Client IR Policy           |
| Per-client FP patterns                   | Client environment profile |
| Per-client maintenance windows           | Client environment profile |
| Per-client approved activity (whitelist) | Client environment profile |
| Per-client business hours                | Client environment profile |
| Per-client containment authority         | Client IR policy           |

References:
`09_MSSP-SPECIFIC/09.1_Client-Management/Client-Environment-Profile-Template.md`

---

# 13. Stage 6: Escalation (Mandatory)

## 13.1 Standard Escalation Path

```
L1 Triage
   │
   ▼
L2 Investigation (per-client playbook)
   │
   ▼
L3 Deep Investigation / Forensics (if needed)
   │
   ▼
IR Team Lead (incident-level)
   │
   ▼
SOC Manager (multi-incident / portfolio impact)
   │
   ▼
MSSP CISO + Client CISO (strategic / material)
```

## 13.2 Per-Client Escalation Adherence

Every escalation must follow per-client escalation matrix:

- Per-client escalation contacts used
- Per-client Reach SLAs honored
- Per-client approval authorities respected
- Per-client communication templates used

References:
`09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/[CLIENT-NAME]/Client-Escalation-Matrix.md`

---

# 14. SLA Management (Mandatory)

## 14.1 SLA Clocks

| SLA Metric                    | Definition                                 | Tracked Per             |
| ----------------------------- | ------------------------------------------ | ----------------------- |
| **Time to Acknowledge (TTA)** | Alert generation → analyst acknowledgement | Per-client              |
| **Time to Triage (TTT)**      | Acknowledgement → triage classification    | Per-client              |
| **Time to Escalate (TTE)**    | Triage → escalation to L2 (if escalated)   | Per-client              |
| **Time to Containment (TTC)** | Escalation → containment action            | Per-client per severity |
| **Time to Resolution (TTR)**  | Alert generation → resolution              | Per-client per severity |

## 14.2 SLA at Risk Indicators

| Indicator                                            | Action                                                |
| ---------------------------------------------------- | ----------------------------------------------------- |
| Alert approaching 50% of SLA without acknowledgement | SOC Lead notification                                 |
| Alert approaching 75% of SLA                         | SOC Lead intervention; reassignment                   |
| SLA breached                                         | SDM notification; client communication per breach SOP |
| Recurring SLA breach pattern                         | SOC Manager escalation; capacity review               |

References:
`00_GOVERNANCE/00.4_SLA-and-SLO/SLA-Breach-Escalation-Procedure.md`
`00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`

## 14.3 SLA Reporting

| Report                    | Frequency      | Audience                |
| ------------------------- | -------------- | ----------------------- |
| Daily SLA dashboard       | Daily          | SOC Manager + SOC Lead  |
| Per-client SLA report     | Weekly/Monthly | Per-client SDM + client |
| Portfolio SLA performance | Monthly        | SOC Manager + CISO      |
| SLA breach trend analysis | Quarterly      | CISO + SOC Manager      |

References:
`07_REPORTING/07.3_MSSP-Client-Reports/MSSP-SLA-Compliance-Report.md`

---

# 15. Analyst Workload Management (Mandatory)

## 15.1 Workload Distribution Principles

| Principle                                 | Requirement                          |
| ----------------------------------------- | ------------------------------------ |
| Even distribution across assigned tenants | Per analyst assignment               |
| Severity-weighted load                    | P1 counted heavier than P4           |
| Specialization respected                  | Cloud/identity alerts to specialists |
| Burst capacity reserved                   | 20% capacity for surges              |
| Cross-shift balance                       | Avoid loading one shift              |

## 15.2 Workload Monitoring

| Metric                      | Threshold                 |
| --------------------------- | ------------------------- |
| Active alerts per analyst   | < 10 simultaneous         |
| Average TTT per analyst     | Within SLA                |
| FP rate per analyst         | Within team average ± 20% |
| Escalation rate per analyst | Within team average       |

## 15.3 Overload Response

| Condition                  | Action                                     |
| -------------------------- | ------------------------------------------ |
| Single analyst overloaded  | Reassign by SOC Lead                       |
| Tier overloaded            | Escalate to surge capacity                 |
| Portfolio-wide alert storm | Activate alert storm response (Section 17) |
| Recurring overload         | Capacity planning review by SOC Manager    |

---

# 16. Shift Management and Handover (Mandatory)

## 16.1 Shift Structure (Standard)

| Shift          | Coverage                       |
| -------------- | ------------------------------ |
| Day Shift      | 0800 – 1600 local              |
| Evening Shift  | 1600 – 0000 local              |
| Night Shift    | 0000 – 0800 local              |
| Follow-the-Sun | Multi-region rotating coverage |

## 16.2 Shift Handover Process

| Step | Action                                                     | Owner                       | Timeline             |
| ---- | ---------------------------------------------------------- | --------------------------- | -------------------- |
| 1    | Outgoing shift completes in-progress alerts where possible | Outgoing analysts           | Last 30 min of shift |
| 2    | Outgoing SOC Lead prepares handover briefing               | Outgoing SOC Lead           | Last 15 min          |
| 3    | Handover meeting (10-15 min)                               | Both Shift Leads + analysts | Shift overlap        |
| 4    | Active alerts handed over individually                     | Per analyst                 | Per alert            |
| 5    | Incoming shift acknowledges handover                       | Incoming Shift Lead         | Handover meeting     |
| 6    | Handover log captured                                      | Incoming SOC Lead           | At handover          |

## 16.3 Handover Briefing Contents

| Element                                 | Required |
| --------------------------------------- | -------- |
| Active P1/P2 incidents (per tenant)     | Yes      |
| In-flight alerts requiring continuation | Yes      |
| Pending escalations                     | Yes      |
| Awaiting client response                | Yes      |
| Tool issues / outages                   | Yes      |
| Detection rule changes during shift     | Yes      |
| Known suppressions in effect            | Yes      |
| Cross-client incidents (CCIC reference) | Yes      |
| Special operational notes               | Yes      |

References:
`03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Shift-Handover-Template.md`
`03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Shift-Handover-Template.md`

---

# 17. Alert Storm Response (Mandatory)

## 17.1 Alert Storm Definition

| Trigger                                  | Threshold                       |
| ---------------------------------------- | ------------------------------- |
| Portfolio-wide alert volume              | >2x daily average within 1 hour |
| Single-tenant alert volume               | >5x daily average within 1 hour |
| Single rule alert volume                 | >100 alerts within 1 hour       |
| Multiple severity P1 within short window | ≥3 P1 within 1 hour             |

## 17.2 Alert Storm Response Steps

| Step | Action                                                       | Owner                       |
| ---- | ------------------------------------------------------------ | --------------------------- |
| 1    | Storm detected (auto or manual)                              | SOAR / SOC Lead             |
| 2    | SOC Lead notified                                            | SOC Lead                    |
| 3    | Storm assessed (legitimate threat vs FP storm vs tool issue) | SOC Lead + Detection Eng    |
| 4    | Surge capacity activated (if real threat)                    | SOC Manager                 |
| 5    | Alert suppression (if FP storm; with approval)               | Detection Eng + SOC Manager |
| 6    | Tool team engaged (if tool issue)                            | SOC Lead + IT               |
| 7    | Per-client SDMs notified                                     | SOC Lead                    |
| 8    | Cross-client correlation triggered (if portfolio-wide)       | Threat Intel Lead → CCIC    |
| 9    | Storm response documented                                    | SOC Lead                    |
| 10   | Post-storm RCA                                               | Detection Eng               |

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md`

---

# 18. Alert Suppression (Mandatory)

## 18.1 Suppression Categories

| Category               | Use Case                               |
| ---------------------- | -------------------------------------- |
| **Maintenance Window** | Pre-approved client maintenance        |
| **Known FP**           | Recurring FP pattern under tuning      |
| **Tool Issue**         | Erroneous alerts during tool problem   |
| **Approved Activity**  | Client-approved testing/red team       |
| **Client Request**     | Client-initiated temporary suppression |

## 18.2 Suppression Approval

| Suppression Type        | Approver                              | Max Duration      |
| ----------------------- | ------------------------------------- | ----------------- |
| Maintenance window      | SOC Lead                              | Window duration   |
| Known FP (under tuning) | Detection Eng Lead                    | 7 days            |
| Tool issue              | SOC Manager                           | Issue resolution  |
| Approved activity       | Per-client SDM + SOC Lead             | Activity duration |
| Client request          | Client written approval + SOC Manager | Per request       |
| Indefinite suppression  | CISO + Client                         | Per justification |

## 18.3 Suppression Audit

All suppressions logged with:

- Suppression ID
- Tenant ID
- Suppression rule (rule ID, IoC, entity)
- Justification
- Approver
- Start/end time
- Auto-expiry
- Post-expiry review

---

# 19. False Positive Feedback Loop (Mandatory)

## 19.1 FP Classification

L1 analysts classify FPs with reason:

| FP Reason             | Examples                         |
| --------------------- | -------------------------------- |
| Known benign behavior | Approved internal scanner        |
| Misconfiguration      | Tool generating noise            |
| Rule too broad        | Detection logic needs refinement |
| Asset whitelist gap   | Asset not in whitelist           |
| Maintenance activity  | Untagged maintenance             |
| Approved testing      | Untagged red team                |

## 19.2 FP Feedback to Detection Engineering

| Step | Action                                   | Owner                      |
| ---- | ---------------------------------------- | -------------------------- |
| 1    | Analyst classifies FP with reason        | L1 Analyst                 |
| 2    | FP logged in feedback queue              | SOAR                       |
| 3    | Recurring FP pattern detected            | Detection Eng (auto-alert) |
| 4    | Tuning ticket created                    | Detection Eng              |
| 5    | Tuning evaluated (per-client or generic) | Detection Eng              |
| 6    | Rule update / exclusion (per client)     | Detection Eng              |
| 7    | Tuning logged                            | Detection Improvement Log  |

References:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`
`04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md`

---

# 20. Cross-Client Correlation Hooks (Mandatory)

## 20.1 When to Trigger Cross-Client Correlation

| Trigger                                            | Action                         |
| -------------------------------------------------- | ------------------------------ |
| Same IoC seen in 2nd client within 24 hours        | Auto-flag to Threat Intel Lead |
| Same CVE exploit alert in 2nd client within 7 days | Auto-flag to Threat Intel Lead |
| Same TTP cluster in 2nd client within 30 days      | Manual flag by L3 → CCIC       |
| External advisory matches alerts in MSSP base      | Manual flag by Threat Intel    |

## 20.2 Correlation Handoff

| Step | Action                                                                        |
| ---- | ----------------------------------------------------------------------------- |
| 1    | Correlation flagged to Threat Intel Lead                                      |
| 2    | Threat Intel Lead validates correlation                                       |
| 3    | If confirmed cross-client → trigger Cross-Client Incident Procedure           |
| 4    | Per-client alerts continue tenant-scoped handling                             |
| 5    | Cross-client coordination via CCIC (per `Cross-Client-Incident-Procedure.md`) |

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md`

---

# 21. Tenant Context Switching Safeguards (Mandatory)

When analyst handles multiple tenants in a shift:

| Safeguard                           | Implementation                            |
| ----------------------------------- | ----------------------------------------- |
| **Visual tenant indicator**         | Mandatory at all times in UI              |
| **Tenant context switch warning**   | Confirmation prompt on switch             |
| **No simultaneous tenant sessions** | Single tenant context per session         |
| **Tenant-scoped queries enforced**  | Tool-level enforcement                    |
| **Action confirmation per tenant**  | Confirm tenant before containment actions |
| **Audit log per tenant action**     | All actions tenant-tagged                 |

---

# 22. Auto-Response Authorization (Mandatory)

## 22.1 Per-Client Auto-Response Matrix

Each client must have documented auto-response authorizations:

| Auto-Action                      | Default           | Per-Client Override |
| -------------------------------- | ----------------- | ------------------- |
| Block IoC at perimeter           | Pre-approved      | Per client config   |
| Endpoint isolation (single host) | Per client policy | Per client config   |
| Email quarantine                 | Pre-approved      | Per client config   |
| Account disable (standard user)  | Per client policy | Per client config   |
| Account disable (privileged)     | Manual approval   | Always manual       |
| Process termination              | Per client policy | Per client config   |
| Network segment isolation        | Manual approval   | Always manual       |
| Cloud account suspension         | Manual approval   | Always manual       |

References:
`09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/[CLIENT-NAME]/Client-IR-Policy.md` (Section 9)

## 22.2 Auto-Response Failure Handling

If auto-response fails:

- Failure logged with reason
- Alert auto-escalated to L2
- Per-client SDM notified
- Manual response initiated

---

# 23. Quality Checklist (Daily Operations)

SOC Lead reviews daily:

- [ ] All tenant tagging functioning (no quarantine queue buildup)
- [ ] All tenants within SLA performance
- [ ] No tenant context switching incidents
- [ ] Alert volumes within normal ranges
- [ ] No active alert storms unaddressed
- [ ] All suppressions within approved scope
- [ ] FP feedback queue processed
- [ ] Cross-client correlation flags reviewed
- [ ] Shift handover completed for all transitions
- [ ] Analyst workloads balanced

---

# 24. Monthly Review (Mandatory)

SOC Manager reviews monthly:

| Item                                | Metric              | Target                  |
| ----------------------------------- | ------------------- | ----------------------- |
| Per-client SLA compliance           | % within SLA        | ≥95%                    |
| Average TTA (per severity)          | Minutes             | Within SLA              |
| Average TTT (per severity)          | Minutes             | Within SLA              |
| FP rate                             | % of alerts         | <10% (target)           |
| Tuning iterations                   | Count               | Continuous improvement  |
| Alert storm incidents               | Count + RCA closure | <2 per month / 100% RCA |
| Analyst workload distribution       | Variance            | Even ± 20%              |
| Cross-client correlations triggered | Count               | Monitor trend           |
| Auto-response success rate          | %                   | ≥95%                    |
| Auto-response failures investigated | %                   | 100%                    |

---

# 25. MSSP Considerations (Mandatory)

| Aspect                     | Requirement                                     |
| -------------------------- | ----------------------------------------------- |
| Tenant segregation         | Strictly enforced throughout alert lifecycle    |
| Cross-client visibility    | Only aggregated views to authorized roles       |
| Per-client confidentiality | Alert data scoped to assigned analysts          |
| Per-client SLA tracking    | Independent per tenant                          |
| Per-client configuration   | Severity, FP patterns, auto-response per tenant |
| Audit logging              | All actions tenant-tagged                       |
| Multi-tenant tool config   | Verified per-tenant configuration               |
| Backup segregation         | Tenant-scoped alert and ticket backups          |

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 26. Integration with Other Processes

| Process                         | Integration                                      |
| ------------------------------- | ------------------------------------------------ |
| Client Data Segregation Policy  | Enforced in alert handling                       |
| Cross-Client Incident Procedure | Correlation triggers feed cross-client procedure |
| Per-Client Playbooks            | Applied per tenant during triage/escalation      |
| Detection Engineering           | FP feedback drives tuning                        |
| Threat Intelligence             | Auto-enrichment + correlation                    |
| SOAR Automation                 | Auto-triage and auto-response                    |
| Ticketing                       | Alert-to-ticket lifecycle                        |
| Shift Management                | Handover process                                 |
| SLA Management                  | Per-client SLA tracking                          |
| Client Reporting                | Alert metrics in client reports                  |
| Audit / Compliance              | Audit logs for compliance evidence               |

---

# 27. Related Documents

| Document                              | Path                                                                                            |
| ------------------------------------- | ----------------------------------------------------------------------------------------------- |
| Client Data Segregation Policy        | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`               |
| Cross-Client Incident Procedure       | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md`              |
| Client Environment Profile            | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-Environment-Profile-Template.md`                |
| Client IR Contacts                    | `09_MSSP-SPECIFIC/09.1_Client-Management/Client-IR-Contacts.md`                                 |
| Client IR Policy (per client)         | `09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/[CLIENT-NAME]/Client-IR-Policy.md`         |
| Client Escalation Matrix (per client) | `09_MSSP-SPECIFIC/09.2_Client-Playbook-Customization/[CLIENT-NAME]/Client-Escalation-Matrix.md` |
| L1 Alert Handling SOP                 | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Alert-Handling-SOP.md`                            |
| L1 False Positive Handling            | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-False-Positive-Handling.md`                       |
| L1 Shift Handover Template            | `03_SOC-TIER-PROCEDURES/03.1_L1-Procedures/L1-Shift-Handover-Template.md`                       |
| L2 Investigation SOP                  | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Investigation-SOP.md`                             |
| L2 Shift Handover Template            | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Shift-Handover-Template.md`                       |
| SIEM Alert Tuning Guide               | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md`                                  |
| SIEM Integration Map                  | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Integration-Map.md`                                     |
| EDR Alert Handling Guide              | `04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Alert-Handling-Guide.md`                                  |
| Ticket Lifecycle SOP                  | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Lifecycle-SOP.md`                                |
| Ticket Priority Matrix                | `04_TOOLS-AND-TECHNOLOGY/04.3_Ticketing/Ticket-Priority-Matrix.md`                              |
| Severity Classification Guide         | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`              |
| SLA Breach Escalation Procedure       | `00_GOVERNANCE/00.4_SLA-and-SLO/SLA-Breach-Escalation-Procedure.md`                             |
| SLO Metrics Definition                | `00_GOVERNANCE/00.4_SLA-and-SLO/SLO-Metrics-Definition.md`                                      |
| MSSP-Client SLA Template              | `00_GOVERNANCE/00.4_SLA-and-SLO/MSSP-Client-SLA-Template.md`                                    |
| Detection Improvement Log             | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`                       |
| MSSP SLA Compliance Report            | `07_REPORTING/07.3_MSSP-Client-Reports/MSSP-SLA-Compliance-Report.md`                           |
| Multi-Client Triage MSSP              | `01_INCIDENT-CLASSIFICATION/01.3_Triage-Decision-Trees/Multi-Client-Triage-MSSP.md`             |

---

# 28. Revision History

| Version | Date        | Author                      | Changes         |
| ------- | ----------- | --------------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP SOC Manager / SOC Lead | Initial version |

---

# 29. Approval

Approved by:

| Role             | Name | Signature | Date |
| ---------------- | ---- | --------- | ---- |
| MSSP SOC Lead    |      |           |      |
| MSSP SOC Manager |      |           |      |
| MSSP CISO        |      |           |      |

---

**End of Document**
