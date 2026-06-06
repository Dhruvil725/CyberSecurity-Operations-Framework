# Tool Command Reference

---

# 1. Document Control

| Field          | Value                                         |
| -------------- | --------------------------------------------- |
| Document Name  | Tool Command Reference                        |
| Document ID    | MSSP-TRN-KB-003                               |
| Version        | 1.0                                           |
| Effective Date | 30-May-2026                                   |
| Owner          | MSSP Detection Engineering Lead / SOC Manager |
| Approved By    | MSSP CISO                                     |
| Classification | Confidential – MSSP Internal                  |
| Review Cycle   | Quarterly (or upon tool platform update)      |

---

# 2. Purpose

This document defines the standardized Tool Command Reference providing SOC analysts (L1/L2/L3), IR Team members, Threat Intelligence analysts, and Detection Engineers with a consolidated quick-lookup reference for the most frequently-used commands, queries, and operational actions across the MSSP primary security toolchain — enabling rapid, accurate, multi-tenant-safe tool operation during alert triage, investigations, threat hunting, containment, and forensic activities.

A formal Tool Command Reference is critical because:

- SOC analysts use multiple tools daily with different query languages and syntaxes
- inconsistent command usage produces inconsistent investigation outcomes
- new analysts require structured tool reference to operate confidently
- L1 analysts during high-volume triage need rapid command lookup
- L2/L3 analysts need pre-validated investigation queries
- IR Team members need pre-validated containment commands
- Detection Engineers need consistent query patterns for rule development
- Threat Intel analysts need consistent enrichment commands
- multi-tenant MSSPs need tenant-scoped command discipline
- containment commands have high blast radius — incorrect syntax causes operational impact
- ISO 27001 A.5.24 (incident response) and NIST CSF RS.MI (mitigation) require operational discipline
- RBI Cyber Security Framework requires demonstrable operational competency
- audit trails require consistent command attribution
- without consolidated reference, analysts rely on inconsistent personal notes or external sources
- this reference is the operational quick-lookup companion to tool training and SOPs

This reference ensures:

- consolidated quick-lookup for SIEM, EDR, SOAR, NDR, identity, cloud, forensics tools
- pre-validated query patterns for common investigation scenarios
- pre-validated containment commands with safety notes
- tenant-scoping guidance for every command
- linkage to deeper tool guides and SOPs
- multi-tenant safety considerations
- audit-ready documentation of standard command usage
- quarterly update cycle aligned to tool changes
- consistent operational discipline across the SOC

Reference alignment:

- 04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Query-Library.md
- 04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Investigation-Queries.md
- 04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Containment-Commands.md
- 04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Forensics-Toolkit-Reference.md

---

# 3. Scope

This reference covers:

| Scope Element          | Coverage                                       |
| ---------------------- | ---------------------------------------------- |
| SIEM platforms         | KQL (Sentinel), SPL (Splunk), generic patterns |
| EDR platforms          | Generic patterns with vendor-specific examples |
| NDR and Network tools  | Generic patterns                               |
| SOAR                   | Action patterns                                |
| Identity and IdP       | Azure AD, Okta, AD                             |
| Cloud platforms        | AWS, Azure, GCP (audit log queries)            |
| Email security         | Generic gateway patterns                       |
| Forensics tools        | Memory, disk, network                          |
| Threat intel platforms | Enrichment commands                            |
| Containment commands   | Network, endpoint, identity, cloud             |
| OS-native commands     | Windows, Linux quick reference                 |
| Multi-tenant scoping   | Per-command guidance                           |

Out of scope:

- Full tool training (covered by 10.1_Onboarding)
- Detailed query libraries (covered by 04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Query-Library.md)
- Detailed forensic procedures (covered by 04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools)
- Vendor-specific deep features (covered by vendor documentation)
- Detection rule code (covered by Detection Engineering repository)
- Specific IoC values (covered by Common-IoC-Reference.md)

---

# 4. Definitions

| Term                | Definition                                  |
| ------------------- | ------------------------------------------- |
| Query               | Search expression in tool-specific language |
| Command             | Action executed in tool or CLI              |
| Containment Command | High-impact action affecting production     |
| Read-Only Query     | Investigation query without state change    |
| Tenant-Scoped Query | Query limited to specific client            |
| Cross-Tenant Query  | Aggregated query (restricted access)        |
| Pre-Validated Query | Reviewed query safe for operational use     |
| KQL                 | Kusto Query Language (Sentinel, Defender)   |
| SPL                 | Search Processing Language (Splunk)         |
| LOLBins             | Living-off-the-Land Binaries                |
| Hash                | MD5/SHA1/SHA256 file fingerprint            |

---

# 5. Roles and Responsibilities

| Role                            | Responsibilities                           |
| ------------------------------- | ------------------------------------------ |
| MSSP Detection Engineering Lead | Query and command ownership and validation |
| MSSP SOC Manager                | Operational use validation                 |
| MSSP IR Team Lead               | Containment command authority              |
| MSSP L1/L2/L3 Analysts          | Reference users and feedback providers     |
| MSSP IT Lead                    | Tool platform changes coordination         |
| All SOC Personnel               | Apply commands per multi-tenant scoping    |

---

# 6. Multi-Tenant Command Safety Principles (Mandatory)

| Principle                       | Requirement                                                   |
| ------------------------------- | ------------------------------------------------------------- |
| Tenant scope first              | Every query and command starts with tenant scope verification |
| Read-only before write          | Investigation queries before containment commands             |
| Containment authority verified  | Per containment authority matrix before execution             |
| Logged and attributable         | Every command attributable to analyst and tenant              |
| Blast radius awareness          | Understand impact before high-impact commands                 |
| Cross-tenant queries restricted | Only authorized roles (TI Lead, Detection Eng)                |
| Per-client confirmation         | High-impact actions confirmed with per-client SDM             |

Reference:

- 09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md
- 03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md

---

# 7. SIEM Quick Reference (Mandatory)

## 7.1 KQL (Kusto Query Language) — Sentinel / Defender / Log Analytics

### 7.1.1 Common Pattern — Tenant Filter (Always First)

Query: Filter by tenant — always start every query with this pattern. Replace tenant-id with the specific client tenant identifier. Add time filter and limit for safety.

KQL Pattern: TableName pipe where TenantId equals "tenant-id" pipe where TimeGenerated greater than ago(24h) pipe limit 100

### 7.1.2 Failed Logons

Purpose: Identify accounts with excessive failed logon attempts in last 24 hours.

KQL Pattern: SigninLogs pipe where TenantId equals "tenant-id" pipe where TimeGenerated greater than ago(24h) pipe where ResultType not equal 0 pipe summarize FailCount equals count() by UserPrincipalName, IPAddress pipe where FailCount greater than 10 pipe order by FailCount desc

### 7.1.3 Successful Logon from Unusual Country

Purpose: Identify successful authentications from unexpected geographic locations.

KQL Pattern: SigninLogs pipe where TenantId equals "tenant-id" pipe where TimeGenerated greater than ago(24h) pipe where ResultType equals 0 pipe where Location not in ("IN", "US", "UK") pipe project TimeGenerated, UserPrincipalName, IPAddress, Location, AppDisplayName

### 7.1.4 PowerShell Encoded Command

Purpose: Detect PowerShell execution with encoded (base64) commands — common malware technique.

KQL Pattern: DeviceProcessEvents pipe where TenantId equals "tenant-id" pipe where TimeGenerated greater than ago(24h) pipe where ProcessCommandLine has_any ("-enc ", "-EncodedCommand", "-e ") pipe project TimeGenerated, DeviceName, AccountName, ProcessCommandLine, InitiatingProcessCommandLine

### 7.1.5 LSASS Access (Credential Dumping)

Purpose: Detect processes accessing LSASS memory — indicator of credential dumping (Mimikatz-like).

KQL Pattern: DeviceEvents pipe where TenantId equals "tenant-id" pipe where TimeGenerated greater than ago(24h) pipe where ActionType equals "OpenProcessApiCall" pipe where InitiatingProcessFileName not in ("System", "lsass.exe") pipe where AdditionalFields has "lsass.exe" pipe project TimeGenerated, DeviceName, InitiatingProcessFileName, AccountName

### 7.1.6 Large Outbound Transfer (Possible Exfil)

Purpose: Identify hosts with large outbound data transfers — possible data exfiltration.

KQL Pattern: DeviceNetworkEvents pipe where TenantId equals "tenant-id" pipe where TimeGenerated greater than ago(24h) pipe where ActionType equals "ConnectionSuccess" pipe summarize TotalBytes equals sum(SentBytes) by DeviceName, RemoteIP, RemoteUrl pipe where TotalBytes greater than 1073741824 pipe order by TotalBytes desc

Note: 1073741824 bytes equals 1 GB. Adjust threshold per client environment.

### 7.1.7 Mass File Modification (Ransomware Pattern)

Purpose: Detect mass file modifications on a single host — indicator of ransomware encryption.

KQL Pattern: DeviceFileEvents pipe where TenantId equals "tenant-id" pipe where TimeGenerated greater than ago(1h) pipe where ActionType equals "FileModified" pipe summarize FileCount equals count() by DeviceName, InitiatingProcessFileName pipe where FileCount greater than 500 pipe order by FileCount desc

---

## 7.2 SPL (Splunk Search Processing Language)

### 7.2.1 Common Pattern — Index Filter

SPL Pattern: index equals tenant-index sourcetype equals source pipe eval _time equals strftime(_time, "%Y-%m-%d %H:%M:%S") pipe stats count by host, user pipe sort minus count

### 7.2.2 Failed Logons (Splunk)

SPL Pattern: index equals tenant-index sourcetype equals "WinEventLog:Security" EventCode equals 4625 pipe stats count as FailCount by Account_Name, src_ip pipe where FailCount greater than 10 pipe sort minus FailCount

### 7.2.3 PowerShell Encoded (Splunk)

SPL Pattern: index equals tenant-index sourcetype equals "WinEventLog:Microsoft-Windows-Sysmon/Operational" EventCode equals 1 pipe search CommandLine equals "*-enc*" OR CommandLine equals "*-EncodedCommand*" pipe table _time, host, User, CommandLine, ParentCommandLine

### 7.2.4 Outbound Connection Volume (Splunk)

SPL Pattern: index equals tenant-index sourcetype equals firewall action equals allowed pipe stats sum(bytes_out) as TotalBytes by src_ip, dest_ip pipe where TotalBytes greater than 1073741824 pipe sort minus TotalBytes

---

## 7.3 Generic SIEM Use Case Tags

| Use Case             | Search Pattern Concept                                         |
| -------------------- | -------------------------------------------------------------- |
| Brute force          | Multiple failed auth events to same account                    |
| Impossible travel    | Two successful logons from distant locations within short time |
| Privilege escalation | New admin assignment events                                    |
| Persistence          | New scheduled task or service or registry run key              |
| Lateral movement     | RDP or SMB or WinRM from non-typical sources                   |
| Data exfiltration    | Large outbound transfer to non-typical destination             |
| C2 beaconing         | Regular interval connections to suspicious destination         |
| Ransomware           | Mass file modification plus ransom note creation               |

---

# 8. EDR Quick Reference (Mandatory)

## 8.1 Read-Only Investigation Queries (Generic)

| Query Purpose                    | Pattern                                      |
| -------------------------------- | -------------------------------------------- |
| List processes by user           | processes where username equals "user"       |
| List network connections by host | connections where hostname equals "host"     |
| Find file by hash                | files where sha256 equals "hash"             |
| Find file by name                | files where filename contains "name"         |
| Find registry modifications      | registry where key contains "Run"            |
| Find scheduled tasks created     | events where action equals "TaskCreated"     |
| Find services created            | events where action equals "ServiceCreated"  |
| Find PowerShell execution        | processes where name equals "powershell.exe" |
| Find lateral movement            | events where remote_logon equals true        |

## 8.2 Containment Commands (HIGH IMPACT — Authority Required)

WARNING: All containment commands require per-client containment authority verification before execution.

| Action                       | Generic Command Pattern            | Authority Required                   |
| ---------------------------- | ---------------------------------- | ------------------------------------ |
| Isolate endpoint             | isolate host hostname              | Per IRT Containment Authority Matrix |
| Release isolation            | release host hostname              | Per IRT Containment Authority Matrix |
| Kill process                 | kill process pid on host           | L2 plus per-client authority         |
| Quarantine file              | quarantine file hash on host       | L2 plus                              |
| Delete file                  | delete file path on host           | L3 plus per-client authority         |
| Block hash org-wide (tenant) | block hash sha256 tenant tenant-id | Detection Eng plus per-client SDM    |
| Block IP org-wide (tenant)   | block ip address tenant tenant-id  | Detection Eng plus per-client SDM    |

Reference:

- 04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Containment-Commands.md
- 03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md

---

# 9. Identity / IdP Quick Reference (Mandatory)

## 9.1 Azure AD / Microsoft Entra ID

### 9.1.1 Investigation Queries

Failed sign-ins for user:

KQL Pattern: SigninLogs pipe where TenantId equals "tenant-id" pipe where UserPrincipalName equals "user@domain" pipe where ResultType not equal 0 pipe project TimeGenerated, IPAddress, Location, ResultType, AppDisplayName

MFA-bypassed sign-ins:

KQL Pattern: SigninLogs pipe where TenantId equals "tenant-id" pipe where AuthenticationRequirement equals "singleFactorAuthentication" pipe where RiskLevelAggregated equals "high" pipe project TimeGenerated, UserPrincipalName, IPAddress, AppDisplayName

Privileged role assignments:

KQL Pattern: AuditLogs pipe where TenantId equals "tenant-id" pipe where OperationName equals "Add member to role" pipe project TimeGenerated, InitiatedBy, TargetResources

### 9.1.2 Containment Actions (Authority Required)

| Action               | Method                                                          |
| -------------------- | --------------------------------------------------------------- |
| Disable user         | Set-AzureADUser -ObjectId user -AccountEnabled false            |
| Revoke sessions      | Revoke-AzureADUserAllRefreshToken -ObjectId user                |
| Force password reset | Via portal or PowerShell                                        |
| Remove from role     | Remove-AzureADDirectoryRoleMember -ObjectId role -MemberId user |

## 9.2 Okta

### 9.2.1 Investigation Queries

Failed logins: type equals "user.authentication.auth_via_mfa" AND outcome.result equals "FAILURE"

Suspicious geographic logins: type equals "user.session.start" AND outcome.reason equals "INVALID_CREDENTIALS"

MFA bypass attempts: type equals "user.mfa.attempt.bypass"

### 9.2.2 Containment Actions (Authority Required)

| Action         | API Endpoint                                     |
| -------------- | ------------------------------------------------ |
| Suspend user   | POST /api/v1/users/id/lifecycle/suspend          |
| Clear sessions | DELETE /api/v1/users/id/sessions                 |
| Reset password | POST /api/v1/users/id/credentials/reset_password |

## 9.3 Active Directory (On-Premises)

### 9.3.1 Investigation Commands

Recent failed logons: Get-EventLog -LogName Security -InstanceId 4625 -Newest 100

Recent successful logons for user: Get-EventLog -LogName Security -InstanceId 4624 pipe Where-Object Message -match "username"

Disabled account check: Get-ADUser -Identity username -Properties Enabled, LockedOut, LastBadPasswordAttempt

Recent password resets: Search-ADAccount -PasswordExpired

### 9.3.2 Containment Commands (Authority Required)

| Action               | Command                                            |
| -------------------- | -------------------------------------------------- |
| Disable user         | Disable-ADAccount -Identity user                   |
| Force password reset | Set-ADAccountPassword -Identity user -Reset        |
| Unlock account       | Unlock-ADAccount -Identity user                    |
| Remove from group    | Remove-ADGroupMember -Identity group -Members user |

---

# 10. Cloud Platform Quick Reference (Mandatory)

## 10.1 AWS

### 10.1.1 Investigation Queries (CloudTrail via Athena)

Failed console logins: SELECT useridentity.username, sourceipaddress, eventtime FROM cloudtrail_logs WHERE accountid equals 'account-id' AND eventname equals 'ConsoleLogin' AND responseelements LIKE '%Failure%' AND eventtime greater than timestamp '24h ago'

Suspicious S3 access: SELECT useridentity.arn, requestparameters.bucketname, eventtime FROM cloudtrail_logs WHERE accountid equals 'account-id' AND eventname IN ('GetObject', 'ListObjects') AND requestparameters.bucketname LIKE '%sensitive%'

IAM changes: SELECT useridentity.arn, eventname, eventtime FROM cloudtrail_logs WHERE accountid equals 'account-id' AND eventsource equals 'iam.amazonaws.com' AND eventname IN ('CreateUser', 'AttachUserPolicy', 'CreateAccessKey')

### 10.1.2 Containment (AWS CLI — Authority Required)

| Action                      | Command                                                                         |
| --------------------------- | ------------------------------------------------------------------------------- |
| Disable IAM access key      | aws iam update-access-key --access-key-id id --status Inactive --user-name user |
| Delete IAM access key       | aws iam delete-access-key --access-key-id id --user-name user                   |
| Revoke all sessions         | aws iam delete-login-profile --user-name user                                   |
| Stop EC2 instance           | aws ec2 stop-instances --instance-ids i-xxxx                                    |
| Isolate EC2 (quarantine SG) | aws ec2 modify-instance-attribute --instance-id i-xxxx --groups quarantine-sg   |

## 10.2 Azure

### 10.2.1 Investigation Queries (Azure Activity Log via KQL)

Failed Azure portal logins: AzureActivity pipe where SubscriptionId equals "sub-id" pipe where OperationNameValue equals "MICROSOFT.AUTHORIZATION/POLICIES/AUDIT/ACTION" pipe where ActivityStatusValue equals "Failure"

Resource creation: AzureActivity pipe where SubscriptionId equals "sub-id" pipe where OperationNameValue endswith "/WRITE" pipe project TimeGenerated, Caller, ResourceId, OperationNameValue

Role assignment changes: AzureActivity pipe where SubscriptionId equals "sub-id" pipe where OperationNameValue equals "MICROSOFT.AUTHORIZATION/ROLEASSIGNMENTS/WRITE"

### 10.2.2 Containment (Azure CLI — Authority Required)

| Action                  | Command                                                                                      |
| ----------------------- | -------------------------------------------------------------------------------------------- |
| Disable user            | az ad user update --id user --account-enabled false                                          |
| Revoke user sessions    | az ad user revoke-sign-in-sessions --id user                                                 |
| Stop VM                 | az vm deallocate --resource-group rg --name vm                                               |
| Isolate VM (NSG change) | az network nic update --resource-group rg --name nic --network-security-group quarantine-nsg |

## 10.3 GCP

### 10.3.1 Investigation Queries (Audit Logs via Log Explorer)

Failed authentication: resource.type equals "audited_resource" AND protoPayload.authenticationInfo.principalEmail equals "user@domain" AND severity equals "ERROR"

Storage bucket access: resource.type equals "gcs_bucket" AND protoPayload.methodName equals "storage.objects.get" AND resource.labels.bucket_name equals "bucket-name"

IAM changes: protoPayload.methodName equals "SetIamPolicy" AND protoPayload.serviceName equals "iam.googleapis.com"

### 10.3.2 Containment (gcloud — Authority Required)

| Action             | Command                                                                                 |
| ------------------ | --------------------------------------------------------------------------------------- |
| Suspend user       | Use Admin SDK (gcloud does not directly suspend Workspace users)                        |
| Stop VM instance   | gcloud compute instances stop instance --zone zone                                      |
| Remove IAM binding | gcloud projects remove-iam-policy-binding project --member user:user@domain --role role |

---

# 11. Network / NDR Quick Reference (Mandatory)

## 11.1 Common Investigation Patterns

| Investigation                   | Pattern                                          |
| ------------------------------- | ------------------------------------------------ |
| Find connections to specific IP | dest_ip equals ip                                |
| Find DNS lookups for domain     | query equals "domain"                            |
| Find large outbound transfers   | bytes_out greater than 100MB                     |
| Find suspicious user-agents     | user_agent contains "curl" OR "wget" OR "python" |
| Find newly registered domains   | Cross-reference with TI domain age               |
| Find C2 beaconing               | Regular interval connections                     |
| Find DNS tunneling              | Very long DNS query strings                      |

## 11.2 Tcpdump Quick Reference (Linux)

Capture by host: tcpdump -i any -w capture.pcap host ip-address

Capture by port: tcpdump -i any -w capture.pcap port 443

Capture by network: tcpdump -i any -w capture.pcap net 10.0.0.0/24

Read with filter: tcpdump -r capture.pcap 'host ip-address and port 443'

## 11.3 Wireshark Display Filters

| Filter Purpose | Filter                         |
| -------------- | ------------------------------ |
| Specific host  | ip.addr == ip-address          |
| Specific port  | tcp.port == 443                |
| HTTP only      | http                           |
| DNS queries    | dns.qry.name contains "domain" |
| TLS only       | tls                            |
| Failed TCP     | tcp.flags.reset == 1           |
| Large packets  | frame.len > 1000               |

---

# 12. Email Security Quick Reference (Mandatory)

## 12.1 Microsoft Defender for Office 365 (KQL)

Suspicious emails to user: EmailEvents pipe where TenantId equals "tenant-id" pipe where RecipientEmailAddress equals "user@domain" pipe where TimeGenerated greater than ago(24h) pipe project TimeGenerated, Subject, SenderFromAddress, ThreatTypes, DeliveryAction

Bulk phishing campaign: EmailEvents pipe where TenantId equals "tenant-id" pipe where ThreatTypes has "Phish" pipe summarize Count equals count() by Subject, SenderFromAddress pipe where Count greater than 5

### 12.1.1 Containment

| Action            | Method                                                |
| ----------------- | ----------------------------------------------------- |
| Soft delete email | Via portal: Hunting then Take action                  |
| Block sender      | New-TenantAllowBlockListItems -ListType Sender -Block |
| Block URL         | New-TenantAllowBlockListItems -ListType Url -Block    |

## 12.2 Proofpoint / Mimecast / Generic Gateway

| Action             | Pattern                   |
| ------------------ | ------------------------- |
| Search by sender   | Filter by sender domain   |
| Search by subject  | Subject contains pattern  |
| Quarantine release | Per platform admin action |
| Add to deny list   | Per platform admin action |

---

# 13. Forensics Tools Quick Reference (Mandatory)

## 13.1 Memory Acquisition

| Tool             | Quick Command                                      |
| ---------------- | -------------------------------------------------- |
| WinPMEM          | winpmem.exe -o memory.raw                          |
| FTK Imager (CLI) | ftkimager --memdump memory.raw                     |
| DumpIt           | DumpIt.exe /OUTPUT C:\memory.raw                   |
| LiME (Linux)     | insmod lime.ko "path=/mnt/memory.lime format=lime" |
| AVML (Linux)     | avml memory.lime                                   |

## 13.2 Volatility 3 Quick Commands

Process list: vol -f memory.raw windows.pslist

Process tree: vol -f memory.raw windows.pstree

Network connections: vol -f memory.raw windows.netscan

Command line history: vol -f memory.raw windows.cmdline

Loaded DLLs per process: vol -f memory.raw windows.dlllist --pid pid

Malfind (injected code): vol -f memory.raw windows.malfind

Hash dump (credentials): vol -f memory.raw windows.hashdump

Registry hive list: vol -f memory.raw windows.registry.hivelist

## 13.3 Disk Acquisition

| Tool       | Quick Command                                                      |
| ---------- | ------------------------------------------------------------------ |
| dd (Linux) | dd if=/dev/sda of=disk.img bs=4M status=progress conv=sync,noerror |
| dcfldd     | dcfldd if=/dev/sda hash=sha256 of=disk.img                         |
| FTK Imager | GUI or ftkimager source dest                                       |
| EnCase     | Via EnCase imaging                                                 |

## 13.4 Hash Verification (Always After Acquisition)

Linux: sha256sum disk.img greater than disk.img.sha256

Windows PowerShell: Get-FileHash disk.img -Algorithm SHA256

## 13.5 Velociraptor Quick Hunts

File hash hunt: SELECT star FROM hash(path equals 'C:\Windows\System32\file', hashselect equals ['MD5','SHA1','SHA256'])

Recent process executions: SELECT star FROM Artifact.Windows.Forensics.Prefetch()

Recently modified files: SELECT star FROM glob(globs equals 'C:\Users\star\Desktop\star') WHERE Mtime greater than timestamp(epoch equals ts)

---

# 14. Threat Intelligence Enrichment Quick Reference (Mandatory)

## 14.1 IoC Lookup Patterns

| IoC Type   | Lookup Sources                                |
| ---------- | --------------------------------------------- |
| IP address | VirusTotal, AbuseIPDB, TI platform, GreyNoise |
| Domain     | VirusTotal, URLScan, TI platform, WHOIS       |
| URL        | VirusTotal, URLScan, Phishtank                |
| File hash  | VirusTotal, hybrid-analysis, TI platform      |
| Email      | EmailRep, TI platform                         |
| CVE        | NVD, vendor advisories, TI platform           |

## 14.2 Generic TI Platform Query Patterns

IoC reputation: ioc equals "value" type equals "ip or domain or url or hash"

Actor TTPs: actor equals "actor-name"

Campaign IoCs: campaign equals "campaign-name"

Recent indicators: created greater than now-7d severity greater than or equal high

## 14.3 VirusTotal API Quick Reference

IP lookup: GET https://www.virustotal.com/api/v3/ip_addresses/ip with header x-apikey: api-key

File hash lookup: GET https://www.virustotal.com/api/v3/files/sha256 with header x-apikey: api-key

URL submission: POST https://www.virustotal.com/api/v3/urls with header x-apikey: api-key and data url equals url

---

# 15. OS Native Commands Quick Reference (Mandatory)

## 15.1 Windows Investigation

Network connections: netstat -anob

Process list: tasklist /v OR wmic process get name,processid,parentprocessid,commandline

Scheduled tasks: schtasks /query /fo LIST /v

Services: sc query type=service

Running PowerShell: Get-Process powershell

Registry run keys: reg query HKLM\Software\Microsoft\Windows\CurrentVersion\Run AND reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Run

Event log query: wevtutil qe Security /c:50 /rd:true /f:text

## 15.2 Linux Investigation

Network connections: ss -anptu OR netstat -anptu

Process tree: ps auxf OR pstree

Recently modified files: find / -mtime -1 -type f 2 greater than /dev/null

Logged in users: w OR last -a pipe head -50

Cron jobs: crontab -l AND ls -la /etc/cron.star

Open files by process: lsof -p pid

Loaded kernel modules: lsmod

Recent auth events: tail -100 /var/log/auth.log OR journalctl -u sshd --since "1 hour ago"

## 15.3 macOS Investigation

Process list: ps aux

Launch agents and daemons: ls -la /Library/LaunchAgents /Library/LaunchDaemons ~/Library/LaunchAgents

Login items: osascript -e 'tell application "System Events" to get login items'

Recent unified log: log show --last 1h --predicate 'process == "process"'

---

# 16. SOAR Action Quick Reference (Mandatory)

## 16.1 Common SOAR Playbook Actions

| Action                | Use Case                         |
| --------------------- | -------------------------------- |
| Enrich IoC            | Add TI context to alert          |
| Block IoC             | Push to firewall or EDR or proxy |
| Isolate endpoint      | EDR isolation                    |
| Disable user          | IdP user disable                 |
| Quarantine email      | Email security action            |
| Create ticket         | Ticketing system                 |
| Notify on-call        | Page or SMS or email             |
| Send approval request | Manager approval workflow        |
| Run query in SIEM     | SIEM API                         |
| Run EDR investigation | EDR API                          |

## 16.2 SOAR Best Practices

| Practice                       | Detail              |
| ------------------------------ | ------------------- |
| Tenant scope in every action   | Mandatory           |
| Approval gates for high-impact | Mandatory           |
| Audit logging                  | Every action logged |
| Rollback capability            | Where feasible      |
| Per-client SOAR customization  | Per tenant          |

---

# 17. Containment Authority Quick Reference (Mandatory)

| Action                                  | Default Authority                 | Per-Client Override |
| --------------------------------------- | --------------------------------- | ------------------- |
| Block IoC at MSSP perimeter             | L2 plus                           | Per client          |
| EDR isolate single endpoint             | L2 plus per-client policy         | Per client          |
| EDR isolate critical asset (server, DC) | IR Team plus per-client SDM       | Per client          |
| Disable standard user                   | L2 plus per-client policy         | Per client          |
| Disable privileged user                 | IR Team plus per-client SDM       | Per client          |
| Disable executive account               | IR Team Lead plus per-client CISO | Per client          |
| Force password reset (bulk)             | IR Team plus per-client SDM       | Per client          |
| Network segment isolation               | IR Team plus per-client CISO      | Per client          |
| Cloud account suspension                | IR Team Lead plus per-client CISO | Per client          |
| Service stop on production              | IR Team Lead plus per-client CISO | Per client          |

Reference:

- 03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md

---

# 18. Common Pitfalls (Avoid These)

| Pitfall                                          | Correct Behavior                         |
| ------------------------------------------------ | ---------------------------------------- |
| Running query without tenant filter              | Always include tenant filter first       |
| Executing containment without authority          | Verify per-client authority              |
| Cross-tenant query by unauthorized role          | Restricted to TI Lead plus Detection Eng |
| Quick command without logging context            | Always document context                  |
| Reusing personal notes instead of this reference | Use validated reference                  |
| Skipping hash verification post-acquisition      | Always verify                            |
| Sharing screenshot with another tenant data      | Sanitize before sharing                  |

---

# 19. Quarterly Update Process (Mandatory)

| Step | Action                            | Owner              | Cadence   |
| ---- | --------------------------------- | ------------------ | --------- |
| 1    | Tool platform changes review      | Detection Eng Lead | Quarterly |
| 2    | New query patterns from incidents | IR Team Lead       | Quarterly |
| 3    | Containment command validation    | IR Team Lead       | Quarterly |
| 4    | Multi-tenant safety review        | Compliance Lead    | Quarterly |
| 5    | Update reference document         | Detection Eng Lead | Quarterly |
| 6    | Communicate updates to SOC        | Training Lead      | Quarterly |

---

# 20. Quality Checklist (Per Update)

- [ ] All current tools represented
- [ ] All queries tested in lab or sandbox
- [ ] All containment commands have authority notes
- [ ] Multi-tenant scoping in every example
- [ ] Containment authority matrix linked
- [ ] Forensics commands current
- [ ] Cloud command syntax current
- [ ] Identity command syntax current
- [ ] OS native commands accurate
- [ ] Version updated
- [ ] CISO plus IR Team Lead approval
- [ ] SOC communication issued

---

# 21. Related Documents

| Document                         | Path                                                                               |
| -------------------------------- | ---------------------------------------------------------------------------------- |
| Attack Technique Reference       | 10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Attack-Technique-Reference.md        |
| MITRE ATT&CK Quick Reference     | 10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md      |
| Common IoC Reference             | 10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Common-IoC-Reference.md              |
| SIEM Query Library               | 04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Query-Library.md                            |
| SIEM Use Cases Master            | 04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Use-Cases-Master.md                         |
| SIEM Alert Tuning Guide          | 04_TOOLS-AND-TECHNOLOGY/04.1_SIEM/SIEM-Alert-Tuning-Guide.md                       |
| EDR Investigation Queries        | 04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Investigation-Queries.md                      |
| EDR Containment Commands         | 04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Containment-Commands.md                       |
| EDR Alert Handling Guide         | 04_TOOLS-AND-TECHNOLOGY/04.2_EDR/EDR-Alert-Handling-Guide.md                       |
| Firewall Block Request SOP       | 04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Block-Request-SOP.md        |
| Network Isolation Procedure      | 04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Isolation-Procedure.md       |
| Network Capture SOP              | 04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Capture-SOP.md               |
| Forensics Toolkit Reference      | 04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Forensics-Toolkit-Reference.md        |
| Memory Acquisition SOP           | 04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Memory-Acquisition-SOP.md             |
| Disk Acquisition SOP             | 04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Disk-Acquisition-SOP.md               |
| Log Collection SOP               | 04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Log-Collection-SOP.md                 |
| Tool Chain of Custody            | 04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Tool-Chain-of-Custody.md              |
| IRT Containment Authority Matrix | 03_SOC-TIER-PROCEDURES/03.5_IR-Team-Procedures/IRT-Containment-Authority-Matrix.md |
| Client Data Segregation Policy   | 09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md    |
| L1 Onboarding Program            | 10_TRAINING-AND-EXERCISES/10.1_Onboarding/L1-Onboarding-Program.md                 |
| L2 Onboarding Program            | 10_TRAINING-AND-EXERCISES/10.1_Onboarding/L2-Onboarding-Program.md                 |
| L3 Onboarding Program            | 10_TRAINING-AND-EXERCISES/10.1_Onboarding/L3-Onboarding-Program.md                 |

---

# 22. Revision History

| Version | Date        | Author                                        | Changes         |
| ------- | ----------- | --------------------------------------------- | --------------- |
| 1.0     | 30-May-2026 | MSSP Detection Engineering Lead / SOC Manager | Initial version |

---

# 23. Approval

Approved by:

| Role                            | Name | Signature | Date |
| ------------------------------- | ---- | --------- | ---- |
| MSSP Detection Engineering Lead |      |           |      |
| MSSP SOC Manager                |      |           |      |
| MSSP IR Team Lead               |      |           |      |
| MSSP CISO                       |      |           |      |

---

**End of Document**
