# Playbook: Distributed Denial of Service (DDoS) Response (Master)

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Distributed Denial of Service (DDoS) Response (Master) |
| Document ID | IR-PB-DDoS-001 |
| Version | 1.0 |
| Effective Date | 16-May-2026 |
| Owner | SOC Manager / Network Security Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 DDoS incident |

---

## 2. Purpose

This master playbook defines the end-to-end response procedures for
Distributed Denial of Service (DDoS) incidents affecting enterprise or
MSSP-managed environments.

The objectives of this playbook are to:
- rapidly identify DDoS activity
- minimize business disruption
- coordinate mitigation activities
- maintain service availability
- preserve evidence and attack telemetry
- coordinate with ISPs, cloud providers, and mitigation vendors
- standardize escalation and communication procedures
- improve resilience against future attacks

This playbook applies to:
- volumetric DDoS attacks
- application-layer DDoS attacks
- protocol abuse attacks
- reflection/amplification attacks
- hybrid DDoS campaigns
- extortion-based DDoS threats

---

## 3. Scope

Applies to:
- internet-facing applications
- APIs and web services
- VPN gateways
- DNS infrastructure
- cloud-hosted workloads
- on-premises infrastructure
- MSSP-managed client environments

Includes:
- network-layer mitigation
- application-layer mitigation
- ISP coordination
- cloud mitigation coordination
- incident communications
- post-incident analysis

Out of scope:
- hardware failure outages
- non-malicious traffic spikes
- application bugs unrelated to malicious activity

---

## 4. Definitions

| Term | Definition |
|------|------------|
| DDoS | Distributed Denial of Service |
| Volumetric Attack | High-bandwidth traffic flood |
| L7 Attack | Application-layer attack targeting HTTP/HTTPS |
| Reflection Attack | Attack using third-party services to amplify traffic |
| Amplification Attack | Attack multiplying traffic volume using protocols like DNS/NTP |
| Scrubbing Center | Traffic filtering infrastructure |
| Botnet | Network of compromised systems used in attack |
| SYN Flood | TCP connection exhaustion attack |
| RPS | Requests Per Second |

---

## 5. Severity Classification Guidance

Severity depends on:
- business impact
- service availability
- attack scale
- customer impact
- mitigation effectiveness

---

### 5.1 DDoS Severity Matrix

| Scenario | Recommended Severity |
|----------|----------------------|
| Critical customer-facing outage | P1 |
| Large-scale attack impacting multiple services | P1 |
| Service degradation with active mitigation | P2 |
| Localized application slowdown | P3 |
| Low-volume blocked attack | P4 |

Reference:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

---

## 6. Activation Criteria

Activate this playbook when any of the following occur:

| Trigger | Example |
|---------|---------|
| Sudden traffic spike | Unexpected inbound bandwidth |
| HTTP flood | High request rate to web app |
| SYN flood alert | TCP exhaustion attack |
| ISP notification | Upstream provider alert |
| WAF alert | Application-layer flood |
| CDN alert | Edge mitigation triggered |
| Service degradation | Slow or unavailable application |
| Extortion email | Threat actor demands payment |

---

## 7. DDoS Attack Categories

| Attack Type | Description | Common Target |
|-------------|-------------|----------------|
| Volumetric | Consumes bandwidth | Internet links |
| Protocol Attack | Exhausts infrastructure resources | Firewalls/load balancers |
| Application Layer | Targets web applications | APIs/web apps |
| Reflection/Amplification | Uses third-party services | Public services |
| Multi-Vector | Combines multiple techniques | Enterprise environments |

---

# 8. Roles and Responsibilities

| Role | Responsibilities |
|------|------------------|
| L1 SOC Analyst | Alert validation and escalation |
| L2 SOC Analyst | Traffic analysis and scoping |
| Network Team | Firewall and routing changes |
| SOC Lead | Incident coordination |
| ISP/Vendor | Upstream mitigation |
| Cloud Team | CDN/WAF scaling and protection |
| IR Team | Major incident coordination |
| MSSP SDM | Client communication |

Reference:
`00_GOVERNANCE/00.3_Roles-and-Responsibilities/RACI-Matrix-IR.xlsx`

---

# 9. DDoS Incident Lifecycle

| Phase | Description |
|------|-------------|
| Detection | Identify attack activity |
| Analysis | Determine type and scope |
| Containment | Apply mitigation controls |
| Stabilization | Restore service performance |
| Recovery | Return to normal operations |
| Post-Incident | Review and improve defenses |

---

# 10. High-Level Response Workflow

---

## Phase A – Detection and Qualification

Performed by:
- L1 SOC
- Monitoring teams
- CDN/WAF providers

Activities:
- validate attack indicators
- identify impacted services
- determine traffic abnormality
- classify severity

Outputs:
- incident ticket
- initial traffic metrics
- escalation recommendation

Reference:
`02_PLAYBOOKS/02.4_DDoS/PB-DDoS-L1-Triage.md`

---

## Phase B – Analysis and Scoping

Performed by:
- L2 SOC
- Network team

Activities:
- identify attack type
- determine source distribution
- identify targeted applications/services
- review traffic patterns
- determine mitigation strategy

Outputs:
- attack profile
- source analysis
- mitigation recommendations

Reference:
`02_PLAYBOOKS/02.4_DDoS/PB-DDoS-L2-Investigation.md`

---

## Phase C – Mitigation and Containment

Activities:
- apply firewall blocks
- enable rate limiting
- engage CDN/WAF protections
- coordinate ISP mitigation
- reroute traffic to scrubbing provider

Outputs:
- reduced attack impact
- stabilized services
- blocked malicious traffic

Reference:
`02_PLAYBOOKS/02.4_DDoS/PB-DDoS-Mitigation-Steps.md`

---

## Phase D – Recovery

Activities:
- restore normal traffic flow
- remove temporary controls carefully
- validate application stability
- monitor for recurring attacks

Outputs:
- stable production services
- temporary mitigations reviewed

---

## Phase E – Post-Incident Activities

Activities:
- attack analysis
- mitigation review
- lessons learned
- detection tuning
- resilience improvements

Outputs:
- PIR documentation
- updated mitigations
- detection improvements

Reference:
`08_POST-INCIDENT/`

---

# 11. Key Investigation Areas

| Investigation Area | Purpose |
|--------------------|---------|
| Source IP distribution | Identify attack spread |
| Traffic protocol analysis | Identify attack type |
| Requests per second | Measure impact |
| Geographic distribution | Understand attack origin |
| User-agent analysis | Detect bot behavior |
| Targeted endpoints | Identify attack objective |
| CDN/WAF telemetry | Mitigation effectiveness |

---

# 12. Escalation Criteria

---

## 12.1 Escalate to Network Team if:

| Condition | Reason |
|-----------|--------|
| Bandwidth saturation | Routing changes required |
| Firewall exhaustion | Infrastructure impact |
| SYN flood detected | Protocol mitigation required |
| Multiple subnets impacted | Enterprise-wide mitigation |

---

## 12.2 Escalate to IR Team if:

| Condition | Reason |
|-----------|--------|
| Customer-facing outage | Business impact |
| Extortion demand received | Legal and executive involvement |
| Multi-vector attack | Coordinated response required |
| Mitigation ineffective | Crisis response needed |

---

# 13. Communication Requirements

| Audience | Trigger | Frequency |
|----------|---------|-----------|
| SOC Lead | P2+ incidents | Immediate |
| Management | P1 incidents | Per SLA |
| Clients | MSSP incidents | Per contract |
| ISP/Cloud Vendor | Upstream impact | Immediate |
| Application Owners | Service degradation | Immediate |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/`

---

# 14. Evidence Preservation Requirements

Preserve:
- NetFlow data
- firewall logs
- WAF logs
- CDN telemetry
- packet captures
- ISP reports
- attack timelines
- screenshots and dashboards

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

# 15. Common DDoS Response Mistakes

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Blocking entire regions too early | Business disruption | Use targeted mitigation |
| Ignoring application-layer attacks | Mitigation bypass | Monitor L7 traffic |
| Failing to coordinate with ISP | Upstream saturation | Escalate early |
| Removing mitigations too quickly | Attack resumes | Monitor stabilization |
| Not preserving traffic data | Weak analysis | Preserve logs and PCAPs |

---

# 16. MSSP Considerations

For MSSP-managed environments:
- follow client-specific escalation rules
- coordinate mitigation approvals
- maintain traffic and evidence segregation
- communicate mitigation status regularly
- follow contractual SLA timelines

Reference:
`09_MSSP-SPECIFIC/`

---

# 17. Related Documents

| Document | Path |
|---------|------|
| DDoS L1 Triage | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-L1-Triage.md` |
| DDoS L2 Investigation | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-L2-Investigation.md` |
| DDoS Mitigation Steps | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-Mitigation-Steps.md` |
| ISP Coordination | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-ISP-Coordination.md` |
| DDoS MITRE Mapping | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-MITRE-Mapping.md` |
| Firewall SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Rule-Change-Process.md` |
| Network Capture SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Capture-SOP.md` |

---

## 18. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 16-May-2026 | SOC Manager / Network Security Lead | Initial version |

---

## 19. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**