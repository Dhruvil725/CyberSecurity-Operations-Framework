# Playbook: APT Campaign – L3 Forensics

---

## 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | Playbook – APT Campaign (L3 Forensics)                       |
| Document ID    | IR-PB-APT-002                                                |
| Version        | 1.0                                                          |
| Effective Date | 21-May-2026                                                  |
| Owner          | L3 Lead / Incident Response Team Lead                        |
| Approved By    | CISO                                                         |
| Classification | Internal – Confidential                                      |
| Review Cycle   | Quarterly and after any confirmed APT campaign               |

---

## 2. Purpose

This document defines the Level 3 (L3) forensic investigation procedures for Advanced Persistent Threat (APT) campaigns.

APT forensics represents the most complex category of incident investigation because:

- Dwell time may extend months or years
- Attacker behavior is deliberately stealthy
- Multiple overlapping persistence mechanisms exist
- Custom tooling may evade signature detection
- Evidence may be deliberately destroyed
- Investigation must balance intelligence gathering with containment
- Attribution analysis requires specialized tradecraft
- Legal implications may require strict evidence handling

L3 APT forensics objectives:

- Establish full historical dwell time
- Reconstruct complete attack chain across all stages
- Identify all compromised systems
- Map all persistence mechanisms
- Validate credential theft scope
- Confirm data exfiltration
- Extract and analyze custom malware
- Provide attribution indicators
- Support legal proceedings if required
- Enable complete eradication

This document is used alongside:

- PB-APT-Master.md
- PB-APT-ThreatIntel-Integration.md
- PB-APT-Attribution-Analysis.md

---

## 3. Scope

Applies to:

- Multi-stage APT campaign forensics
- Nation-state or organized threat actor investigations
- Long-dwell intrusion investigations
- Custom malware analysis
- Domain-wide compromise forensics
- Cloud-hybrid APT investigations
- Insider-assisted APT investigations
- Supply chain APT campaigns

---

## 4. Preconditions (Inputs from IR Team)

Before beginning L3 forensics, confirm:

| Required Input | Minimum Content |
|----------------|----------------|
| Confirmed APT indicators | Multiple TTPs |
| Affected asset list | Hostnames and IPs |
| Initial dwell time estimate | UTC based |
| Known C2 infrastructure | IPs and domains |
| Containment status | Actions taken |
| Evidence preservation status | Logs and snapshots |
| Legal hold confirmed | Yes/No |

---

## 5. L3 Forensic Objectives

| Output | Required Detail |
|--------|----------------|
| Full dwell timeline | UTC high-resolution |
| Complete persistence inventory | All mechanisms |
| Lateral movement map | All pivot paths |
| Credential compromise scope | All dumped credentials |
| C2 infrastructure profile | All endpoints |
| Malware analysis | Custom toolset |
| Data exfiltration validation | Volume and content |
| Attribution indicators | TTP and infrastructure match |
| Evidence package | Chain-of-custody records |

---

# 6. Forensic Workflow

| Phase | Objective | Output |
|-------|----------|--------|
| Phase 1 | Evidence preservation | CoC records |
| Phase 2 | Dwell time investigation | Historical timeline |
| Phase 3 | Memory forensics | In-memory artifact extraction |
| Phase 4 | Disk forensics | Filesystem artifact analysis |
| Phase 5 | Network forensics | C2 and exfiltration analysis |
| Phase 6 | Malware analysis | Custom tool identification |
| Phase 7 | Credential analysis | Compromise scope |
| Phase 8 | Lateral movement reconstruction | Full pivot map |
| Phase 9 | Exfiltration validation | Data theft confirmation |
| Phase 10 | Attribution | Threat actor linkage |

---

# 7. Phase 1 – Evidence Preservation (CRITICAL)

APT evidence preservation requires strict procedures because:

- Evidence may span months of logs
- Attackers may have tampered with logs
- Legal proceedings may require court-admissible evidence
- Multiple systems require simultaneous preservation

---

## 7.1 Evidence Preservation Requirements

| Evidence Type | Priority | Method |
|--------------|---------|--------|
| Memory images | Critical | Immediate acquisition |
| Disk images | High | Before containment where possible |
| Network logs | Critical | Export before rotation |
| Authentication logs | Critical | Include all domain controllers |
| DNS logs | High | Extended historical export |
| EDR telemetry | Critical | Full historical export |
| Email logs | High | Mail server export |
| Cloud audit logs | High | Export immediately |

All evidence must be hashed immediately after collection.

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 7.2 Chain-of-Custody Table

| Evidence ID | Type | Source System | Collected By | Hash | Storage Location |
|-------------|------|--------------|--------------|------|-----------------|
|             |      |              |              |      |                 |

---

# 8. Phase 2 – Dwell Time Investigation (IMPORTANT)

Establishing accurate dwell time is one of the most critical APT forensic activities.

APT actors routinely maintain access for 90 to 365 days before detection. Every day of dwell time represents additional potential data exfiltration, privilege escalation, and persistence establishment.

---

## 8.1 Dwell Time Investigation Steps

- Review the oldest available log sources for anomalies
- Search for the first occurrence of each known IoC across all log sources
- Look for dormant accounts that were created but not immediately used
- Identify periods where logging gaps may conceal activity
- Analyze authentication logs for seasonal or off-hours activity
- Review DNS logs for C2 domain first-resolution events
- Analyze EDR telemetry for earliest known suspicious process
- Review firewall logs for earliest outbound communication to known C2

---

## 8.2 Log Retention Gap Assessment

| Log Source | Retention Available | First Entry UTC | Sufficient? |
|------------|--------------------|--------------------|-------------|
| SIEM | | | |
| Firewall | | | |
| DNS | | | |
| VPN | | | |
| Authentication | | | |
| EDR | | | |

Retention gaps must be documented as investigation limitations.

---

## 8.3 Historical Timeline Table

| Date (UTC) | Host | Event | Technique | Significance | Evidence Ref |
|------------|------|-------|----------|-------------|--------------|
|            |      |       |          |             |              |

---

# 9. Phase 3 – Memory Forensics

Memory analysis is essential for APT campaigns because:

- APT actors frequently use memory-resident malware
- Custom implants may never touch disk
- C2 communication details may only exist in memory
- Credential harvesting tools operate in memory
- Rootkits and kernel-level implants require memory analysis

---

## 9.1 Memory Forensic Objectives

- Identify injected code in legitimate processes
- Detect reflective DLL loading
- Identify memory-resident C2 beacons
- Extract decrypted configuration blocks
- Identify LSASS memory access patterns
- Detect process hollowing
- Extract active network connections
- Identify kernel-level rootkit indicators

---

## 9.2 APT-Specific Memory Indicators

| Indicator | Meaning |
|-----------|--------|
| Unsigned module in legitimate process | Code injection |
| RWX memory pages | Shellcode staging area |
| Unlinked VAD entries | Evasive injection |
| Process hollowing evidence | Execution hijacking |
| LSASS handle open | Credential harvesting |
| Suspicious named pipes | Cobalt Strike or similar |
| Encrypted memory regions | C2 configuration hiding |

Reference:
`03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Memory-Forensics-SOP.md`

---

# 10. Phase 4 – Disk Forensics

Disk analysis identifies file-based artifacts that memory analysis may miss.

---

## 10.1 Key Investigation Areas

- Review recently created files across system and user directories
- Identify unauthorized binaries in system paths
- Examine web server directories for web shells
- Review prefetch and shimcache for execution history
- Review BAM/DAM for recent execution records
- Analyze USN journal for file creation and deletion history
- Review LNK files and recent documents
- Examine scheduled task XML files
- Review installed services and drivers

---

## 10.2 APT-Specific Disk Indicators

| Indicator | Location | Significance |
|-----------|---------|-------------|
| Web shell | Web root | Persistent access |
| Renamed system tools | Temp directories | LOLBin abuse |
| Compressed archives | Staging directories | Pre-exfiltration |
| Modified registry hives | HKLM/Run | Persistence |
| Unauthorized drivers | System32 | Rootkit |

Reference:
`03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Disk-Forensics-SOP.md`

---

# 11. Phase 5 – Network Forensics (IMPORTANT)

APT campaigns rely on sustained network C2 communication that must be forensically confirmed.

---

## 11.1 C2 Pattern Analysis

APT C2 traffic commonly exhibits:

- Long beacon intervals (hours or days)
- Encrypted payloads using TLS or custom encryption
- Domain fronting via CDNs
- Use of legitimate cloud services as relay
- Domain generation algorithms (DGA)
- Slow low-volume exfiltration over extended periods
- Geographic consistency in C2 infrastructure

---

## 11.2 Network Forensic Activities

- Extract all external IPs and domains contacted by compromised hosts
- Analyze beacon intervals and packet consistency
- Identify JA3 TLS fingerprints linked to known APT tools
- Examine DNS query volume for tunneling patterns
- Extract files transferred over HTTP/HTTPS
- Analyze NetFlow for long-duration low-volume sessions
- Identify use of cloud services for C2 relay

---

## 11.3 C2 Infrastructure Mapping Table

| C2 Domain/IP | First Seen | Last Seen | Protocol | Volume | TI Match | Evidence Ref |
|--------------|-----------|----------|---------|--------|---------|--------------|
|              |           |          |         |        |         |              |

---

# 12. Phase 6 – Malware Analysis (IMPORTANT)

APT malware requires specialized analysis.

---

## 12.1 APT Malware Characteristics

APT malware often exhibits:

- Custom or modified open-source frameworks
- Encrypted communications
- Anti-analysis techniques
- Anti-sandbox behavior
- Living-off-the-land abuse
- Modular architecture
- Signed or stolen certificate abuse
- Self-deletion after execution

---

## 12.2 Static Analysis Steps

- Hash and TI lookup
- Extract strings and embedded URLs
- Identify import tables and API calls
- Identify packers or obfuscation
- Identify compile timestamp
- Identify language artifacts
- Identify code signing certificate

---

## 12.3 Dynamic Analysis Steps

- Execute in isolated sandbox
- Capture network behavior
- Identify C2 endpoints
- Identify dropped files
- Identify persistence installation
- Identify privilege escalation behavior
- Identify anti-analysis triggers

---

## 12.4 Malware Comparison Table

| Sample | Hash | TI Match | Tool Family | Confidence |
|--------|------|---------|------------|-----------|
|        |      |         |            |           |

---

# 13. Phase 7 – Credential Compromise Analysis

APT actors harvest credentials systematically.

---

## 13.1 Credential Dumping Indicators

| Indicator | Evidence Source |
|-----------|----------------|
| LSASS memory access | EDR + Event ID 4656 |
| NTDS.dit access | DC event logs |
| Volume shadow copy access | Windows logs |
| DCSync activity | Security event logs |
| Pass-the-Ticket | Kerberos logs |

---

## 13.2 Credential Scope Assessment

| Credential Type | Compromised? | Scope | Reset Required? |
|----------------|-------------|-------|----------------|
| Domain Admin | | | |
| Service Accounts | | | |
| Local Admin | | | |
| Cloud Credentials | | | |

---

# 14. Phase 8 – Lateral Movement Reconstruction

APT lateral movement spans extended periods.

---

## 14.1 Movement Reconstruction Steps

- Map all internal connections from each compromised host
- Identify pivot chain from initial foothold to sensitive systems
- Reconstruct authentication sequence
- Identify service accounts abused
- Identify systems accessed but not exploited
- Map timing of each pivot

---

## 14.2 Lateral Movement Map Table

| Source Host | Destination | Method | Credential Used | Date/Time UTC |
|-------------|------------|--------|----------------|--------------|
|             |            |        |                |              |

---

# 15. Phase 9 – Exfiltration Validation

Data exfiltration is typically the final APT objective.

---

## 15.1 Exfiltration Forensic Steps

- Extract files transferred in PCAP analysis
- Analyze compressed archive artifacts
- Review staging directories for collected data
- Analyze DNS query payload sizes
- Review cloud upload logs
- Identify cloud storage access from internal hosts
- Validate data classification of transferred content
- Estimate total volume exfiltrated

---

## 15.2 Exfiltration Validation Table

| Host | Method | Data Type | Volume | Period | Confirmed? |
|------|--------|----------|--------|--------|------------|
|      |        |          |        |        |            |

---

# 16. Phase 10 – Attribution Forensic Indicators

L3 must collect evidence for attribution analysis.

---

## 16.1 Attribution Artifact Collection

| Artifact | Example |
|----------|---------|
| Malware compile timestamps | UTC timezone |
| Language artifacts | Error messages |
| Infrastructure reuse | IP/domain match |
| Code similarity | Public actor tools |
| TTP match | ATT&CK group profile |

Reference:
`PB-APT-Attribution-Analysis.md`

---

# 17. MITRE ATT&CK Mapping

L3 must map all confirmed techniques.

Reference:
`PB-APT-MITRE-Mapping.md`

---

# 18. Reporting Requirements

L3 must deliver:

- Technical forensic report
- Timeline reconstruction
- Malware analysis summary
- Attribution indicators
- Evidence inventory

Reference:
`07_REPORTING/07.1_Incident-Reports/Technical-Deep-Dive-Template.md`

---

# 19. MSSP Considerations

For MSSP environments:

- Segregate forensic artifacts per client
- Preserve client-specific evidence
- Coordinate with client legal teams
- Monitor cross-client infrastructure for related activity

---

## 20. Related Documents

| Document | Path |
|----------|------|
| APT Master | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-Master.md` |
| APT Threat Intel Integration | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-ThreatIntel-Integration.md` |
| APT Long-Term Monitoring | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-LongTerm-Monitoring.md` |
| APT Attribution Analysis | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-Attribution-Analysis.md` |
| APT MITRE Mapping | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-MITRE-Mapping.md` |
| Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |

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