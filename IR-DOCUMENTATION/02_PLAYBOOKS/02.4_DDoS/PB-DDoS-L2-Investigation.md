# Playbook: DDoS – L2 Investigation

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – DDoS (L2 Investigation) |
| Document ID | IR-PB-DDoS-003 |
| Version | 1.0 |
| Effective Date | 16-May-2026 |
| Owner | L2 SOC Lead / Network Security Lead |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 DDoS incident |

---

## 2. Purpose

This document defines the Level 2 (L2) investigation procedures for
Distributed Denial of Service (DDoS) incidents escalated from L1 triage.

The objective of L2 investigation is to:
- confirm the DDoS attack type and characteristics
- determine attack scope and business impact
- identify attack vectors and infrastructure being targeted
- distinguish malicious traffic from legitimate high-volume traffic
- determine mitigation effectiveness
- coordinate escalation to network, cloud, ISP, or IR teams
- support rapid containment and recovery decisions

Unlike L1 triage, L2 focuses on:
- detailed traffic analysis
- attack pattern identification
- infrastructure-level scoping
- mitigation optimization
- attack attribution indicators (where applicable)

This phase is highly time-sensitive because prolonged DDoS activity may:
- cause extended outages
- exhaust infrastructure resources
- trigger cascading failures
- disrupt customer access and business operations

---

## 3. Scope

Applies to:
- volumetric DDoS attacks
- SYN floods
- UDP floods
- HTTP/HTTPS floods
- DNS amplification attacks
- NTP amplification attacks
- CDN/WAF-triggered mitigation events
- API abuse and request floods
- MSSP-managed client environments

Includes:
- on-premises infrastructure
- cloud environments
- hybrid architectures
- edge services
- CDN and WAF platforms

---

## 4. Preconditions Before Investigation

L2 investigation begins after:
- L1 validation completed
- incident ticket created
- severity assigned
- SOC Lead notified (P1/P2)
- initial containment actions initiated where applicable

Required inputs from L1:

| Required Input | Purpose |
|---------------|---------|
| Attack type estimate | Initial classification |
| Impacted service/IP/domain | Scope identification |
| Traffic metrics | Initial baseline comparison |
| Traffic screenshots | Quick visual review |
| Alert source | Correlation |
| Initial severity | Escalation context |

Reference:
`02_PLAYBOOKS/02.4_DDoS/PB-DDoS-L1-Triage.md`

---

# 5. L2 Investigation Objectives

| Objective | Description |
|-----------|-------------|
| Confirm Attack Type | Identify exact DDoS technique |
| Measure Attack Scale | Quantify impact and intensity |
| Identify Attack Sources | Understand source distribution |
| Determine Business Impact | Evaluate operational disruption |
| Validate Mitigation Effectiveness | Confirm controls are working |
| Identify Infrastructure Weaknesses | Determine bottlenecks |
| Support Containment | Recommend mitigation changes |
| Identify Recurring Patterns | Detect repeated campaigns |

---

# 6. Investigation Workflow Overview

| Phase | Focus Area |
|------|-------------|
| Phase 1 | Traffic and attack validation |
| Phase 2 | Traffic profiling and classification |
| Phase 3 | Infrastructure impact analysis |
| Phase 4 | Source and geographic analysis |
| Phase 5 | Application-layer analysis |
| Phase 6 | Mitigation effectiveness review |
| Phase 7 | Scope expansion and correlation |
| Phase 8 | Escalation and containment recommendations |

---

# 7. Phase 1 – Traffic and Attack Validation

The first step is confirming that the observed activity is malicious
and not caused by legitimate business traffic spikes.

---

## 7.1 Baseline Comparison

Compare current traffic to:
- normal traffic baseline
- same-day historical traffic
- scheduled campaigns/events
- maintenance windows

---

### Traffic Validation Checklist

| Validation Check | Purpose |
|------------------|---------|
| Compare current bandwidth to normal peak | Detect volumetric spikes |
| Compare requests per second (RPS) | Detect L7 floods |
| Compare packet rate (pps) | Detect protocol floods |
| Review user-agent diversity | Detect automation |
| Review ASN concentration | Detect botnet patterns |

---

## 7.2 Legitimate Traffic vs DDoS Indicators

| Indicator | Legitimate Traffic | DDoS Traffic |
|-----------|-------------------|--------------|
| User-Agent Diversity | High | Often repetitive or fake |
| Geographic Distribution | Expected customer regions | Global/randomized |
| Session Behavior | Full sessions | Short or incomplete sessions |
| Request Pattern | Natural browsing flow | Repetitive targeting |
| Source ASN | ISP/customer mix | VPS/cloud-heavy |

---

## 7.3 Key Questions

| Question | Investigation Purpose |
|----------|----------------------|
| Is traffic saturating the link? | Volumetric confirmation |
| Are requests valid but excessive? | Application-layer attack |
| Is the attack distributed globally? | Botnet assessment |
| Is there a single targeted endpoint? | Attack objective analysis |
| Is mitigation already active? | Containment validation |

---

# 8. Phase 2 – Traffic Profiling and Classification

This phase identifies the exact attack type and traffic characteristics.

---

## 8.1 Volumetric Attack Indicators

| Indicator | Description |
|-----------|-------------|
| High bandwidth utilization | Link saturation |
| Large UDP packets | UDP flood |
| ICMP spikes | ICMP flood |
| DNS/NTP responses | Amplification attack |
| Multi-gigabit traffic | Large-scale volumetric attack |

---

## 8.2 Protocol Attack Indicators

| Indicator | Description |
|-----------|-------------|
| SYN packet spikes | SYN flood |
| Half-open TCP connections | Connection exhaustion |
| ACK floods | Stateful device exhaustion |
| Fragmented packets | Evasion attempt |

---

## 8.3 Application Layer Indicators

| Indicator | Description |
|-----------|-------------|
| High HTTP GET/POST requests | HTTP flood |
| Specific URI targeted | Application exhaustion |
| Valid TCP handshake but malicious behavior | Layer 7 flood |
| High requests from limited sessions | Automated attack |

---

## 8.4 Hybrid Attack Indicators

Hybrid attacks combine:
- volumetric floods
- application floods
- protocol abuse

---

### Common Hybrid Attack Pattern

| Attack Stage | Objective |
|--------------|-----------|
| Volumetric flood | Distract and overload |
| HTTP flood | Crash application |
| Login/API abuse | Exhaust backend services |

---

# 9. Phase 3 – Infrastructure Impact Analysis

This phase determines what systems are failing or degrading.

---

## 9.1 Impact Review Areas

| Infrastructure Component | Investigation Focus |
|--------------------------|---------------------|
| Internet links | Saturation |
| Firewalls | Session exhaustion |
| Load balancers | Connection exhaustion |
| Web servers | CPU/RAM exhaustion |
| APIs | Request queue saturation |
| Databases | Backend overload |
| CDN/WAF | Mitigation status |

---

## 9.2 Resource Exhaustion Indicators

| Indicator | Meaning |
|-----------|---------|
| High CPU on edge devices | Packet flood |
| Memory exhaustion | Session tracking overload |
| High SYN backlog | TCP flood |
| Increased 5xx errors | Application failure |
| High latency | Resource exhaustion |

---

## 9.3 Business Impact Assessment

| Impact Area | Assessment Questions |
|-------------|---------------------|
| Customer access | Can users access services? |
| Authentication | Are login systems affected? |
| APIs | Are integrations failing? |
| Revenue impact | Are transactions disrupted? |
| SLA impact | Are contractual thresholds breached? |

---

# 10. Phase 4 – Source and Geographic Analysis

Understanding attack source distribution helps optimize mitigation.

---

## 10.1 Source Analysis

Review:
- source IP distribution
- autonomous systems (ASN)
- countries/regions
- cloud provider usage
- spoofing indicators

---

### Common Source Indicators

| Indicator | Meaning |
|-----------|---------|
| Thousands of distributed IPs | Botnet |
| Heavy cloud/VPS presence | Hosted attack infrastructure |
| Single-country concentration | Regional attack source |
| Spoofed IPs | Reflection/amplification |

---

## 10.2 Reflection and Amplification Analysis

| Protocol | Amplification Risk |
|----------|-------------------|
| DNS | High |
| NTP | High |
| Memcached | Very High |
| SSDP | Medium |
| CLDAP | High |

---

## 10.3 Geographic Analysis

Key questions:
- are requests coming from expected customer regions?
- is traffic heavily concentrated from unusual geographies?
- are known proxy/VPN providers involved?

---

# 11. Phase 5 – Application-Layer Analysis

Layer 7 attacks often bypass traditional volumetric mitigation.

---

## 11.1 HTTP/HTTPS Flood Analysis

Review:
- target URLs
- request headers
- session behavior
- cookie handling
- authentication attempts

---

### Common L7 Attack Indicators

| Indicator | Meaning |
|-----------|---------|
| Same URI repeatedly requested | Resource exhaustion |
| No browser rendering behavior | Automation |
| Invalid or fake user-agents | Bot traffic |
| High login requests | Credential abuse attempt |
| API endpoint flooding | Backend exhaustion |

---

## 11.2 Bot Behavior Analysis

| Behavior | Suspicious Indicator |
|----------|---------------------|
| Missing JavaScript execution | Non-browser bot |
| Repeated identical headers | Automation |
| No cookie persistence | Scripted attack |
| High request concurrency | Botnet |

---

# 12. Phase 6 – Mitigation Effectiveness Review

L2 must continuously evaluate whether mitigation is working.

---

## 12.1 Mitigation Validation Checklist

| Check | Expected Result |
|------|----------------|
| Bandwidth reduced | Attack absorbed |
| Error rates decreased | Service stabilizing |
| CDN mitigation active | Requests filtered |
| WAF blocks increasing | Malicious traffic identified |
| User access restored | Business impact reduced |

---

## 12.2 Common Mitigation Actions

| Mitigation | Purpose |
|------------|---------|
| Rate limiting | Reduce abusive traffic |
| Geo-blocking | Restrict attack regions |
| CAPTCHA challenge | Filter bots |
| CDN/WAF under attack mode | L7 protection |
| ISP scrubbing | Upstream filtering |

---

## 12.3 Signs Mitigation Is Failing

| Indicator | Meaning |
|-----------|---------|
| Traffic still saturates links | Upstream filtering insufficient |
| CPU continues increasing | Application still overloaded |
| WAF bypass detected | Attack adaptation |
| New attack vectors appear | Multi-vector escalation |

---

# 13. Phase 7 – Scope Expansion and Correlation

Determine whether:
- multiple services are targeted
- attacks are recurring
- attacks correlate with prior incidents

---

## 13.1 Correlation Activities

| Activity | Purpose |
|----------|---------|
| Compare attack fingerprints | Recurring campaign |
| Review historical attacks | Pattern identification |
| Review extortion messages | Threat actor correlation |
| Compare source ASN patterns | Botnet tracking |

---

## 13.2 Multi-Service Targeting Indicators

| Indicator | Risk |
|-----------|------|
| API and web targeted together | Coordinated attack |
| DNS infrastructure targeted | Enterprise-wide risk |
| VPN targeted | Remote workforce disruption |
| Authentication service targeted | Business outage risk |

---

# 14. Phase 8 – Escalation and Containment Recommendations

---

## 14.1 Escalate to Network Team if:

| Condition | Reason |
|-----------|--------|
| Link saturation exceeds thresholds | Routing changes required |
| Firewall performance degraded | Infrastructure exhaustion |
| Multiple edge devices impacted | Enterprise impact |
| ISP involvement required | Upstream filtering needed |

---

## 14.2 Escalate to IR Team if:

| Condition | Reason |
|-----------|--------|
| Customer-facing outage | Major business disruption |
| Extortion demand present | Executive/legal involvement |
| Mitigation failing | Crisis coordination required |
| Multi-vector attack evolving | Complex incident management |

---

## 14.3 Containment Recommendations

| Finding | Recommended Action |
|---------|-------------------|
| Volumetric flood | ISP scrubbing |
| HTTP flood | WAF challenge mode |
| Login/API abuse | Aggressive rate limiting |
| Single-region attack | Geo-blocking |
| Bot traffic | CAPTCHA and behavioral filtering |

Reference:
`02_PLAYBOOKS/02.4_DDoS/PB-DDoS-Mitigation-Steps.md`

---

# 15. Investigation Documentation Requirements

The following must be documented:

| Documentation Item | Required |
|-------------------|----------|
| Attack type confirmed | Yes |
| Peak traffic metrics recorded | Yes |
| Source analysis completed | Yes |
| Impact assessment completed | Yes |
| Mitigation effectiveness reviewed | Yes |
| Escalation actions documented | Yes |
| IOC list updated | Yes |

---

# 16. Common L2 Investigation Mistakes

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Treating all spikes as volumetric | Wrong mitigation |
| Ignoring Layer 7 traffic | App outage continues |
| Blocking entire countries too early | Customer impact |
| Failing to monitor mitigation effectiveness | Ongoing outage |
| Not reviewing backend resource exhaustion | Partial outage missed |
| Failing to correlate recurring attacks | Missed campaign patterns |

---

# 17. MSSP Client Handling Notes

For MSSP-managed environments:
- coordinate all mitigation changes with client-approved procedures
- maintain client traffic segregation
- follow client-specific SLA escalation
- document all ISP and vendor coordination
- maintain communication cadence during active attack

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

# 18. Related Documents

| Document | Path |
|---------|------|
| DDoS Master | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-Master.md` |
| DDoS L1 Triage | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-L1-Triage.md` |
| DDoS Mitigation Steps | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-Mitigation-Steps.md` |
| ISP Coordination | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-ISP-Coordination.md` |
| DDoS MITRE Mapping | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-MITRE-Mapping.md` |
| Network Capture SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Capture-SOP.md` |

---

## 19. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 16-May-2026 | L2 SOC Lead / Network Security Lead | Initial version |

---

## 20. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

End of Document