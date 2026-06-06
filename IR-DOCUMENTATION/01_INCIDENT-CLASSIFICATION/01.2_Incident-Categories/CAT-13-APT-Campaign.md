# CAT-13 – APT Campaign Incident Category

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Incident Category – APT Campaign |
| Document ID | IR-CAT-013 |
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
| Category ID | CAT-13 |
| Default Severity | P1 – Critical (confirmed persistence/impact/data exposure) / P2 – High (strong indicators of targeted intrusion) |
| Escalation Priority | Immediate; APT implies persistent, stealthy, and high-risk activity |
| Attack Goal | Long-term access, intelligence collection, data theft, disruption, strategic impact |
| Threat Actors | Nation-state or state-aligned groups; highly capable adversaries |
| Typical Targets | Identity systems, email, critical servers, sensitive repositories, cloud control plane |
| Playbook Reference | `02_PLAYBOOKS/02.13_APT-Campaign/` |

---

## 3. What is an APT Campaign?

An Advanced Persistent Threat (APT) campaign is a coordinated, targeted
intrusion where attackers seek long-term access and operate with stealth
to achieve strategic objectives.

APT incidents commonly include:

- Multiple stages over long time windows (days/weeks/months)
- Multiple compromised systems (pivoting and layered persistence)
- Advanced tradecraft (living-off-the-land, covert channels, log tampering)
- Data collection and exfiltration focused on sensitive targets
- Multiple tactics combined: phishing + exploit + credential theft + lateral movement
- Continuous re-entry attempts after containment

APT classification does not require attribution certainty. It is based on
the observed characteristics: persistence, stealth, and targeted intent.

---

## 4. APT Campaign Characteristics (Operational Criteria)

| Characteristic | Indicators |
|---------------|------------|
| Advanced | Custom tooling, stealth techniques, defensive evasion |
| Persistent | Multiple persistence mechanisms, re-entry attempts |
| Targeted | Focused targeting of specific systems or high-value users |
| Coordinated | Multiple related incidents across time and systems |
| Stealthy | Low-and-slow behavior, minimal noise, log tampering |
| Strategic | Focus on intelligence, IP theft, or long-term access |

---

## 5. Common APT Attack Techniques

| Area | Examples |
|------|----------|
| Initial Access | Spear phishing, watering hole, supply chain, exploited perimeter services |
| Persistence | Backdoors, scheduled tasks, services, web shells, cloud tokens |
| Credential Access | Credential dumping, token theft, Kerberos abuse |
| Lateral Movement | Remote services (RDP/SMB/WMI), admin shares, VPN pivoting |
| Command and Control | Encrypted channels, covert DNS, cloud-based C2 |
| Collection | Email collection, file share staging, DB exports |
| Exfiltration | Web services, cloud storage, alternative protocols, covert channels |
| Defense Evasion | LOLBins, log clearing, disabling security tools, masquerading |

---

## 6. Indicators of APT Activity (IoCs and Observables)

### 6.1 Behavioral Indicators (High Confidence)

| Indicator | Description |
|----------|-------------|
| Repeated Re-Entry | Persistence remains despite remediation; attacker returns |
| Multi-Stage Activity | Discovery → credential access → lateral movement → collection |
| Low-and-Slow | Activity spread over days with minimal alert triggers |
| Unusual Admin Paths | Privileged actions from non-admin endpoints |
| Covert C2 | Beaconing with low frequency and encrypted traffic |
| Log Tampering | Clearing or disabling logs to remove evidence |
| Use of LOLBins | Abuse of legitimate tools to avoid malware signatures |

### 6.2 Identity and Privilege Indicators

| Indicator | Description |
|----------|-------------|
| New Privileged Accounts | New admin users or role assignments |
| Token Abuse | OAuth grants, refresh token replay, session hijacking |
| Kerberos Abuse | Unusual ticket requests, golden ticket indicators |
| Admin Group Changes | Domain Admins/Enterprise Admins membership changes |
| Service Account Misuse | Service account used interactively or outside expected scope |

### 6.3 Network and Data Indicators

| Indicator | Description |
|----------|-------------|
| Staging Directories | Large archives created prior to transfer |
| Unusual Egress | Outbound traffic to uncommon destinations or protocols |
| Cloud Exfiltration | Uploads to attacker-controlled cloud storage |
| DNS Tunneling | High-volume/large DNS queries |
| Internal Recon | Repeated scanning and enumeration of internal hosts and shares |

### 6.4 Key Log Sources (Minimum)

| Source | What to Review |
|--------|----------------|
| EDR Telemetry | Process trees, persistence mechanisms, suspicious tools |
| AD / IAM Logs | Privilege changes, Kerberos patterns, new accounts |
| Proxy/Firewall | Low-frequency beaconing, unusual destinations |
| DNS Logs | New/rare domains, tunneling patterns |
| Email Logs | Mailbox access, forwarding rules, OAuth grants |
| Cloud Audit Logs | Token creation, role assignments, storage access |
| SIEM Correlation | Multi-stage patterns across sources |

---

## 7. Severity Classification

| Scenario | Severity |
|----------|----------|
| Confirmed persistent attacker presence across multiple systems | P1 – Critical |
| Confirmed exfiltration of sensitive data or intelligence collection | P1 – Critical |
| Identity infrastructure compromised (AD/SSO/Cloud admin) | P1 – Critical |
| Confirmed lateral movement with privileged compromise | P1 – Critical |
| Strong indicators of APT tradecraft but scope not fully confirmed | P2 – High |
| Targeted spear phishing with suspicious post-exploitation on single host | P2 – High |
| Suspicious patterns that may indicate APT (low confidence) | P3 – Medium |

---

## 8. Immediate Response Actions

### 8.1 First 15 Minutes

- Create incident ticket and assign initial severity based on confidence and scope
- Notify SOC Lead immediately for P2 and above
- Preserve logs immediately for the suspected timeframe (APT often spans longer windows)
- Identify affected identities, hosts, and observed techniques
- Initiate scoping actions:
  - identify related alerts and historical indicators
  - correlate across SIEM, EDR, IAM, DNS, proxy, and cloud logs
- If privileged compromise suspected, request immediate containment approval:
  - revoke sessions
  - disable suspected accounts
  - isolate high-risk endpoints

### 8.2 First 1 Hour

- Establish working hypothesis of intrusion chain:
  - initial access vector
  - pivot hosts
  - persistence mechanisms
  - objectives (collection/exfiltration)
- Engage L3 and IR Team immediately for advanced analysis
- Begin threat hunting to find:
  - additional persistence
  - additional compromised hosts
  - similar indicators across environment
- Assess data exposure risk and begin breach assessment if needed
- Prepare management update indicating:
  - confidence level
  - affected scope (known)
  - containment actions in progress
  - next steps for validation

### 8.3 First 4 Hours

- Confirm containment plan prioritizing identity and privileged access systems
- Preserve forensic evidence for critical systems:
  - memory capture (where safe)
  - disk triage image
  - log exports covering extended timeframe
- Implement containment:
  - isolate compromised hosts
  - rotate credentials, keys, tokens
  - restrict remote admin access temporarily
- Evaluate requirement for external IR retainer or specialized support (if contracted)
- Increase monitoring and deploy temporary detection logic based on observed TTPs

---

## 9. Containment Strategy Guidance (APT Context)

APT containment must be careful to avoid:

- tipping off the attacker prematurely
- triggering destructive actions (wipers, ransomware)
- losing visibility by removing tools/logging too early

Recommended approach:

| Priority | Focus | Actions |
|---------|------|---------|
| 1 | Identity Control | revoke sessions, rotate tokens, protect admin accounts |
| 2 | Stop Egress | block known C2/exfil routes while monitoring for alternates |
| 3 | Isolate Key Hosts | isolate confirmed compromised hosts and jump boxes |
| 4 | Remove Persistence | only after evidence capture and scope confirmation |
| 5 | Recovery and Hardening | patch, segmentation, logging improvements, detection tuning |

---

## 10. MITRE ATT&CK Mapping (APT-Relevant)

APT campaigns commonly span multiple tactics. Common mappings include:

| Tactic | Technique | ID |
|--------|-----------|----|
| Initial Access | Spearphishing Link/Attachment | T1566.002 / T1566.001 |
| Initial Access | Exploit Public-Facing Application | T1190 |
| Initial Access | Supply Chain Compromise | T1195 |
| Execution | Command and Scripting Interpreter | T1059 |
| Persistence | Scheduled Task/Job | T1053 |
| Persistence | Web Shell | T1505.003 |
| Persistence | Account Manipulation | T1098 |
| Privilege Escalation | Exploitation for Priv Esc | T1068 |
| Defense Evasion | Obfuscated Files/Info | T1027 |
| Defense Evasion | Disable or Modify Tools | T1562 |
| Credential Access | OS Credential Dumping | T1003 |
| Discovery | Account/Network Discovery | T1087 / T1046 |
| Lateral Movement | Remote Services | T1021 |
| Command and Control | Application Layer Protocol | T1071 |
| Exfiltration | Exfiltration Over Web Service | T1567 |
| Exfiltration | Exfiltration Over C2 Channel | T1041 |

---

## 11. Key Investigation Questions

1. What is the suspected initial access vector and earliest timestamp?
2. Which identities and hosts are confirmed compromised?
3. What persistence mechanisms exist and where?
4. Is there evidence of privileged compromise (AD/Cloud admin)?
5. Is there evidence of lateral movement (which protocols/tools)?
6. Is there evidence of collection and staging (archives, staging directories)?
7. Is data exfiltration confirmed or likely (volume, destinations, channels)?
8. Are logging and monitoring systems intact, or were they tampered with?
9. Are there re-entry attempts after containment actions?
10. Are observed TTPs consistent with known threat actors (without asserting attribution)?
11. What is the likely objective (intelligence, IP theft, disruption)?
12. What containment actions minimize risk without losing visibility?
13. Do we need external forensics or IR retainer engagement?

---

## 12. Critical Do's and Do Not's

### Do

- Assume scope is larger than currently visible until proven otherwise
- Preserve evidence over longer time windows than standard incidents
- Protect identity systems and privileged accounts first
- Use threat hunting to find hidden persistence and additional hosts
- Document findings with timeline, evidence, and confidence level
- Coordinate actions carefully to avoid attacker escalation
- Increase monitoring and detection based on observed TTPs

### Do Not

- Remove persistence before evidence capture and scoping are sufficient
- Publicly attribute threat actor without validated intelligence and approvals
- Assume a single host is the only compromise point
- Make aggressive changes without evaluating impact on visibility
- Close incident without confirming persistence removal and monitoring plan

---

## 13. Escalation Path

| Stage | Action |
|-------|--------|
| L1 Triage | Identify suspicious indicators, open ticket, preserve initial evidence |
| L2 Investigation | Validate indicators and begin scoping |
| SOC Lead | Coordinate resources, manage comms, approve escalations |
| L3 / Threat Specialist | Lead hunting, ATT&CK mapping, and technical direction |
| IR Team | Lead containment, forensics, and eradication plan |
| GRC / Compliance | Assess breach and regulatory obligations |
| Legal | Guide evidence handling and disclosure constraints |
| Management / CISO | Approve major actions and strategic communications |
| MSSP SDM / Client Owner | Coordinate client communication and evidence segregation |

---

## 14. Regulatory and Client Reporting Considerations

| Trigger | Action |
|--------|--------|
| Confirmed sensitive data exposure or exfiltration | Engage Compliance and Legal immediately |
| Critical infrastructure or regulated entity impacted | Assess reporting obligations (RBI/CERT-In) |
| MSSP client impact | Notify client per SLA; maintain client data segregation |
| Supply chain involvement | Coordinate vendor communication and disclosure strategy |

Reference: `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

## 15. Evidence Collection Requirements

| Evidence Type | Priority | Notes |
|--------------|----------|-------|
| EDR telemetry export | Critical | Process trees, persistence artifacts, suspicious tooling |
| AD/IAM logs export | Critical | Privilege changes, Kerberos/NTLM patterns, new accounts |
| Proxy/firewall logs export | High | C2 and exfiltration destinations and patterns |
| DNS logs export | High | New domains, tunneling indicators |
| Cloud audit logs export | High | Tokens, roles, storage access, app registrations |
| Email platform logs | High | Mailbox access, forwarding rules, OAuth grants |
| Memory capture (selected critical hosts) | As needed | For fileless persistence and injection |
| Disk triage images (selected hosts) | As needed | For forensic reconstruction |
| Timeline documentation | Critical | Single source of truth for actions and events |
| Chain-of-custody forms | As needed | Required for legal-grade evidence packages |

Reference: `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 16. Related Documents

| Document | Path |
|---------|------|
| APT Master Playbook | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-Master.md` |
| L3 Forensics | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-L3-Forensics.md` |
| Threat Intel Integration | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-ThreatIntel-Integration.md` |
| Long-Term Monitoring | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-LongTerm-Monitoring.md` |
| Attribution Analysis | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-Attribution-Analysis.md` |
| MITRE Mapping | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-MITRE-Mapping.md` |
| Network Intrusion Category | `01_INCIDENT-CLASSIFICATION/01.2_Incident-Categories/CAT-11-Network-Intrusion.md` |
| Data Breach Category | `01_INCIDENT-CLASSIFICATION/01.2_Incident-Categories/CAT-06-Data-Breach-Exfiltration.md` |
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