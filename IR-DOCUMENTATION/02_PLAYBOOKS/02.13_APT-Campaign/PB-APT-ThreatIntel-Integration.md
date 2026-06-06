# Playbook: APT Campaign – Threat Intelligence Integration

---

## 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | Playbook – APT Campaign (Threat Intelligence Integration)    |
| Document ID    | IR-PB-APT-004                                                |
| Version        | 1.0                                                          |
| Effective Date | 21-May-2026                                                  |
| Owner          | Threat Intelligence Lead / SOC Manager                       |
| Approved By    | CISO                                                         |
| Classification | Internal – Confidential                                      |
| Review Cycle   | Quarterly and after major threat intelligence updates        |

---

## 2. Purpose

This document defines how Threat Intelligence (TI) must be integrated into Advanced Persistent Threat (APT) campaign investigations and response activities.

Threat intelligence integration is critical during APT incidents because:

- APT actors reuse infrastructure, tooling, and tradecraft over time
- Attribution often depends on TI correlation rather than a single indicator
- Campaigns evolve dynamically during active response
- New infrastructure may appear after containment
- Intelligence helps predict likely next-stage attacker behavior
- Threat actor targeting patterns may reveal campaign objectives
- TI supports proactive hunting beyond known indicators

This playbook establishes:

- Intelligence collection procedures
- Threat actor profiling methodology
- Indicator enrichment workflow
- Intelligence-to-detection integration
- TI-driven hunting methodology
- Infrastructure correlation processes
- Intelligence sharing and escalation
- MSSP multi-client intelligence handling

---

## 3. Scope

Applies to:

- Nation-state and suspected nation-state campaigns
- Financially motivated APT operations
- Supply chain APT campaigns
- Long-dwell intrusion investigations
- Hybrid cloud/on-prem campaigns
- Multi-client MSSP APT investigations
- Campaigns involving custom malware
- Coordinated phishing and intrusion campaigns

---

## 4. Threat Intelligence Objectives

During APT response, Threat Intelligence must help answer:

| Question | Objective |
|----------|-----------|
| Who may be behind the campaign? | Attribution assessment |
| What infrastructure is associated? | IoC expansion |
| What techniques are likely next? | Predictive defense |
| Has the actor targeted similar organizations? | Threat context |
| Which TTPs are characteristic of this actor? | ATT&CK mapping |
| Are additional systems likely compromised? | Scope expansion |
| Is active exploitation increasing globally? | Risk escalation |

---

## 5. Threat Intelligence Sources

APT investigations must leverage multiple intelligence sources.

---

## 5.1 Internal Intelligence Sources

| Source | Purpose |
|--------|---------|
| Historical incident data | Infrastructure reuse |
| Previous IoC register | Campaign overlap |
| SIEM historical logs | Long-term correlation |
| Internal malware repository | Variant comparison |
| Detection improvement logs | Repeat TTP analysis |

---

## 5.2 External Intelligence Sources

| Source | Purpose |
|--------|---------|
| Commercial TI feeds | Actor IoCs |
| ISAC sharing groups | Sector intelligence |
| CERT advisories | Campaign alerts |
| Vendor reports | Tooling and TTPs |
| Open-source intelligence (OSINT) | Infrastructure correlation |
| MITRE ATT&CK | TTP mapping |
| Malware repositories | Sample comparison |

---

# 6. Threat Intelligence Workflow

| Phase | Objective | Owner |
|-------|----------|-------|
| Phase 1 | Collect indicators | TI Team |
| Phase 2 | Enrich indicators | TI Analysts |
| Phase 3 | Correlate with known actors | TI + L3 |
| Phase 4 | Expand infrastructure mapping | TI Team |
| Phase 5 | Generate detection content | Detection Team |
| Phase 6 | Share intelligence internally | SOC/TI |
| Phase 7 | Monitor actor evolution | TI Team |

---

# 7. Phase 1 – Indicator Collection (IMPORTANT)

APT intelligence begins with accurate indicator collection.

---

## 7.1 Required Indicator Types

| Indicator Type | Examples |
|---------------|----------|
| IP addresses | C2 infrastructure |
| Domains | Beaconing domains |
| URLs | Payload delivery |
| File hashes | Malware samples |
| JA3 fingerprints | TLS beaconing |
| User agents | Tool fingerprints |
| Mutexes | Malware execution |
| Named pipes | C2 framework indicators |
| Registry keys | Persistence indicators |
| Scheduled task names | Persistence artifacts |

---

## 7.2 Collection Sources

Indicators should be collected from:

- EDR telemetry
- Firewall logs
- Proxy logs
- DNS logs
- Memory analysis
- Malware analysis
- PCAP analysis
- Threat hunting results
- Cloud audit logs

---

## 7.3 Indicator Quality Assessment

| Quality Level | Description |
|---------------|-------------|
| High Confidence | Directly observed in confirmed intrusion |
| Medium Confidence | Correlated via trusted TI source |
| Low Confidence | Weak association or broad indicator |

Indicators with low confidence should not be blocked automatically without review.

---

# 8. Phase 2 – Indicator Enrichment

Indicators must be enriched before operational use.

---

## 8.1 Enrichment Activities

| Indicator Type | Enrichment Required |
|---------------|--------------------|
| IP address | ASN, geolocation, hosting provider |
| Domain | WHOIS, registrar, creation date |
| Hash | Malware family, sandbox behavior |
| TLS fingerprint | Known framework match |
| User agent | Tool or malware family association |

---

## 8.2 Important Correlation Checks

APT actors frequently:

- Reuse registrars
- Reuse TLS certificates
- Reuse naming conventions
- Reuse infrastructure providers
- Reuse malware encryption routines
- Reuse phishing themes

Correlating these patterns significantly increases attribution confidence.

---

## 8.3 Enrichment Table

| Indicator | Enrichment Result | Confidence | Source |
|-----------|------------------|------------|--------|
|           |                  |            |        |

---

# 9. Phase 3 – Threat Actor Correlation (CRITICAL)

APT attribution requires correlation across multiple evidence sources.

---

## 9.1 Correlation Categories

| Category | Example |
|----------|---------|
| Infrastructure reuse | Same C2 ASN |
| Malware similarity | Shared code patterns |
| TTP overlap | Same ATT&CK techniques |
| Operational timing | Same active hours |
| Target profile | Same industry focus |
| Tool overlap | Same loaders or implants |

---

## 9.2 Attribution Confidence Model

| Confidence | Criteria |
|------------|----------|
| Low | Single weak overlap |
| Medium | Multiple TTP overlaps |
| High | Infrastructure + malware + TTP overlap |

Attribution must never rely on:

- Single IP match
- Single malware family
- Public rumors
- Geolocation alone

---

## 9.3 Threat Actor Profile Table

| Actor | Associated Techniques | Infrastructure Match | Confidence |
|-------|----------------------|----------------------|------------|
|       |                      |                      |            |

---

# 10. Phase 4 – Infrastructure Expansion (IMPORTANT)

APT infrastructure evolves rapidly during active campaigns.

---

## 10.1 Expansion Activities

- Pivot from known IPs to associated domains
- Pivot from TLS certificates to related hosts
- Identify domains sharing registrar patterns
- Identify cloud hosting overlap
- Identify DGA patterns
- Correlate DNS passive history

---

## 10.2 Infrastructure Mapping Table

| Type | Indicator | First Seen | Related To | Status |
|------|-----------|------------|------------|--------|
|      |           |            |            |        |

---

## 10.3 Infrastructure Rotation Monitoring

APT actors often:

- Rotate domains every few days
- Move infrastructure across cloud providers
- Reissue certificates
- Use short-lived VPS infrastructure

TI team must continuously update monitoring rules accordingly.

---

# 11. Phase 5 – Detection Engineering Integration

Threat intelligence must feed directly into detection content.

---

## 11.1 Detection Content Types

| Type | Example |
|------|---------|
| SIEM correlation rules | Beaconing detection |
| EDR rules | Process chain anomalies |
| DNS detections | High-entropy domains |
| Proxy detections | Suspicious user agents |
| YARA rules | Malware detection |
| Sigma rules | Log-based detection |

---

## 11.2 Intelligence-to-Detection Workflow

1. New IoC identified
2. Validate confidence
3. Search historical logs
4. Deploy detection rule
5. Monitor alert quality
6. Tune if necessary
7. Add to long-term monitoring

---

## 11.3 Rule Deployment Tracking

| Rule | Source Intelligence | Platform | Deployed? |
|------|--------------------|----------|-----------|
|      |                    |          |           |

---

# 12. Phase 6 – Threat Hunting Integration (IMPORTANT)

Threat intelligence must drive proactive hunting.

---

## 12.1 TI-Driven Hunting Objectives

- Identify additional compromised systems
- Detect dormant persistence
- Detect credential reuse
- Detect infrastructure rotation
- Identify unknown malware variants
- Detect secondary access channels

---

## 12.2 Example Hunting Activities

| Hunt Type | Objective |
|----------|-----------|
| DNS hunt | Detect new actor domains |
| JA3 hunt | Detect reused TLS fingerprints |
| Authentication hunt | Detect dormant account activation |
| Process hunt | Detect LOLBin abuse |
| PowerShell hunt | Detect encoded execution |

---

## 12.3 Hunting Pivot Strategy

Pivot from:

- Hash → domains
- Domain → IPs
- IP → JA3 fingerprints
- JA3 → malware family
- User agent → known framework
- Service account → lateral movement

---

# 13. Intelligence Sharing and Escalation

---

## 13.1 Internal Sharing

Threat Intelligence must provide:

- Daily actor update briefings during active campaign
- Updated IoC packages
- New ATT&CK technique mapping
- Detection recommendations
- Attribution confidence updates

---

## 13.2 External Sharing

External sharing may include:

- CERT coordination
- ISAC sharing
- Law enforcement
- Industry intelligence groups

External sharing requires:

- Legal approval
- Sanitization of sensitive data
- Executive approval for strategic sharing

---

# 14. MSSP Multi-Client Intelligence Handling

For MSSP environments:

- Maintain strict tenant segregation
- Avoid cross-client attribution assumptions
- Share only sanitized intelligence between clients
- Track actor activity across clients carefully
- Escalate if actor appears targeting multiple tenants

---

# 15. Intelligence Retention Requirements

| Intelligence Type | Retention |
|------------------|-----------|
| IoC records | Minimum 2 years |
| Attribution reports | Minimum 5 years |
| Malware samples | Minimum 2 years |
| Campaign timelines | Minimum 5 years |
| Threat actor profiles | Ongoing |

---

# 16. Common TI Integration Mistakes

| Mistake | Risk |
|---------|------|
| Overconfidence in attribution | Strategic error |
| Blocking low-confidence indicators | Operational disruption |
| Ignoring historical log search | Missed compromise |
| Not updating detections | Detection gaps |
| Failing to track infrastructure rotation | Missed reinfection |
| Treating TI as static | Outdated monitoring |

---

# 17. Documentation Requirements

| Requirement | Status |
|------------|--------|
| IoCs enriched | ☐ |
| Actor profile generated | ☐ |
| ATT&CK mapping completed | ☐ |
| Detection rules updated | ☐ |
| Hunting activities completed | ☐ |
| Infrastructure map updated | ☐ |

---

# 18. Related Documents

| Document | Path |
|----------|------|
| APT Master | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-Master.md` |
| APT L3 Forensics | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-L3-Forensics.md` |
| APT Long-Term Monitoring | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-LongTerm-Monitoring.md` |
| APT Attribution Analysis | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-Attribution-Analysis.md` |
| APT MITRE Mapping | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-MITRE-Mapping.md` |
| TI Feed Management | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Feed-Management.md` |
| TI IoC Handling SOP | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md` |

---

## 19. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 21-May-2026 | Threat Intelligence Lead | Initial version |

---

## 20. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**