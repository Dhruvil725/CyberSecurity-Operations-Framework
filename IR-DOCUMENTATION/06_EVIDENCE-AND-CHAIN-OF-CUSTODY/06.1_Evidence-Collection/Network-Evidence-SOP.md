# SOP: Network Evidence Collection and Handling

---

# 1. Document Control

| Field | Value |
|---|---|
| Document Name | SOP – Network Evidence Collection and Handling |
| Document ID | EVD-COL-005 |
| Version | 1.0 |
| Effective Date | 30-May-2026 |
| Owner | Network Security Lead / Evidence Custodian |
| Approved By | IR Team Lead |
| Classification | Internal – Confidential / Restricted (case-dependent) |
| Review Cycle | Quarterly |

---

# 2. Purpose

This SOP defines how to collect, preserve, validate, store, and reference **network evidence** used for investigations, incident response, forensic analysis, regulatory reporting, and audits.

Network evidence is critical because:

- It validates attacker communications (C2), exfiltration paths, scanning, and lateral movement
- It corroborates endpoint and SIEM findings with independent telemetry
- Some network evidence is highly time-sensitive (short retention buffers)
- Poor handling can expose sensitive data (PCAP may include credentials/PII)
- Evidence integrity must be protected for legal/regulatory contexts
- MSSP operations require strict tenant segregation of evidence and routing

This SOP ensures:

- Consistent standards for collecting network logs and packet data (PCAP)
- Priority-driven collection aligned to P1/P2 incident timelines
- Evidence-grade integrity controls (hashing, CoC when required)
- Secure storage and controlled access
- Clear documentation and traceability to tickets and evidence logs

---

# 3. Scope

This SOP applies to network evidence from:

| Source | Examples |
|---|---|
| Firewall | allow/deny logs, NAT logs, rule hit counters |
| Proxy / Secure Web Gateway | URL logs, bytes in/out, user mapping |
| DNS | query logs, response logs |
| VPN / Remote access | authentication logs, session logs, source IPs |
| IDS/IPS | alerts, signature hits, packet extracts |
| Network flow | NetFlow/sFlow/IPFIX metadata |
| Packet capture | PCAP from SPAN/TAP/firewall capture |
| Cloud network | VPC/VNET flow logs, cloud firewall logs |

Out of scope:

- Disk/memory forensic acquisitions (covered elsewhere)
- Long-term network architecture redesign

References:  
`04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Capture-SOP.md`  
`04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Block-Request-SOP.md`

---

# 4. Definitions

| Term | Definition |
|---|---|
| Network evidence | Logs, metadata, and packet data proving network events |
| PCAP | Packet capture containing full packet payloads and headers |
| Flow logs | Aggregated metadata (no payload) of network connections |
| C2 | Command-and-control communications |
| Exfiltration | Unauthorized data transfer out of the environment |
| TTL | Time-to-live (operational): how long evidence remains available before rotation |
| Evidence-grade | Evidence requiring hash/CoC for defensibility |
| Tenant | MSSP client environment |

---

# 5. Roles and Responsibilities

| Role | Responsibilities |
|---|---|
| L1 Analyst | Capture initial network indicators; request urgent log preservation via ticket |
| L2 Analyst | Define evidence scope and time window; request PCAP/exports; validate relevance |
| L3/Forensics | Evidence-grade handling; correlation with host artifacts; integrity validation |
| SOC Lead | Prioritizes network evidence collection for P1/P2; manages escalation and SLA |
| Network Security Engineer | Executes device exports/PCAP captures; implements safe filters and time boxing |
| Network Security Lead | Approves high-impact captures/changes; ensures safe execution |
| Evidence Custodian | Ensures secure storage, access control, retention, and transfer documentation |
| Compliance/Legal | Determines CoC needs and disclosure constraints |
| MSSP SDM | Ensures tenant scoping and client approvals where required |

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md`  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`

---

# 6. Network Evidence Principles (Mandatory)

| Principle | Requirement |
|---|---|
| Preserve early | Network logs/PCAP can rotate quickly; collect early for P1/P2 |
| Scope and minimize | Use filters and time-boxing; avoid capturing unnecessary sensitive traffic |
| Integrity protection | Hash evidence packages when evidence-grade |
| Secure storage | Store only in evidence repository; avoid local storage |
| Traceability | Document device, interface, query/filter, window, and collector |
| Avoid disruption | Captures and exports must not degrade network performance |
| Tenant segregation (MSSP) | Evidence must be client-scoped and stored separately |

---

# 7. Evidence Priority (By Severity)

## 7.1 P1/P2 Priority Network Evidence (Immediate)

Collect as feasible:

- Firewall logs for suspected destinations and bytes transferred
- Proxy logs for URL/domain access and download events
- DNS logs for suspicious domain resolution
- VPN logs for suspicious sessions/locations
- IDS/IPS alerts and packet extracts
- PCAP (targeted, filtered) when:
  - exfiltration suspected
  - exploit traffic needs validation
  - C2 patterns require confirmation

## 7.2 P3/P4 Priority Network Evidence (Targeted)

Collect only:

- logs relevant to the alert entity and time window
- evidence required for FP/TP decision and tuning recommendations

---

# 8. Evidence-Grading and CoC Triggers

Network evidence is evidence-grade when:

- regulatory reporting is required/likely
- legal hold is issued
- law enforcement engagement occurs
- P1/P2 incidents with high impact
- client contract requires forensic-grade handling

Evidence-grade requirements:

- SHA256 hashing of exported log bundles/PCAP
- controlled access
- CoC for transfers when required

References:  
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Transfer-Form.md`  
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`

---

# 9. Network Evidence Collection Workflow (Standard)

## 9.1 Step 1 — Define Scope and Time Window (UTC)

Owner: L2/L3

Define:

- entities: src/dst IPs, hostnames, usernames, ports, protocols
- devices: firewall/proxy/DNS/VPN/IDS
- window: start/end time (UTC) including context

Recommended baseline windows:

- P1/P2: ±24 hours around detection (or more if dwell suspected)
- P3/P4: minimum necessary window

---

## 9.2 Step 2 — Select Evidence Type (Logs vs Flow vs PCAP)

Use this decision guidance:

| Need | Best Evidence Type |
|---|---|
| Confirm connection occurred | Firewall logs / flow logs |
| Confirm URL accessed and bytes downloaded | Proxy logs |
| Confirm domain resolution | DNS logs |
| Confirm exploit payload or protocol details | PCAP (filtered) |
| Confirm exfiltration volume and destination | Proxy/firewall logs + flow logs; PCAP only if necessary |
| Correlate with endpoint process | EDR + proxy/firewall logs |

PCAP is the most sensitive; use only when required and filtered.

---

## 9.3 Step 3 — Export Logs / Collect PCAP

Owner: Network Security Engineer (execution) + L2 (requirements)

### Export Requirements (Mandatory)

For every export/capture record:

| Item | Requirement |
|---|---|
| Device name and location | Mandatory |
| Interface/zone (if relevant) | Mandatory |
| Query/filter parameters | Mandatory |
| Time window (UTC) | Mandatory |
| Export format | Mandatory |
| Collector | Mandatory |
| Export time (UTC) | Mandatory |
| Output filename(s) | Mandatory |

### PCAP Safety Requirements (Mandatory)

- Must be filtered (BPF) where feasible
- Must be time-boxed (e.g., 5–15 minutes) unless justified
- Must avoid capturing sensitive unrelated segments
- Must be coordinated with SOC Lead for P1/P2
- Must be documented in ticket

Reference:
`04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Capture-SOP.md`

---

## 9.4 Step 4 — Validate Completeness and Relevance

Owner: L2/L3

Validation checks:

- logs contain expected fields (src/dst/port/action/bytes)
- time range correct and in UTC
- captures are not empty/truncated
- PCAP file opens and has traffic matching filter
- document any gaps (e.g., “DNS logging not enabled”)

---

## 9.5 Step 5 — Package, Hash, and Store (Evidence-Grade)

Owner: Evidence Custodian / L3

If evidence-grade:

- package exports/captures into ZIP/TAR
- compute SHA256 of package (and PCAP itself if standalone)
- store in evidence repository
- restrict access appropriately
- record hashes and paths in ticket + evidence log

---

# 10. Source-Specific Guidance (Minimum)

## 10.1 Firewall Logs

Collect:

- deny/allow events
- rule ID/name
- NAT translations (if relevant)
- bytes and session durations (if available)

Best for:

- C2 destinations
- exfil destination validation
- inbound exploit attempts

## 10.2 Proxy Logs

Collect:

- URL/domain
- user identity mapping
- bytes downloaded/uploaded
- response codes
- user-agent (if available)

Best for:

- phishing payload downloads
- exfil via web protocols
- malicious URL access validation

## 10.3 DNS Logs

Collect:

- query name
- response IPs
- client IP/host
- timestamp (UTC)

Best for:

- detecting malicious domain resolution
- building campaign scope

## 10.4 VPN Logs

Collect:

- login successes/failures
- source IP/country (if available)
- MFA events
- session duration

Best for:

- suspicious access validation
- credential attack scoping

## 10.5 IDS/IPS Evidence

Collect:

- signature ID/name
- severity
- packet extracts if available
- sensor location and traffic direction

Best for:

- exploit validation
- attack method evidence

## 10.6 Flow Logs

Collect:

- src/dst IP/port
- bytes
- start/end timestamps

Best for:

- large-scale scoping
- exfil volume estimation without payload exposure

---

# 11. Storage and Naming Standards

## 11.1 Naming Convention (Recommended)

`INC-[ID]_NET_[SOURCE]_[SCOPE]_[YYYYMMDD_HHMM]UTC.[ext]`

Examples:

- `INC-2026-0102_NET_FW_outboundIOC_20260530_0415UTC.csv`
- `INC-2026-0102_NET_PCAP_exfilSuspect_FIN-WS-12_20260530_0430UTC.pcap`

## 11.2 Storage Requirements

- evidence repository only
- encrypted at rest
- access-controlled
- tenant segregated (MSSP)

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md`

---

# 12. MSSP Multi-Tenant Requirements (Mandatory)

| Requirement | Standard |
|---|---|
| Tenant/client verified before export/capture | Mandatory |
| Client evidence stored separately | Mandatory |
| No cross-client logs/captures | Mandatory |
| Client approval for PCAP (if required) | Mandatory (contract-dependent) |
| Client-safe evidence references for reporting | Mandatory |

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`

---

# 13. Common Mistakes and Controls

| Mistake | Risk | Control |
|---|---|---|
| Capturing broad PCAP without filter | Sensitive data exposure | Filter + time-box mandatory |
| Waiting too long (logs rotate) | Evidence loss | Prioritize early collection for P1/P2 |
| Missing device context | Non-reproducible | Record device/zone/interface |
| No hashes for evidence-grade items | Integrity challenge | SHA256 mandatory |
| Storing PCAP locally | Data leak | Evidence repository only |
| Cross-tenant capture (MSSP) | Compliance breach | Tenant verification |

---

# 14. Related Documents

| Document | Path |
|---|---|
| Evidence Collection SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| Digital Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Digital-Evidence-Handling.md` |
| Log Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Log-Evidence-SOP.md` |
| Memory Evidence SOP | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Memory-Evidence-SOP.md` |
| Network Capture SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Network-Capture-SOP.md` |
| Firewall Block Request SOP | `04_TOOLS-AND-TECHNOLOGY/04.5_Firewall-Network/Firewall-Block-Request-SOP.md` |
| CoC Digital Evidence | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.2_Chain-of-Custody/CoC-Digital-Evidence.md` |
| Evidence Storage Policy | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.3_Evidence-Storage/Evidence-Storage-Policy.md` |

---

# 15. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0 | 30-May-2026 | Network Security Lead / Evidence Custodian | Initial version |

---

# 16. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**