# Playbook: Web Application Attack Response (Master)

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Web Application Attack Response (Master) |
| Document ID | IR-PB-WEB-001 |
| Version | 1.0 |
| Effective Date | 19-May-2026 |
| Owner | SOC Manager / IR Team Lead / Application Security Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 web application incident |

---

## 2. Purpose

This master playbook defines the end-to-end response procedures for **web application attacks** across enterprise and MSSP-managed environments.

Web application incidents are high-risk because they can lead to:
- customer-facing outages
- unauthorized access to sensitive data (PII/financial/IP)
- credential theft and session takeover
- server-side compromise (webshells, RCE)
- cloud credential exposure (metadata SSRF, secret leaks)
- lateral movement into internal networks
- regulatory and legal obligations (if breach occurs)

This playbook standardizes:
- alert qualification and severity assignment
- investigation and scoping across WAF, web server, app, DB, cloud, and endpoint logs
- containment actions (WAF/CDN rules, endpoint restrictions, secret rotation, egress controls)
- escalation to L3 forensics and IR Team
- evidence preservation and chain-of-custody
- reporting alignment and MITRE mapping
- post-incident improvements and detection tuning

---

## 3. Scope

### 3.1 In Scope

Applies to:
- SQL injection (SQLi)
- Cross-Site Scripting (XSS)
- Server-Side Request Forgery (SSRF)
- Remote Code Execution (RCE)
- Local/Remote File Inclusion (LFI/RFI)
- Directory traversal
- Authentication bypass
- API abuse (enumeration, token abuse, rate-limit bypass)
- Webshell deployment and persistence
- Misconfiguration-driven exposure through web endpoints (public admin panels, debug endpoints)

Environments:
- production, staging, dev (shared infra risk)
- on-prem web servers and application tiers
- cloud workloads (VMs, containers, serverless, PaaS)
- CDNs, WAF/WAAP, API gateways

### 3.2 Out of Scope (Use Other Playbooks)

| Scenario | Use Playbook |
|----------|--------------|
| Volumetric DDoS | `02.4_DDoS/` |
| Credential attack only (no web exploit) | `02.7_Credential-Attack/` |
| Phishing/BEC | `02.2_Phishing-BEC/` |
| Data breach/exfil confirmed | `02.6_Data-Breach-Exfiltration/` |
| Network intrusion not web-originated | `02.11_Network-Intrusion/` |

---

## 4. Definitions (Operational)

| Term | Definition |
|------|------------|
| WAF/WAAP | Web Application Firewall / Web Application and API Protection |
| Virtual Patching | WAF rule mitigating vulnerability without immediate code fix |
| Exploitation Success | Evidence that attacker achieved intended effect (data access, code execution, auth bypass) |
| Webshell | Script planted on server to provide remote control |
| SSRF Metadata | SSRF used to query cloud metadata endpoints to steal credentials |
| Exposure Window | From first possible compromise/exposure to last confirmed |
| Request Sample | Captured HTTP request including headers/params (may include secrets; must be handled carefully) |

---

## 5. Web Application Attack Categories (Operational)

| Category | Description | Typical Risk |
|----------|-------------|--------------|
| Injection | SQLi, command injection, template injection | Data theft / RCE |
| XSS | Reflected/stored/DOM XSS | Session theft / user compromise |
| SSRF | Internal resource access via server-side request | Cloud credential theft / internal pivot |
| RCE | Code execution on server | Full host compromise |
| File attacks | LFI/RFI/traversal | Config leakage / RCE chain |
| Auth/API abuse | bypass, enumeration, token abuse | Account takeover / data exposure |
| Webshell/persistence | backdoors on web hosts | Long-term attacker access |

---

## 6. Severity Classification Guidance (P1–P4)

Severity is based on:
- exploitation success likelihood (allowed + 2xx/3xx anomalies)
- business impact (outage/degradation)
- data sensitivity and breach risk
- privilege impact (admin endpoints)
- evidence of compromise (webshell/RCE)
- scope (single endpoint vs multi-app)

### 6.1 Severity Matrix (Operational Default)

| Scenario | Default Severity |
|----------|------------------|
| Confirmed RCE/webshell/persistence | P1 |
| Confirmed data access/exfiltration via web app | P1 |
| Customer-facing outage due to attack | P1 |
| Exploit traffic allowed + strong success indicators | P1/P2 (SOC Lead decides) |
| Sustained targeted attack against critical app (blocked) | P2 |
| Attack blocked/no impact (scanning) | P3 |
| False positive / benign scanner confirmed | P4 |

Reference:
`01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

---

## 7. Activation Criteria (When to Use This Playbook)

Activate when any of the following occur:

| Trigger | Example |
|--------|---------|
| WAF alert | SQLi/XSS/SSRF/RCE signatures triggered |
| Web logs show exploit patterns | traversal patterns, suspicious params |
| APM anomaly | error spikes, latency spikes tied to exploit events |
| IDS/IPS alert | exploit signatures against web servers |
| External report | bug bounty/security researcher report via approved process |
| Suspicious admin access | unusual access to admin endpoints |
| New web root file changes | webshell suspicion (EDR/FIM) |
| Cloud metadata access attempts | SSRF metadata path indicators |

---

## 8. Roles and Responsibilities (Operational)

| Role | Responsibilities |
|------|------------------|
| L1 SOC Analyst | Validate alert, preserve evidence, severity recommendation, escalate |
| L2 SOC Analyst | Confirm exploitation likelihood, expand scope, recommend containment, breach trigger assessment |
| L3 Analyst / Forensics | Host/runtime/cloud forensics, timeline, webshell/RCE confirmation, exfil analysis |
| SOC Lead | Incident coordination, approvals, bridge call for P1/P2, communications |
| IR Team | Major incident command, cross-team coordination, high-impact decisions |
| AppSec Lead | vulnerability guidance, virtual patching, remediation recommendations |
| App Owner / DevOps | implement feature disablement, deploy fixes, support logging |
| Network Team | WAF/firewall changes, egress controls, segmentation |
| IAM Team | session invalidation, key rotation support (if auth impacted) |
| DBA | DB protections, query audit, export review |
| Cloud Team | cloud audit review, storage exposure control, IAM policy changes |
| Legal/Compliance | breach assessment and reporting (if triggered) |
| MSSP SDM | client communications and approvals (MSSP context) |

Reference:
`00_GOVERNANCE/00.3_Roles-and-Responsibilities/RACI-Matrix-IR.xlsx`

---

## 9. Evidence Handling Requirements (Mandatory)

Web app incident evidence often contains sensitive information:
- cookies/tokens
- credentials in query strings
- PII in responses
- internal hostnames/IPs

### 9.1 Minimum Evidence Set (All Incidents)

| Evidence | Source |
|---------|--------|
| WAF/WAAP event export | WAF console/SIEM |
| Web access logs (raw) | NGINX/Apache/IIS |
| App logs (auth/errors) | application logging |
| Reverse proxy/LB logs | load balancer |
| APM screenshots | APM tool |
| Attacker IP/UA summary | SIEM/WAF |

### 9.2 Additional Evidence (P1/P2 or Compromise Suspected)

| Evidence | Purpose |
|---------|---------|
| EDR telemetry on web hosts | process/file/network evidence |
| File integrity diffs | webshell detection |
| Cloud audit logs | IAM/secret/storage evidence |
| DB audit logs | extraction confirmation |
| PCAP/NetFlow | exfil and C2 validation |
| Snapshots/images (selected) | legally defensible forensics |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 10. Web Application Incident Lifecycle

| Phase | Description | Primary Owner |
|------|-------------|---------------|
| Triage | validate alert, preserve evidence, severity | L1 |
| Investigation | confirm success, expand scope, breach trigger | L2 |
| Containment | WAF rules, endpoint restriction, egress controls | SOC Lead + AppSec/Network |
| Forensics | host/cloud/db analysis, timeline, persistence | L3/IR |
| Eradication/Remediation | patch, remove webshell, rotate secrets | AppSec/App Owner/IR |
| Recovery | stabilize service, rollback emergency controls safely | App Owner/SOC Lead |
| Post-incident | PIR, detection improvements, reporting | IR/SOC |

---

## 11. Standard Workflow (End-to-End)

### Phase A — L1 Triage
- validate alert and target context
- preserve WAF/web logs
- determine blocked vs allowed
- recommend severity
- escalate to L2 + SOC Lead for P1/P2

Reference:
`02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L1-Triage.md`

### Phase B — L2 Investigation
- confirm attack type and exploitation likelihood
- expand scope across endpoints, apps, sources
- assess compromise indicators (webshell/RCE)
- assess data breach triggers
- recommend containment actions

Reference:
`02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L2-Investigation.md`

### Phase C — Containment
- apply targeted WAF rules/virtual patches
- restrict admin endpoints and risky methods
- implement egress controls where needed
- isolate compromised hosts/pods if confirmed
- coordinate secrets rotation if exposure suspected
- validate containment effectiveness

Reference:
`02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-Containment.md`

### Phase D — L3 Forensics (If Required)
- reconstruct authoritative timeline
- confirm patient zero and persistence
- confirm data access/exfiltration scope
- collect defensible evidence package
- provide eradication guidance

Reference:
`02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L3-Forensics.md`

### Phase E — Attack-Specific Procedures
- SQLi deep dive
- XSS deep dive

References:
- `PB-WebApp-SQLi-Specific.md`
- `PB-WebApp-XSS-Specific.md`

### Phase F — Post-Incident
- RCA + lessons learned
- detection engineering improvements
- audit evidence pack updates

Reference:
`08_POST-INCIDENT/`

---

## 12. Escalation Criteria

### 12.1 Escalate to L3 if:

| Condition | Reason |
|----------|--------|
| exploitation success suspected but unclear | advanced correlation needed |
| SSRF metadata access suspected | credential theft risk |
| RCE indicators present | host compromise risk |
| webshell/persistence suspected | forensic confirmation needed |
| logs insufficient / rotated | forensic recovery needed |

### 12.2 Escalate to IR Team if:

| Condition | Reason |
|----------|--------|
| RCE/webshell confirmed | major incident |
| data breach indicators present | legal/regulatory risk |
| critical customer-facing outage | crisis coordination |
| lateral movement suspected | broader compromise |
| multi-app/multi-tenant impact | coordinated response required |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/`

---

## 13. Data Breach Trigger (Mandatory Decision Gate)

Any web app incident must evaluate breach triggers:

| Trigger Question | If YES |
|------------------|--------|
| Sensitive data accessible from exploited route? | Activate Data Breach playbook |
| Evidence of DB extraction/export? | Activate Data Breach playbook |
| Evidence of large outbound transfers/exfil? | Activate Data Breach playbook |
| Evidence of customer PII exposure? | Engage Legal/Compliance immediately |

Reference:
`02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/`

---

## 14. Common Mistakes to Avoid

| Mistake | Risk | Correct Approach |
|--------|------|------------------|
| Treating WAF “blocked” as resolved | bypass may exist | scope + verify web/app logs |
| Applying broad blocks too early | outage | targeted virtual patching first |
| Redeploying before exporting logs | evidence loss | export first |
| Not rotating secrets after SSRF/RCE | persistent compromise | rotate/revoke keys and tokens |
| Not checking egress | silent exfil | validate outbound traffic |
| Poor documentation | audit failure | tables + evidence references |

---

## 15. Related Documents

| Document | Path |
|---------|------|
| Web App L1 Triage | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L1-Triage.md` |
| Web App L2 Investigation | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L2-Investigation.md` |
| Web App L3 Forensics | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L3-Forensics.md` |
| Web App Containment | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-Containment.md` |
| Web App MITRE Mapping | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-MITRE-Mapping.md` |
| SQLi Specific | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-SQLi-Specific.md` |
| XSS Specific | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-XSS-Specific.md` |
| Data Breach Playbooks | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/` |
| Credential Attack Playbooks | `02_PLAYBOOKS/02.7_Credential-Attack/` |
| Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |

---

## 16. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 19-May-2026 | SOC Manager / IR Team Lead / AppSec Lead | Initial version |

---

## 17. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**