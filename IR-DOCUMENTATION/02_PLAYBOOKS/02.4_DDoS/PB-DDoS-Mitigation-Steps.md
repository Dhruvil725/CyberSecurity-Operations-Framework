# Playbook: DDoS – Mitigation Steps

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – DDoS (Mitigation Steps) |
| Document ID | IR-PB-DDoS-004 |
| Version | 1.0 |
| Effective Date | 16-May-2026 |
| Owner | Network Security Lead / IR Team Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any major DDoS incident |

---

## 2. Purpose

This document defines the operational mitigation procedures for
Distributed Denial of Service (DDoS) attacks.

The objective of mitigation is to:
- maintain service availability
- absorb or filter malicious traffic
- reduce infrastructure exhaustion
- stabilize impacted applications and services
- coordinate upstream filtering and scrubbing
- minimize customer impact
- restore operational stability as quickly as possible

This document focuses on active mitigation execution after:
- DDoS activity has been validated
- investigation has identified attack characteristics
- containment decisions have been approved

---

## 3. Scope

Applies to:
- volumetric attacks
- protocol attacks
- application-layer attacks
- hybrid DDoS campaigns
- CDN/WAF-based mitigations
- ISP-based mitigation
- on-premises and cloud-hosted infrastructure
- MSSP-managed environments

Includes:
- firewall mitigation
- WAF tuning
- CDN protections
- upstream filtering
- traffic engineering
- rate limiting
- emergency segmentation

---

## 4. Mitigation Principles

| Principle | Description |
|-----------|-------------|
| Preserve Availability | Primary goal is service continuity |
| Mitigate Closest to Source | Filter traffic upstream where possible |
| Layer Mitigation | Use network, CDN, WAF, and application controls together |
| Minimize Customer Impact | Avoid broad blocks unless necessary |
| Monitor Continuously | Attack patterns evolve during mitigation |
| Document Every Change | All mitigation changes must be tracked |

---

## 5. Mitigation Priority Order

| Priority | Objective | Example Actions |
|----------|-----------|----------------|
| P0 | Maintain service availability | Upstream scrubbing |
| P1 | Reduce malicious traffic volume | Firewall filtering |
| P2 | Protect application resources | WAF/rate limiting |
| P3 | Prevent infrastructure exhaustion | Connection limits |
| P4 | Reduce attack surface | Geo restrictions |
| P5 | Stabilize environment | Traffic tuning |

---

# 6. Mitigation Workflow Overview

| Phase | Focus Area |
|------|-------------|
| Phase 1 | Initial emergency mitigation |
| Phase 2 | Traffic filtering |
| Phase 3 | Application-layer protection |
| Phase 4 | Infrastructure stabilization |
| Phase 5 | Validation and monitoring |
| Phase 6 | Controlled rollback |

---

# 7. Phase 1 – Initial Emergency Mitigation

The first objective is reducing immediate business impact.

---

## 7.1 Immediate Mitigation Actions

| Scenario | Immediate Action |
|----------|------------------|
| Link saturation | Engage ISP scrubbing |
| HTTP flood | Enable CDN/WAF protection |
| SYN flood | Enable SYN cookies and rate limiting |
| API abuse | Apply aggressive API throttling |
| Multi-vector attack | Activate emergency mitigation profile |

---

## 7.2 Emergency Mitigation Checklist

| Action | Purpose |
|--------|---------|
| Confirm attack target | Prevent incorrect mitigation |
| Notify network team | Infrastructure coordination |
| Notify ISP/CDN | Upstream mitigation |
| Enable enhanced monitoring | Real-time visibility |
| Validate backup connectivity | Continuity assurance |

---

## 7.3 Critical Infrastructure Protection

Priority systems:
- authentication platforms
- DNS services
- VPN gateways
- customer portals
- payment systems
- APIs

---

### Protection Strategy Matrix

| Infrastructure Type | Recommended Protection |
|---------------------|------------------------|
| Public Web App | CDN + WAF |
| API Gateway | Rate limiting |
| VPN | Connection limiting |
| DNS | Anycast + provider mitigation |
| Firewall | Traffic filtering |

---

# 8. Phase 2 – Traffic Filtering and Network Mitigation

This phase focuses on reducing malicious traffic before it reaches the target.

---

## 8.1 Firewall-Based Mitigation

---

### Common Firewall Mitigation Actions

| Action | Purpose |
|--------|---------|
| Rate limiting | Reduce excessive traffic |
| Connection limiting | Prevent session exhaustion |
| Block malformed packets | Remove malicious traffic |
| Geo-blocking | Restrict attack regions |
| Protocol filtering | Block attack protocol |

---

### High-Risk Filtering Actions

| Action | Risk |
|--------|------|
| Full country block | Legitimate customer disruption |
| Broad ASN block | Business traffic impact |
| Full protocol block | Service functionality impact |

These actions require SOC Lead or Management approval.

---

## 8.2 SYN Flood Mitigation

Actions:
- enable SYN cookies
- reduce TCP timeout values
- increase SYN backlog limits
- enable rate limiting

---

### SYN Flood Indicators

| Indicator | Meaning |
|-----------|---------|
| High half-open connections | Connection exhaustion |
| SYN retransmissions | Flooding |
| Firewall session exhaustion | Infrastructure stress |

---

## 8.3 UDP Flood Mitigation

Actions:
- block unnecessary UDP services
- apply upstream filtering
- rate limit high-volume traffic
- monitor DNS/NTP amplification

---

### Common Amplification Protocols

| Protocol | Risk Level |
|----------|------------|
| DNS | High |
| NTP | High |
| Memcached | Critical |
| SSDP | Medium |
| CLDAP | High |

---

# 9. Phase 3 – Application Layer Mitigation

Layer 7 attacks target applications directly.

This phase focuses on protecting:
- web applications
- APIs
- authentication systems
- backend resources

---

## 9.1 WAF Mitigation Actions

| Action | Purpose |
|--------|---------|
| Enable challenge mode | Block bots |
| CAPTCHA enforcement | Human verification |
| URI rate limiting | Protect endpoints |
| Bot filtering | Reduce automation |
| Header validation | Detect fake requests |

---

## 9.2 HTTP Flood Mitigation

Common mitigation techniques:
- rate limiting
- session restrictions
- connection throttling
- caching static content
- prioritizing authenticated traffic

---

### HTTP Flood Indicators

| Indicator | Meaning |
|-----------|---------|
| Repeated GET requests | HTTP flood |
| Single endpoint targeting | Resource exhaustion |
| Missing browser behavior | Bot traffic |
| Excessive login requests | Auth abuse |

---

## 9.3 API Protection Measures

| Protection | Purpose |
|------------|---------|
| Per-token rate limits | Prevent abuse |
| Per-IP throttling | Reduce automated requests |
| Request quotas | Backend protection |
| API gateway filtering | Traffic management |

---

# 10. Phase 4 – Infrastructure Stabilization

After initial mitigation, infrastructure must be stabilized.

---

## 10.1 Stabilization Objectives

| Objective | Purpose |
|-----------|---------|
| Restore application responsiveness | Customer recovery |
| Reduce infrastructure load | Prevent cascading failure |
| Normalize resource usage | Stable operations |
| Validate mitigation effectiveness | Prevent recurring outages |

---

## 10.2 Resource Monitoring Requirements

| Resource | Threshold Concern |
|----------|------------------|
| CPU | Sustained >85% |
| Memory | Sustained >80% |
| Connections | Near device/session limits |
| Bandwidth | >80% utilization |
| Requests Per Second | Above baseline |

---

## 10.3 Temporary Scaling Measures

| Action | Purpose |
|--------|---------|
| Increase CDN cache usage | Reduce backend load |
| Scale cloud instances | Increase capacity |
| Enable autoscaling | Dynamic resource adjustment |
| Redirect traffic | Reduce hotspot pressure |

---

# 11. Phase 5 – Mitigation Validation and Monitoring

Mitigation is NOT complete until effectiveness is verified.

---

## 11.1 Validation Checklist

| Validation Check | Expected Result |
|------------------|----------------|
| Service reachable | Users can access application |
| Traffic stabilized | No sustained spikes |
| CPU/memory normalized | Stable infrastructure |
| WAF/CDN filtering traffic | Mitigation active |
| Error rates reduced | Service recovering |
| Attack traffic reduced | Effective filtering |

---

## 11.2 Monitoring During Active Attack

Monitor continuously for:
- attack vector changes
- mitigation bypass attempts
- traffic spikes
- backend stress
- new targeted endpoints

---

### Indicators Mitigation Is Failing

| Indicator | Meaning |
|-----------|---------|
| Traffic volume continues rising | Filtering insufficient |
| New attack protocol observed | Multi-vector escalation |
| WAF bypass indicators | L7 adaptation |
| Backend latency increasing | Resource exhaustion continues |

---

# 12. Phase 6 – Controlled Mitigation Rollback

Mitigations must NOT be removed immediately after traffic decreases.

Attackers often:
- pause attacks temporarily
- switch vectors
- test mitigation removal timing

---

## 12.1 Rollback Conditions

Rollback should occur only when:
- attack traffic remains stable at low levels
- no new vectors observed
- services stable for monitoring window
- SOC Lead approves rollback

---

## 12.2 Recommended Monitoring Window

| Severity | Monitoring Before Rollback |
|----------|---------------------------|
| P1 | Minimum 24 hours |
| P2 | Minimum 12 hours |
| P3 | Minimum 4 hours |

---

## 12.3 Rollback Sequence

| Step | Action |
|------|--------|
| 1 | Reduce aggressive rate limiting |
| 2 | Remove temporary geo-blocks |
| 3 | Reduce challenge mode |
| 4 | Remove emergency routing changes |
| 5 | Return firewall rules to normal baseline |

---

# 13. ISP and CDN Coordination

DDoS mitigation frequently requires external provider involvement.

---

## 13.1 ISP Coordination Triggers

| Trigger | Action |
|---------|--------|
| Upstream saturation | ISP scrubbing request |
| Traffic exceeds enterprise capacity | Upstream filtering |
| Reflection attack | Source filtering request |

---

## 13.2 CDN/WAF Coordination

| Action | Purpose |
|--------|---------|
| Enable under attack mode | Aggressive filtering |
| Increase challenge enforcement | Bot reduction |
| Enable emergency caching | Backend protection |
| Increase logging | Better visibility |

Reference:
`02_PLAYBOOKS/02.4_DDoS/PB-DDoS-ISP-Coordination.md`

---

# 14. Documentation Requirements

The following must be documented during mitigation.

| Documentation Item | Required |
|-------------------|----------|
| Attack type | Yes |
| Peak traffic metrics | Yes |
| Mitigation actions applied | Yes |
| Firewall changes | Yes |
| ISP/CDN engagement | Yes |
| Service impact | Yes |
| Rollback timing | Yes |

---

# 15. Common Mitigation Mistakes

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Blocking broad traffic too early | Legitimate outage |
| Ignoring Layer 7 attacks | Application remains impacted |
| Removing mitigations too early | Attack resumes |
| Failing to monitor backend resources | Hidden degradation |
| Delaying ISP escalation | Link saturation continues |
| Using single-layer mitigation only | Bypass risk |

---

# 16. MSSP Client Handling Notes

For MSSP-managed environments:
- obtain approval for high-impact filtering
- follow client-specific communication procedures
- maintain detailed mitigation logs
- coordinate ISP engagement with client stakeholders
- document all temporary controls

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

# 17. Related Documents

| Document | Path |
|---------|------|
| DDoS Master | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-Master.md` |
| DDoS L1 Triage | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-L1-Triage.md` |
| DDoS L2 Investigation | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-L2-Investigation.md` |
| ISP Coordination | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-ISP-Coordination.md` |
| DDoS MITRE Mapping | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-MITRE-Mapping.md` |
| Firewall Rule Change SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Rule-Change-Process.md` |
| IDS/IPS Tuning Guide | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/IDS-IPS-Tuning-Guide.md` |

---

## 18. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 16-May-2026 | Network Security Lead / IR Team Lead | Initial version |

---

## 19. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**