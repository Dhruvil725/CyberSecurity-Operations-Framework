# Playbook: Supply Chain Attack – Master

---

## 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | Playbook – Supply Chain Attack (Master)                      |
| Document ID    | IR-PB-SC-001                                                 |
| Version        | 1.0                                                          |
| Effective Date | 19-May-2026                                                  |
| Owner          | SOC Manager / IR Team Lead                                   |
| Approved By    | CISO                                                         |
| Classification | Internal – Confidential                                      |
| Review Cycle   | Quarterly and after any P1/P2 supply chain incident          |

---

## 2. Purpose

This master playbook defines the end-to-end response procedures for **supply chain attacks** across enterprise and MSSP-managed environments.

Supply chain attacks are among the most dangerous and difficult-to-detect attack categories because:

- The attacker compromises a **trusted third party** (vendor, software provider, managed service provider) to reach the ultimate target organization
- Malicious code or access arrives through **legitimate, trusted, and often signed channels** — bypassing standard security controls
- The **blast radius is extremely wide** — a single compromised vendor or software package can simultaneously impact hundreds or thousands of organizations
- **Dwell time is long** — attackers often remain undetected for weeks or months while performing reconnaissance and data collection
- Standard perimeter and endpoint defenses offer **limited protection** because the attack originates from within trusted software, update mechanisms, or vendor connections

**Common supply chain attack vectors include:**

- Compromised software update mechanisms delivering malicious payloads to all customers (SolarWinds SUNBURST)
- Malicious packages published to public repositories targeting developers (npm, PyPI, RubyGems, Maven)
- Compromised open-source library maintainer accounts injecting backdoors
- Dependency confusion attacks where malicious public packages override internal private packages
- Compromised CI/CD pipelines injecting malicious code into builds before deployment
- Compromised managed service providers (MSP/MSSP) used as a pivot to access client environments
- Malicious code injected into third-party SDKs, JavaScript libraries, or APIs embedded in applications
- Hardware implants introduced during manufacturing, shipping, or logistics handling
- Compromised development tools (compilers, IDEs, build tools) introducing backdoors at compile time

This playbook standardizes:

- Detection and triage of supply chain attack indicators across all detection sources
- Investigation and scoping across internal systems and vendor environments
- Containment actions while preserving evidence and managing vendor relationships
- Escalation to L3 forensics and IR Team for confirmed compromises
- Regulatory, legal, and client communication coordination
- Post-incident vendor risk management improvements and detection engineering

---

## 3. Scope

### 3.1 In Scope

This playbook applies to:

- **Software supply chain attacks** — malicious updates, packages, libraries delivered through legitimate channels
- **Managed service provider (MSP/MSSP) compromise** — vendor environment used as pivot into client environments
- **CI/CD pipeline compromise** — build and deployment infrastructure tampered with to inject malicious code
- **Third-party API/SDK compromise** — embedded components in applications modified by attacker
- **Open-source dependency compromise** — malicious or hijacked packages used in internal development
- **Cloud provider or SaaS vendor compromise** — vendor-side breach affecting organization's data or access
- **Hardware supply chain incidents** — where digital forensic evidence is available to support investigation

### 3.2 Out of Scope (Use Other Playbooks)

| Scenario                                                     | Use Playbook                          |
| ------------------------------------------------------------ | ------------------------------------- |
| Direct network intrusion not involving supply chain          | 02.11_Network-Intrusion/              |
| Ransomware deployed as secondary payload post-supply chain   | 02.1_Ransomware/                      |
| Data breach resulting from supply chain attack (post-confirmation) | 02.6_Data-Breach-Exfiltration/   |
| Phishing used as initial access vector (not supply chain)    | 02.2_Phishing-BEC/                    |
| Web application attack not supply chain related              | 02.8_Web-Application-Attack/          |
| APT campaign investigation (may overlap, coordinate)         | 02.13_APT-Campaign/                   |

---

## 4. Definitions

| Term                         | Definition                                                   |
| ---------------------------- | ------------------------------------------------------------ |
| Supply Chain Attack          | An attack that targets a less-secure element in the supply chain (vendor, software, hardware) to compromise the ultimate target organization |
| Trusted Vendor               | Third-party organization whose software, services, or hardware is integrated into the organization's environment |
| Software Bill of Materials (SBOM) | A complete inventory of all software components, dependencies, libraries, and their versions used in an application or system |
| Dependency Confusion         | Attack where a malicious public package with a matching internal package name is pulled automatically by build tools |
| Typosquatting                | Publishing a malicious package with a name visually similar to a legitimate popular package to catch developer mistakes |
| Lateral Movement             | Attacker movement from the initially compromised vendor or software entry point to other systems within the target environment |
| Backdoor                     | Hidden access mechanism installed by the attacker via the supply chain compromise for persistent access |
| Integrity Verification       | Process of validating that software, packages, or hardware have not been tampered with, using hashes, signatures, or attestations |
| C2 (Command and Control)     | Attacker-controlled infrastructure used to issue commands to and receive data from compromised systems |
| SBOM Analysis                | Process of reviewing the software bill of materials to identify vulnerable or compromised components |
| Sideloading                  | Loading a malicious library or component alongside or in place of a legitimate one |
| Build Pipeline               | Automated sequence of steps that compile, test, and package software for deployment |
| Software Attestation         | Cryptographic proof that software was built from a specific source and has not been tampered with |

---

## 5. Supply Chain Attack Categories and Examples

| Category                    | Description                                                  | Real-World Example                   |
| --------------------------- | ------------------------------------------------------------ | ------------------------------------ |
| Software Update Compromise  | Malicious code delivered via legitimate update mechanism signed by vendor | SolarWinds SUNBURST (2020)           |
| Package Repository Attack   | Malicious package published to public software repository    | event-stream npm incident (2018)     |
| Dependency Confusion        | Malicious public package overrides private internal package  | Alex Birsan research (2021)          |
| CI/CD Pipeline Compromise   | Attacker injects malicious code into build/delivery pipeline | Codecov supply chain breach (2021)   |
| MSP/MSSP Compromise         | Managed service provider used as pivot to reach client environments | Kaseya VSA attack (2021)          |
| Open-Source Maintainer Compromise | Hijacked or malicious maintainer injects backdoor into widely used library | XZ Utils backdoor (2024)  |
| SDK/API Compromise          | Third-party SDK or embedded API modified to include malicious functionality | Polyfill.io compromise (2024)    |
| Hardware Implant            | Physical tampering during manufacturing, logistics, or shipping | Reported in supply chain research    |
| Compiler/Build Tool Compromise | Malicious compiler introduces backdoor at compile time     | Ken Thompson's reflections on trusting trust |
| Container Image Compromise  | Malicious base container image published to registry         | Various Docker Hub incidents         |

---

## 6. Severity Classification (Supply Chain Specific)

Standard severity guidance applies, but supply chain incidents have unique amplifying factors:

| Scenario                                                     | Default Severity         |
| ------------------------------------------------------------ | ------------------------ |
| Confirmed supply chain compromise with active C2 or lateral movement in environment | P1         |
| Confirmed malicious software installed and executed across multiple systems | P1           |
| Vendor confirmed compromised AND organization confirmed using affected product version | P1        |
| Active attacker confirmed pivoting from vendor environment into organization | P1           |
| Data exfiltration confirmed or strongly suspected via supply chain vector | P1           |
| Suspicious indicators in third-party software requiring urgent investigation | P2          |
| Malicious package identified in dependency tree, no confirmed execution evidence | P2          |
| Vendor advisory confirms compromise but impact to organization unknown | P2            |
| Typosquatting package installed in development environment, no production execution | P3        |
| Public disclosure of supply chain issue with no confirmed organizational usage | P3          |
| Vendor advisory for product not used in organization         | P4                       |

Reference: `01_INCIDENT-CLASSIFICATION/01.1_Severity-Matrix/Severity-Classification-Guide.md`

---

## 7. Activation Criteria

Activate this playbook when **any of the following** occur:

**From threat intelligence or public disclosure:**
- Threat intelligence feed indicates a vendor or software used by the organization is compromised
- Public disclosure (CERT-In, CISA, NCSC, vendor advisory) of supply chain attack affecting software in use
- Industry peer sharing of IoCs related to supply chain attack on tools or vendors used

**From internal detection sources:**
- SIEM correlation fires on suspicious behavior originating from a trusted third-party process or update service
- EDR detects unexpected process execution, network connection, or file modification from vendor software
- Unexpected network connections originating from vendor software or agent processes
- CI/CD pipeline anomalies — unexpected code commits, new secrets accessed, build behavior changed
- Package integrity verification failure or hash mismatch during software installation
- File integrity monitoring (FIM) alerts on unexpected changes to vendor-installed files

**From external notification:**
- Vendor directly notifies organization of security incident affecting their product or services
- Law enforcement or government agency notifies organization of supply chain compromise
- Security researcher reports indicators related to supply chain attack

---

## 8. Roles and Responsibilities

| Role                   | Responsibilities                                             |
| ---------------------- | ------------------------------------------------------------ |
| L1 SOC Analyst         | Validate initial alerts, identify affected software/vendor, preserve minimum evidence, recommend severity, escalate |
| L2 SOC Analyst         | Confirm organizational impact, identify affected systems and scope, assess lateral movement risk, recommend containment |
| L3 Analyst / Forensics | Deep forensic analysis, IOC extraction, persistence identification, timeline reconstruction, evidence for legal |
| SOC Lead               | Incident coordination, vendor communication initiation, management notification, bridge call for P1/P2 |
| IR Team                | Major incident command, cross-team coordination, high-impact decisions, regulatory coordination |
| Threat Intelligence    | Enrich with external intelligence, monitor vendor advisories, develop hunting queries, maintain IOC register |
| Vendor Management      | Coordinate with affected vendor, obtain forensic data and IoCs, manage contractual obligations |
| Legal/Compliance       | Regulatory reporting, legal hold, vendor contract review, law enforcement engagement |
| Platform/Infrastructure| System isolation, rebuild coordination, patch deployment, integrity verification |
| Development/DevSecOps  | CI/CD pipeline investigation, SBOM analysis, dependency review, package integrity checks |
| CISO                   | Executive decisions, board notification, vendor relationship management, regulatory liaison |
| MSSP SDM               | Client communications, client-specific containment approvals, multi-client coordination |

Reference: `00_GOVERNANCE/00.3_Roles-and-Responsibilities/RACI-Matrix-IR.xlsx`

---

## 9. Evidence Handling Requirements (Mandatory)

Supply chain incidents require careful evidence handling because:

- Malicious artifacts are often **deleted or overwritten** during software updates
- Vendor-side evidence may be **beyond the organization's control**
- Evidence may be needed for **legal proceedings** against vendor or threat actor
- Evidence may span **multiple systems and time periods** due to long dwell times

### 9.1 Minimum Evidence Set (All Incidents)

| Evidence Item                     | Source                      | Priority | Notes                                   |
| --------------------------------- | --------------------------- | -------- | --------------------------------------- |
| Affected software version details | Asset inventory / SIEM      | P0       | Version, install date, update history   |
| Software update/install logs      | OS logs / software logs     | P0       | When was affected version installed     |
| Network connection logs from vendor software | Firewall / proxy / EDR | P0  | Unusual outbound connections            |
| Process execution logs            | EDR / OS audit logs         | P0       | Processes spawned by vendor software    |
| File system changes               | FIM / EDR                   | P1       | Files created/modified by vendor software |
| SIEM alert details                | SIEM                        | P1       | All correlated alerts for time window   |
| Package/dependency manifests      | Development environment      | P1       | package.json, requirements.txt, pom.xml |
| Vendor advisory details           | Public / vendor portal      | P1       | Affected versions, IoCs, remediation    |

### 9.2 Additional Evidence (P1/P2 or Active Compromise Suspected)

| Evidence Item                     | Source                      | When Needed                        | Purpose                         |
| --------------------------------- | --------------------------- | ---------------------------------- | ------------------------------- |
| Memory captures                   | EDR / forensic tools        | Active process suspected           | Capture runtime malicious artifacts |
| Disk images / snapshots           | Forensic tools              | Deep compromise confirmed          | Legally defensible evidence     |
| CI/CD pipeline logs               | Build system                | Pipeline compromise suspected      | Code injection evidence         |
| Cloud audit logs                  | AWS/Azure/GCP               | Cloud services involved            | IAM and access evidence         |
| Secrets/vault access logs         | Secrets management platform | Credential theft suspected         | Stolen secrets identification   |
| Network PCAP                      | Network TAP / cloud         | Active C2 suspected                | C2 communication evidence       |

Reference: `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`

---

## 10. Supply Chain Incident Lifecycle

| Phase                   | Description                                                   | Primary Owner              |
| ----------------------- | ------------------------------------------------------------- | -------------------------- |
| Detection and Triage    | Identify affected software/vendor, confirm organizational use, initial scope | L1/L2            |
| Initial Investigation   | Confirm impact, identify affected systems, assess lateral movement risk | L2                |
| Containment             | Isolate affected systems, block vendor access paths, stop active compromise | SOC Lead / IR Team |
| Vendor Coordination     | Obtain IoCs, forensic data, patch or workaround from vendor   | Vendor Mgmt / IR Team      |
| Deep Forensics          | Full timeline reconstruction, persistence analysis, data access assessment | L3/IR Team      |
| Eradication             | Remove malicious components, rebuild if needed, verify clean state | IR / Platform Teams    |
| Recovery                | Restore from clean state, verify integrity, return to service  | IR / Platform / App Teams  |
| Post-Incident           | PIR, vendor risk review, SBOM improvements, detection tuning  | IR / SOC / Vendor Mgmt     |

---

## 11. Standard Investigation Workflow (End-to-End)

### Phase A — Detection and Triage (L1)

**Objectives:**
- Identify the affected vendor, software, or package
- Determine if affected version is in use in the organization
- Preserve initial evidence before software updates or changes occur
- Recommend severity and escalate appropriately

**Key actions:**
- Cross-reference affected product/version against asset inventory
- Preserve software version information before any updates are applied
- Capture initial network connection logs from affected software processes
- Document IoCs from vendor advisory or threat intelligence

Reference: `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-L2-Investigation.md`

---

### Phase B — L2 Investigation

**Objectives:**
- Confirm whether the affected software actually executed malicious functionality
- Identify all affected systems across the organization
- Assess whether lateral movement has occurred
- Evaluate data breach triggers

**Key actions:**
- Query asset inventory for all instances of affected software/version
- Analyze network logs for C2 patterns described in vendor advisory or threat intel
- Check EDR for process execution anomalies from affected software
- Begin data breach trigger assessment

Reference: `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-L2-Investigation.md`

---

### Phase C — Containment

**Objectives:**
- Stop active compromise without creating unnecessary operational disruption
- Block attacker access paths while preserving evidence
- Prevent lateral movement and data exfiltration

**Key containment actions (priority order):**
- Block C2 destinations identified in IoCs at firewall and proxy
- Isolate actively compromised systems from network
- Revoke vendor access (VPN, API tokens, remote support) if vendor is confirmed compromised
- Block automatic software updates temporarily to prevent further compromise
- Invalidate secrets/credentials that vendor software had access to

Reference: Containment decision framework in Section 13 of this document

---

### Phase D — Vendor Coordination

**Objectives:**
- Obtain forensic data, IoCs, and remediation guidance from vendor
- Understand the vendor's own investigation status and timeline
- Manage legal and contractual aspects of information sharing

**Key actions:**
- Engage vendor security/incident response team through official channels
- Request: affected version list, IoC list, forensic artifacts, patch/workaround timeline
- Coordinate legal review before sharing organization's forensic data with vendor
- Track vendor investigation updates and incorporate new IoCs

Reference: `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-Vendor-Coordination.md`

---

### Phase E — L3 Forensics

**Objectives:**
- Reconstruct the full attack chain and authoritative timeline
- Confirm persistence mechanisms and compromise depth
- Assess data access and exfiltration scope
- Generate defensible evidence for legal and regulatory needs

Reference: `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-L3-Forensics.md`

---

### Phase F — Post-Incident

**Objectives:**
- Conduct post-incident review with all stakeholders
- Update SBOM processes and vendor risk management
- Improve detection capabilities for supply chain threats
- Update vendor contracts and security requirements

Reference: `08_POST-INCIDENT/`

---

## 12. Key Differences from Standard Incidents

Supply chain incidents require special considerations that differ from typical incidents:

**Evidence challenges:**
- Malicious activity originates from **signed and trusted software** making attribution difficult
- Vendor forensic data may be **needed but not readily available** or may be delayed
- Attacker **dwell time is often measured in weeks or months** making log retention critical
- Multiple systems may show the same artifact making **patient zero identification complex**

**Containment challenges:**
- Blocking vendor software may cause **significant operational disruption**
- Multiple systems are often affected **simultaneously** requiring coordinated response
- Removing affected software may not be immediately possible if **business-critical**
- Other organizations using the same vendor are **also victims** — coordination with peers may be appropriate

**Vendor coordination requirements:**
- **Legal review** of information sharing with vendor is required before sharing forensic data
- Non-disclosure obligations may apply during the **active investigation phase**
- Vendor may be **unaware of their own compromise** — organization may be first to notify
- Vendor's incident response capability and **timeline may be unknown**

**Regulatory complexity:**
- Organization may be **both a victim and potentially liable** (especially in MSSP context)
- **Multiple simultaneous regulatory notifications** may be required
- Regulators may require evidence that **due diligence** was performed on vendor selection

---

## 13. Containment Decision Framework

Unlike standard incidents, supply chain containment requires careful balancing of risk:

| Containment Action                       | When to Execute                                 | Business Risk          | Security Risk if Not Taken    | Approval Required  |
| ---------------------------------------- | ----------------------------------------------- | ---------------------- | ----------------------------- | ------------------ |
| Block C2 destinations at firewall/proxy  | IoCs identified with high confidence            | Low                    | Ongoing C2 communication      | SOC Lead           |
| Block vendor software automatic updates  | Active supply chain update attack confirmed      | Medium (delayed patches) | Further compromise via updates | SOC Lead          |
| Isolate affected high-value systems      | Active lateral movement or C2 confirmed         | High (service disruption) | Data loss, spread            | IR Team / CISO     |
| Revoke vendor VPN/remote access          | Vendor environment confirmed compromised        | Medium (support disruption) | Continued pivot access      | SOC Lead / CISO    |
| Revoke vendor API tokens/service accounts | Vendor access or token exposure confirmed      | Medium (integration break) | Unauthorized data access    | SOC Lead           |
| Remove/rollback affected software version | Confirmed malicious version with IoCs           | High (compatibility)   | Persistent backdoor           | IR Team / App Owner |
| Full system rebuild                      | Deep compromise confirmed, persistence unresolved | Very High             | Undetected persistent access  | CISO / Management  |
| Block affected package across all environments | Malicious package confirmed in build tools | Medium (build breaks)  | Backdoored builds deployed   | IR Team / DevSecOps |
| Disable CI/CD pipeline                  | Pipeline compromise confirmed                   | High (no deployments)  | Backdoored code released      | CISO / DevSecOps   |

---

## 14. Escalation Criteria

### 14.1 Escalate to L2 Immediately if:

- Affected software/version confirmed present in production environment
- Any network connections to IoC destinations detected from affected software
- More than 10 systems affected by the compromised software/package
- CI/CD pipeline anomalies are detected

### 14.2 Escalate to L3 if:

- Lateral movement suspected beyond initial entry point
- Persistence mechanisms identified in affected systems
- Large-scale deployment of affected software across organization
- Forensic reconstruction needed for legal or regulatory evidence
- Attacker tools, techniques, or additional payloads discovered

### 14.3 Escalate to IR Team if:

- Active attacker confirmed in environment
- Data exfiltration confirmed or strongly suspected
- Critical systems compromised (domain controllers, PAM, key management)
- Multi-client impact confirmed (MSSP context)
- Executive/board notification required
- Regulatory notification timelines may be triggered

### 14.4 Escalate to Legal/Compliance if:

- Customer or employee data potentially accessed
- Regulatory notification timelines triggered
- Vendor contract review or legal action being considered
- Law enforcement engagement being considered
- Organization may have downstream liability (MSSP context)

---

## 15. Data Breach Trigger Assessment (Mandatory Decision Gate)

Supply chain attacks frequently result in data access. This assessment is mandatory at every investigation phase.

| Trigger Question                                                     | Answer (Yes/No/Unknown) | If YES → Immediate Action                        |
| -------------------------------------------------------------------- | ----------------------- | ------------------------------------------------ |
| Did compromised software have access to sensitive data or credentials? |                        | Activate Data Breach playbook; engage Legal       |
| Is there evidence of data collection, staging, or exfiltration?      |                         | Activate Data Breach playbook; engage Legal       |
| Did compromised vendor have contractual access to organization data?  |                         | Assess breach scope; engage Legal/Compliance      |
| Is customer PII, financial data, or health data potentially exposed?  |                         | Engage Legal/Compliance immediately               |
| Did compromised software have access to privileged credentials?       |                         | Rotate all exposed credentials; assess scope      |
| Did compromised CI/CD pipeline deploy backdoored code to production?  |                         | Assess all deployments; activate breach review    |

Reference: `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/PB-DataBreach-Master.md`

---

## 16. Communication Requirements

### 16.1 Internal Communication

| Audience           | When                              | Method                            | Content                              |
| ------------------ | --------------------------------- | --------------------------------- | ------------------------------------ |
| SOC Lead           | Immediately for P1/P2             | Bridge call + ticket              | Affected software, systems, severity |
| IR Team            | Confirmed P1 or active compromise | Bridge call + war room            | Full situation report                |
| Management/CISO    | P1 and significant P2             | Management notification template  | Business impact, actions, timeline   |
| Legal/Compliance   | Data breach indicators            | Direct call + formal notification | Legal hold, regulatory timelines     |
| Platform/DevSecOps | Containment actions required      | Task assignment + ticket          | Specific actions and timelines       |

Reference: `05_ESCALATION-AND-COMMUNICATION/05.2_Communication-Templates/`

### 16.2 External Communication

| Audience                | When                                          | Method                          | Content                                     |
| ----------------------- | --------------------------------------------- | ------------------------------- | ------------------------------------------- |
| Affected Vendor         | As soon as compromise confirmed               | Secure channel + vendor portal  | IoCs, affected versions, organizational impact |
| MSSP Clients            | Per SLA and contractual obligations           | Client notification template    | Impact, containment actions, timeline       |
| Regulatory Bodies       | Per regulatory timelines (RBI, CERT-In, etc.) | Regulatory reporting SOP        | Incident details, data impact, remediation  |
| Law Enforcement         | If criminal activity confirmed                | Legal counsel coordination      | Formal report with evidence                 |
| Industry Peers (ISACs)  | If IoC sharing is appropriate                 | Anonymized sharing              | Technical IoCs only, anonymized             |

Reference: `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/`

---

## 17. MSSP-Specific Considerations

For MSSP environments, supply chain attacks create amplified and complex scenarios:

**Multi-client impact:**
- A single compromised tool used across multiple clients creates **simultaneous multi-client P1 incidents**
- Each client's impact must be assessed and documented **independently**
- Client notification obligations must be evaluated for **each client individually** based on their contract and regulatory requirements

**Evidence and data segregation:**
- Evidence must be strictly segregated **per client** even when the same tool is affected across all
- IoC sharing across clients requires **anonymization and explicit approval**
- Chain-of-custody records must be maintained **separately per client**

**SLA implications:**
- Service disruption from containment actions may trigger **SLA breach notifications**
- Proactive client communication is required **before SLA breach** where possible
- Document all decisions and timelines to support **SLA dispute resolution**

**Vendor management:**
- MSSP may have negotiated **different contractual terms** with vendor than individual clients
- MSSP should coordinate vendor communication **centrally** while keeping clients informed
- Client contracts should be reviewed for **vendor risk and notification obligations**

Reference: `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md`

---

## 18. Regulatory and Compliance Context

Supply chain incidents frequently trigger multiple regulatory obligations simultaneously:

| Regulation    | Trigger Condition                                        | Notification Timeline       | Required Evidence                          |
| ------------- | -------------------------------------------------------- | --------------------------- | ------------------------------------------ |
| RBI           | Customer data breach in financial sector via supply chain | As per RBI circular         | Incident report, root cause, affected data |
| CERT-In       | Significant cyber incident including supply chain attacks | 6 hours (initial report)    | Technical details, IoCs, affected systems  |
| GDPR          | EU personal data accessed or exfiltrated                 | 72 hours to supervisory authority | Breach details, data scope, remediation |
| PCI-DSS       | Cardholder data potentially exposed                      | Immediate to payment brands | Forensic report, scope, remediation plan   |
| ISO 27001     | Significant information security incident                | Per ISMS incident procedure | Incident record, evidence, corrective action |

Reference: `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md`

---

## 19. Post-Incident Requirements

### 19.1 Lessons Learned Session (Required for P1/P2)

Schedule within **5 business days** of incident closure.

**Attendees:**
- CISO
- SOC Lead
- IR Team Lead
- L2/L3 Analysts involved
- Vendor Management
- Legal/Compliance
- Platform/DevSecOps Lead
- Application Owners (if affected)

**Agenda items:**

| Topic                             | Questions to Answer                                                    |
| --------------------------------- | ---------------------------------------------------------------------- |
| Detection effectiveness           | How was the supply chain attack detected? Were there earlier missed signals? |
| SBOM coverage                     | Did we have a current SBOM? Did it help identify affected systems?     |
| Asset inventory accuracy          | Was our software inventory accurate enough for rapid impact assessment? |
| Vendor risk management            | Was this vendor assessed for security risk? Were assessments adequate? |
| Containment decision speed        | Were containment decisions made quickly enough? Any delays?            |
| Evidence quality                  | Was evidence collected and preserved adequately?                       |
| Communication effectiveness       | Were all stakeholders notified appropriately and timely?               |
| Regulatory compliance             | Were regulatory notification timelines met?                            |
| Tooling gaps                      | What detection or response tooling gaps were identified?               |

### 19.2 Vendor Risk Management Improvements

After every supply chain incident, complete:

| Improvement Action                                              | Owner              | Target Date  | Status |
| --------------------------------------------------------------- | ------------------ | ------------ | ------ |
| Review and update vendor security assessment for affected vendor | Vendor Mgmt       | +14 days     | Open   |
| Implement or update SBOM process for affected application       | DevSecOps          | +30 days     | Open   |
| Add integrity verification to software update process           | Platform/DevSecOps | +30 days     | Open   |
| Review contractual security requirements with affected vendor   | Legal/Vendor Mgmt  | +30 days     | Open   |
| Implement package signing verification in CI/CD pipeline        | DevSecOps          | +60 days     | Open   |
| Add supply chain IoCs to SIEM detection rules                   | L3/Detection       | +7 days      | Open   |
| Review all vendors with similar access levels for risk          | Vendor Mgmt / CISO | +60 days     | Open   |

Reference: `08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx`

### 19.3 Detection Engineering Improvements

Add to Detection Improvement Log:

| Improvement                                                         | Owner          | Target Date | Status |
| ------------------------------------------------------------------- | -------------- | ----------- | ------ |
| Create SIEM rule for network connections from vendor software processes to known C2 ranges | L3/Detection | +7 days | Open |
| Implement hash verification alert for vendor-installed binaries     | L3/Detection   | +30 days    | Open   |
| Add anomaly detection for unusual process trees from vendor agents  | L3/Detection   | +30 days    | Open   |
| Implement CI/CD pipeline integrity monitoring                       | DevSecOps      | +45 days    | Open   |
| Deploy package repository scanning in build pipeline                | DevSecOps      | +30 days    | Open   |

Reference: `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`

---

## 20. Common Mistakes to Avoid

| Mistake                                           | Risk                                  | Correct Approach                               |
| ------------------------------------------------- | ------------------------------------- | ---------------------------------------------- |
| Applying vendor patch immediately without verification | Patch itself may be malicious    | Verify patch integrity and test before deploying |
| Blocking all vendor software without business approval | Major operational disruption    | Use targeted containment; get approvals        |
| Sharing organization forensic data with vendor without legal review | Legal exposure | Review vendor NDA and legal implications first |
| Not checking SBOM or asset inventory immediately  | Missing affected systems               | Run SBOM analysis as first investigation step  |
| Assuming single-system impact                     | Supply chain attacks are broad         | Always assume wide impact until proven otherwise |
| Not preserving software version before updating   | Evidence destruction                   | Snapshot or document version before any changes |
| Closing incident before all affected systems remediated | Persistent compromise remains    | Validate all affected systems before closure   |
| Not notifying regulators within required timelines | Regulatory penalties                  | Check notification timelines at incident start |
| Treating supply chain as standard malware         | Miss vendor coordination and SBOM work | Follow supply chain-specific procedures        |

---

## 21. Related Documents

| Document                         | Path                                                         |
| -------------------------------- | ------------------------------------------------------------ |
| Supply Chain L2 Investigation    | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-L2-Investigation.md` |
| Supply Chain L3 Forensics        | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-L3-Forensics.md` |
| Supply Chain Vendor Coordination | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-Vendor-Coordination.md` |
| Supply Chain MITRE Mapping       | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-MITRE-Mapping.md` |
| Data Breach Playbooks            | `02_PLAYBOOKS/02.6_Data-Breach-Exfiltration/`                |
| Network Intrusion Playbooks      | `02_PLAYBOOKS/02.11_Network-Intrusion/`                      |
| APT Campaign Playbooks           | `02_PLAYBOOKS/02.13_APT-Campaign/`                           |
| Evidence Handling                | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/`                          |
| Vendor Contacts                  | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Vendor-Contacts.md` |
| Regulatory Communication         | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/` |
| Cross-Client Incident Procedure  | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md` |
| Security Improvement Register    | `08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx` |
| Detection Improvement Log        | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md` |

---

## 22. Revision History

| Version | Date        | Author                    | Changes         |
| ------- | ----------- | ------------------------- | --------------- |
| 1.0     | 19-May-2026 | SOC Manager / IR Team Lead | Initial version |

---

## 23. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**