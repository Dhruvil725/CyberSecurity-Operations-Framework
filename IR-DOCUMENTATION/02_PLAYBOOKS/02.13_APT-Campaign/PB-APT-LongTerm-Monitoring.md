# Playbook: APT Campaign – Long-Term Monitoring

---

## 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | Playbook – APT Campaign (Long-Term Monitoring)               |
| Document ID    | IR-PB-APT-003                                                |
| Version        | 1.0                                                          |
| Effective Date | 21-May-2026                                                  |
| Owner          | SOC Manager / Threat Detection Lead / IR Team Lead           |
| Approved By    | CISO                                                         |
| Classification | Internal – Confidential                                      |
| Review Cycle   | Quarterly and after any confirmed APT campaign               |

---

## 2. Purpose

This document defines the long-term monitoring procedures required after an Advanced Persistent Threat (APT) campaign is identified and initial containment is executed.

Long-term monitoring is one of the most critical and often underestimated phases of APT response. Unlike opportunistic attacks where containment and eradication may be sufficient, APT actors routinely:

- Return after initial containment
- Reuse dormant persistence mechanisms that were not fully identified
- Reuse valid credentials harvested months before detection
- Activate secondary C2 channels when primary channels are blocked
- Establish access through trusted third-party relationships
- Leverage different tools in subsequent intrusion waves

Long-term monitoring ensures that:

- Reinfection is detected immediately
- Dormant persistence is identified before reactivation
- Attacker infrastructure rotation is tracked
- Any reuse of harvested credentials is identified quickly
- New TTPs from the same actor are detected early
- Security improvements remain effective over time
- Threat intelligence remains up to date

This playbook defines the monitoring architecture, detection procedures, alert escalation criteria, and review cadences required to maintain sustained detection capability after an APT campaign.

---

## 3. Scope

Applies to:

- All environments affected by confirmed APT campaign
- Adjacent environments with potential lateral movement exposure
- Cloud and hybrid infrastructure
- Third-party and vendor-connected networks
- MSSP-managed client environments affected by campaign
- Authentication and identity infrastructure
- Email and communication platforms
- DevOps and CI/CD infrastructure

---

## 4. Roles and Responsibilities

| Role | Responsibility |
|------|----------------|
| SOC Manager | Oversees long-term monitoring program |
| L2 Analysts | Daily monitoring and alert investigation |
| L3 Analysts | Deep investigation of reinfection indicators |
| Threat Detection Lead | Maintains and tunes detection rules |
| Threat Intelligence Lead | Tracks actor infrastructure and new IoCs |
| IR Team Lead | Activates response if reinfection confirmed |
| CISO | Executive oversight and decision authority |
| MSSP SDM | Client-specific monitoring coordination |

---

## 5. Long-Term Monitoring Framework

Post-APT monitoring must cover five core areas:

| Area | Objective |
|------|----------|
| Identity and Authentication | Detect credential reuse |
| Network Telemetry | Detect C2 reactivation |
| Endpoint Behavior | Detect persistence reactivation |
| Threat Intelligence | Track actor infrastructure |
| Cloud and SaaS | Detect cloud-based re-entry |

Each area requires dedicated detection rules, monitoring procedures, and escalation criteria.

---

# 6. Identity and Authentication Monitoring (CRITICAL)

Authentication monitoring is the highest-priority monitoring activity after an APT campaign because:

- APT actors may have harvested credentials months before detection
- Harvested credentials may not have been used yet at time of containment
- Password resets may be incomplete if scope was underestimated
- Service account credentials are frequently overlooked
- Cloud credentials may have been harvested separately

---

## 6.1 Authentication Monitoring Requirements

| Activity | Monitoring Approach | Detection Logic |
|----------|-------------------|----------------|
| Dormant account activation | Alert on accounts inactive for 30+ days | SIEM rule |
| Off-hours privileged login | Alert on admin logins outside business hours | SIEM rule |
| Impossible travel | Alert on geographic anomalies | Identity platform |
| MFA bypass attempts | Alert on authentication without MFA | Identity platform |
| Service account anomalies | Alert on service accounts logging interactively | SIEM |
| Credential stuffing | Alert on failed login volume spike | SIEM |
| New device enrollment | Alert on new device MFA enrollment | Identity platform |
| Token replay | Alert on duplicate token usage | Identity platform |

---

## 6.2 Privileged Account Monitoring

Post-APT:

- All privileged accounts must be monitored individually
- Any use of domain admin credentials must generate an alert
- New privileged group memberships must trigger immediate review
- All Kerberos golden or silver ticket indicators must escalate immediately
- DCSync activity must escalate to P1 immediately

---

## 6.3 Authentication Alert Escalation

| Alert | Severity |
|-------|---------|
| Dormant admin account activated | P1 |
| Domain admin used on workstation | P1 |
| Impossible travel for privileged account | P1 |
| Service account interactive login | P2 |
| Kerberos anomaly | P1 |

---

# 7. Network Telemetry Monitoring (IMPORTANT)

APT C2 channels frequently rotate or reactivate after initial blocking.

---

## 7.1 C2 Reactivation Monitoring

After confirmed APT campaign:

- All known C2 IPs and domains must remain on block list
- Block list must be reviewed and refreshed weekly
- DNS queries for previously seen C2 domains must alert immediately
- Proxy logs must be monitored for previously identified user agents
- JA3 TLS fingerprints linked to APT tools must be monitored continuously
- NetFlow analysis must continue across all affected segments

---

## 7.2 Beaconing Detection

Beaconing detection must remain enhanced post-APT:

- Deploy time-delta analysis for outbound connections
- Alert on consistent outbound connections at regular intervals
- Alert on connections to newly registered domains from internal hosts
- Alert on DNS queries with high-entropy subdomains
- Alert on abnormal outbound data volumes from previously compromised hosts

---

## 7.3 New Infrastructure Detection

APT actors frequently register new infrastructure after initial IOCs are blocked.

Monitor for:

- New domain registrations in actor-associated registrar patterns
- IP ranges associated with previous campaigns
- TLS certificate patterns linked to actor infrastructure
- ASN numbers previously associated with C2 hosting

---

## 7.4 Network Monitoring Coverage Table

| Segment | Flow Logging | Packet Capture | DNS Logging | Proxy Logging |
|---------|-------------|---------------|-------------|--------------|
| Corporate LAN | | | | |
| Data Center | | | | |
| DMZ | | | | |
| Cloud | | | | |

---

# 8. Endpoint Behavioral Monitoring

Endpoint monitoring must remain enhanced post-APT to detect persistence reactivation.

---

## 8.1 Endpoint Monitoring Requirements

| Activity | Detection Method |
|----------|----------------|
| New scheduled task creation | EDR alert |
| New service installation | EDR alert |
| Registry run key modification | EDR alert |
| WMI subscription creation | EDR alert |
| Unusual process parent-child | EDR behavioral |
| Unsigned binary execution | EDR alert |
| LOLBin abuse | EDR behavioral |
| Memory injection | EDR alert |
| LSASS access | EDR alert |

---

## 8.2 Enhanced EDR Rules

Post-APT, deploy enhanced EDR rules for:

- All processes spawned by known APT malware parent hashes
- All network connections from previously compromised processes
- All file writes to known attacker staging directories
- All command-line arguments matching known APT patterns

---

## 8.3 Endpoint Coverage Validation

Confirm:

- EDR agent deployed on all affected systems
- EDR agent deployed on all adjacent systems
- EDR telemetry flowing to SIEM
- Alert rules active and tested
- No monitoring gaps in affected segments

---

# 9. Threat Intelligence Monitoring (IMPORTANT)

Threat intelligence is the backbone of long-term APT monitoring because it allows the organization to detect new actor infrastructure before it is used against them.

---

## 9.1 Intelligence Requirements

Post-APT monitoring must maintain:

- Actor-specific threat intelligence profile
- Updated IoC feed from TI provider
- Internal IoC register updated after each new finding
- Subscription to sector-specific threat feeds
- Participation in ISAC sharing groups if applicable
- Regular review of MITRE ATT&CK group profiles

---

## 9.2 TI Feed Integration

| Feed Type | Integration Point | Update Frequency |
|-----------|-----------------|-----------------|
| C2 IPs | Firewall + SIEM | Daily |
| Malicious domains | DNS + Proxy | Daily |
| Malware hashes | EDR | Real-time |
| JA3 fingerprints | Proxy | Weekly |
| YARA rules | EDR + SIEM | Weekly |

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Feed-Management.md`

---

## 9.3 New IoC Processing

When new IoCs are received:

- Immediately search across SIEM for historical matches
- Deploy to blocking infrastructure
- Search EDR for hash or behavior matches
- Review DNS logs for domain resolution history
- Update internal IoC register

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md`

---

# 10. Cloud and SaaS Monitoring

Cloud environments require dedicated post-APT monitoring because:

- APT actors frequently establish cloud-based backdoors
- Cloud credentials may have been harvested separately
- OAuth grants may provide persistent access
- Cloud API activity may not be integrated into SIEM

---

## 10.1 Cloud Monitoring Activities

| Platform | Monitoring Activity |
|---------|-------------------|
| AWS | CloudTrail anomaly detection |
| Azure | Entra ID sign-in monitoring |
| GCP | Cloud Audit Log monitoring |
| SaaS | OAuth grant review |
| Cloud Storage | Access pattern monitoring |

---

## 10.2 Cloud-Specific Alert Rules

Deploy alerts for:

- New API keys created
- New OAuth applications granted
- New privileged role assignments
- Cross-account access from unusual locations
- New service principal creation
- Logging disabled in any cloud environment

---

# 11. Monitoring Schedule and Review Cadence

Post-APT monitoring must follow a structured review schedule.

---

## 11.1 Daily Monitoring Activities

| Activity | Owner |
|----------|-------|
| Review authentication anomaly alerts | L2 |
| Review C2 block list effectiveness | L2 |
| Review new IoCs from TI feeds | TI Team |
| Review endpoint behavioral alerts | L2 |
| Review cloud audit logs | L2 |

---

## 11.2 Weekly Review Activities

| Activity | Owner |
|----------|-------|
| Review block list for expired or rotated IoCs | TI Team |
| Review detection rule effectiveness | Detection Lead |
| Review new actor infrastructure reports | TI Team |
| Validate monitoring coverage | SOC Manager |
| Review privileged account activity | L2 |

---

## 11.3 Monthly Review Activities

| Activity | Owner |
|----------|-------|
| Full monitoring program effectiveness review | SOC Manager |
| Update actor threat profile | TI Team |
| Review detection gap register | Detection Lead |
| Present monitoring status to executive | CISO briefing |

---

## 11.4 Monitoring Duration

| Environment | Recommended Duration |
|-------------|---------------------|
| Directly affected systems | Minimum 12 months |
| Adjacent systems | Minimum 6 months |
| Authentication infrastructure | Minimum 12 months |
| Cloud environments | Minimum 12 months |
| Third-party connections | Minimum 6 months |

---

# 12. Reinfection Response Procedure

If reinfection indicators are detected:

---

## 12.1 Immediate Actions

- Escalate to L3 immediately
- Notify SOC Lead and IR Team
- Activate incident response procedures
- Do not immediately block if intelligence value assessment is pending
- Preserve evidence before containment

---

## 12.2 Reinfection Escalation Table

| Indicator | Severity | Immediate Action |
|-----------|---------|-----------------|
| Known C2 beacon detected | P1 | Escalate immediately |
| Dormant admin account activated | P1 | Escalate immediately |
| Known APT malware hash detected | P1 | Escalate immediately |
| New persistence matching actor TTP | P1 | Escalate immediately |
| Known actor infrastructure contacted | P1 | Escalate immediately |

---

# 13. Detection Rule Maintenance

Detection rules must be maintained throughout monitoring period.

---

## 13.1 Rule Maintenance Activities

- Review all APT-specific SIEM rules monthly
- Validate EDR rules are active and triggering correctly
- Test detection rules against known indicators quarterly
- Update rules when new actor TTPs are identified
- Retire rules only after executive approval

---

## 13.2 Detection Rule Register

| Rule Name | Source | Platform | Last Reviewed | Status |
|-----------|--------|---------|--------------|--------|
|           |        |         |              |        |

---

# 14. MSSP Client Monitoring Considerations

For MSSP-managed environments:

- Maintain separate monitoring dashboards per client
- Ensure client-specific IoC sets are applied
- Report monitoring status monthly to client
- Escalate reinfection indicators to client IR contacts immediately
- Maintain evidence segregation throughout monitoring period

---

# 15. Documentation Requirements

| Requirement | Status |
|------------|--------|
| Monitoring scope documented | ☐ |
| Detection rules deployed | ☐ |
| TI feed integration confirmed | ☐ |
| Review schedule confirmed | ☐ |
| Escalation criteria defined | ☐ |
| Cloud monitoring active | ☐ |

---

# 16. Common Long-Term Monitoring Mistakes

| Mistake | Risk |
|---------|------|
| Removing enhanced monitoring too early | Missed reinfection |
| Not updating IoC feeds | Missed new infrastructure |
| Ignoring service account monitoring | Credential reuse missed |
| No cloud monitoring | Cloud backdoor undetected |
| Not reviewing detection rule effectiveness | False confidence |
| Failing to track actor TTPs | Missed new techniques |

---

## 17. Related Documents

| Document | Path |
|----------|------|
| APT Master | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-Master.md` |
| APT L3 Forensics | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-L3-Forensics.md` |
| APT Threat Intel Integration | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-ThreatIntel-Integration.md` |
| APT Attribution Analysis | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-Attribution-Analysis.md` |
| APT MITRE Mapping | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-MITRE-Mapping.md` |
| TI Feed Management | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Feed-Management.md` |
| TI IoC Handling SOP | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md` |
| Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |

---

## 18. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 21-May-2026 | SOC Manager / Threat Detection Lead | Initial version |

---

## 19. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**