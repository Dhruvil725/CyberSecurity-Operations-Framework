# Playbook: APT Campaign – MITRE ATT&CK Mapping

---

## 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | Playbook – APT Campaign (MITRE ATT&CK Mapping)               |
| Document ID    | IR-PB-APT-MITRE-006                                          |
| Version        | 1.0                                                          |
| Effective Date | 21-May-2026                                                  |
| Owner          | Threat Intelligence Lead / L3 IR Lead                        |
| Approved By    | CISO                                                         |
| Classification | Internal – Confidential                                      |
| Review Cycle   | Quarterly and after every confirmed APT campaign             |

---

## 2. Purpose

This document provides comprehensive MITRE ATT&CK Enterprise mapping for Advanced Persistent Threat (APT) campaigns handled by the organization.

APT campaigns differ significantly from opportunistic attacks because they:

- Operate across long timeframes
- Use multiple attack stages and fallback paths
- Leverage stealth and persistence
- Reuse infrastructure strategically
- Combine malware, credential abuse, and living-off-the-land techniques
- Target specific business functions or sensitive assets
- Adapt rapidly after detection or containment

This mapping serves to:

- Standardize documentation of advanced attacker behavior
- Support structured investigation and forensic reconstruction
- Improve detection engineering and SOC coverage
- Enable ATT&CK-based threat hunting
- Support attribution analysis
- Identify monitoring and control gaps
- Align reporting with industry-standard frameworks
- Support red team and purple team exercises
- Improve long-term resilience against recurring APT campaigns

This document must be used together with:

- PB-APT-Master.md
- PB-APT-L3-Forensics.md
- PB-APT-ThreatIntel-Integration.md
- PB-APT-Attribution-Analysis.md
- PB-APT-LongTerm-Monitoring.md

---

## 3. Scope

Applies to:

- Nation-state campaigns
- Financially motivated advanced actors
- Long-term persistence operations
- Supply chain APT operations
- Hybrid cloud/on-prem APT campaigns
- Multi-stage espionage operations
- Insider-assisted advanced attacks
- Cloud-integrated APT activity

Environments covered:

- Enterprise networks
- Cloud environments
- Identity infrastructure
- Email systems
- SaaS platforms
- Kubernetes and containerized environments
- DevOps pipelines

---

## 4. ATT&CK Framework Reference

| Field | Value |
|------|------|
| Framework | MITRE ATT&CK Enterprise |
| ATT&CK Version | v14 (verify at attack.mitre.org) |
| Supplementary | ATT&CK for Cloud / Containers |
| Focus | Enterprise APT operations |

---

# 5. APT Campaign – Full ATT&CK TTP Matrix

---

# 5.1 Reconnaissance

APT campaigns often begin with long-term reconnaissance activities that may occur weeks or months before exploitation.

---

## 5.1.1 External Reconnaissance Techniques

| Technique ID | Technique Name | Description |
|--------------|---------------|-------------|
| T1595 | Active Scanning | Internet-facing service scanning |
| T1592 | Gather Victim Host Information | Identifying infrastructure versions |
| T1589 | Gather Victim Identity Information | Harvesting employee identity data |
| T1593 | Search Open Websites/Domains | OSINT gathering |
| T1596 | Search Open Technical Databases | Shodan/Censys reconnaissance |
| T1598 | Phishing for Information | Targeted credential gathering |

---

## 5.1.2 APT Recon Characteristics (IMPORTANT)

APT reconnaissance frequently includes:

- Slow distributed scanning to avoid detection
- Monitoring employee social media profiles
- Collection of VPN and SSO portal information
- Mapping third-party vendors and MSP relationships
- Identifying cloud providers and SaaS platforms used
- Monitoring public Git repositories for secrets

---

# 5.2 Initial Access (CRITICAL)

APT initial access methods are usually highly targeted and carefully planned.

---

## 5.2.1 Initial Access Techniques

| Technique ID | Technique Name | Description |
|--------------|---------------|-------------|
| T1190 | Exploit Public-Facing Application | Exploiting internet-facing service |
| T1133 | External Remote Services | VPN/RDP compromise |
| T1078 | Valid Accounts | Stolen credentials |
| T1566.001 | Spearphishing Attachment | Malicious document delivery |
| T1566.002 | Spearphishing Link | Credential harvesting |
| T1195 | Supply Chain Compromise | Vendor or software compromise |
| T1189 | Drive-by Compromise | Browser-based exploitation |
| T1199 | Trusted Relationship | MSP/vendor access abuse |

---

## 5.2.2 Common APT Entry Targets

| Target | Why High Value |
|--------|----------------|
| VPN gateways | Remote enterprise access |
| OWA / Exchange | Email and credentials |
| SSO portals | Enterprise-wide access |
| Cloud admin accounts | Broad cloud control |
| Citrix / VDI | Remote desktop access |
| Web applications | Initial foothold |

---

## 5.2.3 Initial Access Indicators

Indicators requiring immediate escalation:

- Login from impossible geography
- MFA bypass
- OAuth consent abuse
- New VPN enrollment
- Authentication success after repeated failures
- Exploit followed by shell execution

---

# 5.3 Execution

APT actors frequently rely on living-off-the-land execution to reduce detection.

---

## 5.3.1 Execution Techniques

| Technique ID | Technique Name | Description |
|--------------|---------------|-------------|
| T1059.001 | PowerShell | Encoded PowerShell |
| T1059.003 | CMD | Windows command execution |
| T1059.004 | Unix Shell | Linux shell execution |
| T1059.005 | Visual Basic | Script execution |
| T1204 | User Execution | User-triggered execution |
| T1106 | Native API | Direct API usage |
| T1218 | Signed Binary Proxy Execution | LOLBin abuse |

---

## 5.3.2 Common LOLBins Used by APT Actors

| LOLBin | Typical Usage |
|--------|---------------|
| rundll32.exe | DLL execution |
| regsvr32.exe | Remote script execution |
| mshta.exe | HTA execution |
| powershell.exe | In-memory execution |
| certutil.exe | File download |
| wmic.exe | Remote execution |

---

# 5.4 Persistence (IMPORTANT)

Persistence is a defining characteristic of APT campaigns.

APT actors typically establish multiple redundant persistence mechanisms so that removal of one access path does not eliminate attacker presence.

---

## 5.4.1 Persistence Techniques

| Technique ID | Technique Name | Description |
|--------------|---------------|-------------|
| T1053.005 | Scheduled Task | Recurring execution |
| T1547.001 | Registry Run Keys | Startup persistence |
| T1543.003 | Windows Service | Service installation |
| T1136 | Create Account | Backdoor account |
| T1505 | Server Software Component | Web shell |
| T1546 | Event Triggered Execution | WMI persistence |
| T1098 | Account Manipulation | Privileged account changes |

---

## 5.4.2 Advanced Persistence Patterns

APT persistence often includes:

- Dormant accounts activated months later
- Secondary hidden admin accounts
- Cloud IAM persistence
- Kerberos Golden Ticket capability
- Multiple scheduled tasks with random naming
- Registry modifications hidden under legitimate software paths
- Modified startup scripts on Linux systems
- Persistence in backup or disaster recovery systems

---

## 5.4.3 Persistence Detection Priorities

SOC must prioritize detection of:

- New service installation
- Unauthorized scheduled tasks
- WMI subscription creation
- New privileged account creation
- Cloud IAM role modifications
- SSH authorized_keys changes

---

# 5.5 Privilege Escalation

APT actors escalate privileges strategically rather than immediately.

---

## 5.5.1 Privilege Escalation Techniques

| Technique ID | Technique Name | Description |
|--------------|---------------|-------------|
| T1068 | Exploitation for Privilege Escalation | Kernel exploit |
| T1548 | Abuse Elevation Control Mechanism | UAC bypass |
| T1134 | Access Token Manipulation | Token impersonation |
| T1484 | Domain Policy Modification | GPO abuse |
| T1098 | Account Manipulation | Group membership abuse |

---

## 5.5.2 High-Risk Escalation Indicators

| Indicator | Significance |
|-----------|-------------|
| Domain Admin added unexpectedly | Critical |
| New GPO linked to admin OU | Critical |
| SYSTEM shell after low-priv login | High |
| LSASS access after service exploit | High |

---

# 5.6 Defense Evasion (CRITICAL)

APT actors prioritize stealth heavily.

---

## 5.6.1 Defense Evasion Techniques

| Technique ID | Technique Name | Description |
|--------------|---------------|-------------|
| T1562 | Impair Defenses | Disable security controls |
| T1562.001 | Disable or Modify Tools | Disable EDR |
| T1562.008 | Disable Cloud Logs | Logging suppression |
| T1070 | Indicator Removal | Log deletion |
| T1027 | Obfuscated Files or Information | Encoded payloads |
| T1036 | Masquerading | Legitimate process names |
| T1218 | Signed Binary Proxy Execution | LOLBin abuse |

---

## 5.6.2 Evasion Patterns

APT actors frequently:

- Use signed binaries for execution
- Clear logs selectively rather than globally
- Disable only specific logging sources
- Use low-and-slow beaconing
- Hide within normal admin activity
- Use encrypted C2 channels
- Rotate infrastructure frequently

---

# 5.7 Credential Access

Credential theft is central to APT operations.

---

## 5.7.1 Credential Access Techniques

| Technique ID | Technique Name | Description |
|--------------|---------------|-------------|
| T1003 | OS Credential Dumping | LSASS dumping |
| T1555 | Credentials from Password Stores | Browser theft |
| T1552 | Unsecured Credentials | Config file theft |
| T1550 | Use Alternate Authentication Material | Pass-the-Hash |
| T1110 | Brute Force | Password spraying |
| T1040 | Network Sniffing | Credential interception |

---

## 5.7.2 Credential Targets

APT actors frequently target:

- Domain admin credentials
- Service account credentials
- Cloud administrator tokens
- VPN credentials
- Password managers
- Browser session cookies

---

# 5.8 Discovery

APT actors perform extensive internal discovery.

---

## 5.8.1 Discovery Techniques

| Technique ID | Technique Name | Description |
|--------------|---------------|-------------|
| T1082 | System Information Discovery | Host profiling |
| T1018 | Remote System Discovery | Internal host mapping |
| T1046 | Network Service Discovery | Port scanning |
| T1069 | Permission Groups Discovery | Privileged group mapping |
| T1087 | Account Discovery | User enumeration |
| T1482 | Domain Trust Discovery | Trust relationship mapping |

---

# 5.9 Lateral Movement

APT lateral movement is usually methodical and privilege-driven.

---

## 5.9.1 Lateral Movement Techniques

| Technique ID | Technique Name | Description |
|--------------|---------------|-------------|
| T1021.001 | RDP | Interactive movement |
| T1021.002 | SMB/Admin Shares | File share movement |
| T1021.004 | SSH | Linux pivoting |
| T1550.002 | Pass-the-Hash | NTLM replay |
| T1550.003 | Pass-the-Ticket | Kerberos replay |
| T1210 | Exploitation of Remote Services | Internal exploitation |

---

## 5.9.2 High-Risk Movement Indicators

| Indicator | Risk |
|-----------|------|
| Workstation initiating RDP to server | High |
| Service account authenticating interactively | High |
| Kerberos anomalies | Critical |
| Lateral movement into backup systems | Critical |

---

# 5.10 Collection

APT campaigns collect sensitive data systematically.

---

## 5.10.1 Collection Techniques

| Technique ID | Technique Name | Description |
|--------------|---------------|-------------|
| T1005 | Data from Local System | File collection |
| T1039 | Data from Network Shared Drive | Shared drive collection |
| T1119 | Automated Collection | Scripted collection |
| T1074 | Data Staging | Temporary staging |
| T1560 | Archive Collected Data | Compression before exfil |

---

# 5.11 Command and Control

APT C2 infrastructure is often resilient and redundant.

---

## 5.11.1 C2 Techniques

| Technique ID | Technique Name | Description |
|--------------|---------------|-------------|
| T1071.001 | Web Protocols | HTTPS C2 |
| T1071.004 | DNS | DNS tunneling |
| T1573 | Encrypted Channel | TLS encryption |
| T1090 | Proxy | Domain fronting |
| T1102 | Web Service | Cloud relay |

---

## 5.11.2 C2 Characteristics

APT C2 often demonstrates:

- Long beacon intervals
- Consistent packet sizes
- Cloud-hosted relay infrastructure
- TLS certificate reuse
- DGA-generated domains
- Fallback channels

---

# 5.12 Exfiltration

APT exfiltration prioritizes stealth over speed.

---

## 5.12.1 Exfiltration Techniques

| Technique ID | Technique Name | Description |
|--------------|---------------|-------------|
| T1041 | Exfiltration Over C2 Channel | Encrypted exfil |
| T1567 | Exfiltration Over Web Service | Cloud storage upload |
| T1020 | Automated Exfiltration | Scripted transfer |
| T1030 | Data Transfer Size Limits | Chunked transfer |

---

## 5.12.2 Common Exfiltration Targets

| Target | Typical Value |
|--------|---------------|
| Intellectual property | Strategic value |
| Source code | Supply chain leverage |
| Customer databases | Financial value |
| Credentials | Continued access |
| Financial data | Fraud or extortion |

---

# 5.13 Impact

APT campaigns may culminate in disruption or extortion.

---

## 5.13.1 Impact Techniques

| Technique ID | Technique Name | Description |
|--------------|---------------|-------------|
| T1486 | Data Encrypted for Impact | Ransomware |
| T1485 | Data Destruction | Destructive attack |
| T1490 | Inhibit System Recovery | Backup destruction |
| T1499 | Endpoint DoS | Service disruption |

---

# 6. ATT&CK Coverage Validation

Organizations must regularly assess:

- Which ATT&CK techniques are detectable
- Which techniques are partially visible
- Which techniques have no monitoring coverage

---

## 6.1 Coverage Matrix

| Technique | Detection Coverage | Tool Source | Gap? |
|-----------|------------------|-------------|------|
|           |                  |             |      |

---

# 7. ATT&CK-Based Threat Hunting (IMPORTANT)

APT ATT&CK mapping must directly support proactive hunting.

---

## 7.1 Hunting Priorities

| Hunt Type | Objective |
|----------|-----------|
| Authentication hunt | Detect dormant account usage |
| DNS hunt | Detect new actor infrastructure |
| PowerShell hunt | Detect encoded execution |
| Lateral movement hunt | Detect RDP/SMB anomalies |
| Persistence hunt | Detect hidden tasks/services |

---

# 8. Detection Engineering Recommendations

Detection engineering should prioritize:

- Behavioral detection over signatures
- Long-term beaconing analysis
- Credential abuse detection
- Service account anomaly detection
- Cloud IAM monitoring
- DNS anomaly detection
- Memory injection detection

---

# 9. MSSP Considerations

For MSSP-managed environments:

- Maintain ATT&CK coverage per client
- Separate actor tracking per tenant
- Avoid cross-client assumptions
- Share generalized TTP intelligence safely

---

# 10. Common ATT&CK Mapping Mistakes

| Mistake | Risk |
|---------|------|
| Mapping only malware behavior | Missed campaign scope |
| Ignoring cloud techniques | Partial visibility |
| Focusing only on IoCs | Missed behavioral indicators |
| Not updating mappings post-incident | Stale detection logic |

---

## 11. Related Documents

| Document | Path |
|----------|------|
| APT Master | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-Master.md` |
| APT L3 Forensics | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-L3-Forensics.md` |
| APT Threat Intel Integration | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-ThreatIntel-Integration.md` |
| APT Long-Term Monitoring | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-LongTerm-Monitoring.md` |
| APT Attribution Analysis | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-Attribution-Analysis.md` |
| MITRE ATT&CK Reference | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md` |

---

## 12. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 21-May-2026 | Threat Intelligence Lead | Initial version |

---

## 13. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**