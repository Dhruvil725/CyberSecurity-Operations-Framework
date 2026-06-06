# Playbook: Network Intrusion – L3 Forensics

---

## 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | Playbook – Network Intrusion (L3 Forensics)                  |
| Document ID    | IR-PB-NI-004                                                 |
| Version        | 1.0                                                          |
| Effective Date | 21-May-2026                                                  |
| Owner          | L3 Lead / Incident Response Team Lead                        |
| Approved By    | CISO                                                         |
| Classification | Internal – Confidential                                      |
| Review Cycle   | Quarterly and after any P1/P2 network intrusion incident     |

---

## 2. Purpose

This document defines the Level 3 (L3) forensic procedures for network intrusion incidents.

L3 investigation is required when:

- Advanced attacker techniques are suspected
- Malware reverse engineering is required
- Memory forensics is needed
- Packet-level analysis is required
- Domain controller compromise is suspected
- Data exfiltration must be validated at forensic level
- Attribution or APT-level tradecraft is identified

L3 objectives:

- Conduct deep forensic analysis across network and host layers
- Reconstruct attacker tradecraft and tooling
- Identify all persistence mechanisms
- Validate scope beyond L2 findings
- Confirm data exfiltration at forensic level
- Support legal and regulatory documentation
- Provide technically defensible evidence
- Support law enforcement engagement if required

L3 must produce:

- Forensic evidence package
- Confirmed attacker TTP mapping
- Detailed timeline with artifact references
- Root cause analysis inputs
- Technical deep-dive report
- Detection improvement recommendations

---

## 3. Scope

Applies to advanced forensic investigation of:

- Multi-stage network intrusions
- APT-style attacks
- Domain controller compromise
- Advanced lateral movement
- Credential dumping cases
- C2 frameworks (e.g., Cobalt Strike)
- Encrypted tunneling mechanisms
- DNS tunneling
- Memory-resident malware
- Data exfiltration confirmation
- Hybrid network-cloud intrusions
- MSSP critical client incidents

---

## 4. Preconditions (Inputs from L2)

Before L3 begins, confirm:

| Required Input                     | Minimum Content                                |
| ---------------------------------- | ---------------------------------------------- |
| Confirmed intrusion status         | Confirmed / Highly likely                      |
| Affected host inventory            | List of compromised systems                    |
| Timeline from L2                   | Preliminary UTC timeline                       |
| Identified entry point             | Known or suspected                             |
| Lateral movement assessment        | Summary                                        |
| C2 indicators                      | IPs/domains/beaconing patterns                 |
| Evidence exported                  | Logs, PCAP, authentication logs                |
| Containment status                 | Actions already taken                          |
| Escalation rationale               | Why L3 engagement required                     |

Reference:
`02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-L2-Investigation.md`

---

## 5. L3 Required Outputs

| Output                              | Required Detail                                       |
| ----------------------------------- | ----------------------------------------------------- |
| Forensic evidence summary           | Host and network artifacts                            |
| Confirmed attack chain              | Mapped to MITRE ATT&CK                                |
| Advanced persistence identification | Hidden tasks, registry, WMI, services, implants      |
| Credential compromise confirmation  | Dumping evidence and scope                            |
| C2 framework identification         | Tool fingerprint confirmation                         |
| Data exfiltration validation        | Forensic-level confirmation                           |
| Attribution indicators              | Threat actor linkage if applicable                    |
| Root cause input                    | Technical cause for RCA                               |
| Detection improvement list          | New detection recommendations                         |

---

# 6. Forensic Investigation Workflow

| Phase   | Goal                                               | Output                                |
| ------- | -------------------------------------------------- | -------------------------------------- |
| Phase 1 | Secure and preserve evidence                       | Chain-of-custody initiated             |
| Phase 2 | Host forensic acquisition                          | Disk and memory images                |
| Phase 3 | Network forensic analysis                          | PCAP deep analysis                    |
| Phase 4 | Malware analysis                                   | Payload identification                 |
| Phase 5 | Credential compromise validation                   | Dump verification                     |
| Phase 6 | Persistence discovery                              | Hidden mechanisms identified           |
| Phase 7 | Exfiltration forensic validation                   | Confirmed data theft or ruled out      |
| Phase 8 | MITRE TTP mapping                                  | ATT&CK technique confirmation          |
| Phase 9 | Final technical report                             | L3 report submission                   |

---

# 7. Phase 1 – Evidence Preservation

Before deep investigation begins:

- Confirm affected hosts are isolated but not powered off (unless required)
- Preserve volatile memory before reboot
- Export firewall and IDS logs immediately
- Preserve NetFlow and DNS logs
- Preserve VPN logs
- Preserve Active Directory logs
- Hash all exported artifacts
- Document evidence handling chain-of-custody

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 7.1 Chain-of-Custody Table

| Evidence ID | Description | Source System | Collected By | Hash | Storage Location |
|-------------|------------|--------------|-------------|------|-----------------|
|             |            |              |             |      |                 |

---

# 8. Phase 2 – Host Forensic Acquisition

---

## 8.1 Memory Acquisition

Memory analysis is critical for detecting:

- In-memory malware
- Injected processes
- Cobalt Strike beacons
- LSASS credential dumps
- Unlinked DLLs
- Active network connections

Memory acquisition requirements:

- Use approved forensic toolkit
- Acquire full memory image
- Generate SHA256 hash
- Document acquisition time (UTC)
- Store in secure evidence repository

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Memory-Acquisition-SOP.md`

---

## 8.2 Disk Acquisition

Disk imaging required when:

- Malware persistence suspected
- Web shells suspected
- Domain controller compromise suspected
- Data exfiltration suspected

Disk acquisition requirements:

- Full disk image or targeted acquisition
- Preserve file system metadata
- Hash before and after acquisition
- Store image securely

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.6_Forensics-Tools/Disk-Acquisition-SOP.md`

---

# 9. Phase 3 – Network Forensic Analysis

---

## 9.1 Packet Capture Analysis

L3 must analyze PCAP files to:

- Identify exploit payload delivery
- Confirm C2 traffic patterns
- Extract malware payloads
- Validate encrypted tunneling
- Identify protocol misuse
- Confirm exfiltration payloads

PCAP analysis tasks:

- Filter traffic by compromised host
- Reconstruct HTTP sessions
- Analyze DNS query payload size
- Identify TLS fingerprint (JA3)
- Extract suspicious files
- Identify beacon intervals
- Validate encryption method used

---

## 9.2 Beaconing Pattern Validation

| Indicator                      | Confirmation Method                      |
| ------------------------------ | ---------------------------------------- |
| Fixed interval connections     | Time delta analysis                      |
| Small consistent packet size   | Payload size comparison                  |
| External IP persistence        | IP reputation check                      |
| HTTP POST with base64 payload  | Content decoding                         |

---

# 10. Phase 4 – Malware Analysis

If malicious binaries or scripts are identified:

---

## 10.1 Static Analysis

- Hash file and compare with known malware databases
- Extract strings
- Review embedded URLs and IPs
- Identify suspicious API calls
- Identify packers or obfuscation

---

## 10.2 Dynamic Analysis

- Execute in sandbox
- Observe network behavior
- Capture runtime C2 endpoints
- Identify dropped files
- Identify persistence mechanism

---

## 10.3 Common Network Intrusion Tools

| Tool/Framework | Indicators |
|---------------|-----------|
| Cobalt Strike | Beaconing, named pipes, HTTP POST patterns |
| Metasploit    | Reverse shell signatures |
| Mimikatz      | LSASS memory access |
| PowerShell Empire | Encoded PowerShell commands |
| Sliver C2     | Custom TLS fingerprint |
| Rclone        | Cloud exfiltration patterns |
| PsExec        | SMB service execution |

---

# 11. Phase 5 – Credential Compromise Validation

---

## 11.1 LSASS Dump Analysis

Confirm:

- LSASS process access events
- Dump file presence
- EDR memory alerts
- Mimikatz signature evidence

Check Windows Event IDs:
- 4624 (logon)
- 4672 (privileged logon)
- 4688 (process creation)
- 4656 (object access to LSASS)

---

## 11.2 Kerberos and NTLM Abuse

Check for:

- Pass-the-Hash
- Pass-the-Ticket
- Golden Ticket indicators
- Abnormal ticket lifetimes
- Unusual service ticket requests

---

# 12. Phase 6 – Persistence Discovery

---

## 12.1 Windows Persistence

| Mechanism | Evidence Source |
|-----------|-----------------|
| Scheduled Tasks | Event ID 4698 |
| Services | Event ID 7045 |
| Registry Run Keys | Registry hive |
| WMI Event Subscription | WMI logs |
| Startup Folder | File system |
| Group Policy | GPO change logs |

---

## 12.2 Linux Persistence

| Mechanism | Evidence Source |
|-----------|-----------------|
| Cron jobs | /var/spool/cron |
| Systemd services | /etc/systemd/system |
| SSH keys | ~/.ssh/authorized_keys |
| Bash profile modifications | .bashrc |

---

# 13. Phase 7 – Exfiltration Forensic Validation

L3 must confirm exfiltration at packet or artifact level.

---

## 13.1 Validation Steps

- Extract files transferred in PCAP
- Confirm compression/archive artifacts
- Identify cloud upload API usage
- Decode base64 DNS payloads
- Validate file hashes against sensitive repositories
- Confirm data classification of transferred files

---

## 13.2 Exfiltration Confirmation Table

| Host | Method | Data Type | Volume | Confirmed? | Evidence Ref |
|------|--------|----------|--------|-----------|--------------|
|      |        |          |        |           |              |

---

# 14. Phase 8 – MITRE ATT&CK Mapping

L3 must map confirmed attacker activity to MITRE techniques.

Example mapping:

| Tactic | Technique ID | Description |
|--------|-------------|------------|
| Initial Access | T1190 | Exploit Public-Facing Application |
| Execution | T1059.001 | PowerShell |
| Persistence | T1053.005 | Scheduled Task |
| Credential Access | T1003.001 | LSASS Dump |
| Lateral Movement | T1021.002 | SMB |
| C2 | T1071.001 | HTTPS |
| Exfiltration | T1041 | Over C2 Channel |

Reference:
`02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-MITRE-Mapping.md`

---

# 15. Root Cause Analysis Input

L3 must provide technical root cause:

- Vulnerability exploited?
- Credential reused?
- MFA disabled?
- Patch missing?
- Segmentation misconfiguration?
- Logging gap?
- Monitoring gap?

These findings feed into:

`08_POST-INCIDENT/08.2_Root-Cause-Analysis/`

---

# 16. Escalation Criteria

---

## 16.1 Escalate to IR Team if:

| Condition | Reason |
|----------|--------|
| Domain controller compromise confirmed | Enterprise-wide risk |
| Data exfiltration confirmed | Regulatory impact |
| APT activity identified | Crisis-level response |
| Multi-segment compromise | Large-scale containment needed |
| Ransomware deployment observed | Immediate business impact |

---

# 17. Reporting Requirements

L3 must deliver:

- Technical deep-dive report
- Executive summary
- MITRE mapping summary
- Evidence inventory
- Containment effectiveness assessment
- Detection gap recommendations

Reference:
`07_REPORTING/07.1_Incident-Reports/Technical-Deep-Dive-Template.md`

---

# 18. Common L3 Mistakes to Avoid

| Mistake | Risk |
|---------|------|
| Not preserving volatile memory | Lost malware evidence |
| Failing to correlate host and network logs | Incomplete scope |
| Ignoring DNS telemetry | Missed C2 |
| Overlooking time normalization | Timeline errors |
| Not validating encryption fingerprint | Missed C2 tool identification |
| Failing to document evidence chain | Legal inadmissibility |

---

# 19. MSSP Considerations

For MSSP:

- Segregate forensic artifacts per client
- Maintain client-specific evidence storage
- Follow contractual notification timelines
- Coordinate with client IR teams
- Protect cross-client infrastructure integrity

---

## 20. Related Documents

| Document | Path |
|----------|------|
| Network Intrusion Master | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-Master.md` |
| Network Intrusion L2 | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-L2-Investigation.md` |
| Network Intrusion Containment | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-Containment.md` |
| Network Intrusion MITRE Mapping | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-MITRE-Mapping.md` |
| Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |
| Malware Analysis SOP | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Malware-Analysis-SOP.md` |
| Memory Forensics SOP | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Memory-Forensics-SOP.md` |
| Disk Forensics SOP | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Disk-Forensics-SOP.md` |

---

## 21. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 21-May-2026 | L3 Lead / IR Team Lead | Initial version |

---

## 22. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**