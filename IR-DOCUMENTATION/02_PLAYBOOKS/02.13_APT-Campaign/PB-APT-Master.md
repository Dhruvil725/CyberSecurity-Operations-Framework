 
# Playbook: APT Campaign – Incident Response (Master)

---

## 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | Playbook – APT Campaign Incident Response (Master)           |
| Document ID    | IR-PB-APT-001                                                |
| Version        | 1.0                                                          |
| Effective Date | 21-May-2026                                                  |
| Owner          | IR Team Lead / SOC Manager / Threat Intelligence Lead        |
| Approved By    | CISO                                                         |
| Classification | Internal – Confidential                                      |
| Review Cycle   | Quarterly and after any confirmed APT campaign               |

---

## 2. Purpose

This playbook defines the structured response framework for Advanced Persistent Threat (APT) campaigns.

APT campaigns are characterized by:

- Highly targeted objectives
- Long dwell time
- Multi-stage attack chains
- Sophisticated evasion techniques
- Credential harvesting and reuse
- Lateral movement across multiple segments
- Persistence across remediation attempts
- Custom malware and tooling
- Strategic data exfiltration
- Potential geopolitical or economic motives

Unlike opportunistic attacks, APT campaigns are:

- Often state-sponsored or well-funded
- Conducted over weeks or months
- Designed to evade traditional detection
- Focused on specific assets or data
- Likely to return after initial containment

This playbook standardizes:

- Detection and validation of APT activity
- Multi-stage campaign scoping
- Long-term persistence identification
- Threat intelligence integration
- Attribution analysis framework
- Strategic containment approach
- Long-term monitoring requirements
- Executive-level communication
- Regulatory and legal considerations
- MSSP multi-client campaign handling

---

## 3. Scope

Applies to:

- Multi-stage intrusion campaigns
- Nation-state or suspected state-sponsored attacks
- Long-dwell-time network intrusions
- Supply chain related persistent attacks
- Cloud-hybrid coordinated campaigns
- Insider-assisted advanced attacks
- Credential-based long-term persistence
- Covert data exfiltration campaigns
- Attacks leveraging custom malware

Environments covered:

- Corporate network
- Data centers
- Cloud environments
- Hybrid infrastructure
- MSSP-managed client tenants
- OT-adjacent environments (if integrated)

---

## 4. Definition of APT Campaign

An incident qualifies as an APT campaign when:

- Evidence suggests prolonged attacker presence
- Multiple tactics across ATT&CK lifecycle observed
- Advanced evasion techniques are present
- Persistence mechanisms survive remediation
- Multiple compromised accounts observed
- Multiple segments or environments affected
- Attribution suggests organized actor group

---

## 5. APT Campaign Characteristics (IMPORTANT)

### 5.1 Behavioral Indicators

APT campaigns often demonstrate:

- Low-and-slow network beaconing
- Credential harvesting followed by delayed use
- Lateral movement over extended timeframe
- Use of legitimate administrative tools (LOLBins)
- Custom or rare malware variants
- Encrypted C2 infrastructure
- Use of compromised third-party infrastructure
- Log tampering and detection evasion
- Dormant persistence mechanisms

---

### 5.2 Operational Patterns

| Pattern | Description |
|---------|-------------|
| Staged intrusion | Initial foothold followed by pause |
| Privilege escalation delay | Escalation occurs days after entry |
| Targeted asset selection | Specific systems repeatedly accessed |
| Covert exfiltration | Slow and encrypted data transfer |
| Infrastructure rotation | C2 servers change frequently |
| Cleanup activity | Logs cleared periodically |

---

## 6. APT Incident Lifecycle

| Phase | Objective | Owner |
|-------|----------|-------|
| Phase 1 | Confirm advanced persistent activity | L2/L3 |
| Phase 2 | Establish historical dwell time | L3 |
| Phase 3 | Identify persistence mechanisms | L3 |
| Phase 4 | Map lateral movement paths | L3 |
| Phase 5 | Identify campaign objective | IR Team |
| Phase 6 | Threat intelligence correlation | TI Team |
| Phase 7 | Strategic containment | IR + Executive |
| Phase 8 | Long-term monitoring | SOC |
| Phase 9 | Attribution assessment | TI + IR |
| Phase 10 | Post-campaign hardening | Security Engineering |

---

## 7. Phase 1 – Confirm APT-Level Activity

Indicators suggesting APT rather than isolated intrusion:

| Indicator | Significance |
|-----------|-------------|
| Repeated reinfection after containment | Strong persistence |
| Dormant accounts activated weeks later | Delayed action |
| Custom malware not matching public samples | Targeted toolset |
| Credential harvesting without immediate use | Strategic planning |
| Log tampering across multiple systems | Operational discipline |
| Compromise of backup systems | Anti-recovery planning |
| Multiple C2 domains over time | Infrastructure management |
| Use of rare encryption or tunneling | Sophisticated evasion |

---

## 8. Phase 2 – Dwell Time Assessment (CRITICAL)

APT campaigns may persist undetected for extended periods.

---

### 8.1 Dwell Time Analysis Steps

- Review earliest known IoC
- Search logs for earliest suspicious activity
- Identify first anomalous authentication event
- Analyze long-term DNS logs
- Review historical VPN activity
- Examine endpoint telemetry for earliest compromise
- Review SIEM alerts over past 90–365 days
- Validate log retention sufficiency

---

### 8.2 Historical Timeline Table

| Date (UTC) | Host | Event | Technique | Evidence Ref |
|------------|------|-------|----------|--------------|
|            |      |       |          |              |

---

## 9. Phase 3 – Persistence Mapping (IMPORTANT)

APT actors establish multiple redundant persistence methods.

---

### 9.1 Persistence Types

| Mechanism | Example |
|-----------|---------|
| Scheduled tasks | Hidden recurring tasks |
| Service modifications | Malicious service injection |
| Domain accounts | Backdoor domain admin |
| SSH keys | Hidden authorized_keys entries |
| GPO modifications | Persistence via policy |
| WMI event subscriptions | Fileless persistence |
| Web shells | Hidden in web directories |
| Cloud IAM backdoors | Additional API keys |

---

### 9.2 Persistence Inventory Table

| System | Mechanism | Removed? | Revalidated? | Evidence Ref |
|--------|-----------|----------|--------------|--------------|
|        |           |          |              |              |

---

## 10. Phase 4 – Lateral Movement Analysis

APT actors typically move laterally in phases.

---

### 10.1 Lateral Movement Techniques

| Technique | Description |
|-----------|-------------|
| Pass-the-Hash | NTLM replay |
| Pass-the-Ticket | Kerberos replay |
| RDP pivoting | Internal remote access |
| SMB lateral movement | Admin share abuse |
| Credential reuse | Service account abuse |
| Remote service exploitation | Secondary vulnerability exploitation |

---

### 10.2 Lateral Movement Mapping

| Source | Destination | Method | Privilege | Evidence Ref |
|--------|------------|--------|----------|--------------|
|        |            |        |          |              |

---

## 11. Phase 5 – Campaign Objective Identification

APT campaigns often target:

- Intellectual property
- Financial data
- Strategic business information
- Customer databases
- Operational infrastructure
- Political or regulatory data
- Cryptographic keys
- Source code repositories

Identify:

- Which systems repeatedly accessed
- Which files frequently read
- Which databases queried
- Which exports staged

---

## 12. Phase 6 – Threat Intelligence Integration (IMPORTANT)

APT response requires strong TI correlation.

---

### 12.1 TI Correlation Steps

- Compare malware hash to known actor toolsets
- Match C2 infrastructure to known campaigns
- Compare TTPs to MITRE profiles
- Analyze language artifacts in malware
- Review geopolitical targeting patterns
- Correlate timestamps with known campaigns
- Compare encryption patterns

---

### 12.2 TI Correlation Table

| Indicator | Matched Threat Actor | Confidence | Source |
|-----------|---------------------|-----------|--------|
|           |                     |           |        |

Reference:
`PB-APT-ThreatIntel-Integration.md`

---

## 13. Phase 7 – Strategic Containment (CRITICAL)

APT containment differs from opportunistic attack containment.

---

### 13.1 Strategic Considerations

- Avoid immediate full containment if intelligence value needed
- Consider intelligence-gathering period
- Coordinate with executive leadership
- Coordinate with legal and possibly law enforcement
- Preserve C2 communication evidence before blocking
- Avoid tipping attacker prematurely

---

### 13.2 Containment Options

| Option | Risk |
|--------|------|
| Immediate isolation | Loss of intelligence |
| Gradual credential reset | Controlled removal |
| Network segmentation | Business disruption |
| Domain rebuild | Major operational impact |

Executive-level approval required for:

- Domain rebuild
- Mass credential resets
- Extended monitoring without blocking
- Public disclosure

---

## 14. Phase 8 – Long-Term Monitoring

After containment:

- Monitor for reinfection
- Enable enhanced logging
- Deploy additional EDR controls
- Monitor dormant accounts
- Track new scheduled tasks
- Monitor DNS anomalies
- Monitor C2 infrastructure rotation
- Monitor authentication anomalies
- Track reappearance of known IoCs

Reference:
`PB-APT-LongTerm-Monitoring.md`

---

## 15. Phase 9 – Attribution Assessment

Attribution must be cautious and evidence-based.

---

### 15.1 Attribution Factors

- Infrastructure reuse
- Malware code similarity
- Compile timestamps
- Language artifacts
- TTP consistency
- Targeting patterns
- Tool reuse
- Encryption style
- Known campaign overlap

Attribution must be labeled:

| Confidence Level | Meaning |
|------------------|--------|
| Low | Possible overlap |
| Medium | Multiple correlated indicators |
| High | Strong infrastructure + TTP match |

Reference:
`PB-APT-Attribution-Analysis.md`

---

## 16. Executive Communication

APT incidents require:

- Clear executive summary
- Risk and impact assessment
- Estimated dwell time
- Data exposure risk
- Remediation plan
- Attribution confidence
- Regulatory implications

Reference:
`07_REPORTING/07.1_Incident-Reports/Executive-Summary-Template.md`

---

## 17. MSSP Considerations

For MSSP environments:

- Determine whether campaign is cross-client
- Protect client isolation boundaries
- Notify affected clients individually
- Preserve tenant-specific artifacts
- Avoid cross-client attribution assumptions
- Coordinate with multiple client legal teams

---

## 18. Common APT Response Mistakes

| Mistake | Risk |
|---------|------|
| Treating as isolated malware event | Missed campaign scope |
| Not checking historical logs | Underestimated dwell time |
| Immediate mass credential reset | Alerting attacker |
| Ignoring cloud environments | Partial containment |
| Not mapping persistence fully | Reinfection |
| Overconfident attribution | Legal risk |

---

## 19. Related Documents

| Document | Path |
|----------|------|
| APT L3 Forensics | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-L3-Forensics.md` |
| APT Threat Intel Integration | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-ThreatIntel-Integration.md` |
| APT Long-Term Monitoring | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-LongTerm-Monitoring.md` |
| APT Attribution Analysis | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-Attribution-Analysis.md` |
| APT MITRE Mapping | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-MITRE-Mapping.md` |
| Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |

---

## 20. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 21-May-2026 | IR Team Lead / TI Lead | Initial version |

---

## 21. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**