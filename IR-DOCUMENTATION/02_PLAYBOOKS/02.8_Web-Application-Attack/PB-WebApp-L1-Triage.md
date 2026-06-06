# Playbook: Web Application Attack – L1 Triage

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Web Application Attack (L1 Triage) |
| Document ID | IR-PB-WEB-002 |
| Version | 1.0 |
| Effective Date | 19-May-2026 |
| Owner | SOC Lead / SOC Manager |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 web application incident |

---

## 2. Purpose

This document defines the Level 1 (L1) SOC Analyst procedures for triaging **web application attack** alerts and reports.

L1 triage objectives:
- validate whether the alert indicates a real web attack vs noise/false positive
- identify the targeted application, endpoint, and environment (prod/stage/dev)
- determine if exploitation may be successful (blocked vs allowed)
- assess immediate business impact (outage, defacement, data exposure risk)
- preserve critical evidence (WAF logs, web logs, request samples)
- assign severity recommendation (P1–P4) and escalate to L2/SOC Lead appropriately
- initiate immediate containment recommendations (via SOC Lead/AppSec/Network)

L1 must prioritize **speed + evidence preservation**. Deeper confirmation and scoping is performed by L2/L3.

---

## 3. Scope

Applies to alerts/reports from:
- WAF / WAAP platforms
- CDN security (bot/challenge events)
- load balancer / reverse proxy telemetry
- web server logs (NGINX/Apache/IIS)
- API gateway logs
- SIEM correlation rules for web exploit patterns
- IDS/IPS alerts for web exploitation attempts
- APM (error rate spikes, latency anomalies)
- bug bounty / external security researcher reports (via approved process)
- MSSP client web applications (client approvals apply)

Attack classes include (non-exhaustive):
- SQL injection (SQLi)
- Cross-Site Scripting (XSS)
- Server-Side Request Forgery (SSRF)
- Remote Code Execution (RCE)
- Local/Remote File Inclusion (LFI/RFI)
- Directory traversal
- Authentication bypass / brute-force against login/API
- API abuse and enumeration
- Webshell deployment indicators

---

## 4. L1 Safety Rules (Web Application Incidents)

| Rule | Why it Matters |
|------|----------------|
| Do NOT “test” payloads against production systems | May worsen impact / cause legal exposure |
| Do NOT click attacker URLs from corporate endpoints | Infection / credential theft risk |
| Do NOT alter WAF rules directly unless authorized | Risk of outage/overblocking |
| Do NOT restart web servers to “fix” performance | Evidence loss |
| Preserve logs before any remediation or redeploy | Logs may rotate quickly |
| Use UTC timestamps for all evidence | Timeline integrity |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 5. L1 SLA Targets (Web Application Attacks)

| Severity (likely) | L1 Triage Target | Escalation Target |
|-------------------|------------------|-------------------|
| P1 | 5 minutes | SOC Lead immediately + L2 immediately |
| P2 | 10 minutes | SOC Lead immediately; L2 within 15 minutes |
| P3 | 20 minutes | L2 within 30 minutes if required |
| P4 | 30 minutes | close/monitor per SOP |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

## 6. Inputs to Collect at L1 (Minimum Required)

### 6.1 Application and Target Context (Mandatory)

| Data Point | Required Detail |
|-----------|------------------|
| Application name | Business service name |
| Environment | Prod / DR / Stage / Dev |
| Target | Domain, IP, VIP, API gateway |
| Endpoint | URI path + method (GET/POST/etc.) |
| Owner | App owner/on-call group (if known) |

### 6.2 Alert Context (Mandatory)

| Data Point | Required Detail |
|-----------|------------------|
| Alert source | WAF/CDN/SIEM/IDS/APM |
| Detection time | UTC timestamp |
| Attack classification | SQLi/XSS/SSRF/RCE/etc. |
| WAF disposition | Blocked / Allowed / Challenged |
| Response status codes | 2xx/3xx/4xx/5xx distribution |
| Volume | event count + time window |

### 6.3 Attacker Context (Mandatory)

| Data Point | Required Detail |
|-----------|------------------|
| Source IP(s) | Top IPs and counts |
| Geo / ASN | Country + provider |
| User-Agent | Top UA strings |
| Referrer | If present |
| Headers | Suspicious headers (X-Forwarded-For anomalies, etc.) |

### 6.4 Business Impact Signals (Mandatory)

| Signal | What to Capture |
|--------|------------------|
| Availability | Service up/down? |
| Performance | latency spike? error rate? |
| Customer impact | user complaints/tickets? |
| Data risk | any signs of unauthorized data access? |

---

## 7. L1 Triage Decision Flow (Fast)

Use this sequence to avoid missing critical incidents.

| Step | Question | If YES | If NO |
|------|----------|--------|-------|
| 1 | Is the application **down** or severely degraded? | P1 → SOC Lead + App Owner immediately | Step 2 |
| 2 | Did the WAF/CDN **allow** exploit traffic (not blocked)? | P1/P2 → escalate to L2 immediately | Step 3 |
| 3 | Do logs show **2xx/3xx** responses for suspicious payloads? | Likely successful exploitation → escalate | Step 4 |
| 4 | Is the target a **critical app** or sensitive dataset? | Raise severity + escalate | Step 5 |
| 5 | Is this likely scanning/noise only (blocked, no impact)? | P3/P4 + monitor | Escalate if unsure |

---

## 8. Step-by-Step L1 Triage Procedure

### Step 1: Validate Alert Type and Source

Classify the alert/report as one of:

| Type | Example Sources |
|------|-----------------|
| WAF exploit detection | SQLi/XSS rule triggers |
| API abuse / auth attack | API gateway + SIEM |
| Web server anomaly | unusual 500 errors + spikes |
| IDS/IPS web exploit | signature hits |
| External report | bug bounty / customer report |

If unclear, treat as suspected web app attack and escalate to L2 for confirmation.

---

### Step 2: Preserve Evidence Immediately (Mandatory)

Preserve evidence before any containment changes occur.

#### 8.2A Minimum Evidence Set (Always)

| Evidence Item | Where to Collect | Notes |
|--------------|------------------|------|
| WAF event export | WAF console / SIEM | include request sample if allowed |
| Top attacker IPs | WAF/SIEM | counts + timestamps |
| Target endpoint list | WAF/web logs | URI + method |
| Response codes trend | WAF/LB/APM | 2xx vs 5xx |
| Web server logs (time window) | NGINX/Apache/IIS | preserve raw logs if possible |

#### 8.2B Request Sample Handling Rules

| Rule | Reason |
|------|--------|
| Store request samples in secured evidence storage | May contain sensitive data |
| Do not paste full payload into open chat channels | Data leakage risk |
| Mask tokens/cookies when sharing | Credential risk |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

### Step 3: Determine “Blocked vs Allowed vs Successful”

This is the most important L1 determination.

| Scenario | Evidence | Interpretation |
|----------|----------|----------------|
| Blocked by WAF | WAF action=blocked, no 2xx responses | Attack attempted; may be low impact |
| Allowed by WAF | WAF action=allow or bypass | High risk; potential exploitation |
| Challenge passed | CDN/WAF challenge passed | Actor may be real attacker; investigate |
| Suspicious payload + 2xx/3xx | web logs show success codes | Possible exploit success |
| 5xx spike after payload | APM/web logs show failures | Potential exploitation or DoS-like effect |

Output requirement:
- record the disposition and supporting evidence in the ticket.

---

### Step 4: Quick Impact Assessment (Availability + Data Risk)

#### 8.4A Availability Checks

| Check | How | Output |
|------|-----|--------|
| Is site reachable? | monitoring or browser check (safe internal) | Up/Down |
| Error rate spike? | APM/load balancer/WAF | % errors |
| Latency spike? | APM | baseline vs current |

#### 8.4B Data Risk Checks (L1 Level)

| Signal | What it Suggests |
|--------|-------------------|
| Unusual large responses | data leakage |
| Repeated requests to export endpoints | extraction attempt |
| Many 200 responses on suspicious payloads | likely exploit success |
| Admin endpoints targeted | privilege escalation attempt |

If data risk indicators appear, escalate to L2 immediately.

---

### Step 5: Severity Recommendation (P1–P4)

Use the following mapping for L1 recommendations:

| Condition | Severity Recommendation |
|----------|--------------------------|
| customer-facing outage or severe degradation | P1 |
| exploit traffic allowed + suspicious success indicators | P1 |
| confirmed suspicious 2xx/3xx on exploit payload | P1/P2 (SOC Lead decides) |
| attack blocked but against critical app; sustained attempts | P2 |
| attack blocked; no impact; scanning/noise | P3 |
| clear false positive / benign scanner | P4 |

Reference:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

---

### Step 6: Ticket Creation/Update (Mandatory Fields)

Ticket must include:

| Field | Required |
|------|----------|
| Incident category | CAT-08 Web Application Attack |
| App name + environment | Yes |
| Target endpoint(s) | Yes |
| Attack type | Yes |
| WAF disposition | Yes |
| Evidence references | Yes |
| Severity recommendation + justification | Yes |
| Escalations made + timestamps | Yes |
| Containment recommendation | Yes |

---

### Step 7: Escalate Appropriately

Escalation rules:

| Trigger | Escalate To | Timing |
|--------|-------------|--------|
| P1 or exploit allowed | SOC Lead + L2 | Immediately |
| Evidence of data exposure/exfiltration | SOC Lead + IR Team | Immediately |
| Webshell/RCE suspected | L2 → L3/IR | Immediately |
| Attack impacting critical apps | SOC Lead + App Owner | Immediately |
| MSSP client impacted | SOC Lead/SDM | Per SLA |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L1-to-L2-Escalation.md`

---

## 9. L1 Allowed Actions (Without Additional Approval)

L1 may:
- preserve evidence
- extract IOCs (IP, UA, URI, domains)
- submit WAF/firewall block requests via SOP (not implement unless authorized)
- notify SOC Lead and app on-call per escalation path
- initiate request for log retention increase (temporary)

L1 must not:
- deploy WAF rules directly (unless explicitly authorized)
- restart servers, redeploy apps, or change configurations
- run vulnerability scans against production without approval
- disclose details broadly (confidentiality)

---

## 10. Evidence to Capture at L1 (Minimum Set)

Attach or reference in ticket:
- WAF alert export (time window)
- top attacker IPs + geo/ASN
- target endpoints list
- response code trends
- web server log snippet/exports
- APM screenshot (if outage/degradation)
- any client/user reports (if applicable)

---

## 11. Ticket Notes Template (Copy-Paste)

Title:
- Web App Attack suspected – [App] – [Env] – [Attack Type] – [Severity Recommendation]

Required fields:
- Alert Source:
- Detection Time (UTC):
- Application / Environment:
- Target (Domain/IP/VIP):
- Target Endpoint(s) (URI + method):
- Attack Type (SQLi/XSS/SSRF/RCE/LFI/Auth Abuse/Other):
- WAF/CDN Disposition (Blocked/Allowed/Challenged):
- Response Code Trend (2xx/3xx/4xx/5xx):
- Attacker IPs (Top 5) + Geo/ASN:
- User-Agent Summary:
- Evidence Captured (WAF export, web logs, APM, SIEM refs):
- Business Impact (Outage/Degradation/None):
- Data Risk Indicators (Yes/No/Unknown):
- Recommended Severity + Justification:
- Escalations Made (SOC Lead/L2/App Owner/SDM) + timestamps:
- Containment Recommended (WAF rule, rate limit, disable endpoint, etc.):

---

## 12. Common L1 Mistakes to Avoid

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Closing as blocked without checking response codes | missed successful bypass | verify 2xx/3xx outcomes |
| Capturing no request samples | weak investigation | preserve at least WAF event details |
| Testing payloads on production | service impact | use sandbox/staging only |
| Not escalating “allowed” attacks | missed exploitation | escalate immediately |
| Not recording environment (prod vs dev) | wrong impact assessment | always record environment |
| Sharing payloads/tokens in open channels | data leak | sanitize and restrict sharing |

---

## 13. MSSP Notes (Client Handling)

For MSSP operations:
- confirm tenant/client attribution before evidence capture
- store evidence in client-approved evidence location only
- follow client-specific notification and approval process
- do not apply high-impact WAF/app changes without client authorization (unless emergency authority exists)

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

## 14. Related Documents

| Document | Path |
|---------|------|
| Web App Master | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-Master.md` |
| Web App L2 Investigation | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L2-Investigation.md` |
| Web App L3 Forensics | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L3-Forensics.md` |
| Web App Containment | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-Containment.md` |
| SQLi Specific | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-SQLi-Specific.md` |
| XSS Specific | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-XSS-Specific.md` |
| MITRE Mapping | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-MITRE-Mapping.md` |
| Network Capture SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Capture-SOP.md` |
| Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |

---

## 15. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 19-May-2026 | SOC Lead / SOC Manager | Initial version |

---

## 16. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**