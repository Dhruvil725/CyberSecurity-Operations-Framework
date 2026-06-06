# Playbook: DDoS – ISP and Vendor Coordination

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – DDoS (ISP and Vendor Coordination) |
| Document ID | IR-PB-DDoS-005 |
| Version | 1.0 |
| Effective Date | 16-May-2026 |
| Owner | Network Security Lead / SOC Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 DDoS incident |

---

## 2. Purpose

This document defines the coordination procedures between the organization,
Internet Service Providers (ISPs), cloud providers, CDN vendors, and
DDoS mitigation vendors during active DDoS incidents.

The objective of external coordination is to:
- mitigate attacks upstream before traffic reaches enterprise infrastructure
- activate scrubbing or filtering services
- reduce bandwidth saturation
- coordinate routing and mitigation changes
- obtain provider-level telemetry and support
- ensure communication is structured and timely

DDoS mitigation is often ineffective without external provider support,
especially during:
- volumetric attacks
- reflection/amplification attacks
- ISP saturation
- multi-vector attacks
- cloud-based attack campaigns

---

## 3. Scope

Applies to:
- upstream ISP coordination
- cloud provider coordination
- CDN/WAF provider coordination
- third-party DDoS mitigation providers
- MSSP-managed environments

Includes:
- mitigation requests
- routing changes
- scrubbing activation
- emergency escalation
- status communications
- evidence requests

---

## 4. Coordination Principles

| Principle | Description |
|-----------|-------------|
| Escalate Early | Upstream mitigation delays increase outage risk |
| Maintain Clear Communication | Use structured updates and timestamps |
| Preserve Technical Accuracy | Share verified metrics only |
| Document All Requests | Track actions and approvals |
| Minimize Operational Risk | Validate routing/filter changes carefully |
| Coordinate Changes Centrally | Prevent conflicting mitigation actions |

---

## 5. External Coordination Triggers

External provider coordination must begin immediately when:

| Trigger | Required Coordination |
|---------|----------------------|
| Link saturation > 70% | ISP engagement |
| Multi-gigabit volumetric attack | Scrubbing activation |
| CDN/WAF overwhelmed | Vendor escalation |
| Reflection/amplification attack | Upstream filtering |
| Repeated DDoS campaigns | Vendor intelligence support |
| BGP routing issues during attack | ISP and network coordination |
| Cloud-hosted workload targeted | Cloud provider engagement |

---

# 6. Coordination Workflow Overview

| Phase | Focus Area |
|------|-------------|
| Phase 1 | Initial provider engagement |
| Phase 2 | Technical information exchange |
| Phase 3 | Mitigation activation |
| Phase 4 | Ongoing coordination |
| Phase 5 | Stabilization and rollback |
| Phase 6 | Post-incident review |

---

# 7. Phase 1 – Initial Provider Engagement

This phase establishes communication with external providers.

---

## 7.1 ISP Engagement Procedure

Contact:
- ISP security operations
- ISP DDoS response team
- account manager (if required)

---

### Required Information for ISP

| Information | Example |
|-------------|---------|
| Target IP or subnet | 203.0.113.10 |
| Attack type | UDP flood |
| Start time | UTC timestamp |
| Peak bandwidth | 8 Gbps |
| Peak packet rate | 5 Mpps |
| Impact | Customer outage |

---

## 7.2 Cloud/CDN Vendor Engagement

For cloud or CDN environments:
- open emergency support ticket
- activate emergency mitigation profile
- request attack telemetry
- request mitigation validation

---

### Common Vendor Actions

| Vendor Capability | Purpose |
|-------------------|---------|
| Under Attack Mode | Aggressive filtering |
| Scrubbing | Remove malicious traffic |
| Bot Management | Block automated requests |
| Emergency Caching | Reduce backend load |

---

## 7.3 Escalation Priority Matrix

| Situation | Escalation Priority |
|-----------|--------------------|
| Full service outage | Critical |
| Partial degradation | High |
| Attack mitigated automatically | Medium |
| Threat intelligence request only | Low |

---

# 8. Phase 2 – Technical Information Exchange

Accurate technical details are essential for effective mitigation.

---

## 8.1 Required Attack Metrics

| Metric | Purpose |
|--------|---------|
| Bandwidth usage | Volumetric assessment |
| Packet rate | Infrastructure stress analysis |
| Requests per second | L7 flood assessment |
| Source IP count | Botnet distribution |
| ASN distribution | Traffic origin analysis |
| Top protocols | Attack classification |

---

## 8.2 Technical Evidence to Share

| Evidence Type | Shared With |
|---------------|------------|
| NetFlow data | ISP |
| PCAP samples | Vendor/ISP |
| WAF logs | CDN/WAF provider |
| Firewall logs | ISP |
| Error metrics | Cloud provider |

---

## 8.3 Communication Standards

All communications must include:
- UTC timestamps
- ticket/reference number
- affected systems
- attack metrics
- mitigation status

---

### Status Update Template

| Field | Example |
|-------|---------|
| Incident ID | INC-2026-001 |
| Current Status | Active mitigation |
| Attack Type | HTTP flood |
| Current Impact | Partial degradation |
| Mitigation Active | CDN challenge mode |
| Additional Support Required | Upstream filtering |

---

# 9. Phase 3 – Mitigation Activation

External providers may apply:
- traffic filtering
- scrubbing
- rerouting
- challenge-response protections

---

## 9.1 ISP Mitigation Options

| Mitigation Type | Purpose |
|----------------|---------|
| RTBH (Blackholing) | Protect upstream infrastructure |
| Traffic Scrubbing | Filter malicious traffic |
| ACL Filtering | Block attack signatures |
| Rate Limiting | Reduce traffic volume |
| BGP Diversion | Redirect to scrubbing center |

---

## 9.2 CDN/WAF Mitigation Options

| Mitigation Type | Purpose |
|----------------|---------|
| Challenge mode | Human verification |
| Bot filtering | Remove automation |
| Geo restrictions | Reduce regional traffic |
| Rate limiting | Protect backend |
| Request anomaly filtering | Detect attack patterns |

---

## 9.3 Cloud Provider Mitigation

| Action | Purpose |
|--------|---------|
| Autoscaling | Increase capacity |
| Traffic engineering | Reduce congestion |
| Load balancing | Distribute requests |
| DDoS protection services | Managed mitigation |

---

# 10. Phase 4 – Ongoing Coordination During Active Attack

Continuous coordination is required during prolonged attacks.

---

## 10.1 Coordination Cadence

| Severity | Update Frequency |
|----------|------------------|
| P1 | Every 15–30 minutes |
| P2 | Every 60 minutes |
| P3 | As required |

---

## 10.2 Required Ongoing Metrics

| Metric | Monitoring Goal |
|--------|----------------|
| Attack volume | Detect escalation |
| Filtered traffic | Mitigation effectiveness |
| Remaining malicious traffic | Residual risk |
| Service availability | Business impact |
| Resource utilization | Infrastructure stability |

---

## 10.3 Indicators of Mitigation Failure

| Indicator | Meaning |
|-----------|---------|
| Link saturation persists | Upstream filtering insufficient |
| Backend errors continue | L7 mitigation insufficient |
| New attack vectors appear | Multi-vector escalation |
| Increased packet rate after mitigation | Attack adaptation |

---

# 11. Phase 5 – Stabilization and Rollback Coordination

Mitigations must be removed carefully.

---

## 11.1 Rollback Conditions

Rollback should occur only when:
- traffic remains stable
- attack vectors disappear
- services operate normally
- providers confirm attack reduction

---

## 11.2 Rollback Sequence

| Step | Action |
|------|--------|
| 1 | Reduce aggressive filtering |
| 2 | Remove temporary ACLs |
| 3 | Reduce challenge mode |
| 4 | Restore normal routing |
| 5 | Continue monitoring |

---

## 11.3 Rollback Risks

| Risk | Impact |
|------|--------|
| Early rollback | Attack resumes |
| Removing all controls simultaneously | Infrastructure instability |
| Failure to monitor | Missed resurgence |

---

# 12. Phase 6 – Post-Incident Coordination Review

After mitigation:
- review provider performance
- review mitigation timelines
- review communication effectiveness
- identify SLA issues
- document lessons learned

---

## 12.1 Post-Incident Review Questions

| Question | Purpose |
|----------|---------|
| Was ISP escalation timely? | Process review |
| Did mitigation activate quickly enough? | SLA review |
| Were attack metrics accurate? | Reporting improvement |
| Was communication effective? | Coordination review |
| Were any mitigation gaps identified? | Security improvement |

---

## 12.2 Vendor Performance Tracking

| Metric | Purpose |
|--------|---------|
| Time to engage | SLA measurement |
| Time to mitigation | Operational efficiency |
| Mitigation effectiveness | Service quality |
| Communication quality | Coordination review |

---

# 13. Documentation Requirements

The following must be documented:

| Documentation Item | Required |
|-------------------|----------|
| ISP ticket numbers | Yes |
| Vendor case IDs | Yes |
| Mitigation start/end times | Yes |
| Routing/filter changes | Yes |
| Traffic metrics shared | Yes |
| Escalation timeline | Yes |

---

# 14. Common Coordination Mistakes

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Delaying ISP engagement | Prolonged outage |
| Sharing incomplete metrics | Incorrect mitigation |
| Multiple teams making independent changes | Mitigation conflict |
| Removing controls too early | Attack resurgence |
| Not documenting vendor actions | Audit gaps |

---

# 15. MSSP Client Handling Notes

For MSSP-managed environments:
- obtain client approval before major routing changes
- maintain client-specific communication channels
- document all provider interactions
- follow contractual escalation timelines
- provide client-facing summaries during active attacks

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

# 16. Related Documents

| Document | Path |
|---------|------|
| DDoS Master | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-Master.md` |
| DDoS L1 Triage | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-L1-Triage.md` |
| DDoS L2 Investigation | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-L2-Investigation.md` |
| DDoS Mitigation Steps | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-Mitigation-Steps.md` |
| DDoS MITRE Mapping | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-MITRE-Mapping.md` |
| Firewall Rule Change SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Rule-Change-Process.md` |
| Network Capture SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Capture-SOP.md` |

---

## 17. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 16-May-2026 | Network Security Lead / SOC Lead | Initial version |

---

## 18. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**