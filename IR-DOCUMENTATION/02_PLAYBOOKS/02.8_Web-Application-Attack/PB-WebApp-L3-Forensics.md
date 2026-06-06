# Playbook: Web Application Attack – L3 Forensics and Advanced Analysis

---

## 1. Document Control

| Field | Value |
|-------|-------|
| Document Name | Playbook – Web Application Attack (L3 Forensics and Advanced Analysis) |
| Document ID | IR-PB-WEB-004 |
| Version | 1.0 |
| Effective Date | 19-May-2026 |
| Owner | L3 Lead / IR Team Lead / Application Security Lead |
| Approved By | CISO |
| Classification | Internal – Confidential |
| Review Cycle | Quarterly and after any P1/P2 web application incident |

---

## 2. Purpose

This document defines Level 3 (L3) forensic and advanced analysis procedures for web application attacks.

L3 involvement is required when:
- exploitation success is **confirmed or likely**
- webshell/backdoor/persistence is suspected
- RCE/SSRF/LFI exploitation may have exposed secrets or credentials
- data access/exfiltration is suspected (activate Data Breach playbook)
- lateral movement from the application to internal systems is suspected
- the incident may require **legal/regulatory evidence** (P1/P2)
- the attack involves complex cloud/container/serverless infrastructure

L3 objectives:
- reconstruct the full attack chain and authoritative timeline
- confirm the **initial access vector** and vulnerable component
- confirm compromise status (webshells, persistence, privilege changes)
- confirm data access/exfiltration scope (what/when/how much)
- generate defensible evidence (hashing, chain-of-custody)
- produce IOC/TTP package for blocking + hunting
- provide “eradication-ready” guidance and validation criteria

---

## 3. Scope

Applies to web incidents including:
- SQLi, XSS, SSRF, RCE, LFI/RFI, directory traversal
- authentication bypass and session abuse
- API abuse with sensitive data impact
- webshell deployments (PHP/ASPX/JSP/Node/Python, etc.)
- container compromise (Kubernetes, Docker)
- cloud workloads (VMs, PaaS, serverless) hosting web apps
- attacks that may impact:
  - databases
  - internal services
  - secrets vaults
  - CI/CD pipelines
  - cloud IAM roles/keys

---

## 4. Preconditions (Inputs from L2 / SOC Lead)

L3 begins after L2 has:
- validated the attack and performed initial scoping
- preserved minimum logs and request samples
- initiated containment where required
- documented exploitation confidence level

Minimum required inputs:

| Input | Minimum Content |
|------|------------------|
| Incident summary | attack type, target app, env, severity |
| Evidence references | WAF export, web logs, app logs, APM snapshots |
| Exploitation status | Confirmed/Likely/Not Confirmed + reasoning |
| Scope tables | targeted endpoints, attacker sources, impacted assets |
| Containment actions | rules applied, endpoints disabled, egress blocks |
| Access to systems | approvals for forensic collection (prod constraints acknowledged) |

Reference:
`02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L2-Investigation.md`

---

## 5. L3 Required Outputs (Deliverables)

L3 must deliver the following to IR Team/SOC Lead:

| Deliverable | Description |
|------------|-------------|
| Authoritative Timeline | UTC timeline with evidence references |
| Patient Zero Identification | earliest compromised host/container/function |
| Root Cause | vulnerable component (CVE/misconfig/code flaw) + exploit path |
| Compromise Confirmation | webshell/persistence/credential access status |
| Data Access / Exfil Assessment | confirmed/likely/possible + dataset summary + volume estimate |
| IOC Package | hashes, paths, domains, IPs, UA, payload patterns |
| TTP / MITRE Mapping Notes | technique mapping summary (for report) |
| Eradication Guidance | what to remove/rotate/rebuild + validation checks |
| Detection & Hunt Recommendations | queries, alert gaps, coverage improvements |

---

## 6. Forensic Principles and Evidence Rules

### 6.1 Evidence Integrity

| Rule | Requirement |
|------|-------------|
| Preserve first | collect and export logs/artifacts before deletion/redeploy where possible |
| Hash artifacts | compute hash for files/images/log exports where applicable |
| Chain-of-custody | maintain transfer records for P1/P2 and any legal-risk incident |
| Least disruption | avoid actions that crash production without approvals |
| UTC timestamps | normalize all events to UTC |

Reference:
`06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

### 6.2 Confidentiality

Web app forensics can contain:
- tokens, cookies, API keys
- credentials in logs
- customer data

Therefore:
- redact secrets before sharing broadly
- store evidence in restricted access locations
- for MSSP: strict client segregation

---

## 7. L3 Investigation Workflow Overview

| Phase | Focus | Output |
|------|-------|--------|
| Phase 1 | Evidence acquisition plan | collection checklist + evidence IDs |
| Phase 2 | Attack reconstruction (WAF/web/app) | exploit narrative + timeline anchors |
| Phase 3 | Host/runtime compromise analysis | webshell/persistence status |
| Phase 4 | Cloud/IAM/secrets analysis | credential exposure + role abuse |
| Phase 5 | Database/data access analysis | data scope + extraction evidence |
| Phase 6 | Exfiltration analysis | destinations + volume + method |
| Phase 7 | Root cause confirmation | vulnerable code/config + patch/workaround |
| Phase 8 | Reporting outputs | IOC package + eradication guidance |

---

# 8. Phase 1 – Evidence Acquisition Plan (What to Collect)

## 8.1 Minimum Evidence Set (All P1/P2; as possible for P3)

| Evidence | Source | Notes |
|---------|--------|------|
| WAF/WAAP logs export | WAF console/SIEM | include request sample IDs if available |
| Reverse proxy/LB access logs | LB/proxy | include headers + status codes |
| Web server logs | NGINX/Apache/IIS | raw logs preferred |
| Application logs | app logging | include auth, admin actions, errors |
| APM metrics | APM | latency, error spikes, DB timings |
| Cloud audit logs | AWS/Azure/GCP | IAM changes, storage access, key use |
| DB logs/audit | DB | query/export evidence |
| EDR telemetry (web hosts) | EDR | processes, file changes, network |
| Network telemetry | proxy/firewall/NetFlow | egress/exfil validation |

## 8.2 Additional Evidence (When Compromise Suspected)

| Evidence | When Needed | Why |
|---------|-------------|-----|
| Memory capture (selected systems) | fileless/injection suspected | capture runtime artifacts |
| Disk image or snapshot | webshell/persistence suspected | defensible artifact recovery |
| Container image snapshot | container compromise | preserve filesystem layers |
| Kubernetes audit logs | k8s environments | track exec, secrets access, deployments |
| CI/CD audit logs | pipeline compromise suspected | supply-chain risk |
| Secrets vault logs | secrets exposure suspected | key/token access evidence |

## 8.3 Evidence ID Standard (Recommended)

Use a consistent evidence reference ID:
- `EV-[INC-ID]-[SOURCE]-[YYYYMMDD]-[SEQ]`

Example:
- `EV-INC123-WAF-20260519-001`

---

# 9. Phase 2 – Attack Reconstruction (WAF/Web/App Correlation)

## 9.1 Establish “Ground Truth” Attack Timeline Anchors

Determine these anchor points:

| Anchor | Meaning | Evidence Sources |
|--------|---------|------------------|
| First seen | earliest exploit attempt | WAF/web logs |
| First allowed | first time payload reached app | WAF allow + web logs |
| First likely success | anomaly indicates exploit effect | 2xx/3xx + app behavior |
| Peak activity | highest request rate | WAF/APM |
| First containment | first block/rate-limit applied | change records |
| Post-containment attempts | attacker adaptation | WAF logs |

## 9.2 Correlation Table (Required)

| Time (UTC) | Source | Event | Key Details | Evidence Ref |
|-----------|--------|------|------------|--------------|
| | WAF | rule hit/allow | URI, parameter, action | |
| | Web | request | status, bytes, UA, IP | |
| | App | error/admin action | auth events, exceptions | |
| | DB | query/export | query class, rows | |
| | Network | egress | destination, volume | |

## 9.3 “Exploit Success” Indicators (Cross-Signal Validation)

| Indicator | What it Suggests | Confirm With |
|----------|-------------------|--------------|
| 2xx response with abnormal size | data leakage | response bytes + DB logs |
| time-based response delays | blind SQLi | repeated pattern + DB time |
| sudden 5xx spike after payload | exploitation impact | APM + app errors |
| new file in web root | webshell drop | EDR + file integrity |
| process spawn on web host | RCE | EDR process tree |
| outbound to internal IPs | SSRF | egress logs + app fetch logs |
| outbound to external storage | exfil | proxy/firewall + DLP |

---

# 10. Phase 3 – Host / Runtime Compromise Analysis

This phase answers: “Did the attacker gain code execution or persistence?”

## 10.1 Webshell and Persistence Hunt Checklist

Check for:

| Item | Evidence Source | Notes |
|------|------------------|------|
| New/modified files in web root | file integrity / EDR | look for recent writes |
| Suspicious extensions | file system | .php/.aspx/.jsp/.war/.py etc. |
| Suspicious upload directories | app config | often abused |
| New scheduled tasks/cron | host logs | persistence |
| New services | OS logs | persistence |
| Unexpected reverse shells | network/EDR | outbound to attacker |
| Modified config files | git/CI/CD/app logs | persistence or access |

## 10.2 Host Telemetry Review (If EDR Present)

Required checks:

| Check | What to Look For |
|------|-------------------|
| Process tree | web server process spawning cmd/powershell/bash |
| Command line | curl/wget, base64, python -c, node eval |
| File writes | web root writes, temp file drops |
| Network connections | outbound to suspicious destinations |
| Privilege changes | sudo usage, admin group changes |

## 10.3 Container/Kubernetes Specific Checks (If Applicable)

| Check | Evidence Source | Meaning |
|------|------------------|---------|
| `kubectl exec` events | k8s audit | interactive intrusion |
| secret read events | k8s audit / vault | credential exposure |
| new deployment/image | CI/CD + k8s | persistence |
| unusual outbound traffic from pods | network telemetry | C2/exfil |
| node-level compromise signals | EDR/host logs | escalation beyond container |

---

# 11. Phase 4 – Cloud/IAM/Secrets Analysis

Web exploits often lead to secret theft and cloud pivoting.

## 11.1 Secrets Exposure Indicators

| Indicator | Meaning | Evidence Sources |
|----------|---------|------------------|
| access to env vars/secrets | token leakage | container runtime logs, app logs |
| metadata service access | cloud role credential theft | egress logs + cloud audit |
| vault access anomalies | secrets compromise | vault audit logs |
| new API key usage | stolen key in use | cloud audit logs |
| new OAuth consent/app | persistence | IAM audit |

## 11.2 Immediate Actions if Secrets Exposure Confirmed (Escalate + Coordinate)

If confirmed, L3 must advise:
- rotate keys/tokens/secrets
- revoke sessions
- restrict IAM roles temporarily
- increase auditing and alerting
- check for downstream service abuse

Reference:
`02_PLAYBOOKS/02.10_Cloud-Security-Incident/` (if cloud incident expands)

---

# 12. Phase 5 – Database and Data Access Forensics

This phase answers: “What data was accessed and how?”

## 12.1 Database Evidence Checklist

| Item | What to Collect | Why |
|------|------------------|-----|
| audit logs | query logs, export logs | confirm extraction |
| slow query logs | time-based SQLi | blind SQLi indicator |
| admin actions | user creation/priv changes | persistence |
| connection logs | source app host/user | compromise validation |
| row counts/bytes | estimate impact | reporting |

## 12.2 Data Scope Estimation

L3 must provide:
- datasets/tables impacted (best effort)
- time window of access
- approximate number of records accessed/exported
- sensitivity classification (PII/financial/IP/etc.)

Reference (if breach triggers):
`02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/`

---

# 13. Phase 6 – Exfiltration Analysis

This phase answers: “Did data leave the environment?”

## 13.1 Exfiltration Evidence Sources

| Source | What to Look For |
|--------|------------------|
| proxy logs | uploads, destinations, volumes |
| firewall logs | large outbound sessions |
| NetFlow | sustained outbound volume |
| cloud logs | storage uploads/downloads |
| DLP | content classification + transfers |
| EDR network telemetry | suspicious connections |

## 13.2 Exfiltration Confidence Levels

| Level | Meaning | Minimum Evidence |
|------|---------|------------------|
| Confirmed | direct evidence of transfer out | proxy/firewall logs with volume + destination |
| Likely | strong indicators but missing direct telemetry | staging artifacts + suspicious egress patterns |
| Possible | weak indicators | partial signals; needs more data |

## 13.3 Destination Profiling

For each suspected destination, record:

| Field | Required |
|------|----------|
| Destination domain/IP | Yes |
| Provider/hosting | ASN, cloud provider |
| Protocol | HTTPS/SFTP/DNS/etc. |
| Volume estimate | bytes transferred |
| Time window | first/last seen UTC |
| Blocking status | blocked/allowed |
| Evidence reference | log export ID |

---

# 14. Phase 7 – Root Cause Confirmation (Vulnerability / Misconfiguration)

L3 must confirm root cause to support eradication and prevention.

## 14.1 Root Cause Categories

| Category | Examples |
|---------|----------|
| Vulnerable code | unsanitized SQL, unsafe template rendering |
| Misconfiguration | public debug endpoints, weak CORS/CSP, permissive IAM |
| Vulnerable dependency | outdated framework/library with CVE |
| Weak auth controls | missing rate limits, broken access control |
| Deployment pipeline weakness | exposed secrets in CI/CD |

## 14.2 Root Cause Evidence Requirements

| Requirement | Example |
|------------|---------|
| Proof of vulnerability path | request + response + log correlation |
| Affected component identification | file/module/service name |
| Version and patch status | dependency version, CVE |
| Fix recommendation | patch/workaround/virtual patch |

---

# 15. Eradication Guidance (L3 Output to IR Team/App Owner)

## 15.1 Eradication Decision Guidance (Rebuild vs Clean)

| Scenario | Recommended Approach |
|----------|----------------------|
| Webshell confirmed | rebuild/replace node or image preferred |
| Unknown persistence | rebuild preferred |
| RCE confirmed | rebuild + rotate secrets |
| Only WAF-blocked attempts | clean (no rebuild) + patch |
| SSRF to metadata confirmed | rotate cloud creds + rebuild if runtime compromised |

## 15.2 “Definition of Clean State” for Web App Compromise

L3 should confirm these before return-to-normal:

| Check | Expected Result |
|------|------------------|
| No suspicious files in web root | verified |
| No suspicious processes or scheduled tasks | verified |
| Secrets/keys rotated and old revoked | completed |
| IAM changes reviewed and reverted | completed |
| Vulnerability patched or mitigated | completed |
| Egress controls validated | stable |
| Monitoring enabled | active |

---

# 16. Detection & Hunting Outputs (Required)

L3 must produce:

## 16.1 IOC Package (Attach to Ticket)

| IOC Type | Value | Context | Confidence | Recommended Action |
|---------|-------|---------|------------|-------------------|
| Source IP/ASN | | attacker infra | | block/rate-limit |
| URI patterns | | exploit routes | | WAF rule |
| Payload markers | | signatures | | detection |
| File hash | | webshell/dropper | | EDR block |
| File path | | web root artifact | | hunt/remove |
| Domain/IP | | exfil/C2 | | block |
| User-Agent | | automation | | WAF/IDS rule |

## 16.2 Detection Improvements (Track in Improvement Log)

Examples:
- WAF rules for new patterns
- SIEM correlations for endpoint response anomalies
- alerts for new files in web root
- alerts for metadata service access attempts (SSRF)
- egress anomaly alerts for web server segments
- DB export anomaly alerts

Reference:
`08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

---

# 17. Escalation Guidance (L3)

## 17.1 Escalate to IR Team Immediately if:

| Condition | Reason |
|----------|--------|
| webshell/RCE confirmed | active compromise |
| secrets/keys exposed | cloud/service compromise risk |
| evidence of data exfiltration | breach obligations |
| lateral movement suspected | broader incident |
| critical customer-facing outage | crisis coordination |

## 17.2 Escalate to Legal/Compliance if:

| Condition | Reason |
|----------|--------|
| customer/employee PII accessed | regulatory notification assessment |
| public exposure confirmed | disclosure obligations |
| extortion threats mention data | legal guidance |

Reference:
`05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

# 18. Common L3 Pitfalls to Avoid

| Pitfall | Impact | Prevention |
|--------|--------|-----------|
| Redeploying before log export | evidence loss | export first |
| Focusing only on WAF logs | incomplete picture | correlate WAF + app + host + DB |
| Missing secrets exposure | persistent compromise | check metadata/vault/IAM logs |
| Not validating exfil | underreporting | confirm with proxy/firewall/DLP |
| Poor timeline quality | audit/legal weakness | UTC timeline + evidence refs |

---

# 19. MSSP Client Handling Notes

For MSSP-managed environments:
- maintain strict evidence segregation per client
- do not share payloads or request samples across clients
- obtain client approval for high-impact forensic actions on production
- ensure all transfers use encrypted methods and CoC where required
- provide client-ready summary without exposing other tenant data

Reference:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

# 20. Related Documents

| Document | Path |
|---------|------|
| Web App Master | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-Master.md` |
| Web App L1 Triage | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L1-Triage.md` |
| Web App L2 Investigation | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-L2-Investigation.md` |
| Web App Containment | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-Containment.md` |
| SQLi Specific | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-SQLi-Specific.md` |
| XSS Specific | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-XSS-Specific.md` |
| MITRE Mapping | `02_PLAYBOOKS/02.8_Web-Application-Attack/PB-WebApp-MITRE-Mapping.md` |
| Data Breach Playbooks | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/` |
| Credential Attack Playbooks | `02_PLAYBOOKS/02.7_Credential-Attack/` |
| Cloud Incident Playbooks | `02_PLAYBOOKS/02.10_Cloud-Security-Incident/` |
| Evidence Handling | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/` |

---

## 21. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 19-May-2026 | L3 Lead / IR Team Lead / AppSec Lead | Initial version |

---

## 22. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**