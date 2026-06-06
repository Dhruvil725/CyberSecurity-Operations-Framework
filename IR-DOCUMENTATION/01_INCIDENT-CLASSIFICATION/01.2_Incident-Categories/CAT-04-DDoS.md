# CAT-04 – Distributed Denial of Service (DDoS) Incident Category

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Incident Category – DDoS |
| Document ID | IR-CAT-004 |
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
| Category ID | CAT-04 |
| Default Severity | P1 – Critical (service down) / P2 – High (service degraded) |
| Escalation Priority | Immediate when business-critical services are impacted |
| Attack Goal | Disrupt availability of services by exhausting bandwidth or resources |
| Threat Actors | Cybercriminals, hacktivists, extortion groups, competitors |
| Playbook Reference | `02_PLAYBOOKS/02.4_DDoS/` |

---

## 3. What is a DDoS Attack?

A Distributed Denial of Service (DDoS) attack is an availability attack
in which an attacker uses multiple systems (often botnets) to overwhelm a
target service, application, or network, causing:

- Service outage (complete unavailability)
- Severe service degradation (timeouts, packet loss, latency)
- Resource exhaustion (CPU, memory, connections)
- Business disruption and reputational impact

DDoS attacks may be used as:
- Primary disruption attacks
- Diversion to hide other intrusions
- Extortion leverage (DDoS-for-ransom)

---

## 4. DDoS Attack Types

| Type | Description |
|------|-------------|
| Volumetric | Saturates bandwidth (UDP floods, amplification floods) |
| Protocol | Exhausts network equipment state tables (SYN floods, fragmented packets) |
| Application Layer | Targets application resources (HTTP floods, API floods, login floods) |
| Amplification | Uses third-party services to amplify traffic (DNS/NTP/SSDP/Memcached) |
| Multi-Vector | Combines multiple techniques simultaneously |
| DDoS Extortion | Attacker demands payment to stop the attack |

---

## 5. Common DDoS Attack Vectors

| Vector | Description |
|--------|-------------|
| UDP Flood | High-volume UDP traffic saturating bandwidth |
| SYN Flood | Exhausts TCP handshake capacity and connection tables |
| DNS Amplification | Reflection attack using open resolvers to amplify traffic |
| NTP Amplification | Reflection attack using NTP servers |
| SSDP Amplification | Reflection via UPnP/SSDP devices |
| Memcached Amplification | High amplification factor reflection |
| HTTP Flood | Large number of HTTP requests to web servers |
| API Flood | Targets application APIs with high request rates |
| TLS Handshake Flood | Exhausts CPU via expensive cryptographic operations |

---

## 6. Indicators of Compromise (IoCs) and Observables

### 6.1 Network and Infrastructure Observables

| Observable | Details |
|-----------|---------|
| Bandwidth Spike | Sudden increase in inbound traffic on ISP links |
| PPS Spike | Packets per second spike on edge devices |
| Connection Exhaustion | SYN backlog full, high connection count |
| Latency Increase | Higher response times, packet loss |
| Repeated Source IPs | Botnet patterns, rotating IPs, geo distribution |
| Reflection Patterns | High traffic from DNS/NTP/SSDP servers to victim |
| Targeted Ports | Commonly 80/443/53/123/1900/11211 |

### 6.2 Application Observables

| Observable | Details |
|-----------|---------|
| 5xx Errors | Increase in 502/503/504 errors |
| Web Server CPU High | CPU spikes on web/app servers |
| Thread Exhaustion | Application pools maxed out |
| Authentication Flood | High rate of login attempts |
| Cache Miss Surge | Increased backend DB calls due to cache bypass |

### 6.3 Log Sources

| Log Source | What to Check |
|-----------|---------------|
| Firewall / Edge Router | Traffic volume, drops, rate-limit events |
| Load Balancer / WAF | Request rate, bot patterns, rate-limit triggers |
| Web Server Logs | HTTP request surge, user-agent anomalies |
| IDS/IPS | Flood signatures and anomalies |
| ISP / DDoS Provider Portal | Scrubbing events and mitigation status |
| Cloud Provider Logs | DDoS detection events (where applicable) |

---

## 7. Severity Classification

| Scenario | Severity |
|----------|----------|
| Business-critical service down (customer-facing or revenue-impacting) | P1 – Critical |
| Sustained service degradation impacting many users | P2 – High |
| Short-duration degradation recovered quickly with minimal impact | P3 – Medium |
| Low-volume scan/flood blocked automatically with no impact | P4 – Low |
| DDoS used as diversion with concurrent intrusion indicators | P1 – Critical |

---

## 8. Immediate Response Actions

### 8.1 First 15 Minutes

- Create incident ticket and classify severity based on service impact
- Notify SOC Lead immediately for P2 and above
- Confirm scope: which services, domains, IPs, and regions are affected
- Collect baseline metrics: bandwidth, PPS, latency, error rate
- Validate whether this is legitimate traffic spike or malicious
- Engage network team immediately if P2/P1
- If DDoS provider exists, trigger mitigation workflow
- Begin monitoring for concurrent intrusion activity (diversion risk)

### 8.2 First 1 Hour

- Coordinate with ISP or DDoS mitigation provider for traffic scrubbing
- Apply rate limiting and filtering at edge (as approved)
- Enable WAF protections (bot rules, geo restrictions, request throttling)
- Work with application owners to enable caching and scale resources
- Implement temporary blocks for top offending IP ranges (careful with collateral)
- Provide hourly status updates for P2 and every 30 minutes for P1
- Notify management if service impact is significant

### 8.3 First 4 Hours

- Maintain mitigation and monitor effectiveness
- Identify attack type (volumetric, protocol, application)
- Confirm no secondary compromise during disruption window
- Assess whether customer notifications are required
- Track all mitigation changes for later rollback and audit
- Plan for post-incident tuning and mitigation improvements

---

## 9. MITRE ATT&CK Mapping (Contextual)

DDoS is generally categorized under availability impact activities.

| Tactic | Technique | ID |
|--------|-----------|----|
| Impact | Network Denial of Service | T1498 |
| Impact | Endpoint Denial of Service | T1499 |
| Impact | Service Stop | T1489 |

Note: If DDoS is used as diversion, standard intrusion techniques may also apply.

---

## 10. Key Investigation Questions

1. Which services are impacted (IP, domain, application)?
2. What is the impact level (down vs degraded vs localized)?
3. What is the attack type (volumetric, protocol, application, amplification)?
4. What is the peak bandwidth and PPS, and when did it start?
5. Are requests coming from specific geographies or ASNs?
6. Is traffic reflected/amplified (DNS/NTP/SSDP/Memcached patterns)?
7. Are WAF and load balancer protections triggering?
8. Is there evidence of diversion for intrusion (unusual logins, malware alerts)?
9. Is the DDoS mitigation provider engaged and effective?
10. What changes were applied (rate limits, blocks, WAF rules)?
11. What is the estimated time to recovery based on mitigation results?
12. Is this linked to extortion (ransom note, email threat)?

---

## 11. Critical Do's and Do Not's

### Do

- Confirm true service impact before major changes
- Engage ISP or mitigation provider early for P1/P2
- Rate-limit and block with caution to avoid collateral damage
- Document all mitigations and change approvals
- Monitor for intrusion activity during the attack (diversion risk)
- Provide consistent status updates to stakeholders

### Do Not

- Block entire regions without business approval
- Apply permanent firewall changes without change control
- Assume all traffic spikes are DDoS (validate business campaigns)
- Ignore authentication logs and privilege alerts during DDoS window
- Make public statements without legal and management approval

---

## 12. Escalation Path

| Stage | Action |
|-------|--------|
| L1 Triage | Validate alert, confirm service impact, create ticket |
| L2 Investigation | Identify attack type and confirm telemetry from edge/WAF/ISP |
| SOC Lead | Coordinate response, communications, and approvals |
| Network Team | Implement filtering, routing changes, and ISP coordination |
| Application Owner | Apply app-level mitigations (caching, scaling, throttling) |
| IR Team | Engage if diversion attack suspected or other compromise indicators exist |
| Management | Notify for P1/P2 based on business service impact |

---

## 13. Regulatory and Client Reporting Considerations

| Trigger | Action |
|--------|--------|
| Material service disruption to regulated services | Engage Compliance for reporting assessment |
| Customer-facing outage requiring disclosure | Coordinate with Legal and Communications |
| MSSP client impacted | Notify client per SLA and provide mitigation status |
| DDoS extortion threat received | Engage Legal and consider law enforcement coordination |

Reference: `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

## 14. Evidence Collection Requirements

| Evidence Type | Priority | Notes |
|--------------|----------|-------|
| Firewall / edge router traffic stats | Critical | Bandwidth and PPS graphs, drops, rules triggered |
| WAF logs and analytics | Critical | Request patterns, bot detection, rate-limit actions |
| Load balancer logs | High | Connection and request rates |
| Web server access logs | High | URL patterns, user-agents, response codes |
| ISP / DDoS provider reports | High | Scrubbing status and attack classification |
| NetFlow / sFlow data | High | Traffic distribution and top talkers |
| DNS logs (if amplification suspected) | Medium | Reflection source patterns |
| Change records | Critical | All mitigation and rule changes |
| Timeline and comms log | Critical | Updates sent to stakeholders |

Reference: `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 15. Related Documents

| Document | Path |
|---------|------|
| DDoS Master Playbook | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-Master.md` |
| L1 Triage Playbook | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-L1-Triage.md` |
| L2 Investigation Playbook | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-L2-Investigation.md` |
| Mitigation Steps | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-Mitigation-Steps.md` |
| ISP Coordination | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-ISP-Coordination.md` |
| MITRE Mapping | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-MITRE-Mapping.md` |
| P1 Critical Definition | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P1-Critical-Definition.md` |
| P2 High Definition | `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/P2-High-Definition.md` |
| Escalation Paths | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/` |

---

## 16. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 15-May-2026 | SOC Manager | Initial version |

---

## 17. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**