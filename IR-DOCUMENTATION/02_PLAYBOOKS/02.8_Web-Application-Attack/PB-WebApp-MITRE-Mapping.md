# Playbook: Web Application Attack – MITRE ATT&CK Mapping

---

## 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | Playbook – Web Application Attack (MITRE ATT&CK Mapping)     |
| Document ID    | IR-PB-WEB-006                                                |
| Version        | 1.0                                                          |
| Effective Date | 19-May-2026                                                  |
| Owner          | L3 Lead / IR Team Lead / Application Security Lead           |
| Approved By    | CISO                                                         |
| Classification | Internal – Confidential                                      |
| Review Cycle   | Quarterly and after any P1/P2 web application incident       |

---

## 2. Purpose

This document provides the **MITRE ATT&CK framework mapping** for web application attacks.

This mapping serves to:

- Align detected techniques to the MITRE ATT&CK Enterprise framework
- Support threat intelligence enrichment during investigations
- Guide detection engineering and SIEM/EDR rule development
- Support L2/L3 scoping by identifying likely next-stage techniques
- Provide audit-ready documentation for ISO 27001, NIST CSF, and RBI compliance
- Enable structured threat hunting across observed TTPs
- Support post-incident reporting at technical and executive levels

---

## 3. Scope

Applies to all web application attack categories:

- SQL Injection (SQLi)
- Cross-Site Scripting (XSS)
- Server-Side Request Forgery (SSRF)
- Remote Code Execution (RCE)
- Local/Remote File Inclusion (LFI/RFI)
- Directory Traversal
- Authentication Bypass and Session Abuse
- API Abuse and Enumeration
- Webshell Deployment and Persistence
- Cloud Credential Theft via Web App
- Lateral Movement from Compromised Web Tier

---

## 4. MITRE ATT&CK Framework Reference

| Field              | Value                                    |
| ------------------ | ---------------------------------------- |
| Framework          | MITRE ATT&CK Enterprise                  |
| Version Referenced | v14 (verify current at attack.mitre.org) |
| Scope              | Enterprise (on-prem, cloud, containers)  |

---

## 5. Web Application Attack – Full TTP Matrix

### 5.1 Initial Access

| Technique ID | Technique Name                    | Sub-Technique                  | Attack Class              | Description                                                       |
| ------------ | --------------------------------- | ------------------------------ | ------------------------- | ----------------------------------------------------------------- |
| T1190        | Exploit Public-Facing Application | —                              | SQLi/XSS/SSRF/RCE/LFI     | Adversary exploits vulnerability in internet-facing web app/API   |
| T1190        | Exploit Public-Facing Application | —                              | Auth Bypass               | Exploiting weak authentication logic on public endpoints          |
| T1133        | External Remote Services          | —                              | Admin Panel Abuse         | Access to exposed admin consoles or management interfaces         |
| T1078        | Valid Accounts                    | T1078.001/T1078.003            | Auth Bypass/Session Abuse | Use of stolen, default, or weak credentials                       |

---

### 5.2 Execution

| Technique ID | Technique Name                | Sub-Technique         | Attack Class   | Description                                          |
| ------------ | ----------------------------- | --------------------- | -------------- | ---------------------------------------------------- |
| T1059        | Command and Scripting Interp. | T1059.004/T1059.003   | RCE/Webshell   | Attacker executes OS commands via RCE or webshell    |
| T1059        | Command and Scripting Interp. | T1059.006/T1059.007   | RCE/Webshell   | Script-based execution via server-side languages     |
| T1203        | Exploitation for Client Exec. | —                     | XSS            | XSS payload executes in victim browser context       |
| T1569        | System Services               | T1569.002             | Post-RCE       | Malicious service created post-exploitation          |

---

### 5.3 Persistence

| Technique ID | Technique Name            | Sub-Technique    | Attack Class         | Description                                          |
| ------------ | ------------------------- | ---------------- | -------------------- | ---------------------------------------------------- |
| T1505        | Server Software Component | T1505.003        | Webshell Deployment  | Attacker uploads webshell in web root                |
| T1136        | Create Account            | T1136.001/.002   | Post-RCE             | New privileged accounts created                      |
| T1078        | Valid Accounts            | T1078.003        | Credential Reuse     | Reuses stolen credentials for persistent access      |
| T1053        | Scheduled Task/Job        | T1053.003/.005   | Post-RCE             | Cron/task created for backdoor persistence           |

---

### 5.4 Defense Evasion

| Technique ID | Technique Name              | Sub-Technique | Attack Class        | Description                                      |
| ------------ | --------------------------- | ------------- | ------------------- | ------------------------------------------------ |
| T1027        | Obfuscated Files/Info       | T1027.010     | SQLi/XSS/RCE        | Payload obfuscation to evade WAF signatures     |
| T1036        | Masquerading                | T1036.005     | Webshell            | Webshell named to resemble legitimate files      |
| T1070        | Indicator Removal           | T1070.003/004 | Post-RCE            | Attacker removes webshell or clears logs         |
| T1562        | Impair Defenses             | T1562.001     | Post-Compromise     | Disable WAF/EDR on compromised host              |
| T1550        | Use Alternate Auth          | T1550.004     | Session Hijacking   | Stolen session cookies bypass credential checks  |

---

### 5.5 Credential Access

| Technique ID | Technique Name             | Sub-Technique    | Attack Class         | Description                                      |
| ------------ | -------------------------- | ---------------- | -------------------- | ------------------------------------------------ |
| T1110        | Brute Force                | T1110.001/.003   | Auth/API Abuse       | Repeated login attempts against web app/API      |
| T1110        | Brute Force                | T1110.004        | Auth Abuse           | Credential stuffing from external breaches       |
| T1552        | Unsecured Credentials      | T1552.001        | LFI/RCE/Webshell     | Credential files read via file inclusion         |
| T1552        | Unsecured Credentials      | T1552.004        | LFI/SSRF/RCE         | Private keys read from server filesystem         |
| T1528        | Steal App Access Token     | —                | XSS/SSRF/Auth        | OAuth/API token theft                            |
| T1539        | Steal Web Session Cookie   | —                | XSS/Session Abuse    | Cookie theft via XSS for session hijacking       |
| T1606        | Forge Web Credentials      | T1606.001/.002   | Auth Bypass          | Forged tokens or session cookies                 |

---

### 5.6 Discovery

| Technique ID | Technique Name                 | Sub-Technique | Attack Class         | Description                                      |
| ------------ | ------------------------------ | ------------- | -------------------- | ------------------------------------------------ |
| T1046        | Network Service Discovery      | —             | SSRF/RCE             | Internal network scanning via SSRF or post-RCE   |
| T1083        | File and Directory Discovery   | —             | LFI/Traversal/RCE    | Discovers files, paths, configuration files      |
| T1057        | Process Discovery              | —             | Post-RCE (Webshell)  | Process enumeration on compromised web host      |
| T1082        | System Information Discovery   | —             | Post-RCE             | OS and system information enumeration            |
| T1087        | Account Discovery              | T1087.001/002 | Post-RCE             | Enumeration of local or domain accounts          |
| T1580        | Cloud Infrastructure Discovery | —             | SSRF (Cloud Meta)    | Discovery via metadata service SSRF              |

---

### 5.7 Collection

| Technique ID | Technique Name             | Sub-Technique    | Attack Class      | Description                                      |
| ------------ | -------------------------- | ---------------- | ----------------- | ------------------------------------------------ |
| T1530        | Data from Cloud Storage    | —                | SSRF/Cloud Pivot  | Access to cloud storage after credential theft   |
| T1005        | Data from Local System     | —                | LFI/RCE/Webshell  | Files read from web server filesystem            |
| T1213        | Data from Info Repos       | —                | SQLi/RCE          | Database content or repo content collected       |
| T1119        | Automated Collection       | —                | SQLi/API Abuse    | Automated extraction via SQLi or API enumeration |
| T1074        | Data Staged                | T1074.001        | Pre-Exfiltration  | Data staged before exfiltration                  |

---

### 5.8 Exfiltration

| Technique ID | Technique Name                    | Sub-Technique | Attack Class     | Description                                      |
| ------------ | --------------------------------- | ------------- | ---------------- | ------------------------------------------------ |
| T1048        | Exfil Over Alternative Protocol   | T1048.003     | Post-RCE/SQLi    | Data transferred via HTTP/FTP/custom protocol    |
| T1041        | Exfil Over C2 Channel             | —             | Post-RCE/Webshell| Data exfiltrated via C2 connection               |
| T1567        | Exfil Over Web Service            | T1567.002     | Post-RCE/API     | Data uploaded to attacker cloud storage          |
| T1020        | Automated Exfiltration            | —             | SQLi/API Abuse   | Automated bulk extraction                        |

---

### 5.9 Impact

| Technique ID | Technique Name             | Sub-Technique | Attack Class     | Description                                      |
| ------------ | -------------------------- | ------------- | ---------------- | ------------------------------------------------ |
| T1499        | Endpoint Denial of Service | T1499.003     | Web App DoS      | Application-layer exhaustion through exploit     |
| T1491        | Defacement                 | T1491.001/002 | RCE/Webshell     | Web page defacement after compromise             |
| T1486        | Data Encrypted for Impact  | —             | Post-RCE         | Ransomware deployed after web compromise         |
| T1565        | Data Manipulation          | T1565.001     | SQLi/Post-RCE    | Unauthorized modification of database records    |

---

## 6. Attack Chain Mapping by Scenario

### 6.1 SQLi → Data Exfiltration Chain

| Stage              | Technique ID | Technique Name                        |
| ------------------ | ------------ | ------------------------------------- |
| Initial Access     | T1190        | Exploit Public-Facing Application     |
| Credential Access  | T1552.001    | Credentials in Files                  |
| Collection         | T1213        | Data from Information Repositories    |
| Collection         | T1119        | Automated Collection                  |
| Exfiltration       | T1048        | Exfiltration Over Alternative Protocol|

---

### 6.2 RCE → Webshell → Lateral Movement Chain

| Stage              | Technique ID | Technique Name                        |
| ------------------ | ------------ | ------------------------------------- |
| Initial Access     | T1190        | Exploit Public-Facing Application     |
| Execution          | T1059.004    | Unix Shell                            |
| Persistence        | T1505.003    | Web Shell                             |
| Defense Evasion    | T1036.005    | Masquerading                          |
| Discovery          | T1082        | System Information Discovery          |
| Discovery          | T1046        | Network Service Discovery             |
| Lateral Movement   | T1021.004    | Remote Services – SSH                 |
| Exfiltration       | T1041        | Exfiltration Over C2 Channel          |

---

### 6.3 SSRF → Cloud Metadata → Cloud Credential Theft Chain

| Stage              | Technique ID | Technique Name                        |
| ------------------ | ------------ | ------------------------------------- |
| Initial Access     | T1190        | Exploit Public-Facing Application     |
| Discovery          | T1580        | Cloud Infrastructure Discovery        |
| Credential Access  | T1552        | Unsecured Credentials                 |
| Lateral Movement   | T1021        | Remote Services                       |
| Collection         | T1530        | Data from Cloud Storage               |
| Exfiltration       | T1567.002    | Exfiltration to Cloud Storage         |

---

### 6.4 XSS → Session Hijacking → Account Takeover Chain

| Stage              | Technique ID | Technique Name                        |
| ------------------ | ------------ | ------------------------------------- |
| Initial Access     | T1190        | Exploit Public-Facing Application     |
| Execution          | T1203        | Exploitation for Client Execution     |
| Credential Access  | T1539        | Steal Web Session Cookie              |
| Credential Access  | T1528        | Steal Application Access Token        |
| Defense Evasion    | T1550.004    | Web Session Cookie                    |
| Collection         | T1213        | Data from Information Repositories    |

---

## 7. Detection Coverage Map

| Technique ID | Technique Name                    | Primary Detection Source      | Secondary Source         | Tool        |
| ------------ | --------------------------------- | ----------------------------- | ------------------------ | ----------- |
| T1190        | Exploit Public-Facing Application | WAF/WAAP alerts               | Web server logs / SIEM   | WAF + SIEM  |
| T1505.003    | Web Shell                         | File integrity monitoring/EDR | Web server file writes   | EDR + FIM   |
| T1059.004    | Unix Shell                        | EDR process tree              | System audit logs        | EDR         |
| T1110        | Brute Force                       | WAF / API gateway logs        | Auth logs / SIEM         | WAF + SIEM  |
| T1552.001    | Credentials in Files              | EDR file access               | App logs                 | EDR         |
| T1539        | Steal Web Session Cookie          | Proxy logs + anomaly          | WAF/CDN challenge events | WAF + Proxy |
| T1580        | Cloud Infrastructure Discovery    | Cloud audit logs (IMDS)       | Network egress logs      | Cloud+SIEM  |
| T1046        | Network Service Discovery         | Network/IDS alerts            | EDR network telemetry    | IDS + EDR   |
| T1048        | Exfil Over Alt Protocol           | Proxy / firewall logs         | DLP / NetFlow            | Proxy + FW  |
| T1567.002    | Exfil to Cloud Storage            | Proxy / cloud audit           | DLP                      | Cloud+Proxy |

---

## 8. Hunting Queries Reference

### 8.1 T1190 – WAF Bypass / Exploit Attempts (Allowed Traffic)
source: WAF
action: allow OR pass
rule_category: SQLi OR XSS OR SSRF OR RCE OR LFI
response_status: 2xx OR 3xx
timeframe: last 24 hours


---

### 8.2 T1505.003 – Webshell Detection
source: EDR OR FIM
event_type: file_create OR file_modify
path: /var/www/ OR /inetpub/wwwroot/ OR /opt/app/public/
extension: .php OR .aspx OR .jsp OR .phtml OR .py
timeframe: since incident start


---

### 8.3 T1059 – Process Execution from Web Server
source: EDR
parent_process: nginx OR apache2 OR httpd OR w3wp OR node OR python
child_process: bash OR sh OR cmd.exe OR powershell.exe OR curl OR wget
timeframe: since incident start


---

### 8.4 T1110 – Brute Force / Credential Stuffing
source: WAF OR App logs OR API gateway
endpoint: /login OR /api/auth OR /token
event_type: auth_failure
threshold: >50 failures per source IP per 5 minutes
timeframe: last 24 hours


---

### 8.5 T1580 – Cloud Metadata SSRF Detection
source: network egress logs OR proxy logs
destination_ip: 169.254.169.254 OR fd00:ec2::254 OR 169.254.170.2
source_process: web server process OR application runtime
timeframe: since incident start


---

### 8.6 T1048 / T1567 – Data Exfiltration
source: proxy OR firewall OR cloud audit
bytes_out: > [baseline threshold]
destination: external IP/domain
source_host: web server tier OR DB tier
timeframe: since incident start


---

## 9. Analyst Reference – Technique Quick Lookup

| If You Observe This…                          | MITRE Technique | Priority Action                              |
| --------------------------------------------- | --------------- | -------------------------------------------- |
| WAF allowed exploit traffic (no block)        | T1190           | Expand scope, check web/app logs immediately |
| New PHP/ASPX/JSP file in web root             | T1505.003       | Isolate host, escalate to L3 immediately     |
| Web server spawning bash/cmd/powershell       | T1059           | Isolate host, escalate to L3 immediately     |
| High-volume login/API failures                | T1110           | WAF rate limit, CAPTCHA, IAM lockout         |
| Outbound request to 169.254.169.254           | T1580           | Block egress, rotate cloud credentials       |
| Session used from multiple IPs simultaneously | T1539/T1550.004 | Invalidate session, escalate                 |
| Large outbound transfer to cloud storage      | T1567.002       | Block destination, escalate to L3            |
| New scheduled task/cron on web host           | T1053           | Remove and escalate                          |
| DB query volume spike + large response bytes  | T1119/T1213     | DB isolation, escalate data breach playbook  |

---

## 10. Post-Incident Update Requirements

After every P1/P2 web application incident:

| Action                                      | Owner          | Target                          |
| ------------------------------------------- | -------------- | ------------------------------- |
| Review observed techniques vs this mapping  | L3 / IR Lead   | Within 5 days of incident close |
| Add newly observed techniques               | L3 / IR Lead   | Update this document            |
| Update hunting queries with new patterns    | L3 / Detection | Detection-Improvement-Log.md    |
| Update ATT&CK Navigator layer               | L3 / Detection | Internal TI platform            |
| Add new IOCs to IoC register                | L3 / TI Team   | IoC-Output-Register.md          |

---

## 11. Related Documents

| Document                  | Path                                                         |
| ------------------------- | ------------------------------------------------------------ |
| Web App Master            | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-Master.md` |
| Web App L1 Triage         | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L1-Triage.md` |
| Web App L2 Investigation  | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L2-Investigation.md` |
| Web App L3 Forensics      | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L3-Forensics.md` |
| Web App Containment       | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-Containment.md` |
| SQLi Specific             | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-SQLi-Specific.md` |
| XSS Specific              | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-XSS-Specific.md` |
| Detection Improvement Log | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md` |
| IoC Output Register       | `08_POST-INCIDENT/08.4_Threat-Intel-Output/IoC-Output-Register.md` |

---

## 12. Revision History

| Version | Date        | Author                               | Changes         |
| ------- | ----------- | ------------------------------------ | --------------- |
| 1.0     | 19-May-2026 | L3 Lead / IR Team Lead / AppSec Lead | Initial version |

---

## 13. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**