# Playbook: Web Application Attack – L2 Investigation

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Web Application Attack (L2 Investigation) |
| Document ID | IR-PB-WEB-003 |
| Version | 1.0 |
| Effective Date | 19-May-2026 |
| Owner | L2 SOC Lead / Application Security Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 web application incident |

---

## 2. Purpose

This document defines the Level 2 (L2) investigation procedures for web application attacks escalated from L1 triage.

L2 investigation objectives:
- confirm attack type and whether exploitation succeeded
- identify the vulnerable component (endpoint, parameter, library, auth flow)
- determine scope: impacted apps, hosts, users, sessions, APIs, and data stores
- identify evidence of persistence (webshells, backdoors, malicious accounts/keys)
- assess data access/exfiltration risk and whether a breach playbook must be activated
- provide containment recommendations with minimum business disruption
- decide escalation to L3 forensics and/or IR Team

L2 must produce investigation output that is:
- technically defensible (audit-ready)
- operationally actionable (clear “do next” steps)
- readable (tables, short sections, clear decisions)

---

## 3. Scope

Applies to suspected or confirmed web attacks including:
- SQL injection (SQLi)
- Cross-Site Scripting (XSS)
- Server-Side Request Forgery (SSRF)
- Remote Code Execution (RCE)
- Local/Remote File Inclusion (LFI/RFI)
- Directory traversal
- Authentication bypass, session abuse, API token abuse
- Webshell deployment and persistence
- API enumeration and abuse
- Misconfiguration-driven exposure through web apps

Includes:
- on-prem web servers
- cloud workloads (VMs, containers, PaaS)
- CDN/WAF protected services
- APIs and API gateways
- MSSP-managed client environments (client approvals may apply)

---

## 4. Preconditions (Inputs from L1)

Before L2 begins, confirm the ticket includes:

| Required Input | Minimum Content |
|---------------|-----------------|
| Target context | App name + environment + domain/IP |
| Attack evidence | WAF events or web logs with time window |
| Disposition | Blocked/Allowed/Challenged + response code trend |
| Attacker summary | Top IPs + geo/ASN + user-agents |
| Severity recommendation | P1–P4 + justification |
| Evidence preserved | Export references (WAF/web/APM) |

Reference:
`02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L1-Triage.md`

---

## 5. L2 Required Outputs (Minimum Deliverables)

L2 must provide the following in the incident ticket:

| Output | Required Detail |
|--------|------------------|
| Confirmed attack classification | SQLi/XSS/SSRF/RCE/LFI/Auth/API abuse/Other |
| Exploitation status | Confirmed / Likely / Not confirmed (with evidence) |
| Impacted scope | Endpoints, hosts, apps, users/sessions, DBs, APIs |
| Root cause hypothesis | Vulnerable component and why it’s exploitable |
| IOC and TTP list | IPs/ASNs, payload patterns, URIs, headers, tools |
| Containment recommendations | Prioritized actions + owners + approvals |
| Escalation decision | L3/IR Team escalation or justification for not escalating |
| Timeline | First seen / peak / first success / containment start |
| Data breach trigger assessment | Yes/No + rationale and next action |

---

## 6. Investigation Workflow Overview

| Phase | Goal | Key Output |
|------|------|------------|
| Phase 1 | Confirm attack type and success likelihood | Exploitation status |
| Phase 2 | Request and log analysis (WAF, web, app, APM) | Attack profile |
| Phase 3 | Scope expansion | Impacted scope tables |
| Phase 4 | Attack-specific deep dives (SQLi/XSS/SSRF/RCE/LFI/Auth) | Root cause hypothesis |
| Phase 5 | Persistence and compromise checks | Webshell/persistence status |
| Phase 6 | Data access and breach assessment | Breach trigger decision |
| Phase 7 | Containment recommendations | Action plan |
| Phase 8 | Escalation / handoff | L3/IR decision |

---

# 7. Phase 1 – Confirm Attack Type and Exploitation Likelihood

## 7.1 Attack Type Confirmation Table

| Attack Type | Typical Evidence | “Success” Indicators to Look For |
|------------|------------------|----------------------------------|
| SQLi | payloads in parameters, UNION/SELECT patterns | unusual response size, DB errors suppressed, 2xx with anomalous content, time-based delay patterns |
| XSS | script payloads in inputs/headers | reflected payload in response, DOM injection evidence (if captured), repeated parameter variations |
| SSRF | URLs to internal IPs/metadata endpoints | outbound requests from server to internal addresses, metadata access attempts |
| RCE | command patterns, template injection, upload abuse | suspicious process execution, new files in web root, outbound C2 from server |
| LFI/RFI | ../ traversal, file= patterns, include= patterns | 200 responses with file content, access to /etc/passwd or config files |
| Auth/API abuse | repeated login/token calls, enumeration | successful token issuance, high-priv endpoint access, 2xx on restricted routes |

## 7.2 Exploitation Confidence Levels (Standard)

| Level | Meaning | Minimum Evidence |
|------|---------|------------------|
| Confirmed | Exploit succeeded or compromise evidence exists | 2xx/3xx with exploit outcome + server/app evidence |
| Likely | Strong indicators but missing direct artifact | allowed traffic + anomaly patterns + correlated impact |
| Not Confirmed | Attempts detected; no success indicators | blocked traffic + stable logs/metrics |

---

# 8. Phase 2 – Log and Telemetry Analysis (Core L2 Work)

## 8.1 Required Data Sources by Layer

| Layer | Primary Data | Why it Matters |
|------|--------------|----------------|
| WAF/CDN | rule hits, request samples, actions | shows payloads and block/allow decisions |
| Load balancer / reverse proxy | request routing, headers, status codes | confirms what reached app |
| Web server logs | URI, method, status, bytes, user-agent | confirms response and access patterns |
| Application logs | auth events, errors, exceptions, business events | confirms app-level impact |
| APM | latency, error rates, CPU, DB time | identifies exploitation impact |
| Database logs | query volume, errors, exports | SQLi/extraction confirmation |
| Cloud audit logs | IAM changes, storage access | exposure/exfil signals |
| EDR (web hosts) | process exec, file changes, network | RCE/webshell confirmation |

## 8.2 Minimum Time Windows to Export

| Severity | Minimum Log Window |
|----------|--------------------|
| P1 | 24 hours before first seen through containment |
| P2 | 12 hours before first seen through containment |
| P3/P4 | 4 hours before first seen through containment |

Record all times in UTC.

---

# 9. Phase 3 – Scope Expansion

Scope expansion is mandatory even if the attack appears “blocked” because:
- attackers rotate endpoints and payloads
- partial bypass may exist
- exploitation may have occurred earlier

## 9.1 Scope Expansion Checklist

| Scope Question | How to Answer |
|----------------|---------------|
| Are other endpoints targeted? | list top URIs across WAF/web logs |
| Are other apps impacted? | search same IP/UA across other app domains |
| Are multiple source IPs involved? | count unique IPs and ASNs |
| Did attacks occur earlier? | extend time window backward and search for patterns |
| Are other environments impacted? | check staging/dev if shared infra exists |
| Are internal services hit (SSRF)? | check egress logs and internal access logs |

## 9.2 Required Scope Tables (Attach to Ticket)

### 9.2A Targeted Endpoints Summary

| Endpoint (URI) | Method | Attempts | Blocked | Allowed | Top Status Codes | Notes |
|----------------|--------|----------|---------|---------|------------------|------|
| | | | | | | |

### 9.2B Attacker Source Summary

| Source IP | Geo | ASN/Provider | Attempts | Allowed | First Seen (UTC) | Last Seen (UTC) |
|----------|-----|--------------|----------|---------|------------------|-----------------|
| | | | | | | |

### 9.2C Impacted Assets Summary

| Asset | Type (WAF/Web/App/DB/Cloud) | Role | Impact Observed | Notes |
|------|------------------------------|------|-----------------|------|
| | | | | |

---

# 10. Phase 4 – Attack-Specific Deep Dive (Choose Applicable Tracks)

L2 must select the relevant investigation track(s).

---

## 10.1 SQLi Track (If SQLi suspected)

### 10.1A Indicators of SQLi Success

| Indicator | What it Suggests |
|----------|-------------------|
| Response size anomalies | data returned from DB |
| Time-based response delay patterns | blind SQLi |
| DB errors suppressed but behavior changes | injected query execution |
| Sudden increase in DB load | heavy query execution |
| Unusual SELECT/export queries | extraction |

### 10.1B SQLi Evidence Sources

| Source | What to Look For |
|--------|------------------|
| WAF | SQLi rule hits + parameters |
| App logs | DB exceptions, query errors, stack traces |
| DB logs | high query volume, unusual queries |
| APM | DB time spikes |

If extraction is suspected, evaluate Data Breach trigger (Section 12).

Reference:
`02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-SQLi-Specific.md`

---

## 10.2 XSS Track (If XSS suspected)

### 10.2A XSS Success Indicators

| Indicator | What it Suggests |
|----------|-------------------|
| reflected payload in HTML response | reflected XSS |
| stored payload appears for multiple users | stored XSS |
| unusual admin actions after viewing page | session theft via XSS |
| CSP violations (if logged) | attempted script execution |

### 10.2B XSS Risk Assessment

| Risk | Why |
|------|-----|
| session cookie theft | user takeover |
| admin takeover | privilege escalation |
| data access via browser | confidentiality breach |

Reference:
`02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-XSS-Specific.md`

---

## 10.3 SSRF Track (If SSRF suspected)

### 10.3A SSRF Targets to Check

| Target | Why |
|--------|-----|
| cloud metadata endpoints | credential theft |
| internal admin panels | lateral movement |
| internal APIs | data access |
| localhost services | bypass controls |

### 10.3B SSRF Evidence Sources

| Source | What to Look For |
|--------|------------------|
| egress logs | outbound calls to internal/private IP ranges |
| app logs | URL fetch logs, webhook calls |
| cloud logs | role credential usage after SSRF |

---

## 10.4 RCE / Webshell Track (If RCE suspected)

### 10.4A RCE Success Indicators

| Indicator | Meaning |
|----------|---------|
| unexpected process execution on web host | command execution |
| new files in web root | webshell drop |
| outbound connections from web server | C2 / exfil |
| new scheduled tasks/cron | persistence |

### 10.4B Immediate Escalation Triggers (RCE)

| Trigger | Escalate To |
|--------|-------------|
| webshell confirmed | L3 + IR Team immediately |
| outbound C2 confirmed | IR Team immediately |
| privileged secrets accessed | IR Team + Legal/Compliance as needed |

Reference:
`02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L3-Forensics.md`

---

## 10.5 LFI/RFI/Traversal Track (If file read suspected)

### 10.5A File Read Success Indicators

| Indicator | Meaning |
|----------|---------|
| 200 responses returning file content | LFI success |
| access to config files | secret exposure risk |
| credentials/keys in returned files | identity compromise risk |

If secrets exposure is suspected, coordinate with IAM/App Owner to rotate secrets.

---

# 11. Phase 5 – Persistence and Compromise Checks

Even if exploitation is blocked, confirm there is no compromise.

## 11.1 Compromise Indicators Checklist (Web Layer)

| Indicator | Evidence Source |
|----------|------------------|
| web root file changes | file integrity / EDR |
| new admin users / privilege changes | IAM/app logs |
| unusual outbound network connections | firewall/proxy/EDR |
| unexpected cron/jobs/tasks | host telemetry |
| modified app binaries/images | CI/CD logs, container registry |
| suspicious access to secrets vault | cloud audit logs |

If any compromise indicator is confirmed → escalate to L3 and begin containment per `PB-WebApp-Containment.md`.

---

# 12. Phase 6 – Data Access and Data Breach Trigger Assessment

L2 must explicitly decide whether to activate the Data Breach playbooks.

## 12.1 Data Breach Trigger Questions (Answer in Ticket)

| Question | Answer (Yes/No/Unknown) | Evidence Reference |
|----------|--------------------------|-------------------|
| Was sensitive data accessible through the attacked endpoint? | | |
| Do logs indicate data was queried/downloaded/exported? | | |
| Do DB logs show large exports or unusual query patterns? | | |
| Do egress logs show large outbound transfers from app/DB? | | |
| Do cloud logs show unusual storage downloads or sharing? | | |

## 12.2 Trigger Decision

| Condition | Action |
|----------|--------|
| Any “Yes” for sensitive data access/exfil indicators | Activate Data Breach playbook and notify Legal/Compliance per severity |
| All “No” with supporting evidence | Continue web app IR only |
| Unknown due to missing logs | Escalate to L3; preserve logs immediately |

Reference:
`02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/`

---

# 13. Phase 7 – Containment Recommendations (L2 Output)

L2 must provide a prioritized containment plan, even if L2 does not execute it.

## 13.1 Containment Recommendation Matrix

| Finding | Recommended Containment | Owner | Approval |
|--------|--------------------------|-------|----------|
| WAF allowed exploit traffic | deploy targeted WAF virtual patch + rate limit | AppSec/Network | SOC Lead |
| Single endpoint targeted | block/limit endpoint | WAF/App | App Owner |
| Auth/API brute/enumeration | WAF rate limit + CAPTCHA + IAM controls | WAF/IAM | SOC Lead |
| SQLi suspected | disable vulnerable route + DB monitoring | App/DBA | App Owner |
| SSRF suspected | restrict egress + disable URL fetch features | Network/App | SOC Lead |
| RCE/webshell suspected | isolate host/pods + preserve evidence | IR/Platform | IR Lead |
| Secrets exposure suspected | rotate secrets/keys + revoke tokens | IAM/App | IAM Lead |

Reference:
`02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-Containment.md`

---

# 14. Phase 8 – Escalation Criteria (L2)

## 14.1 Escalate to L3 if:

| Condition | Reason |
|----------|--------|
| exploitation success suspected but unclear | advanced correlation needed |
| RCE/webshell indicators exist | forensics required |
| SSRF to metadata suspected | credential theft risk |
| missing logs prevent confirmation | forensic reconstruction required |
| persistence indicators found | deeper host analysis required |

## 14.2 Escalate to IR Team if:

| Condition | Reason |
|----------|--------|
| webshell confirmed / attacker foothold | major incident |
| data breach indicators confirmed | legal/regulatory risk |
| critical application outage | business impact |
| multi-app or multi-tenant impact | coordinated response |
| supply-chain compromise indicators | broad containment needed |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/`

---

## 15. Documentation Requirements (Ticket Checklist)

Before handoff/closure, complete:

| Requirement | Status |
|------------|--------|
| Attack type confirmed | ☐ |
| Exploitation status declared with evidence | ☐ |
| Endpoint/URI scope table completed | ☐ |
| Source IP/ASN scope table completed | ☐ |
| Impacted assets list completed | ☐ |
| Data breach trigger assessment completed | ☐ |
| Containment recommendation documented | ☐ |
| Escalation decision documented | ☐ |
| Evidence references attached | ☐ |
| Timeline entries recorded (UTC) | ☐ |

---

## 16. Common L2 Mistakes to Avoid

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| assuming “blocked” means safe | bypass may exist | expand scope + check web/app logs |
| not checking data breach triggers | missed reporting | complete Section 12 always |
| applying broad WAF blocks prematurely | outage | use targeted rules first |
| failing to check for webshell/persistence | attacker remains | complete Phase 5 |
| not exporting logs quickly | evidence loss | export early and store securely |
| ignoring egress traffic | silent exfil | review outbound telemetry |

---

## 17. MSSP Client Handling Notes

For MSSP environments:
- confirm correct client attribution before exporting logs or applying changes
- high-impact actions (disable endpoint/outage) require client approval unless emergency authority exists
- store evidence per-client in segregated location
- do not disclose one client’s IOCs/payloads to another client without anonymization and approval

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

## 18. Related Documents

| Document | Path |
|---------|------|
| Web App Master | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-Master.md` |
| Web App L1 Triage | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L1-Triage.md` |
| Web App L3 Forensics | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L3-Forensics.md` |
| Web App Containment | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-Containment.md` |
| SQLi Specific | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-SQLi-Specific.md` |
| XSS Specific | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-XSS-Specific.md` |
| MITRE Mapping | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-MITRE-Mapping.md` |
| Data Breach Playbooks | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/` |
| Credential Attack Playbooks | `02_PLAYBOOKS/02.7_Credential-Attack/` |
| Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |

---

## 19. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 19-May-2026 | L2 SOC Lead / AppSec Lead | Initial version |

---

## 20. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**