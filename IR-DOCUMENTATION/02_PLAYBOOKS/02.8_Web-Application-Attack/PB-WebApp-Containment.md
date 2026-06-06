# Playbook: Web Application Attack – Containment

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Web Application Attack (Containment) |
| Document ID | IR-PB-WEB-005 |
| Version | 1.0 |
| Effective Date | 19-May-2026 |
| Owner | IR Team Lead / SOC Lead / Application Security Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 web application incident |

---

## 2. Purpose

This document defines the containment procedures for **web application attacks**.

Containment is the set of actions taken to:
- stop active exploitation
- prevent further compromise, data access, or data exfiltration
- preserve evidence for forensics and legal/regulatory needs
- stabilize customer-facing services while minimizing downtime
- reduce attacker capability to pivot from the application into internal systems

Web application containment must be:
- **fast** (to stop exploitation),
- **precise** (to avoid blocking legitimate traffic and causing unnecessary outage),
- **evidence-aware** (avoid destroying logs or artifacts needed to prove impact).

Containment is executed in parallel workstreams across:
- WAF/CDN
- load balancer / reverse proxy
- application configuration
- authentication/identity
- network controls
- cloud controls (if app is cloud hosted)
- database controls (if data access suspected)

---

## 3. Scope

Applies to:
- SQL injection, XSS, SSRF, RCE, LFI/RFI, directory traversal
- authentication bypass and session abuse against web apps
- API abuse (token misuse, rate limit bypass, enumeration)
- webshell deployment and persistence in app environments
- cloud-hosted web apps (PaaS, containers, serverless) and on-prem web servers
- attacks detected via WAF, SIEM, EDR on web servers, application logs, IDS/IPS, or threat intel

Includes:
- enterprise environments
- MSSP-managed client environments (client approvals may be required)

Out of scope:
- pure DDoS (use DDoS playbooks)
- pure phishing without web exploitation (use Phishing playbooks)

---

## 4. Containment Principles

| Principle | What it Means in Web App Incidents |
|-----------|-------------------------------------|
| Stop the exploitation quickly | Apply WAF/CDN blocks and rate limits immediately |
| Preserve evidence | Export logs before deleting artifacts or redeploying |
| Minimize business impact | Prefer targeted rules over full shutdown |
| Assume persistence | Check for webshells, backdoors, malicious cron/jobs |
| Control access paths | Restrict admin endpoints, rotate secrets, invalidate sessions |
| Layer containment | WAF + app config + network + identity controls together |
| Verify effectiveness | Validate that exploitation attempts no longer succeed |

---

## 5. Containment Priority Order (Recommended Sequence)

| Priority | Objective | Typical Actions |
|----------|-----------|-----------------|
| P0 | Stop active exploitation | WAF rule, endpoint block, virtual patching |
| P1 | Prevent attacker access expansion | Disable vulnerable feature, restrict admin panels, block risky methods |
| P2 | Protect data stores | Restrict DB access, revoke exposed DB credentials, enable read-only mode if needed |
| P3 | Prevent exfiltration | Egress blocks, restrict outbound connectivity, tighten IAM |
| P4 | Preserve and export evidence | WAF logs, web logs, app logs, cloud audit logs |
| P5 | Stabilize and monitor | Enhanced monitoring, error-rate checks, health checks |

---

## 6. Preconditions Before Containment (Minimum Requirements)

Containment may begin immediately for active exploitation, but L2/L3 must ensure minimum evidence is preserved as early as possible.

| Requirement | Minimum Standard | Owner |
|-------------|------------------|------|
| Incident declared and severity assigned | P1/P2 decision recorded | SOC Lead |
| Impacted app and environment identified | URL/service, environment (prod/dev), hosting details | L2 / App Owner |
| Minimum evidence preservation started | Export WAF/web/app logs for relevant time window | L2 / L3 |
| Change control path established | Emergency change approval documented | SOC Lead / App Owner |
| Client approval (MSSP, if required) | Approval recorded for high-impact actions | SDM |

Reference:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

---

## 7. Containment Workstreams (Run in Parallel)

| Workstream | Primary Goal | Primary Owner |
|-----------|--------------|---------------|
| WAF/CDN Containment | Block exploit traffic | Network/AppSec |
| Reverse Proxy / LB | Tighten routing and headers | Network |
| Application Config | Disable vulnerable functions | App Owner |
| Identity/Auth | Invalidate sessions, rotate keys | IAM/App Owner |
| Host/Runtime | Isolate compromised servers/pods | IR/Platform |
| Database | Restrict access, rotate credentials | DBA |
| Network Egress | Block suspicious outbound paths | Network |
| Evidence | Preserve defensible evidence | L3/IR |

---

# 8. Phase 1 – Immediate Attack Suppression (WAF/CDN/Edge)

## 8.1 WAF Emergency Actions (Fastest Containment Lever)

| Action | When to Use | Notes |
|--------|-------------|------|
| Block specific URI/endpoint | Exploit targets a known endpoint | Lowest business impact |
| Block request patterns | Known payload strings, parameters | Use signatures carefully |
| Virtual patch rule | Known vulnerability (CVE) exploited | Prefer vendor recommended rule |
| Rate limit endpoint | API brute/enumeration | Set thresholds with monitoring |
| Block HTTP methods | PUT/DELETE/TRACE as applicable | Ensure business doesn’t rely on it |
| Geo/ASN block (temporary) | Attack source concentrated | Requires approval if customer impact |
| Enable bot/challenge mode | Automated exploitation | Use CAPTCHA/challenges when feasible |

### 8.1A Minimum WAF Rule Documentation (Mandatory)
For every WAF change, record:
- rule name/ID
- timestamp (UTC)
- match criteria (URI/parameter/regex)
- expected impact
- approver
- rollback plan

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Rule-Change-Process.md`

---

## 8.2 Reverse Proxy / Load Balancer Containment

| Action | Purpose | Caution |
|--------|---------|--------|
| Restrict admin paths to allow-list IPs | Protect admin panels | Validate admin access needs |
| Add request size limits | Reduce payload attempts | Avoid breaking legitimate uploads |
| Enforce strict header validation | Reduce injection vectors | Test in staging if possible |
| Disable unused routes | Reduce attack surface | Confirm with app owner |
| Increase logging (temporary) | Improve visibility | Ensure log retention capacity |

---

# 9. Phase 2 – Application-Level Containment

## 9.1 “Disable the Vulnerable Feature” Actions

When exploitation targets a feature, disabling it temporarily is often safer than broad blocking.

| Vulnerability Class | Examples | Containment Action |
|---------------------|----------|-------------------|
| SQLi | login/search/filter | disable vulnerable query route; switch to safe query mode |
| XSS | user content rendering | disable affected UI; sanitize output; block risky input |
| SSRF | URL fetch, webhook, image fetch | disable URL fetch; restrict outbound destinations |
| RCE | file upload, template engine | disable upload; disable dangerous parser; block execution |
| LFI/RFI | file include routes | disable include route; restrict file paths |
| Auth bypass | weak endpoint auth | disable endpoint; require additional auth |

### 9.1A Emergency App Hardening Checklist
| Item | Action |
|------|--------|
| Debug endpoints | Disable in production |
| Admin panels | Restrict to allow-list |
| Secrets in config | Rotate if exposure possible |
| Logging | Increase application audit logging temporarily |
| Error messages | Reduce verbose errors to prevent info leakage |

---

## 9.2 Session and Authentication Containment

If attacker may have obtained tokens/sessions:
- invalidate sessions for impacted users
- rotate session signing keys (if applicable)
- rotate API keys used by the application
- revoke OAuth tokens where appropriate
- force password reset for accounts confirmed compromised (via Credential Attack playbook)

| Action | When Required | Owner |
|--------|---------------|------|
| Force logout / session invalidation | auth bypass, token theft, account takeover | IAM/App |
| Rotate JWT signing keys | token forgery suspected | App/IAM |
| Rotate API keys / secrets | key exposure suspected | App/Platform |
| Revoke OAuth consents | suspicious app grants | IAM |
| Increase login controls (MFA/CAPTCHA) | brute force/enumeration | IAM/WAF |

Reference:
`02_PLAYBOOKS/02.7_Credential-Attack/`

---

# 10. Phase 3 – Host / Runtime Containment (Servers, Containers, PaaS)

If compromise is suspected (webshell, unusual processes, outbound C2), treat as potential intrusion.

## 10.1 Isolation Decision Matrix

| Scenario | Containment Action | Notes |
|----------|--------------------|------|
| Webshell confirmed on one host | Isolate host/pod immediately | Preserve disk/memory if required |
| Multiple pods affected | Quarantine namespace/segment | Coordinate with platform team |
| Suspicious outbound traffic | Egress block + isolate runtime | Prevent exfil/C2 |
| High business criticality | Blue/green replacement | Replace compromised nodes safely |

### 10.1A Evidence Preservation Before Rebuild (If Feasible)
- capture process list
- capture network connections
- preserve web root and suspicious files
- export logs (web/app/system)
- snapshot VM/container image where supported

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

# 11. Phase 4 – Database and Data Store Containment

If data access or extraction is suspected:
- restrict DB access to only required application components
- rotate DB credentials used by app
- enable additional DB auditing
- consider temporary read-only mode for impacted tables (business-approved)

## 11.1 DB Containment Actions

| Action | Purpose | Owner |
|--------|---------|------|
| Rotate DB credentials | Kill stolen creds | DBA/App |
| Restrict network path to DB | Reduce exposure | Network/DBA |
| Enable query auditing | Evidence + detection | DBA |
| Block suspicious queries/patterns | Prevent extraction | DBA |
| Snapshot database logs | Preserve evidence | DBA/L3 |

---

# 12. Phase 5 – Egress and Exfiltration Containment

Web app compromises often lead to outbound exfiltration from servers.

## 12.1 Egress Controls (Recommended)

| Control | Purpose |
|---------|---------|
| Block outbound to suspicious destinations | Stop exfil/C2 |
| Restrict outbound to allow-list only (where feasible) | Strong containment |
| Block unusual ports | Reduce exfil paths |
| DNS sinkhole for malicious domains | Disrupt attacker infra |
| Proxy enforcement for servers | Visibility and control |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Block-Request-SOP.md`

---

# 13. Containment Verification (Definition of Effective Containment)

Containment is complete only when exploitation and unauthorized access are stopped and verified.

## 13.1 Verification Checklist

| Area | Verification Check | Expected Result |
|------|---------------------|----------------|
| WAF/CDN | Exploit attempts blocked | WAF logs show blocks; no 2xx success |
| App behavior | Vulnerable endpoint disabled/mitigated | No successful exploit reproduction |
| Host/runtime | No webshell or malicious process running | EDR/telemetry clean or isolated |
| Database | No suspicious exports continuing | DB audit stable |
| Egress | No outbound to attacker infra | firewall/proxy logs clean |
| Identity | Sessions invalidated if required | no attacker session activity |
| Service | App availability acceptable | health checks stable |

---

## 13.2 Enhanced Monitoring Window

| Severity | Monitoring Window | Notes |
|----------|-------------------|------|
| P1 | Minimum 72 hours | include after rollback of emergency rules |
| P2 | Minimum 48 hours | |
| P3 | Minimum 24 hours | |

Monitor:
- WAF rule hits
- error rate and latency
- new endpoints targeted
- authentication anomalies
- outbound traffic anomalies
- file integrity changes in web roots

---

# 14. Communication During Containment

## 14.1 Internal Communication Rules

| Audience | When | Method |
|---------|------|--------|
| SOC Lead | immediately for P1/P2 | bridge call / ticket |
| App Owner | immediately | incident ticket + call |
| Network/Cloud/DBA | as actions required | task assignment |
| Management | P1 and major P2 | management notification templates |
| Legal/Compliance | breach indicators | per SOP |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/`

## 14.2 MSSP Client Communication

| Trigger | Required Action | Owner |
|---------|-----------------|------|
| P1/P2 confirmed web attack | client notification per SLA | SOC Lead/SDM |
| High-impact containment (disable feature/outage) | client approval where contract requires | SDM |
| Containment complete | provide summary + next steps | SOC Lead/SDM |

---

# 15. Common Containment Mistakes to Avoid

| Mistake | Impact | Correct Approach |
|--------|--------|------------------|
| Blocking too broadly (all traffic/regions) | customer outage | targeted WAF rules first |
| Rebuilding servers before exporting logs | evidence loss | export logs/snapshots first |
| Fixing only the symptom (WAF block) | attacker persists | check for webshell/persistence |
| Not rotating keys/tokens | attacker keeps access | rotate secrets and invalidate sessions |
| Not restricting egress | silent exfiltration continues | apply egress controls |
| No rollback plan for emergency rules | operational risk | document rollback plan |

---

# 16. MSSP Client Handling Notes

For MSSP environments:
- confirm tenant/client attribution before applying changes
- use client-approved change process for WAF/firewall/app changes
- maintain strict evidence segregation per client
- document client approvals for high-impact actions
- do not share cross-client indicators unless anonymized and approved

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

# 17. Related Documents

| Document | Path |
|---------|------|
| Web App Master | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-Master.md` |
| Web App L1 Triage | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L1-Triage.md` |
| Web App L2 Investigation | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L2-Investigation.md` |
| Web App L3 Forensics | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L3-Forensics.md` |
| Web App SQLi Specific | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-SQLi-Specific.md` |
| Web App XSS Specific | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-XSS-Specific.md` |
| Web App MITRE Mapping | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-MITRE-Mapping.md` |
| Firewall Block SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Block-Request-SOP.md` |
| Network Capture SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Capture-SOP.md` |
| Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |

---

## 18. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 19-May-2026 | IR Team Lead / SOC Lead / AppSec Lead | Initial version |

---

## 19. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**