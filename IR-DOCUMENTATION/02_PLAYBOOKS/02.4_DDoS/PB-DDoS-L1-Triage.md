# Playbook: DDoS – L1 Triage

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – DDoS (L1 Triage) |
| Document ID | IR-PB-DDoS-002 |
| Version | 1.0 |
| Effective Date | 16-May-2026 |
| Owner | SOC Lead / Network Security Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 DDoS incident |

---

## 2. Purpose

This document defines the Level 1 (L1) SOC Analyst procedures for triaging
Distributed Denial of Service (DDoS) alerts and reports.

The objective of L1 triage is to:
- validate traffic anomalies or attack alerts
- distinguish between legitimate traffic spikes and malicious floods
- identify the target (IP, URL, Service)
- determine the attack type (Volumetric vs Application Layer) if possible
- assess business impact immediately
- initiate rapid escalation to L2 and Network Teams

DDoS incidents are time-critical; speed of triage directly impacts service availability.

---

## 3. Scope

Applies to:
- volumetric attack alerts (bandwidth saturation)
- protocol attack alerts (SYN floods, UDP floods)
- application layer alerts (HTTP/S floods)
- WAF/CDN mitigation triggers
- ISP notifications regarding upstream attacks
- user reports of service unavailability
- MSSP-managed client environments

---

## 4. L1 Safety Rules

| Rule | Reason |
|------|--------|
| Do not block entire subnets without approval | Risk of blocking legitimate users |
| Do not reboot edge devices during attack | May cause total loss of connectivity |
| Do not ignore "false positive" alerts initially | Verify before dismissing |
| Do not contact ISP directly unless authorized | Protocol requires Network Team/Lead coordination |
| Prioritize availability over investigation depth | Mitigation first, analysis second |

---

## 5. L1 SLA Targets

| Severity | Response Time | Escalation Requirement |
|----------|---------------|------------------------|
| P1 (Service Down) | Immediate | SOC Lead + Network Team immediately |
| P2 (Degraded) | Within 5 minutes | L2 within 10 minutes |
| P3 (Threat/Blocked) | Within 15 minutes | L2 review |
| P4 (Informational) | Within 30 minutes | Log and monitor |

Reference:
`00_GOVERNANCE/00.4_SLA-and-SLO/Internal-SLA-Definitions.md`

---

## 6. Inputs Required During Triage

---

### 6.1 Alert Information

| Data Point | Source |
|------------|--------|
| Alert Type | Volumetric / L7 / Protocol |
| Target IP / Domain | Firewall / WAF / CDN |
| Traffic Volume (bps/pps) | NetFlow / Monitoring |
| Duration | Start time to present |
| Source Distribution | Geo / ASN data |

---

### 6.2 Impact Assessment

| Check | Question |
|-------|----------|
| Service Status | Is the site/app reachable? |
| Latency | Is response time high? |
| Error Rates | Are 5xx errors increasing? |
| User Reports | Are customers complaining? |

---

# 7. Step-by-Step L1 Triage Procedure

---

## Step 1: Validate the Alert

Determine if the alert represents a genuine anomaly.

---

### Validation Checklist

| Check | Action |
|-------|--------|
| Compare with baseline | Is traffic significantly higher than normal? |
| Check scheduled events | Is there a marketing campaign or release causing a spike? |
| Verify source diversity | Are requests coming from thousands of IPs (DDoS) or one source (Scanner)? |
| Check protocol mix | Is there an abnormal ratio of UDP/ICMP/TCP SYN? |

---

## Step 2: Identify Attack Type (Initial Classification)

Classify the attack to guide mitigation strategy.

---

### Attack Type Indicators

| Indicator | Likely Attack Type |
|-----------|--------------------|
| High Bandwidth (Gbps), saturated link | Volumetric (UDP/ICMP Flood) |
| High Packet Rate (pps), low bandwidth | Protocol (SYN Flood) |
| High HTTP Requests (RPS), valid TCP | Application Layer (HTTP Flood) |
| Specific URL targeted | Application Layer (Targeted) |
| DNS Amplification signatures | Reflection Attack |

---

## Step 3: Assess Business Impact

Determine severity based on operational status.

---

### Impact Matrix

| Status | Description | Severity |
|--------|-------------|----------|
| **Total Outage** | Service unreachable, timeout errors | P1 |
| **Severe Degradation** | High latency, intermittent failures | P1/P2 |
| **Partial Impact** | Specific region or feature slow | P2 |
| **Mitigated** | Attack detected but blocked by auto-mitigation | P3/P4 |
| **No Impact** | Traffic spike absorbed by capacity | P4 |

---

## Step 4: Initial Containment Recommendations

L1 recommends immediate actions based on classification.

---

### Recommendation Matrix

| Scenario | Recommended Action |
|----------|-------------------|
| Volumetric Flood | Engage ISP / Scrubbing Center |
| HTTP Flood | Enable "Under Attack Mode" (Cloudflare/Akamai) |
| Single Source Flood | Block Source IP at Edge Firewall |
| Specific URL Flood | Rate limit specific URI at WAF |
| Unknown / Complex | Escalate to L2/Network Team immediately |

---

## Step 5: Ticket Creation and Documentation

Create ticket with standard naming convention.

---

### Ticket Naming Standard

`DDoS-[Target]-[AttackType]-[Severity]-[Date]`

Example:
`DDoS-WebPortal-Volumetric-P1-2026-05-16`

---

### Mandatory Fields

| Field | Required Data |
|-------|---------------|
| Target Asset | IP / URL |
| Attack Vector | UDP / TCP / HTTP |
| Peak Traffic | bps / pps / rps |
| Current Status | Up / Down / Slow |
| Evidence | Screenshots of graphs/logs |

---

## Step 6: Escalation Decision

---

### Escalate to Network Team & SOC Lead Immediately If:

| Condition | Reason |
|-----------|--------|
| Link saturation > 80% | Imminent outage |
| Service unreachable (503/Timeout) | Active business impact |
| Multiple targets attacked | Coordinated campaign |
| Extortion threat received | Legal/Executive involvement required |

---

### Escalate to L2 If:

| Condition | Reason |
|-----------|--------|
| Attack confirmed but mitigated | Investigation required |
| Suspicious traffic pattern | Analysis required |
| Recurring low-level attacks | Tuning required |

---

# 8. Evidence Preservation Requirements

L1 must capture snapshots before dashboards refresh.

| Evidence Item | Source |
|---------------|--------|
| Traffic Graph (Ingress/Egress) | Monitoring Tool |
| Top Talkers List | NetFlow / Firewall |
| Top Protocols | NetFlow |
| Error Rate Graph | APM / Web Server |
| WAF/CDN Logs | Security Console |

---

# 9. Common L1 Mistakes

| Mistake | Risk | Correct Approach |
|---------|------|------------------|
| Treating as standard network issue | Delayed mitigation | Treat as security incident |
| Blocking single IP in volumetric attack | Ineffective | Volumetric requires upstream help |
| Ignoring L7 attacks | App crash | Monitor RPS and error rates |
| Failing to check scheduled events | False alarm | Verify with Change Management |

---

# 10. MSSP Handling Notes

For MSSP environments:
- confirm client ownership of target IP
- notify client SDM immediately upon P1 confirmation
- follow client-specific communication channels
- do not engage ISP without client authorization (unless emergency)

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

# 11. Related Documents

| Document | Path |
|---------|------|
| DDoS Master | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-Master.md` |
| DDoS L2 Investigation | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-L2-Investigation.md` |
| DDoS Mitigation Steps | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-Mitigation-Steps.md` |
| ISP Coordination | `02_PLAYBOOKS/02.4_DDoS/PB-DDoS-ISP-Coordination.md` |
| Network Capture SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Capture-SOP.md` |

---

## 12. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 16-May-2026 | SOC Lead / Network Security Lead | Initial version |

---

## 13. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

End of Document