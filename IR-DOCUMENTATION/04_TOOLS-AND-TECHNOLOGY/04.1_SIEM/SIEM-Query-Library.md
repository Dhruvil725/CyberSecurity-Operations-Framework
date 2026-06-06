# REFERENCE: SIEM Query Library

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | REFERENCE – SIEM Query Library |
| Document ID | TOOL-SIEM-003 |
| Version | 1.0 |
| Effective Date | 22-May-2026 |
| Owner | SOC Manager / Detection Engineering Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Monthly |

---

# 2. Purpose

This document provides a centralized library of **approved SIEM queries** used by SOC analysts (L1/L2/L3), Threat Hunters, Detection Engineers, and Incident Responders for:

- Incident validation and scoping
- Threat hunting (behavior-based)
- IOC searching (tactical intelligence)
- Identity compromise investigations
- Endpoint investigation support
- Network and exfiltration investigations
- Cloud compromise investigations
- Audit and compliance evidence generation
- Operational metrics and health checks

This library ensures:

- **Consistent investigation methodology**
- **Reduced time-to-investigate**
- **Reusable and validated query logic**
- **Standardized documentation of investigative actions**
- **Tenant-safe execution for MSSP environments**
- **Audit-ready practices**

---

# 3. Scope

Applies to investigations using SIEM data sources including (but not limited to):

| Domain | Typical Sources |
|---|---|
| Identity | AD, Entra ID, VPN, MFA, SSO, PAM |
| Endpoint | EDR/XDR telemetry, Windows/Linux logs |
| Network | Firewall, IDS/IPS, DNS, Proxy, NetFlow |
| Cloud | AWS CloudTrail, Azure Activity, GCP Audit, M365 Unified Audit |
| Email | Email gateway, M365 message trace |
| Security Tools | Vulnerability, DLP/CASB, TI platform |
| MSSP | Client-specific workspaces/indexes, tenant tags |

---

# 4. Query Usage Standards (IMPORTANT)

---

## 4.1 Mandatory Execution Rules

| Rule | Requirement |
|---|---|
| Time range must be defined | Mandatory (do not run open-ended searches) |
| Use UTC timestamps | Mandatory |
| Validate tenant/client scope first (MSSP) | Mandatory |
| Use least-privilege and approved accounts | Mandatory |
| Document query usage in the ticket | Mandatory for P1/P2/P3 investigations |
| Export evidence properly (if required) | Follow evidence SOP |
| Do not run destructive actions | SIEM queries must be read-only |

---

## 4.2 MSSP Tenant Safety Controls

For MSSP operations, analysts must:

- Select the correct **client workspace/index**
- Confirm correct **tenant tag** (e.g., `client_id`, `tenant`, `customer`)
- Avoid cross-client wildcard searches (`index=*` across tenants)
- Document **client scope** in the ticket before query execution

**MSSP Pre-Query Checklist**

| Validation Item | Completed |
|---|---|
| Correct client selected | ☐ |
| Correct index/workspace selected | ☐ |
| Query reviewed for cross-tenant risk | ☐ |
| Time range defined | ☐ |
| Ticket reference present | ☐ |

---

## 4.3 Logging and Auditability

All investigative queries should be reproducible. Where possible, record:

- Query name/ID
- Time range
- Filters applied (user/host/IP)
- Output summary (counts + notable events)
- Evidence export reference (if applicable)

---

# 5. Query Catalog & Naming Convention

---

## 5.1 Query ID Format

**Format:** `Q-<DOMAIN>-<NNN>`

Examples:
- `Q-ID-001` (Identity)
- `Q-EP-014` (Endpoint)
- `Q-NW-021` (Network)
- `Q-CLD-006` (Cloud)
- `Q-IOC-003` (IOC Search)
- `Q-AUD-004` (Audit/Compliance)

---

## 5.2 Standard Query Metadata (Required)

Each query below includes:

| Field | Description |
|---|---|
| Query ID | Unique identifier |
| Objective | What the query detects/investigates |
| Data Sources | Expected telemetry sources |
| Primary Use | Triage / Investigation / Hunting / Audit |
| Notes | Tuning considerations / false positives |
| Query | SPL/KQL/AQL (where provided) |

---

## 5.3 Query Entry Template (for adding new queries)

| Field | Value |
|---|---|
| Query ID | Q-XXX-000 |
| Name |  |
| Objective |  |
| Data Sources |  |
| Primary Use |  |
| Severity Relevance | P1 / P2 / P3 / P4 |
| False Positive Notes |  |
| Dependencies | Integration requirements |
| Last Reviewed | YYYY-MM-DD |
| Owner |  |
| SPL | (optional) |
| KQL | (optional) |
| AQL | (optional) |

---

# 6. Common Parameters (Analyst-Friendly)

Use these placeholders when adapting queries:

| Parameter | Meaning |
|---|---|
| `<START_UTC>` / `<END_UTC>` | Investigation window |
| `<USER>` | Username/UPN |
| `<HOST>` | Hostname |
| `<SRC_IP>` / `<DEST_IP>` | IP addresses |
| `<DOMAIN>` | Domain name |
| `<HASH_SHA256>` | SHA-256 hash |
| `<CLIENT_ID>` | MSSP tenant tag |

**Splunk time controls:** `earliest=-24h latest=now` (always define)  
**KQL time controls:** `| where TimeGenerated between (datetime(<START_UTC>) .. datetime(<END_UTC>))`

---

# 7. Identity & Authentication Queries (Q-ID)

---

## Q-ID-001 — High Volume Failed Logins (Brute Force / Spray)

| Field | Value |
|---|---|
| Objective | Detect repeated login failures by user and/or source IP |
| Data Sources | AD/Entra ID/VPN/MFA logs |
| Primary Use | Investigation / Hunting |
| Notes | Tune threshold per environment; exclude known scanners |

### Splunk (SPL)
```spl
index=auth_logs action=failure earliest=-24h latest=now
| stats count as failures values(app) as apps values(src_ip) as src_ips by user
| where failures > 20
| sort - failures
```

### Sentinel (KQL)
```kql
SigninLogs
| where TimeGenerated > ago(24h)
| where ResultType != 0
| summarize failures=count(), src_ips=make_set(IPAddress, 20), apps=make_set(AppDisplayName, 20) by UserPrincipalName
| where failures > 20
| order by failures desc
```

---

## Q-ID-002 — Password Spray (Many Users from One IP)

| Field | Value |
|---|---|
| Objective | Detect a single source attempting logins for many users |
| Data Sources | AD/Entra ID/VPN logs |
| Primary Use | Hunting |
| Notes | Exclude corporate NAT egress if required; focus on failures+some successes |

### Splunk (SPL)
```spl
index=auth_logs action=failure earliest=-24h latest=now
| stats dc(user) as unique_users count as attempts values(user) as sample_users by src_ip
| where unique_users > 15 AND attempts > 50
| sort - attempts
```

### Sentinel (KQL)
```kql
SigninLogs
| where TimeGenerated > ago(24h)
| where ResultType != 0
| summarize attempts=count(), unique_users=dcount(UserPrincipalName), sample_users=make_set(UserPrincipalName, 20) by IPAddress
| where unique_users > 15 and attempts > 50
| order by attempts desc
```

---

## Q-ID-003 — Impossible Travel / Geo-Anomaly (Same User, Different Countries)

| Field | Value |
|---|---|
| Objective | Identify user sign-ins from multiple countries in a short window |
| Data Sources | Entra ID/SSO logs |
| Primary Use | Investigation |
| Notes | Use with MFA logs and device compliance context |

### Sentinel (KQL)
```kql
SigninLogs
| where TimeGenerated > ago(24h)
| summarize countries=dcount(LocationDetails.countryOrRegion), ips=make_set(IPAddress, 20) by UserPrincipalName, bin(TimeGenerated, 1h)
| where countries > 1
| order by TimeGenerated desc
```

---

## Q-ID-004 — MFA Fatigue / Push Bombing Indicators

| Field | Value |
|---|---|
| Objective | Detect repeated MFA prompts for a user within a short time window |
| Data Sources | MFA provider logs, Entra ID |
| Primary Use | Investigation / Hunting |
| Notes | Requires MFA event telemetry; tune thresholds |

### Sentinel (KQL) (example logic)
```kql
SigninLogs
| where TimeGenerated > ago(24h)
| where ResultType != 0 or ConditionalAccessStatus == "failure"
| summarize attempts=count() by UserPrincipalName, bin(TimeGenerated, 10m)
| where attempts > 10
| order by attempts desc
```

---

## Q-ID-005 — Privileged Account Activity Summary (Admin / Service Accounts)

| Field | Value |
|---|---|
| Objective | Review privileged account login patterns and source IPs |
| Data Sources | AD/VPN/Entra ID/PAM |
| Primary Use | Investigation / Audit |
| Notes | Use your org’s privileged account list/patterns |

### Splunk (SPL)
```spl
index=auth_logs earliest=-24h latest=now
| search user="admin*" OR user="svc_*" OR user IN ("Administrator","root")
| stats count values(src_ip) as src_ips values(hostname) as hosts values(action) as actions by user
| sort - count
```

---

## Q-ID-006 — New Account Creation / Admin Role Grant

| Field | Value |
|---|---|
| Objective | Detect account creation or privilege changes |
| Data Sources | AD Security logs, Entra AuditLogs |
| Primary Use | Investigation / Audit |
| Notes | High priority if created outside change window |

### Splunk (SPL) (AD example EventCodes may vary)
```spl
index=windows_security earliest=-24h latest=now (EventCode=4720 OR EventCode=4728 OR EventCode=4732 OR EventCode=4756)
| stats count values(TargetUserName) as target values(SubjectUserName) as actor by EventCode, host
| sort - count
```

### Sentinel (KQL)
```kql
AuditLogs
| where TimeGenerated > ago(24h)
| where OperationName has_any ("Add user", "Add member to role", "Add member to group")
| project TimeGenerated, OperationName, InitiatedBy, TargetResources, Result
| order by TimeGenerated desc
```

---

# 8. Endpoint Queries (Q-EP)

---

## Q-EP-001 — Encoded PowerShell Execution

| Field | Value |
|---|---|
| Objective | Detect PowerShell with encoded commands |
| Data Sources | EDR telemetry, Sysmon, Windows logs |
| Primary Use | Investigation / Hunting |
| Notes | Common in attacks; validate parent process and user context |

### Splunk (SPL)
```spl
index=edr_logs earliest=-24h latest=now process_name="powershell.exe" CommandLine="*EncodedCommand*"
| table _time hostname user parent_process process_name CommandLine
| sort - _time
```

### Sentinel (KQL)
```kql
DeviceProcessEvents
| where TimeGenerated > ago(24h)
| where FileName =~ "powershell.exe"
| where ProcessCommandLine contains "EncodedCommand"
| project TimeGenerated, DeviceName, AccountName, InitiatingProcessFileName, FileName, ProcessCommandLine
| order by TimeGenerated desc
```

---

## Q-EP-002 — Suspicious LOLBins Execution (Common Set)

| Field | Value |
|---|---|
| Objective | Detect common living-off-the-land binaries used for abuse |
| Data Sources | EDR, Sysmon |
| Primary Use | Hunting |
| Notes | Validate against IT automation; include command-line review |

### Splunk (SPL)
```spl
index=edr_logs earliest=-24h latest=now process_name IN ("rundll32.exe","regsvr32.exe","mshta.exe","wscript.exe","cscript.exe","certutil.exe","bitsadmin.exe")
| table _time hostname user parent_process process_name CommandLine
| sort - _time
```

### Sentinel (KQL)
```kql
DeviceProcessEvents
| where TimeGenerated > ago(24h)
| where FileName in~ ("rundll32.exe","regsvr32.exe","mshta.exe","wscript.exe","cscript.exe","certutil.exe","bitsadmin.exe")
| project TimeGenerated, DeviceName, AccountName, InitiatingProcessFileName, FileName, ProcessCommandLine
| order by TimeGenerated desc
```

---

## Q-EP-003 — Credential Dumping Indicators (LSASS Access / Dump Tools)

| Field | Value |
|---|---|
| Objective | Identify potential credential dumping activity |
| Data Sources | EDR, Sysmon, Windows Security |
| Primary Use | Investigation |
| Notes | Prioritize if server/DC; escalate if confirmed |

### Sentinel (KQL) (example heuristic)
```kql
DeviceProcessEvents
| where TimeGenerated > ago(24h)
| where ProcessCommandLine has_any ("comsvcs.dll", "procdump", "sekurlsa", "lsass", "rundll32.exe C:\\Windows\\System32\\comsvcs.dll")
| project TimeGenerated, DeviceName, AccountName, FileName, ProcessCommandLine, InitiatingProcessFileName
| order by TimeGenerated desc
```

---

## Q-EP-004 — New Service Installation (Persistence)

| Field | Value |
|---|---|
| Objective | Detect creation of new Windows services |
| Data Sources | Windows System logs (7045), EDR |
| Primary Use | Investigation / Hunting |
| Notes | Validate against approved deployments |

### Splunk (SPL)
```spl
index=windows_system earliest=-7d latest=now EventCode=7045
| table _time host ServiceName ImagePath AccountName
| sort - _time
```

---

## Q-EP-005 — Scheduled Task Creation (Persistence)

| Field | Value |
|---|---|
| Objective | Detect scheduled task creation or modification |
| Data Sources | Windows logs, EDR |
| Primary Use | Investigation |
| Notes | Validate against IT scheduled jobs |

### Splunk (SPL) (EventCodes vary; example)
```spl
index=windows_security earliest=-7d latest=now (EventCode=4698 OR EventCode=4702)
| table _time host SubjectUserName TaskName
| sort - _time
```

---

# 9. Network Queries (Q-NW)

---

## Q-NW-001 — Beaconing (Repeated Connections to Same Destination)

| Field | Value |
|---|---|
| Objective | Detect repeated outbound connections indicating C2 beaconing |
| Data Sources | Firewall/Proxy/NetFlow |
| Primary Use | Hunting |
| Notes | Validate against known SaaS endpoints; tune interval & count |

### Splunk (SPL) (generic)
```spl
index=network_logs earliest=-24h latest=now
| stats count as hits min(_time) as first max(_time) as last by src_ip dest_ip dest_port
| where hits > 200
| eval duration=(last-first)
| where duration > 3600
| sort - hits
```

---

## Q-NW-002 — Large Outbound Transfers (Potential Exfiltration)

| Field | Value |
|---|---|
| Objective | Identify large outbound data volumes |
| Data Sources | Firewall/Proxy/NetFlow |
| Primary Use | Investigation |
| Notes | Baseline per org; validate backup jobs and sanctioned cloud storage |

### Splunk (SPL) (example fields may differ)
```spl
index=network_logs earliest=-24h latest=now
| stats sum(bytes_out) as total_bytes_out by src_ip dest_ip dest_port
| where total_bytes_out > 100000000
| sort - total_bytes_out
```

### Sentinel (KQL) (CommonSecurityLog example; field names may differ)
```kql
CommonSecurityLog
| where TimeGenerated > ago(24h)
| summarize total_bytes_out=sum(SentBytes) by SourceIP, DestinationIP, DestinationPort
| where total_bytes_out > 100000000
| order by total_bytes_out desc
```

---

## Q-NW-003 — DNS Suspicious Patterns (Possible DGA / Tunneling)

| Field | Value |
|---|---|
| Objective | Identify abnormal DNS query patterns (long labels/high volume) |
| Data Sources | DNS logs |
| Primary Use | Hunting |
| Notes | Requires DNS logging; tune threshold |

### Splunk (SPL) (heuristic)
```spl
index=dns_logs earliest=-24h latest=now
| eval qlen=len(query)
| stats count as qcount avg(qlen) as avg_len max(qlen) as max_len by src_ip
| where qcount > 500 OR max_len > 80
| sort - qcount
```

---

## Q-NW-004 — Lateral Movement via RDP/SMB (Internal Spread)

| Field | Value |
|---|---|
| Objective | Identify unusual internal RDP/SMB connection patterns |
| Data Sources | Firewall/NetFlow/Windows logs |
| Primary Use | Investigation |
| Notes | Validate against IT admin jump hosts |

### Splunk (SPL) (network perspective; port-based)
```spl
index=network_logs earliest=-24h latest=now
| search dest_port IN (3389,445)
| stats count as connections dc(dest_ip) as unique_targets values(dest_ip) as sample_targets by src_ip, dest_port
| where unique_targets > 10
| sort - connections
```

---

# 10. Cloud Queries (Q-CLD)

---

## Q-CLD-001 — AWS Root Usage

| Field | Value |
|---|---|
| Objective | Detect AWS root account activity |
| Data Sources | AWS CloudTrail |
| Primary Use | Investigation / Audit |
| Notes | Root usage should be rare; treat as high severity |

### KQL (example; depends on connector schema)
```kql
AWSCloudTrail
| where TimeGenerated > ago(30d)
| where UserIdentityType == "Root"
| project TimeGenerated, EventName, SourceIpAddress, UserAgent, AwsRegion
| order by TimeGenerated desc
```

---

## Q-CLD-002 — Azure Privileged Role Assignment / Role Changes

| Field | Value |
|---|---|
| Objective | Identify role assignments and privilege changes |
| Data Sources | Azure AuditLogs |
| Primary Use | Investigation / Audit |
| Notes | Validate against change tickets and approvals |

### Sentinel (KQL)
```kql
AuditLogs
| where TimeGenerated > ago(7d)
| where OperationName has_any ("Add member to role","Add eligible member to role","Add member to privileged role")
| project TimeGenerated, OperationName, InitiatedBy, TargetResources, Result
| order by TimeGenerated desc
```

---

## Q-CLD-003 — Cloud API Key Creation / Credential Changes

| Field | Value |
|---|---|
| Objective | Detect creation of new keys/credentials for cloud identities |
| Data Sources | CloudTrail / Azure Audit / GCP Audit |
| Primary Use | Investigation |
| Notes | High risk if created by unusual actor or outside business hours |

### KQL (AWS example schema-dependent)
```kql
AWSCloudTrail
| where TimeGenerated > ago(7d)
| where EventName in ("CreateAccessKey","UpdateAccessKey","CreateLoginProfile")
| project TimeGenerated, EventName, UserIdentityArn, SourceIpAddress, UserAgent
| order by TimeGenerated desc
```

---

## Q-CLD-004 — M365 Suspicious Mailbox Rule Creation (BEC Indicator)

| Field | Value |
|---|---|
| Objective | Identify new inbox rules that auto-forward or hide emails |
| Data Sources | M365 Unified Audit Log |
| Primary Use | Investigation |
| Notes | Common BEC persistence mechanism |

### KQL (schema depends on connector)
```kql
OfficeActivity
| where TimeGenerated > ago(7d)
| where Operation has_any ("New-InboxRule","Set-InboxRule")
| project TimeGenerated, UserId, Operation, ClientIP, Parameters
| order by TimeGenerated desc
```

---

# 11. Email & Phishing Queries (Q-EML)

---

## Q-EML-001 — Phishing Sender / Subject Pivot (Campaign Search)

| Field | Value |
|---|---|
| Objective | Find all recipients of a suspicious sender/subject |
| Data Sources | Email gateway logs / M365 message trace |
| Primary Use | Investigation |
| Notes | Use for rapid scoping and containment |

### Splunk (SPL) (example)
```spl
index=email_logs earliest=-7d latest=now
| search sender="<SENDER_EMAIL>" OR subject="*<SUBJECT_KEYWORD>*"
| stats count values(recipient) as recipients values(message_id) as message_ids by sender, subject
| sort - count
```

---

## Q-EML-002 — URL Click Activity (If Logged)

| Field | Value |
|---|---|
| Objective | Identify users who clicked a suspicious URL |
| Data Sources | Secure web gateway / email security click logs |
| Primary Use | Investigation |
| Notes | Requires click telemetry integration |

### Splunk (SPL) (generic)
```spl
index=proxy_logs earliest=-7d latest=now
| search url="*<SUSPICIOUS_DOMAIN_OR_URL>*"
| stats count dc(user) as unique_users values(user) as users by url
| sort - count
```

---

# 12. IOC Search Queries (Q-IOC)

---

## Q-IOC-001 — IP IOC Search (Any Source)

| Field | Value |
|---|---|
| Objective | Search for an IOC IP across key sources |
| Data Sources | SIEM normalized fields |
| Primary Use | Investigation |
| Notes | Always restrict time window; verify NAT contexts |

### Splunk (SPL)
```spl
earliest=-30d latest=now (index=network_logs OR index=edr_logs OR index=auth_logs)
| search src_ip="<IOC_IP>" OR dest_ip="<IOC_IP>"
| stats count values(index) as sources values(hostname) as hosts values(user) as users by src_ip, dest_ip
| sort - count
```

---

## Q-IOC-002 — Domain IOC Search (DNS/Proxy)

| Field | Value |
|---|---|
| Objective | Identify DNS queries and proxy connections to a malicious domain |
| Data Sources | DNS logs, proxy logs |
| Primary Use | Investigation |
| Notes | Include subdomain wildcard logic where appropriate |

### Splunk (SPL)
```spl
(index=dns_logs OR index=proxy_logs) earliest=-30d latest=now
| search query="*<IOC_DOMAIN>*" OR url="*<IOC_DOMAIN>*"
| stats count values(src_ip) as src_ips values(user) as users values(hostname) as hosts by query, url
| sort - count
```

---

## Q-IOC-003 — SHA-256 IOC Search (Endpoint)

| Field | Value |
|---|---|
| Objective | Identify endpoints that executed/contained a known hash |
| Data Sources | EDR telemetry, file events |
| Primary Use | Investigation |
| Notes | Escalate if seen on servers/DCs |

### Sentinel (KQL)
```kql
DeviceFileEvents
| where TimeGenerated > ago(90d)
| where SHA256 == "<HASH_SHA256>"
| project TimeGenerated, DeviceName, FolderPath, FileName, InitiatingProcessFileName, InitiatingProcessCommandLine, AccountName
| order by TimeGenerated desc
```

---

# 13. Ransomware / Destructive Behavior Queries (Q-RAN)

---

## Q-RAN-001 — Mass File Rename/Modification (Heuristic)

| Field | Value |
|---|---|
| Objective | Detect high-volume file changes indicative of encryption |
| Data Sources | EDR file telemetry |
| Primary Use | Investigation |
| Notes | Highly dependent on EDR schema; use as heuristic and confirm |

### Sentinel (KQL) (example heuristic)
```kql
DeviceFileEvents
| where TimeGenerated > ago(6h)
| summarize file_events=count() by DeviceName, AccountName, bin(TimeGenerated, 10m)
| where file_events > 2000
| order by file_events desc
```

---

## Q-RAN-002 — Shadow Copy Deletion / Backup Tampering

| Field | Value |
|---|---|
| Objective | Detect common ransomware backup-destruction commands |
| Data Sources | EDR process telemetry, Windows logs |
| Primary Use | Investigation |
| Notes | High confidence indicator; escalate immediately if confirmed |

### Sentinel (KQL)
```kql
DeviceProcessEvents
| where TimeGenerated > ago(24h)
| where ProcessCommandLine has_any ("vssadmin delete shadows", "wmic shadowcopy delete", "bcdedit /set", "wbadmin delete catalog")
| project TimeGenerated, DeviceName, AccountName, FileName, ProcessCommandLine, InitiatingProcessFileName
| order by TimeGenerated desc
```

---

# 14. Audit & Compliance Queries (Q-AUD)

---

## Q-AUD-001 — Privileged Group Membership Changes

| Field | Value |
|---|---|
| Objective | Identify membership changes in privileged AD groups |
| Data Sources | AD Security logs |
| Primary Use | Audit |
| Notes | Map group names to org standard privileged groups |

### Splunk (SPL) (EventCodes may vary)
```spl
index=windows_security earliest=-30d latest=now (EventCode=4728 OR EventCode=4732 OR EventCode=4756)
| table _time host SubjectUserName TargetUserName GroupName EventCode
| sort - _time
```

---

## Q-AUD-002 — Disabled/Deleted Accounts Activity (Risk Review)

| Field | Value |
|---|---|
| Objective | Identify activity tied to disabled/deleted accounts (if logged) |
| Data Sources | IAM/Directory logs |
| Primary Use | Audit / Investigation |
| Notes | Depends on directory telemetry availability |

### Sentinel (KQL) (example)
```kql
SigninLogs
| where TimeGenerated > ago(30d)
| where ResultDescription has_any ("account is disabled","account is locked")
| project TimeGenerated, UserPrincipalName, IPAddress, AppDisplayName, ResultDescription
| order by TimeGenerated desc
```

---

# 15. Operational / SIEM Health Queries (Q-OPS)

---

## Q-OPS-001 — Log Source Silence (No Events in Window)

| Field | Value |
|---|---|
| Objective | Detect sources that stopped sending logs (basic heartbeat) |
| Data Sources | SIEM internal source tracking / indexes |
| Primary Use | Operations |
| Notes | Requires consistent source fields; tune by criticality |

### Splunk (SPL) (example)
```spl
| tstats latest(_time) as last_seen where index=* by sourcetype
| eval minutes_since_last=(now()-last_seen)/60
| where minutes_since_last > 30
| sort - minutes_since_last
```

---

# 16. Evidence Handling Notes (When Exporting Query Results)

If query results must be retained as evidence:

- Export in original format where possible (CSV/JSON)
- Include:
  - Query string
  - Time window
  - Execution timestamp (UTC)
  - Analyst name
- Hash exported files (SHA-256)
- Store per evidence policy

Reference:
- `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Evidence-Handling-SOP.md`
- `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

# 17. Change Control & Review

All changes to this library must be logged.

---

## 17.1 Change Log

| Date | Version | Change Summary | Author | Approved By |
|---|---|---|---|---|
| 22-May-2026 | 1.0 | Initial version | Detection Engineering Lead | CISO |

---

# 18. Related Documents

| Document | Path |
|---|---|
| SIEM Alert Tuning Guide | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md` |
| SIEM Use Cases Master | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Use-Cases-Master.md` |
| SIEM Integration Map | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Integration-Map.md` |
| SIEM Troubleshooting SOP | `04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Troubleshooting-SOP.md` |
| L2 SIEM Deep Investigation | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-SIEM-Deep-Investigation.md` |
| TI IOC Handling SOP | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md` |

---

# 19. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**
