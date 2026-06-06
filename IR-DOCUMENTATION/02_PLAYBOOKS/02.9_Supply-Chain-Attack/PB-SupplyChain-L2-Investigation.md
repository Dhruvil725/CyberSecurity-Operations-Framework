# Playbook: Supply Chain Attack – L2 Investigation

---

## 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | Playbook – Supply Chain Attack (L2 Investigation)            |
| Document ID    | IR-PB-SC-003                                                 |
| Version        | 1.0                                                          |
| Effective Date | 19-May-2026                                                  |
| Owner          | L2 SOC Lead / IR Team Lead                                   |
| Approved By    | CISO                                                         |
| Classification | Internal – Confidential                                      |
| Review Cycle   | Quarterly and after any P1/P2 supply chain incident          |

---

## 2. Purpose

This document defines the Level 2 (L2) investigation procedures for supply chain attacks escalated from L1 triage.

Supply chain investigations at L2 are significantly more complex than standard malware or intrusion investigations because:

- The malicious component arrived through a **trusted, signed, and legitimate channel** making standard detection signatures ineffective
- The **scope is potentially very wide** — every system running the affected software version is a potential victim
- **Dwell time is often measured in weeks or months** — L2 must search historical data far beyond standard windows
- The attacker may have already moved laterally, established persistence, and exfiltrated data long before the investigation begins
- Evidence may be spread across **internal systems, vendor environments, and cloud platforms** simultaneously
- **SBOM analysis** and dependency mapping are required skills that go beyond standard L2 investigation

L2 investigation objectives:

- Confirm whether the supply chain attack actually impacted the organization (not just a theoretical exposure)
- Identify all affected systems, environments, and business services with precision
- Determine whether malicious functionality was executed or only installed
- Assess whether lateral movement, persistence, or data collection has occurred
- Evaluate data breach triggers formally and document the decision
- Provide a prioritized, actionable containment plan with clear owners and approvals
- Decide whether L3 forensics and IR Team activation is required

L2 must produce investigation output that is technically defensible, operationally actionable, and audit-ready for regulatory or legal review.

---

## 3. Scope

This playbook applies to L2 investigation of:

- Confirmed or suspected software update supply chain attacks (SolarWinds-style)
- Malicious packages confirmed or suspected in production or development environments
- Dependency confusion attacks identified in build pipelines
- CI/CD pipeline compromise with potential code injection
- Managed service provider (MSP/MSSP) compromise potentially pivoting into client environments
- Open-source library or SDK compromise affecting applications in production
- Container image compromise affecting deployed workloads
- Cloud SaaS vendor compromise with potential data access implications

Includes:

- On-premises systems and servers
- Cloud workloads (VMs, containers, serverless, PaaS)
- Development and build environments (CI/CD pipelines)
- MSSP-managed client environments (client approvals may apply for high-impact actions)

---

## 4. Preconditions (Inputs from L1)

Before L2 begins formal investigation, confirm the ticket contains:

| Required Input                  | Minimum Content                                              |
| ------------------------------- | ------------------------------------------------------------ |
| Alert/notification source       | Vendor advisory / SIEM / EDR / TI feed with reference       |
| Affected vendor and software    | Full vendor and product name                                 |
| Affected versions               | Exact version numbers from advisory                          |
| Organizational exposure check   | Confirmed / Not confirmed / Unknown with evidence            |
| IoC list                        | Network destinations, file hashes, process names from advisory |
| Initial IoC match results       | Results of L1 searches across SIEM, EDR, firewall           |
| Evidence preserved              | Software version, install logs, SIEM export, process snapshot |
| Operations update hold          | Confirmation that operations teams are not applying updates  |
| Severity recommendation         | P1–P4 with justification                                     |
| Business impact summary         | Services affected, data sensitivity, system count            |

If any of the above is missing, L2 must obtain it before proceeding or note the gap formally in the ticket.

---

## 5. L2 Required Outputs (Minimum Deliverables)

L2 must provide the following in the incident ticket before handoff or closure:

| Output                              | Required Detail                                              |
| ----------------------------------- | ------------------------------------------------------------ |
| Confirmed impact status             | Confirmed / Likely / Not confirmed with supporting evidence  |
| Affected systems inventory          | Full list: hostname, IP, environment, software version, business function |
| Execution confirmation              | Did the malicious component actually execute? Evidence basis |
| IoC match summary                   | All IoC types searched, results, time windows, evidence refs |
| Lateral movement assessment         | Confirmed / Suspected / Not confirmed with evidence          |
| Persistence assessment              | Confirmed / Suspected / Not confirmed with evidence          |
| Data breach trigger decision        | Yes / No / Unknown with formal documentation                 |
| Containment plan                    | Prioritized actions, owners, approvals required              |
| Escalation decision                 | L3/IR Team escalation or documented justification for not escalating |
| Authoritative timeline              | UTC timeline with first seen, key events, containment start  |
| IOC and TTP summary                 | Enriched with threat intelligence context                    |

---

## 6. Investigation Workflow Overview

| Phase   | Goal                                                         | Key Output                        |
| ------- | ------------------------------------------------------------ | --------------------------------- |
| Phase 1 | Confirm impact — did malicious functionality execute?        | Execution confirmation            |
| Phase 2 | Full scope identification — all affected systems             | Affected systems inventory        |
| Phase 3 | IoC deep search — extended time window across all sources    | IoC match summary                 |
| Phase 4 | Lateral movement assessment                                  | Lateral movement status           |
| Phase 5 | Persistence assessment                                       | Persistence status                |
| Phase 6 | Data access and breach trigger assessment                    | Breach trigger decision           |
| Phase 7 | SBOM and dependency analysis (if package/code attack)        | Dependency impact map             |
| Phase 8 | CI/CD pipeline assessment (if build compromise suspected)    | Pipeline integrity status         |
| Phase 9 | Containment recommendations                                  | Prioritized containment plan      |
| Phase 10| Escalation decision and handoff                              | L3/IR Team activation or closure  |

---

## 7. Phase 1 – Confirm Impact (Did Malicious Functionality Execute?)

This is the most critical L2 determination. Simply having the affected version installed does not mean the attack succeeded — L2 must determine whether malicious code actually ran.

### 7.1A Execution Confirmation Evidence Sources

| Evidence Source          | What to Look For                                             | Execution Indication                        |
| ------------------------ | ------------------------------------------------------------ | ------------------------------------------- |
| EDR process telemetry    | Processes spawned by vendor software that are unexpected     | Unexpected child processes from vendor agent |
| EDR network telemetry    | Outbound connections from vendor software to IoC destinations | Active C2 communication confirmed           |
| SIEM correlation         | Events matching attack chain described in vendor advisory    | Alert correlation to known attack pattern   |
| Firewall/proxy logs      | Connections to IoC IP/domain destinations                    | C2 or exfiltration communication            |
| File integrity monitoring | New files created by vendor software in unexpected locations | Dropper or backdoor file placed             |
| OS audit logs            | Privilege escalation or account creation events              | Post-execution attacker activity            |
| Application logs         | Errors or behaviors consistent with malicious code execution | Anomalous application behavior              |
| Memory forensics (L3)    | Malicious code loaded in process memory                      | In-memory execution confirmed               |

### 7.1B Execution Confidence Levels

| Level            | Evidence Required                                            | Immediate Action                             |
| ---------------- | ------------------------------------------------------------ | -------------------------------------------- |
| Confirmed        | EDR/network/file evidence directly matches attack chain      | Escalate to IR Team immediately; P1          |
| Highly Likely    | Strong indirect indicators (IoC matches + affected version)  | Escalate to L3; treat as P1                  |
| Possible         | Affected version present; some anomalies but no direct match | Treat as P2; intensive investigation         |
| Not Confirmed    | Affected version present; no anomalies detected              | P3; maintain enhanced monitoring             |
| Not Affected     | Affected version not present in org environment              | P4; document and close with monitoring note  |

### 7.1C Supply Chain Attack-Specific Execution Indicators

Supply chain attacks often use subtle techniques that differ from standard malware:

**Software update attacks:**
- Vendor software process making network connections it should not normally make
- Vendor software spawning command shells, scripting engines, or network tools
- Vendor software reading or writing files outside its normal operational paths
- Vendor software accessing credential stores, certificate stores, or secrets

**Package/dependency attacks:**
- Build process making unexpected network connections during compilation
- Installed package importing or executing additional code from external URLs
- Package accessing environment variables or secrets during installation scripts
- Unexpected files created in project directories during package installation

**CI/CD pipeline attacks:**
- Build logs showing unexpected commands or network calls
- Build artifacts with different hashes than expected from source code
- New environment variables accessed during build that were not previously used
- Unexpected code commits from automated build accounts

---

## 8. Phase 2 – Full Scope Identification (All Affected Systems)

### 8.1A System Inventory Query Approach

L2 must identify every system in the organization running the affected software version.

**Query sequence:**

| Step | Query Action                                                 | Data Source                        | Output                          |
| ---- | ------------------------------------------------------------ | ---------------------------------- | ------------------------------- |
| 1    | Query CMDB/asset inventory for all instances of affected software | Asset management system        | Initial system list             |
| 2    | Query EDR for all endpoints with affected software version   | EDR software inventory             | EDR-confirmed system list       |
| 3    | Query SIEM for events from affected software processes       | SIEM (process/application logs)    | Systems with recent activity    |
| 4    | Query cloud asset inventory for affected software in cloud workloads | Cloud management console      | Cloud system list               |
| 5    | Query container registry and orchestration for affected container images | Kubernetes/Docker           | Container workload list         |
| 6    | Cross-reference all lists for completeness                   | All above                          | Authoritative affected system list |

### 8.1B Affected Systems Inventory Table (Required L2 Output)

For each affected system, document:

| Hostname / Instance | IP Address | Environment | Software Version | Business Function | Data Access | IoC Match? | Priority |
| ------------------- | ---------- | ----------- | ---------------- | ----------------- | ----------- | ---------- | -------- |
|                     |            |             |                  |                   |             |            |          |
|                     |            |             |                  |                   |             |            |          |

**Priority classification for affected systems:**

| Priority | Criteria                                                     |
| -------- | ------------------------------------------------------------ |
| Critical | IoC match confirmed OR system has access to sensitive data/credentials/secrets |
| High     | Production system with affected version; no IoC match yet    |
| Medium   | Staging/DR system with affected version                      |
| Low      | Development system only; isolated from production            |

### 8.1C Environments to Check

Do not limit scope to production — supply chain attacks often enter via development environments and pivot to production:

- Production systems and servers
- Disaster recovery systems (may mirror production state)
- Staging and pre-production environments
- Development workstations and developer systems
- Build servers and CI/CD infrastructure
- Cloud workloads across all cloud accounts
- Container environments and Kubernetes clusters
- Third-party managed systems (if MSSP manages client environments)

---

## 9. Phase 3 – IoC Deep Search (Extended Time Window)

### 9.1A Extended Time Window Requirement

Supply chain attacks have long dwell times. Standard investigation windows are insufficient.

| Minimum Search Window | When to Use                                          |
| --------------------- | ---------------------------------------------------- |
| 90 days               | Default minimum for all supply chain investigations  |
| 6 months              | If vendor advisory indicates early compromise date   |
| 12 months             | If no vendor-provided compromise date is available   |
| Full retention period | If critical data breach indicators are present       |

### 9.1B IoC Search Matrix (Required — Document All Results)

| IoC Type           | IoC Value (from Advisory) | Source Searched         | Time Window  | Result (Match/No Match) | Match Details | Evidence Ref |
| ------------------ | ------------------------- | ----------------------- | ------------ | ----------------------- | ------------- | ------------ |
| IP Address         |                           | Firewall / Proxy / SIEM |              |                         |               |              |
| Domain             |                           | DNS / Proxy / SIEM      |              |                         |               |              |
| File Hash (MD5)    |                           | EDR / FIM               |              |                         |               |              |
| File Hash (SHA256) |                           | EDR / FIM               |              |                         |               |              |
| File Path          |                           | EDR / FIM               |              |                         |               |              |
| Process Name       |                           | EDR / OS Audit          |              |                         |               |              |
| Registry Key       |                           | EDR / Registry audit    |              |                         |               |              |
| Package Name       |                           | Build logs / Package mgr|              |                         |               |              |
| User Agent         |                           | Proxy / WAF             |              |                         |               |              |

### 9.1C Data Sources for IoC Search

| Data Source              | What to Search                                               | Time Window Required     |
| ------------------------ | ------------------------------------------------------------ | ------------------------ |
| Firewall egress logs     | Outbound connections to IoC IP/domain destinations           | 90 days minimum          |
| Proxy logs               | HTTP/HTTPS requests to IoC domains or URLs                   | 90 days minimum          |
| DNS query logs           | DNS lookups for IoC domains from internal systems            | 90 days minimum          |
| EDR telemetry            | File hash matches, process execution, network connections    | Full EDR retention       |
| SIEM correlation         | All events associated with vendor software processes         | Full SIEM retention      |
| Cloud audit logs         | API calls, IAM changes, storage access from affected periods | 90 days minimum          |
| Email gateway logs       | Phishing or vendor communication as part of chain (if applicable) | 90 days minimum     |
| VPN/remote access logs   | Unusual access patterns during potential dwell period        | 90 days minimum          |

### 9.1D Threat Intelligence Enrichment (Required for All IoC Matches)

For every IoC match found, enrich with threat intelligence:

- Confirm the IoC is attributed to the supply chain campaign (not false positive)
- Identify the threat actor group if attribution is available
- Identify additional related IoCs not in the original advisory
- Determine if other TTPs associated with this campaign should be hunted
- Check if other organizations have reported similar matches (ISAC sharing)

Reference: `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md`

---

## 10. Phase 4 – Lateral Movement Assessment

Supply chain attacks are frequently used as the initial access stage of a broader APT campaign. L2 must assess whether the attacker moved laterally from the initial supply chain entry point.

### 10.1A Lateral Movement Indicators to Hunt

| Indicator                                    | Evidence Source                 | Why it Matters                               |
| -------------------------------------------- | ------------------------------- | -------------------------------------------- |
| Unusual authentication events from affected systems | SIEM / Windows Event Logs | Credential use for lateral movement          |
| Pass-the-hash or pass-the-ticket patterns   | SIEM / EDR                      | Credential material reuse                    |
| Unexpected RDP, SSH, or WinRM connections    | Firewall / EDR / SIEM           | Remote access lateral movement               |
| Service account used from unusual source     | Active Directory logs / SIEM    | Service account lateral movement             |
| New local or domain accounts created         | Active Directory / OS logs      | Attacker-created persistence accounts        |
| Unexpected Kerberos ticket requests          | Active Directory / SIEM         | Golden/Silver ticket or Kerberoasting        |
| Lateral movement from affected system to sensitive assets | SIEM correlation | Pivot to high-value targets                 |
| Data staging on affected system before exfil | EDR / file system               | Pre-exfiltration collection                  |

### 10.1B Lateral Movement Investigation Steps

| Step | Action                                                       | Data Source                        | Output                          |
| ---- | ------------------------------------------------------------ | ---------------------------------- | ------------------------------- |
| 1    | Identify all authentication events originating from affected systems during dwell period | AD logs / SIEM | Auth event list |
| 2    | Map network connections from affected systems to other internal systems | Firewall / EDR | Internal connection map |
| 3    | Check for new accounts created on affected systems or from affected systems | AD / OS audit | Account creation events |
| 4    | Review privilege escalation events on affected systems       | Windows Event / Linux audit        | Priv esc events                 |
| 5    | Check for scheduled task or service creation on affected systems | EDR / OS audit | Persistence indicators |
| 6    | Identify any systems that made outbound connections to IoC destinations beyond initial affected system | Firewall / proxy | Spread scope |

### 10.1C Lateral Movement Scope Table (Required L2 Output)

| Source System | Destination System | Protocol/Port | Timestamp (UTC) | Legitimate? | Attacker Controlled? | Evidence Ref |
| ------------- | ------------------ | ------------- | --------------- | ----------- | -------------------- | ------------ |
|               |                    |               |                 |             |                      |              |

---

## 11. Phase 5 – Persistence Assessment

Attackers using supply chain access typically establish independent persistence quickly so they maintain access even if the original supply chain vector is discovered and remediated.

### 11.1A Common Persistence Mechanisms in Supply Chain Attacks

| Persistence Type               | How to Detect                                | Evidence Source              |
| ------------------------------ | -------------------------------------------- | ---------------------------- |
| Scheduled tasks (Windows)      | Compare task list to known-good baseline     | EDR / Windows Task Scheduler |
| Cron jobs (Linux)              | Review crontabs for unexpected entries       | EDR / OS audit logs          |
| New local administrator accounts | Review local admin accounts on affected systems | AD / OS audit logs       |
| New domain accounts            | Review AD for accounts created during dwell period | Active Directory logs   |
| Registry run keys (Windows)    | Check known persistence registry locations   | EDR / Registry audit         |
| New or modified services       | Compare services to known-good baseline      | EDR / OS audit logs          |
| Web shells on web-facing systems | Review web root for new or modified files   | FIM / EDR                    |
| SSH authorized_keys modification | Review authorized_keys files on Linux systems | FIM / EDR                |
| Cloud IAM changes              | New users, roles, or API keys created        | Cloud audit logs             |
| New OAuth applications or consents | Review identity platform for new grants   | IAM platform logs            |

### 11.1B Persistence Investigation Checklist

For each affected system identified in Phase 2, complete:

| Check Item                                        | Status (Done/Pending) | Finding | Evidence Ref |
| ------------------------------------------------- | --------------------- | ------- | ------------ |
| Scheduled tasks reviewed and compared to baseline |                       |         |              |
| Local administrator accounts reviewed             |                       |         |              |
| New services reviewed                             |                       |         |              |
| Registry run keys reviewed (Windows)              |                       |         |              |
| Cron jobs reviewed (Linux)                        |                       |         |              |
| SSH authorized_keys reviewed (Linux)              |                       |         |              |
| Startup items reviewed                            |                       |         |              |
| Cloud IAM changes reviewed (if cloud system)     |                       |         |              |

---

## 12. Phase 6 – Data Access and Breach Trigger Assessment

This phase formally answers: "Was sensitive data accessed, collected, or exfiltrated?"

This assessment is **mandatory** for all supply chain incidents regardless of severity. The decision must be documented in the ticket with supporting evidence.

### 12.1A Data Access Assessment Questions

| Question                                                                | Answer (Yes/No/Unknown) | Evidence Basis                         |
| ----------------------------------------------------------------------- | ----------------------- | -------------------------------------- |
| Did the compromised software have access to credential stores or secrets? |                        |                                        |
| Did the compromised software have access to sensitive databases?         |                         |                                        |
| Did the compromised software have read access to sensitive file shares?  |                         |                                        |
| Did the compromised software have access to cloud storage or object storage? |                      |                                        |
| Do logs show large data transfers from affected systems during dwell period? |                      |                                        |
| Do egress logs show unusual outbound data volumes from affected systems? |                         |                                        |
| Do cloud audit logs show unexpected data downloads or sharing?          |                         |                                        |
| Do secrets vault logs show access from affected systems?                |                         |                                        |
| Were any credentials or API keys exposed to the compromised software?   |                         |                                        |
| Were any OAuth tokens, JWTs, or similar credentials potentially stolen? |                         |                                        |

### 12.1B Data Sensitivity Mapping (Required)

Identify what data was accessible to the compromised software:

| Data Category                    | Accessible? (Yes/No/Unknown) | Volume Estimate | Breach Trigger? |
| -------------------------------- | ---------------------------- | --------------- | --------------- |
| Customer PII (name, email, phone)|                              |                 |                 |
| Financial records                |                              |                 |                 |
| Authentication credentials       |                              |                 |                 |
| Health records (PHI)             |                              |                 |                 |
| Intellectual property            |                              |                 |                 |
| Internal configuration/secrets   |                              |                 |                 |
| Cloud IAM credentials/keys       |                              |                 |                 |
| Source code                      |                              |                 |                 |

### 12.1C Exfiltration Evidence Sources

| Source                   | What to Look For                                              | Time Window     |
| ------------------------ | ------------------------------------------------------------- | --------------- |
| Proxy/firewall egress    | Large outbound transfers from affected systems                | Full dwell period |
| DNS logs                 | DNS exfiltration patterns (high volume, unusual subdomains)   | Full dwell period |
| Cloud audit logs         | Large downloads or unexpected sharing from cloud storage      | Full dwell period |
| DLP alerts               | Data classification matches on egress traffic                 | Full dwell period |
| EDR network telemetry    | Sustained large outbound connections from affected processes  | Full dwell period |
| NetFlow/IPFIX            | Volumetric analysis of outbound traffic from affected systems | Full dwell period |

### 12.1D Breach Trigger Decision

| Condition                                                           | Decision                                     |
| ------------------------------------------------------------------- | -------------------------------------------- |
| Any "Yes" for sensitive data access + any exfiltration indicator    | Activate Data Breach playbook immediately    |
| Sensitive data accessible + exfiltration unknown (logs insufficient)| Activate Data Breach playbook; treat as breach until ruled out |
| Sensitive data accessible but no exfiltration evidence              | Document; continue monitoring; Legal assessment |
| No sensitive data accessible to compromised software                | No breach trigger; document evidence basis   |

Reference: `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Master.md`

---

## 13. Phase 7 – SBOM and Dependency Analysis

This phase applies when the supply chain attack involves a **software package, library, or open-source dependency**.

### 13.1A SBOM Analysis Steps

Software Bill of Materials analysis identifies exactly which applications and systems use the compromised component:

| Step | Action                                                       | Output                              |
| ---- | ------------------------------------------------------------ | ----------------------------------- |
| 1    | Obtain or generate SBOM for all production applications      | Component inventory                 |
| 2    | Search SBOM for affected package name and version            | List of affected applications       |
| 3    | Identify direct dependencies (explicitly imported package)   | Direct exposure map                 |
| 4    | Identify transitive dependencies (package used by another package that uses affected) | Transitive exposure map |
| 5    | Prioritize by application sensitivity and data access        | Prioritized remediation list        |
| 6    | Identify all environments where affected application is deployed | Full deployment scope            |

### 13.1B Package Manifest Files to Review

| Platform / Language | Manifest File           | Lock File                      |
| ------------------- | ----------------------- | ------------------------------ |
| Node.js / npm       | package.json            | package-lock.json / yarn.lock  |
| Python              | requirements.txt        | Pipfile.lock / poetry.lock     |
| Java (Maven)        | pom.xml                 | N/A (resolved at build time)   |
| Java (Gradle)       | build.gradle            | gradle.lockfile                |
| Ruby                | Gemfile                 | Gemfile.lock                   |
| Go                  | go.mod                  | go.sum                         |
| .NET / NuGet        | *.csproj / packages.config | packages.lock.json            |
| PHP                 | composer.json           | composer.lock                  |
| Rust                | Cargo.toml              | Cargo.lock                     |

### 13.1C Dependency Confusion Investigation (If Applicable)

If dependency confusion is suspected:

- Identify all private/internal package names used in the organization
- Check public repositories (npm, PyPI, RubyGems) for packages with the same names
- Determine if build tools retrieved the public version instead of internal version
- Check build logs for the source URL of each package download
- Review network egress logs for connections to public package repositories during build

---

## 14. Phase 8 – CI/CD Pipeline Assessment

This phase applies when the supply chain attack may have **compromised the build or deployment pipeline**.

### 14.1A CI/CD Compromise Indicators

| Indicator                                        | Evidence Source           | Why it Matters                                    |
| ------------------------------------------------ | ------------------------- | ------------------------------------------------- |
| Unexpected commits to repositories from build accounts | Source control logs | Code injection into source                       |
| Build scripts modified without authorized change | Source control / build logs | Malicious build step injection                 |
| Build process making unexpected network calls    | Build logs / firewall     | Exfiltration or download during build            |
| New secrets or environment variables accessed    | CI/CD platform audit logs | Secret theft during build                        |
| Build artifacts with different hashes than expected | Artifact registry      | Backdoored binary deployed                       |
| Deployment to unauthorized environments          | CD pipeline logs          | Unauthorized code deployment                     |
| Unusual timing of builds (off-hours automated)  | CI/CD platform logs       | Attacker-triggered builds                        |

### 14.1B CI/CD Investigation Steps

| Step | Action                                                       | Output                          |
| ---- | ------------------------------------------------------------ | ------------------------------- |
| 1    | Review all pipeline runs during dwell period for anomalies   | Suspicious pipeline run list    |
| 2    | Review all code commits during dwell period for unauthorized changes | Unauthorized commit list   |
| 3    | Compare deployed artifact hashes against source-built hashes | Hash mismatch report            |
| 4    | Review all secrets accessed during pipeline runs             | Secrets exposure assessment     |
| 5    | Review all external network calls made during pipeline runs  | External call list              |
| 6    | Identify all deployments made during dwell period for rollback assessment | Deployment list           |

### 14.1C Deployed Code Integrity Verification

If CI/CD compromise is suspected, all code deployed during the dwell period must be reviewed:

- Obtain list of all deployments made during the suspected dwell period
- For each deployment, compare deployed artifact hash against independently built artifact from the same source commit
- Flag any hash mismatches for L3 forensic analysis
- Consider rolling back all deployments from the dwell period until integrity can be confirmed

---

## 15. Phase 9 – Containment Recommendations (L2 Output)

L2 must provide a prioritized containment plan. L2 may recommend containment actions but must coordinate approvals through SOC Lead and IR Team for high-impact actions.

### 15.1A Containment Recommendation Matrix

| Finding                                              | Recommended Containment                                      | Owner              | Approval Required       |
| ---------------------------------------------------- | ------------------------------------------------------------ | ------------------ | ----------------------- |
| Active C2 communication confirmed                    | Block IoC destinations at firewall and proxy immediately     | Network/SOC Lead   | SOC Lead                |
| Affected software making suspicious outbound connections | Block vendor software process outbound access at host firewall | Platform/EDR    | SOC Lead                |
| Active lateral movement confirmed                    | Isolate affected source systems from network                 | Network/IR Team    | IR Team / CISO          |
| Vendor VPN or remote access active                  | Revoke vendor remote access (VPN/API/SSH) immediately        | Network/IAM        | SOC Lead                |
| Affected version in production with IoC matches      | Isolate highest-priority systems; halt further updates       | Platform/IR Team   | IR Team                 |
| Malicious package in build pipeline                  | Disable CI/CD pipeline; remove malicious package            | DevSecOps          | DevSecOps Lead / CISO   |
| Secrets or credentials potentially exposed           | Rotate all credentials and API keys accessible to compromised software | IAM/Platform | SOC Lead / App Owner  |
| Cloud IAM changes suspected                         | Revoke suspicious IAM roles/keys; enable enhanced CloudTrail | Cloud/Security  | Cloud Lead / SOC Lead   |
| Persistence mechanism identified                     | Remove persistence; rebuild if confirmed deep compromise     | IR Team            | CISO                    |
| Data staging detected                               | Block egress from staging location; preserve evidence        | Network/IR Team    | IR Team                 |

### 15.1B Containment Sequencing (Priority Order)

Execute in this sequence to minimize risk while preserving evidence:

1. Block confirmed C2 destinations at firewall and proxy (lowest business risk, highest security value)
2. Revoke vendor remote access (VPN/API/SSH tokens) — prevents continued vendor-side pivot
3. Block automatic software update mechanisms (prevents further compromise via update)
4. Rotate exposed credentials and API keys (kills stolen credential value)
5. Isolate highest-priority affected systems (highest business risk; requires approvals)
6. Disable CI/CD pipeline (if pipeline compromise confirmed)
7. Remove or rollback affected software (requires compatibility and business review)
8. Rebuild compromised systems (last resort; highest effort and disruption)

---

## 16. Phase 10 – Escalation Decision and Handoff

### 16.1A Escalate to L3 Immediately if:

- Execution of malicious functionality is confirmed or highly likely
- Lateral movement indicators are found beyond the initial affected system
- Persistence mechanisms are identified that require forensic confirmation
- Data exfiltration is confirmed or suspected and requires forensic reconstruction
- The dwell period appears to be greater than 30 days (requires extended forensic timeline)
- Legal or regulatory evidence requirements necessitate forensic-grade collection
- CI/CD pipeline compromise is confirmed (code integrity must be forensically validated)

### 16.1B Escalate to IR Team Immediately if:

- Active attacker is confirmed in the environment (ongoing lateral movement or C2)
- Data breach is confirmed or declared (legal and regulatory coordination required)
- Critical systems are compromised (domain controllers, PKI, PAM, key management, SCADA)
- Multiple clients are affected simultaneously (MSSP context — crisis coordination needed)
- Executive or board notification is required
- Law enforcement engagement is being considered
- The investigation scope exceeds what L2/L3 can handle without major incident command

### 16.1C Do Not Escalate to L3/IR if:

- Affected version is confirmed NOT present in organization AND no IoC matches found
- Only development/sandbox environments are affected with no connection to production
- Vendor patch has been applied, verified clean, and no indicators of prior execution
- Thorough investigation confirms the malicious component was never executed

Document the rationale for NOT escalating clearly in the ticket.

---

## 17. Documentation Requirements (Ticket Checklist)

Before handoff to L3/IR Team or incident closure, complete:

| Requirement                                              | Status |
| -------------------------------------------------------- | ------ |
| Confirmed impact status declared with evidence basis     | ☐      |
| Affected systems inventory table completed               | ☐      |
| Extended IoC search completed (90+ day window)           | ☐      |
| IoC search matrix completed for all IoC types            | ☐      |
| Lateral movement assessment completed                    | ☐      |
| Persistence assessment checklist completed               | ☐      |
| Data breach trigger assessment completed and documented  | ☐      |
| SBOM analysis completed (if package/library attack)      | ☐      |
| CI/CD pipeline assessment completed (if applicable)      | ☐      |
| Containment plan documented with owners and approvals    | ☐      |
| Escalation decision documented with justification        | ☐      |
| Timeline entries recorded in UTC with evidence refs      | ☐      |
| Threat intelligence enrichment completed for IoC matches | ☐      |
| Evidence references attached to ticket                   | ☐      |

---

## 18. Common L2 Mistakes to Avoid

| Mistake                                               | Risk                                           | Correct Approach                                     |
| ----------------------------------------------------- | ---------------------------------------------- | ---------------------------------------------------- |
| Using only 7-day or 30-day search window              | Miss long dwell time activity                  | Use 90-day minimum; extend to 12 months if needed    |
| Only checking production systems                      | Miss dev/CI-CD entry points                    | Check all environments including build infrastructure |
| Treating "no IoC match" as "not compromised"          | IoCs may have changed or be incomplete         | Continue behavioral investigation beyond IoC list    |
| Not completing SBOM analysis for package attacks      | Miss transitive dependency impact              | Always complete SBOM analysis for package attacks    |
| Applying vendor patch without hash verification       | Patch may be malicious; evidence may be lost   | Verify patch integrity before applying               |
| Not rotating credentials exposed to compromised software | Attacker retains access via stolen creds    | Rotate all credentials accessible to compromised software |
| Closing incident before all affected systems confirmed | Persistent compromise in missed systems       | Complete full scope before any closure               |
| Sharing investigation details with vendor without legal review | Legal and contractual risk             | Get legal approval before sharing with vendor        |
| Not checking CI/CD pipelines in software supply chain attacks | Backdoored builds deployed to production | Always assess pipeline integrity                 |
| Treating supply chain as isolated malware event       | Miss broader APT campaign context              | Coordinate with threat intel; consider APT playbook  |

---

## 19. MSSP Client Handling Notes

For MSSP-managed environments at L2:

**Multi-client investigation coordination:**
- Each affected client must be investigated **independently** even if the same software/vendor is involved
- Document findings, timelines, and evidence **separately per client**
- Do not share one client's affected system details or investigation findings with another client

**Client approval requirements at L2:**
- High-impact containment actions (isolating systems, revoking vendor access) require client approval unless emergency authority exists in the contract
- Escalation decisions affecting client SLAs must be communicated to SDM before execution
- Clients must be notified of confirmed P1/P2 supply chain incidents per contractual timelines

**Evidence handling:**
- Store all client evidence in client-specific, segregated evidence locations
- Cross-client IoC sharing requires anonymization and explicit approval from each client
- Maintain separate chain-of-custody records per client

**SLA implications:**
- If investigation or containment actions may breach SLA, notify SDM immediately
- Document all timeline decisions to support SLA discussions

Reference: `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md`

---

## 20. Related Documents

| Document                         | Path                                                         |
| -------------------------------- | ------------------------------------------------------------ |
| Supply Chain Master              | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-Master.md` |
| Supply Chain L1 Triage           | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-L1-Triage.md` |
| Supply Chain L3 Forensics        | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-L3-Forensics.md` |
| Supply Chain Vendor Coordination | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-Vendor-Coordination.md` |
| Supply Chain MITRE Mapping       | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-MITRE-Mapping.md` |
| Data Breach Master               | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Master.md` |
| APT Campaign Playbooks           | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-Master.md`           |
| Network Intrusion Playbooks      | `02_PLAYBOOKS/02.11_Network-Intrusion/PB-NetworkIntrusion-Master.md` |
| TI IoC Handling SOP              | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md` |
| Evidence Collection SOP         | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| L2 to L3 Escalation Path        | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L2-to-L3-Escalation.md` |
| L3 to IR Team Escalation        | `05_ESCALATION-AND-COMMUNICATION/05.1_Escalation-Paths/L3-to-IR-Team-Escalation.md` |
| Multi-Client Alert Handling     | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Multi-Client-Alert-Handling.md` |
| Detection Improvement Log       | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md` |

---

## 21. Revision History

| Version | Date        | Author                    | Changes         |
| ------- | ----------- | ------------------------- | --------------- |
| 1.0     | 19-May-2026 | L2 SOC Lead / IR Team Lead | Initial version |

---

## 22. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**