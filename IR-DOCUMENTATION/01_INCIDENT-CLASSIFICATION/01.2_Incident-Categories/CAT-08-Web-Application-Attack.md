# CAT-08 – Web Application Attack Incident Category

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Incident Category – Web Application Attack |
| Document ID | IR-CAT-008 |
| Version | 1.0 |
| Effective Date | 15-May-2026 |
| Owner | SOC Manager |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly |

---

## 2. Category Overview

| Field | Details |
|-------|---------|
| Category ID | CAT-08 |
| Default Severity | P2 – High (exploit success or unauthorized access) / P3 – Medium (suspicious probing) / P4 – Low (blocked scans) |
| Escalation Priority | High for production systems, public-facing services, or sensitive data exposure |
| Attack Goal | Unauthorized access, data theft, account takeover, service disruption, code execution |
| Threat Actors | Cybercriminals, APT groups, scanners/bots, hacktivists |
| Playbook Reference | `02_PLAYBOOKS/02.8_Web-Application-Attack/` |

---

## 3. What is a Web Application Attack?

A web application attack is any malicious attempt to exploit weaknesses
in a web application, API, or supporting infrastructure (web server,
application server, database, authentication, session management) to:

- Access restricted data or functions
- Bypass authentication or authorization
- Execute commands on the server (remote code execution)
- Modify application logic or stored data
- Perform account takeover
- Conduct denial of service against the application

Web applications are frequently targeted because they are exposed to the
internet and often contain direct paths to sensitive data.

---

## 4. Common Web Application Attack Types

| Attack Type | Description |
|------------|-------------|
| SQL Injection (SQLi) | Injecting SQL to access or modify database data |
| Cross-Site Scripting (XSS) | Injecting scripts into pages viewed by other users |
| Remote Code Execution (RCE) | Executing attacker-controlled commands on server |
| Authentication Bypass | Bypassing login mechanisms or weak authentication |
| Authorization Bypass (IDOR) | Accessing resources without proper permissions |
| File Upload Exploit | Uploading malicious files leading to execution |
| Path Traversal | Accessing files outside intended directories |
| Server-Side Request Forgery (SSRF) | Forcing server to request internal resources |
| Command Injection | Injecting OS commands through user input |
| Deserialization Exploit | Exploiting insecure object deserialization |
| CSRF | Forcing authenticated users to perform actions |
| API Abuse | Excessive requests, endpoint exploitation, token misuse |
| Web Shell Deployment | Dropping a persistent shell for remote control |
| WAF Evasion | Obfuscation and encoding to bypass detection controls |

---

## 5. Attack Vectors and Entry Points

| Entry Point | Examples |
|------------|----------|
| Web Forms | Login forms, search, feedback forms |
| APIs | REST APIs, GraphQL endpoints, mobile APIs |
| File Upload | Profile image upload, document upload |
| Session Handling | Cookies, tokens, JWT, session IDs |
| Authentication | SSO endpoints, password reset flows |
| Admin Interfaces | Exposed admin panels, debug endpoints |
| Third-Party Components | CMS plugins, libraries, outdated frameworks |

---

## 6. Indicators of Web Application Attack (IoCs and Observables)

### 6.1 Application and HTTP Indicators

| Indicator | Examples |
|----------|----------|
| Suspicious Parameters | `' OR 1=1--`, `../..`, `${jndi:ldap://...}` |
| High Error Rate | Increased 500 errors, SQL errors, stack traces |
| Unusual HTTP Methods | PUT/DELETE/TRACE used unexpectedly |
| High Request Rate | Spikes in requests to sensitive endpoints |
| User-Agent Anomalies | Scanner user agents, empty user agents, uncommon clients |
| Repeated Login Attempts | Brute force patterns, credential stuffing |
| New Admin Sessions | Admin login from unusual IP, device, or geo |
| Large Responses | Unexpectedly large response sizes (possible data dump) |

### 6.2 WAF and Perimeter Indicators

| Indicator | Examples |
|----------|----------|
| WAF Blocks | SQLi/XSS signatures repeatedly triggered |
| Rate Limits | Triggered throttling events on login or API routes |
| IP Reputation Hits | Known scanner or botnet IPs targeting endpoints |
| Geo Patterns | Concentrated attack traffic from specific regions |

### 6.3 Backend and Database Indicators

| Indicator | Examples |
|----------|----------|
| Unusual DB Queries | Bulk selects, union selects, export operations |
| New DB Accounts | Unauthorized database user creation |
| Privileged DB Use | Non-DBA accounts running admin queries |
| OS Command Patterns | Shell execution or suspicious system calls |

### 6.4 Key Log Sources

| Source | What to Look For |
|--------|------------------|
| Web Server Logs | Requests, URIs, methods, status codes, response size |
| Application Logs | Authentication errors, stack traces, exception logs |
| WAF Logs | Blocks, rule triggers, bypass attempts |
| API Gateway Logs | Endpoint activity, token usage, throttling events |
| Database Audit Logs | Unusual queries, exports, privilege changes |
| EDR (server) | Suspicious processes, web shells, file changes |
| SIEM | Correlation across WAF, web logs, IAM, and DB logs |

---

## 7. Severity Classification

| Scenario | Severity |
|----------|----------|
| Confirmed RCE or web shell on production server | P1 – Critical |
| Confirmed sensitive data exfiltration via web app | P1 – Critical |
| Confirmed authentication bypass and privileged access | P1 – Critical |
| Confirmed SQL injection with data access | P2 – High |
| Confirmed unauthorized access to restricted functions | P2 – High |
| Confirmed account takeover via web app | P2 – High |
| Repeated suspicious exploit attempts with partial success indicators | P2 – High |
| Suspicious probing/scanning targeting specific endpoints | P3 – Medium |
| Automated scan blocked by WAF with no impact | P4 – Low |

---

## 8. Immediate Response Actions

### 8.1 First 15 Minutes

- Create incident ticket and assign initial severity
- Notify SOC Lead immediately for P2 and above
- Identify affected application, environment (prod/non-prod), and endpoints
- Preserve web logs, WAF logs, and application logs for relevant time window
- Identify attacker source IPs, user agents, and request patterns
- If exploit success suspected, initiate containment approval:
  - block source IPs at WAF/edge
  - enable stricter WAF rules for affected paths
  - temporarily disable vulnerable endpoint if necessary (business approval)

### 8.2 First 1 Hour

- Determine whether exploit succeeded:
  - evidence of unauthorized access
  - database errors indicating injection
  - suspicious file uploads
  - web shell indicators
  - unusual admin sessions
- Identify scope: affected users, accounts, data repositories, servers
- Check server EDR telemetry for suspicious processes or file writes
- Check database audit logs for unusual queries and exports
- Coordinate with application owner and development team
- Escalate to P1 if RCE, web shell, or confirmed data exfiltration is detected

### 8.3 First 4 Hours

- Apply containment:
  - WAF rules, rate-limiting, geo restrictions as needed
  - block IoCs (IPs/domains/hashes)
  - isolate compromised server if confirmed
- Capture forensic artifacts:
  - application code changes, file system modifications, suspicious binaries
- Begin eradication planning:
  - patch vulnerability, disable vulnerable feature
  - rotate secrets and API keys if exposure suspected
- Prepare management status update for P2/P1
- Assess regulatory reporting if sensitive data exposure confirmed

---

## 9. Containment and Eradication Guidance

| Action | Purpose | Notes |
|-------|---------|------|
| WAF Rule Tightening | Stop exploit traffic | Prefer narrow scope to reduce false blocks |
| Rate Limiting / Throttling | Reduce brute force and floods | Apply to login and API endpoints |
| Temporary Feature Disablement | Reduce exposure | Requires business owner approval |
| Patch / Hotfix | Remove vulnerability | Coordinate with change management |
| Secret Rotation | Reduce persistence | Rotate API keys, DB creds, tokens |
| Web Shell Removal | Remove persistence | Preserve evidence before removal |
| Server Isolation | Prevent lateral movement | Use EDR containment if possible |

---

## 10. MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|--------|-----------|----|
| Initial Access | Exploit Public-Facing Application | T1190 |
| Initial Access | External Remote Services | T1133 |
| Execution | Command and Scripting Interpreter | T1059 |
| Execution | Exploitation for Client Execution | T1203 |
| Persistence | Web Shell | T1505.003 |
| Persistence | Server Software Component | T1505 |
| Privilege Escalation | Exploitation for Privilege Escalation | T1068 |
| Defense Evasion | Obfuscated Files or Information | T1027 |
| Credential Access | Credentials from Password Stores | T1555 |
| Discovery | System Information Discovery | T1082 |
| Collection | Data from Information Repositories | T1213 |
| Exfiltration | Exfiltration Over Web Service | T1567 |
| Impact | Endpoint Denial of Service | T1499 |

---

## 11. Key Investigation Questions

1. Which application, domain, and endpoint is targeted?
2. Is the environment production, staging, or development?
3. What is the attack pattern (SQLi, XSS, RCE, IDOR, file upload, SSRF)?
4. Was the exploit successful (evidence of unauthorized access or execution)?
5. Which accounts were impacted (admin, user, service accounts)?
6. What data may have been accessed or extracted?
7. Are there signs of web shell or file upload persistence?
8. Did the attacker obtain secrets (API keys, tokens, DB credentials)?
9. Were any application or server files modified?
10. Do logs indicate lateral movement beyond the web server?
11. What containment actions have been applied (WAF blocks, rate limits)?
12. What patch or configuration change is required to remediate?
13. Does this incident require customer/client notification or regulatory reporting?

---

## 12. Critical Do's and Do Not's

### Do

- Preserve logs before applying changes where possible
- Confirm exploit success using multiple evidence sources (WAF, web logs, EDR, DB logs)
- Coordinate with application owner for safe containment decisions
- Apply targeted WAF blocks and rate limits to minimize collateral
- Validate server integrity for web shell and unauthorized file changes
- Rotate credentials and secrets if exposure suspected
- Document all actions and approvals

### Do Not

- Disable entire application without business owner approval (unless emergency)
- Apply broad geo-blocks or blocks that may impact customers without review
- Clean up web shell or malicious files before preserving evidence
- Assume WAF blocks mean no compromise (verify backend logs)
- Close incident without confirming no persistence remains

---

## 13. Escalation Path

| Stage | Action |
|-------|--------|
| L1 Triage | Identify suspicious web alerts and create ticket |
| L2 Investigation | Validate attack, scope, and evidence of success |
| SOC Lead | Approve severity changes and coordinate communications |
| Application Owner / DevOps | Apply patches, configuration changes, and deployment decisions |
| L3 / IR Team | Engage for RCE, web shell, data breach, or P1 incidents |
| GRC / Compliance | Engage for breach notification assessment |
| Management / CISO | Engage for P1 incidents and major service/data impact |

---

## 14. Regulatory and Client Reporting Considerations

| Trigger | Action |
|--------|--------|
| Confirmed data exposure of sensitive/regulatory data | Engage Compliance and Legal immediately |
| Customer-impacting breach via public application | Assess notification obligations and timelines |
| MSSP client application impacted | Notify client per SLA and contract |
| Critical service outage due to attack | Treat as major incident and assess reporting |

Reference: `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

## 15. Evidence Collection Requirements

| Evidence Type | Priority | Notes |
|--------------|----------|-------|
| WAF logs | Critical | Block events, rule triggers, bypass attempts |
| Web server access logs | Critical | Request patterns, endpoints, response size |
| Application logs | Critical | Errors, auth events, exceptions |
| API gateway logs | High | Token usage, endpoint activity |
| Database audit logs | High | Unusual queries, exports, privilege use |
| Server EDR telemetry | High | Processes, file writes, web shell detection |
| File integrity data | High | Modified files, new files in web roots |
| Configuration snapshots | Medium | WAF policy, app configs before/after changes |
| Change records | Critical | Patching and mitigation approvals |
| Chain-of-custody forms | As needed | If forensic evidence is collected |

Reference: `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 16. Related Documents

| Document | Path |
|---------|------|
| Web App Master Playbook | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-Master.md` |
| L1 Triage Playbook | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L1-Triage.md` |
| L2 Investigation Playbook | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L2-Investigation.md` |
| L3 Forensics Playbook | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L3-Forensics.md` |
| SQLi Specific | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-SQLi-Specific.md` |
| XSS Specific | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-XSS-Specific.md` |
| Containment Playbook | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-Containment.md` |
| MITRE Mapping | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-MITRE-Mapping.md` |
| P1 Critical Definition | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P1-Critical-Definition.md` |
| P2 High Definition | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P2-High-Definition.md` |
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |

---

## 17. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | SOC Manager | Initial version |

---

## 18. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**