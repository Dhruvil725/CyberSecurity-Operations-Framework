# Playbook: Supply Chain Attack – Vendor Coordination

---

## 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | Playbook – Supply Chain Attack (Vendor Coordination)         |
| Document ID    | IR-PB-SC-005                                                 |
| Version        | 1.0                                                          |
| Effective Date | 19-May-2026                                                  |
| Owner          | IR Team Lead / Vendor Management Lead                        |
| Approved By    | CISO                                                         |
| Classification | Internal – Confidential                                      |
| Review Cycle   | Quarterly and after any P1/P2 supply chain incident          |

---

## 2. Purpose

This document defines the **vendor coordination procedures** for supply chain attack incidents where a third-party vendor, software provider, managed service provider, or open-source maintainer is involved in or responsible for the supply chain compromise.

Vendor coordination in supply chain incidents is fundamentally different from standard vendor support calls because:

- The vendor may be **both a victim and the source of the compromise** — this creates complex legal, contractual, and communication dynamics
- The organization may have **critical operational dependency** on the affected vendor making immediate termination of the relationship impossible
- The vendor may be **unaware of their own compromise** — the organization may be first to notify them
- **Information sharing must be carefully controlled** — sharing too much too early may compromise the investigation or expose legal liability
- **Contractual obligations** govern what can be shared, when, and with whom
- Multiple organizations may be simultaneously coordinating with the same vendor creating **coordination complexity**
- Vendor's own incident response timeline and quality is **outside organizational control** but critical to recovery

This playbook defines:

- How and when to initiate contact with affected vendors
- What information to request and what information to share (and when)
- Legal and contractual review requirements before any vendor communication
- How to manage vendor relationships during active incident investigation
- How to coordinate remediation guidance and patch verification
- Post-incident vendor risk management and contractual improvements

---

## 3. Scope

### 3.1 In Scope

Applies to vendor coordination for:

- Software vendors whose products are confirmed or suspected to have delivered malicious code
- Managed service providers (MSPs) whose access or tools were used to pivot into the organization
- Open-source project maintainers or organizations responsible for compromised libraries
- Cloud service providers or SaaS vendors whose infrastructure breach impacted the organization
- Hardware vendors where supply chain tampering is suspected
- Third-party SDK or API providers whose code was compromised and embedded in applications
- Package repository operators (npm, PyPI, etc.) when coordinating malicious package removal

### 3.2 Out of Scope

| Scenario                                         | Where to Look                                              |
| ------------------------------------------------ | ---------------------------------------------------------- |
| Standard vendor support for non-security issues  | Standard vendor support SOP                                |
| Regulatory body communication                    | 05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md |
| Law enforcement engagement                       | Legal Counsel Engagement SOP                               |
| Internal escalation and team coordination        | PB-SupplyChain-Master.md escalation section                |

---

## 4. Definitions

| Term                          | Definition                                                   |
| ----------------------------- | ------------------------------------------------------------ |
| Affected Vendor               | The third-party organization whose software, service, or infrastructure was the supply chain attack vector |
| Vendor IR Team                | The vendor's internal incident response or security team     |
| NDA (Non-Disclosure Agreement) | Legal agreement governing what information can be shared between parties |
| Legal Hold                    | Obligation to preserve documents and communications relevant to potential legal proceedings |
| Responsible Disclosure        | Coordinated process of notifying a vendor of a vulnerability or compromise before public disclosure |
| Vendor Advisory               | Official public or customer-facing statement from vendor about a security incident |
| Patch Verification            | Process of independently verifying that a vendor-provided patch is clean and effective |
| SLA (Service Level Agreement) | Contractual commitments between organization and vendor regarding service standards |
| PSIRT                         | Product Security Incident Response Team — vendor's security team for product vulnerabilities |
| ToC (Table of Contacts)       | Directory of vendor security contacts for escalation during incidents |

---

## 5. Pre-Communication Requirements (Mandatory Before Any Vendor Contact)

Before initiating any contact with an affected vendor, the following must be completed:

### 5.1A Legal Review (Mandatory)

**Never contact a vendor during a supply chain incident without legal review.**

Legal review must assess:

- **NDA and confidentiality obligations** — what can be shared with vendor and under what conditions
- **Contractual liability clauses** — does the vendor contract address breach of service or security incidents
- **Data processing agreements** — obligations regarding notification and data handling
- **Indemnification clauses** — who bears liability if vendor compromise caused organizational damage
- **Right to audit clauses** — does the organization have rights to vendor forensic data
- **Law enforcement implications** — will contacting vendor prematurely compromise a law enforcement investigation
- **Multi-party coordination** — if multiple organizations are affected, is coordinated disclosure preferable

**Legal review approval must be documented before any vendor contact is made.**

Reference: `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md`

### 5.1B Internal Coordination Requirements (Before Vendor Contact)

| Requirement                                    | Status Required | Owner              |
| ---------------------------------------------- | --------------- | ------------------ |
| Incident formally declared with severity assigned | Confirmed    | SOC Lead           |
| Minimum evidence preserved before contact      | Confirmed       | L2/L3              |
| Legal review completed and approval obtained   | Confirmed       | Legal Counsel      |
| CISO or IR Team Lead authorized to contact vendor | Confirmed    | CISO               |
| Designated vendor communication lead assigned  | Confirmed       | IR Team Lead       |
| Talking points and information sharing limits defined | Confirmed | IR Lead + Legal    |
| Vendor contact details verified (official channels only) | Confirmed | Vendor Mgmt     |

### 5.1C Information Sharing Limits (Define Before Contact)

Before the first vendor call, document exactly what can and cannot be shared:

**Information that may be shared (with legal approval):**

- Confirmation that organization is affected and investigation is in progress
- Specific affected versions identified in the environment
- Request for IoCs, forensic data, and remediation guidance
- General timeline of when the organization first observed indicators
- Technical questions about the product related to the investigation

**Information that must NOT be shared without explicit legal approval:**

- Detailed forensic findings from internal investigation
- Specific systems, architecture, or infrastructure details
- Number of affected systems or full scope
- Evidence of specific attacker TTPs beyond what vendor already knows
- Internal investigation status, timeline, or gaps
- Any information that could establish liability or shift blame
- Client or customer details (especially in MSSP context)

---

## 6. Vendor Contact Identification and Verification

### 6.1A Identifying the Correct Vendor Contact

Use official channels only — do not use contacts provided by unknown parties during an incident:

| Contact Type                      | Where to Find                                              | Priority  |
| --------------------------------- | ---------------------------------------------------------- | --------- |
| Vendor PSIRT / Security Team      | Vendor's official security page (e.g., vendor.com/security) | Highest  |
| Vendor dedicated incident hotline | Vendor support portal or contract appendix                 | High      |
| Account manager / TAM             | Internal vendor contact directory                          | Medium    |
| General vendor support            | Vendor support portal                                      | Low       |

Reference: `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Vendor-Contacts.md`

### 6.1B Contact Verification (Critical)

Before sharing any information with a claimed vendor contact:

- Verify the contact's identity through **official vendor portal or previously established contact details**
- Do NOT use phone numbers, email addresses, or contact details provided during the incident by the contacted party
- Verify email domain matches the official vendor domain
- For high-stakes communications, use **encrypted email (S/MIME or PGP)** if vendor supports it
- Document the verification method and outcome in the incident ticket

---

## 7. Vendor Communication Phases

### 7.1 Phase 1 — Initial Notification or First Contact

#### 7.1A When to Make First Contact

| Scenario                                              | When to Contact Vendor                                     |
| ----------------------------------------------------- | ---------------------------------------------------------- |
| Vendor has already published an advisory              | After legal review; to request IoCs and remediation guidance |
| Organization discovers vendor compromise before vendor | After legal review; consider responsible disclosure timing |
| Vendor notifies organization first                    | Verify authenticity; respond through official channels     |
| Government/CERT advisory about vendor                | After legal review; contact vendor for official guidance   |

#### 7.1B Initial Contact Objectives

The first contact with the vendor should accomplish:

- Confirm the organization is a customer using the affected product (without disclosing investigation details)
- Request official IoC list (file hashes, network destinations, process indicators)
- Request confirmation of affected version range
- Request estimated remediation (patch) timeline
- Request access to vendor's incident response updates (mailing list, portal, private briefings)
- Establish a dedicated point of contact and communication cadence

#### 7.1C Initial Contact Script (Template)

### Adapt the following for the specific vendor and situation:
---
Subject: Security Inquiry – [Product Name] – [Advisory Reference or Date] – Confidential

To: [Vendor PSIRT Email]

Dear [Vendor Security Team],

We are contacting you regarding [the reported security incident / advisory reference]
affecting [Product Name].

We are a customer using [Product Name] and are currently assessing potential impact
to our environment. We are requesting the following information to support our
internal assessment:

Complete list of affected product versions
Technical indicators of compromise (IoCs) including file hashes, network
destinations, and process indicators
Recommended immediate mitigation or workaround steps
Expected patch release timeline
Access to ongoing incident updates (private briefing or advisory channel)
Please treat this inquiry as confidential. We would appreciate a response
within [4 hours for P1 / 24 hours for P2].

Our designated point of contact for this matter is:
Name: [IR Team Lead Name]
Title: [Title]
Email: [Secure email]
Phone: [Direct number]

We look forward to your response.

[IR Team Lead Name]
[Organization Name]


---

### 7.2 Phase 2 — Active Investigation Coordination

#### 7.2A Information Requests from Vendor (Ongoing)

Maintain a running request log of all items requested from the vendor:

| Item Requested                          | Date Requested | Date Received | Received? | Notes                               |
| --------------------------------------- | -------------- | ------------- | --------- | ----------------------------------- |
| Complete IoC list (hashes, IPs, domains)|                |               | ☐         |                                     |
| Affected version list (complete)        |                |               | ☐         |                                     |
| Attack chain description                |                |               | ☐         |                                     |
| Forensic artifacts from vendor side     |                |               | ☐         |                                     |
| Clean version/patch release             |                |               | ☐         |                                     |
| Patch integrity verification information|                |               | ☐         |                                     |
| Vendor investigation timeline and status|                |               | ☐         |                                     |
| Vendor's own root cause analysis        |                |               | ☐         |                                     |
| Technical remediation guidance          |                |               | ☐         |                                     |
| Evidence of vendor's own containment    |                |               | ☐         |                                     |

#### 7.2B Evaluating Vendor-Provided IoCs

Do not blindly trust IoCs provided by the vendor — they may be incomplete, incorrect, or evolving:

- Cross-reference vendor IoCs against **independent threat intelligence sources** (VirusTotal, MISP, commercial TI)
- Validate network-based IoCs by searching historical logs **independently** of vendor advisory
- Compare vendor-provided file hashes against artifacts found in forensic investigation
- Treat vendor IoC list as **minimum scope** — assume additional IoCs may exist
- Track IoC updates from vendor and re-run searches when new IoCs are released

**Document IoC validation status:**

| IoC Value | Source (Vendor/TI) | Validated Independently? | Validation Method | Match Found in Org? | Evidence Reference |
| --------- | ------------------ | ------------------------ | ----------------- | ------------------- | ------------------ |
|           |                    |                          |                   |                     |                    |

#### 7.2C Communication Cadence During Active Investigation

Establish a regular communication cadence with vendor:

| Scenario                            | Recommended Cadence         | Method                          |
| ----------------------------------- | --------------------------- | ------------------------------- |
| P1 — Active compromise confirmed    | Every 4–6 hours             | Secure call + written summary   |
| P2 — Impact assessment in progress  | Every 12–24 hours           | Email or secure portal          |
| P3 — Monitoring phase               | Daily updates               | Email or vendor portal          |
| Patch released                      | Immediate notification      | Direct contact + written confirmation |
| New IoCs identified                 | Immediate notification      | Direct contact + written confirmation |

#### 7.2D Vendor Escalation (If Response is Inadequate)

If the vendor is not responding adequately or timely:

| Escalation Step | Action                                                       | When to Use                              |
| --------------- | ------------------------------------------------------------ | ---------------------------------------- |
| Step 1          | Escalate within vendor to CISO, VP Engineering, or CTO       | No response within SLA                  |
| Step 2          | Engage account manager or TAM for escalation within vendor   | Technical team unresponsive              |
| Step 3          | Engage through legal counsel — formal written notice         | Vendor not cooperating within 24 hours for P1 |
| Step 4          | Consider coordinating with other affected organizations for collective pressure | Multiple organizations affected |
| Step 5          | Engage government CERT or regulatory body for vendor pressure | Critical infrastructure risk            |

---

### 7.3 Phase 3 — Patch and Remediation Coordination

#### 7.3A Patch Receipt and Verification (Critical Process)

**Never apply a vendor-provided patch without independent verification.**

The patch itself may be:
- A new vector for further compromise if the vendor's distribution mechanism is still compromised
- Incomplete — not fully removing all malicious components
- Introducing new vulnerabilities or breaking existing security controls

**Patch verification steps:**

| Step | Action                                                       | Owner              | Output                          |
| ---- | ------------------------------------------------------------ | ------------------ | ------------------------------- |
| 1    | Obtain patch from **official vendor distribution channel** — not a link provided in email | Vendor Mgmt  | Patch file |
| 2    | Verify patch file hash against hash published by vendor on **official security advisory** | L3/IR Team  | Hash match confirmation |
| 3    | If vendor provides code signing, verify **digital signature** of patch | L3/IR Team        | Signature verification result   |
| 4    | Submit patch to **malware analysis** in isolated environment before deploying | L3/Malware Analysis | Clean/malicious verdict |
| 5    | Deploy patch to **isolated test environment first** and validate behavior | Platform/IR Team  | Test validation report          |
| 6    | Monitor test environment for **24–48 hours** for anomalous behavior post-patch | SOC/L2          | Post-patch monitoring report    |
| 7    | If patch validated clean — deploy to production in **staged rollout** starting with lowest-risk systems | Platform | Deployment log |
| 8    | Monitor production systems after each deployment stage       | SOC/L2             | Production monitoring report    |
| 9    | Document patch hash and deployment timeline in incident ticket | L2/IR Team        | Patch deployment record         |

#### 7.3B Patch Deployment Communication to Vendor

After deploying verified patch, notify vendor:

- Confirm deployment completion (without sharing architecture details)
- Request confirmation that patch fully addresses the supply chain compromise
- Request confirmation that vendor's own infrastructure is clean before re-enabling vendor access
- Request updated IoC list post-patch to ensure complete coverage

#### 7.3C Workaround Coordination (If No Patch Available)

If vendor cannot provide a patch immediately:

**Vendor workaround assessment:**

| Workaround Option | Effectiveness | Business Impact | Verification Method | Implementation Owner |
| ----------------- | ------------- | --------------- | ------------------- | -------------------- |
| Disable affected feature | High | Medium–High | Test functionality removed | App Owner |
| Network isolation of affected software | High | Medium | Verify no C2 possible | Network Team |
| Rollback to previous clean version | High | Low–Medium | Verify clean version hash | Platform Team |
| Manual IoC blocking (firewall/EDR) | Medium | Low | Verify IoC blocks applied | SOC/Network |
| Enhanced monitoring without containment | Low | Low | Monitoring active | SOC |

---

### 7.4 Phase 4 — Vendor Access Management During Incident

#### 7.4A Vendor Access Revocation Decision

During a confirmed or suspected supply chain incident, all vendor access to the organization's environment must be assessed:

| Access Type                        | Risk During Incident              | Recommended Action                            |
| ---------------------------------- | --------------------------------- | --------------------------------------------- |
| Vendor VPN access                  | Direct pivot into org environment | Revoke immediately if vendor compromise confirmed |
| Vendor remote support tools        | Remote command execution risk     | Revoke or disable until vendor is cleared     |
| Vendor API tokens/service accounts | Data access or lateral movement   | Rotate immediately; revoke if not needed      |
| Vendor-operated monitoring agents  | C2 vector; lateral movement       | Isolate from sensitive network segments       |
| Vendor access to cloud environment | IAM abuse; data access            | Revoke and audit all vendor IAM activity      |
| Vendor access to CI/CD pipelines   | Code injection risk               | Revoke immediately if pipeline compromised    |

#### 7.4B Vendor Access Re-enablement Criteria

Before re-enabling any vendor access after a supply chain incident:

| Criteria                                                     | Evidence Required                              |
| ------------------------------------------------------------ | ---------------------------------------------- |
| Vendor has confirmed their own environment is clean          | Written statement from vendor CISO             |
| Vendor has provided forensic evidence of their own clean state | Vendor investigation report or third-party forensic attestation |
| Patch verified clean and deployed to org environment         | Patch verification report                      |
| All vendor access credentials have been rotated              | IAM change log                                 |
| Monitoring is in place for all vendor access paths           | SOC monitoring confirmation                    |
| Legal review completed for re-engagement                     | Legal approval documented                      |
| CISO approval for re-enablement                             | Written CISO approval                          |

---

## 8. Vendor Communication Log (Mandatory Record)

All communications with the vendor during an incident must be logged:

| Date/Time (UTC) | Communication Type | Participants | Organization Side | Vendor Side | Topics Discussed | Information Shared | Information Received | Action Items | Log Reference |
| --------------- | ------------------ | ------------ | ----------------- | ----------- | ---------------- | ------------------ | -------------------- | ------------ | ------------- |
|                 |                    |              |                   |             |                  |                    |                      |              |               |

**Requirements for communication log:**

- Every call, email, and meeting must be logged
- Record **exact information shared** with vendor in each interaction
- Record **exact information received** from vendor in each interaction
- Note any **commitments made by vendor** with expected delivery dates
- Note any **refusals or delays** from vendor with reasons given
- This log is a **legal document** — treat with appropriate care and access control

---

## 9. Multi-Vendor Coordination (When Multiple Vendors Are Involved)

Some supply chain attacks involve multiple vendors (e.g., a compromised MSP using a compromised software tool). When multiple vendors are involved:

### 9.1A Multi-Vendor Coordination Principles

- Assign a **dedicated coordination lead** for each vendor relationship
- Maintain **separate communication logs** per vendor
- Do not share one vendor's information with another vendor without explicit legal approval
- Coordinate sequencing of vendor notifications with legal counsel
- Identify whether a **coordinating body** (government CERT, ISAC) should manage multi-vendor coordination

### 9.1B Multi-Vendor Coordination Matrix

| Vendor | Role in Incident | Contact Name | Contact Method | First Contacted (UTC) | Current Status | Patch/Remediation ETA | Legal Review Status |
| ------ | ---------------- | ------------ | -------------- | --------------------- | -------------- | --------------------- | ------------------- |
|        |                  |              |                |                       |                |                       |                     |

---

## 10. Industry and Government Coordination

### 10.1A When to Engage External Bodies

| Body                         | When to Engage                                              | Purpose                                    |
| ---------------------------- | ----------------------------------------------------------- | ------------------------------------------ |
| CERT-In                      | Significant supply chain incident with national security implications | Mandatory reporting; coordination support |
| RBI                          | BFSI sector supply chain incident affecting customer data   | Regulatory reporting and guidance          |
| NCSC / CISA (if applicable)  | Critical infrastructure supply chain incident               | Technical coordination and attribution     |
| ISAC (sector-specific)       | Industry-wide supply chain attack                           | Anonymous IoC sharing and peer coordination |
| Law Enforcement              | Criminal activity suspected; evidence of nation-state involvement | Formal investigation support           |

### 10.1B Anonymous IoC Sharing with Peers

When sharing IoCs with industry peers through ISACs or similar bodies:

- Anonymize all organizational identifiers before sharing
- Do not share internal architecture or system details
- Share only technical IoCs (hashes, IPs, domains, process indicators)
- Obtain legal approval before any external sharing
- Document all external sharing in the incident log

---

## 11. Post-Incident Vendor Risk Management

### 11.1A Vendor Security Assessment (Post-Incident Review)

After every supply chain incident, conduct a formal vendor security reassessment:

| Assessment Area                              | Assessment Method                                   | Frequency Post-Incident |
| -------------------------------------------- | --------------------------------------------------- | ----------------------- |
| Vendor security controls and certifications  | Request updated SOC 2 / ISO 27001 / penetration test results | Immediately post-incident |
| Vendor software development security practices | SSDLC questionnaire; code signing practices; SBOM capability | Within 30 days |
| Vendor incident response capability          | Review vendor IR plan; tabletop exercise coordination | Within 60 days     |
| Vendor supply chain security (their vendors) | Request vendor's third-party risk management program details | Within 60 days   |
| Vendor contractual security requirements     | Review and update contractual security clauses       | Within 90 days          |
| Vendor access and privilege review           | Review all access granted to vendor and apply least privilege | Within 30 days   |

### 11.1B Contractual Improvement Requirements

Review and update vendor contracts to include or strengthen:

**Security requirements to add or strengthen:**

- Mandatory notification timeline for security incidents (e.g., within 4 hours for critical)
- Right to audit vendor security controls and incident investigation
- Requirement for vendor to maintain and share SBOM for delivered software
- Requirement for code signing of all software updates
- Requirement for cryptographic integrity verification of updates
- Data breach liability and indemnification clauses
- Right to terminate contract without penalty following confirmed vendor-caused breach
- Requirement for vendor to maintain current security certifications (ISO 27001, SOC 2 Type II)
- Requirement for vendor's key personnel to have security background checks

### 11.1C Vendor Risk Register Update

After incident, update the vendor risk register:

| Vendor | Incident Date | Incident Type | Impact to Org | Vendor Response Quality | Contract Review Status | Continued Use Decision | Risk Level Updated |
| ------ | ------------- | ------------- | ------------- | ----------------------- | ---------------------- | ---------------------- | ------------------ |
|        |               |               |               |                         |                        |                        |                    |

---

## 12. MSSP Client Vendor Coordination Notes

When the organization is an MSSP and a vendor supply chain attack affects managed clients:

**Coordination challenges:**
- The MSSP may have a direct vendor relationship while clients have indirect exposure
- Client contracts may have specific requirements for vendor breach notification
- Different clients may have different risk tolerances for continued vendor use
- The MSSP must coordinate vendor communication **centrally** while keeping each client informed individually

**Client communication requirements:**
- Notify each affected client of the supply chain incident per their contract SLA
- Do not share one client's exposure details with another client
- Coordinate vendor patch deployment timing with each client's change management process
- Provide each client with an independent summary of vendor coordination activities
- Obtain each client's explicit approval before re-enabling vendor access to their environment

**Vendor access management:**
- If vendor access is revoked for the MSSP's management environment, assess whether client environments are separately accessed by vendor
- Revoke or restrict vendor access to each client environment independently based on that client's risk assessment
- Document all vendor access changes per client

Reference: `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md`

---

## 13. Vendor Communication Templates

### 13.1A Template: Request for IoCs and Technical Information
Subject: URGENT – Security Incident Coordination – [Product Name] – [Advisory Ref] – Confidential

To: [Vendor PSIRT / Security Team]

Dear [Vendor Security Team Name],

We are writing in connection with the reported security incident affecting [Product Name].
We are a customer and have initiated our internal incident response procedures.

To support our investigation, we urgently request the following:

TECHNICAL INFORMATION REQUIRED:

Complete list of all affected product versions and build numbers
Full indicator of compromise (IoC) list including:
File hashes (MD5, SHA1, SHA256) for all malicious components
Network destinations (IP addresses, domains, URLs) used by malicious components
Process names, file paths, and registry keys associated with malicious activity
Any additional behavioral indicators
Detailed description of the attack chain (how the malicious component operates)
Specific functionality of the malicious component (what data does it access/exfiltrate)
Recommended immediate mitigation steps pending patch availability
Confirmed patch release date and distribution method
Patch integrity verification information (expected hash of clean patch)
COMMUNICATION REQUIREMENTS:

Dedicated security point of contact for this incident
Access to private incident updates as investigation progresses
Estimated timeline for your own investigation completion
This matter is time-sensitive. We require an initial response within:

2 hours for critical/P1 classification
8 hours for high/P2 classification
All communications regarding this matter should be treated as confidential.

Our incident point of contact:
Name: [Name]
Title: [Title]
Direct: [Phone]
Secure Email: [Email]

Regards,
[IR Team Lead]
[Organization Name]


### 13.2A Template: Vendor Patch Request and Verification Inquiry
Subject: Patch Verification Request – [Product Name] – [Version] – Confidential

To: [Vendor PSIRT]

Dear [Vendor Security Team],

Following our coordination regarding the [Product Name] supply chain incident,
we understand a remediation patch has been released / is expected on [date].

Before deployment, we require the following for independent patch verification:

Official download URL from your verified distribution infrastructure
SHA-256 hash of the clean patch package
Digital signature details and certificate information for verification
Changelog confirming all malicious components addressed
Confirmation that your own build and distribution infrastructure is confirmed clean
Post-deployment validation steps to confirm successful remediation
Please provide the above information through our secure communication channel.

We will conduct independent patch verification before deployment. We will notify
you upon completion of deployment and request confirmation that the patch
fully addresses all aspects of the supply chain compromise.

Regards,
[IR Team Lead]
[Organization Name]


### 13.3A Template: Vendor Access Re-enablement Request
Subject: Vendor Access Re-enablement Request – [Organization Name] – Confidential

To: [Vendor Account Manager / PSIRT]

Dear [Vendor Contact],

As part of our incident response to the [Product Name] supply chain incident,
we temporarily suspended all vendor access to our environment on [date/time UTC].

Before re-enabling vendor access, we require written confirmation of the following:

Your internal investigation is complete and your environment is confirmed clean
The root cause of the supply chain compromise has been identified and remediated
All affected distribution and build infrastructure has been rebuilt or verified clean
New access credentials and authentication mechanisms are in place
Enhanced security monitoring is active on your side
Additionally, we will be implementing the following changes to vendor access:

[List specific access control changes]
[List additional monitoring to be applied]
Please provide written confirmation from your CISO or equivalent authority that
the above conditions are met before we proceed with re-enablement.

Regards,
[CISO / IR Team Lead]
[Organization Name]

## 14. Common Vendor Coordination Mistakes to Avoid

| Mistake                                               | Risk                                              | Correct Approach                                      |
| ----------------------------------------------------- | ------------------------------------------------- | ----------------------------------------------------- |
| Contacting vendor before legal review                 | Legal liability; contractual violation            | Always complete legal review first                    |
| Sharing internal forensic details with vendor         | Compromises investigation; legal exposure         | Share only what legal approves                        |
| Trusting vendor-provided contact details during incident | Contact may be attacker impersonating vendor   | Verify contacts against official pre-incident records |
| Applying vendor patch without verification            | Patch may be malicious or incomplete              | Always verify patch integrity independently           |
| Re-enabling vendor access without clearance criteria  | Attacker retains access through vendor pivot      | Use formal re-enablement criteria checklist           |
| Treating vendor as adversary unnecessarily            | Damages relationship; reduces cooperation         | Treat as partner while protecting investigation       |
| Not logging all vendor communications                 | No audit trail; legal exposure                    | Log every interaction with timestamps                 |
| Accepting vendor's scope assessment without verification | Vendor may understate impact              | Conduct independent investigation regardless          |
| Not reviewing vendor contract post-incident           | Same incident can recur; no accountability        | Always conduct contractual review after supply chain incident |
| Sharing one client's exposure with vendor on MSSP call | Client confidentiality breach                  | Separate client discussions; get client approval      |

---

## 15. Related Documents

| Document                         | Path                                                         |
| -------------------------------- | ------------------------------------------------------------ |
| Supply Chain Master              | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-Master.md` |
| Supply Chain L1 Triage           | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-L1-Triage.md` |
| Supply Chain L2 Investigation    | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-L2-Investigation.md` |
| Supply Chain L3 Forensics        | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-L3-Forensics.md` |
| Supply Chain MITRE Mapping       | `02_PLAYBOOKS/02.9_Supply-Chain-Attack/PB-SupplyChain-MITRE-Mapping.md` |
| Legal Counsel Engagement SOP     | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/Legal-Counsel-Engagement-SOP.md` |
| Vendor Contacts Directory        | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/Vendor-Contacts.md` |
| RBI Incident Reporting SOP       | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/RBI-Incident-Reporting-SOP.md` |
| CERT-In Reporting SOP            | `05_ESCALATION-AND-COMMUNICATION/05.3_Regulatory-Communication/CERT-In-Reporting-SOP.md` |
| MSSP Client Contacts             | `05_ESCALATION-AND-COMMUNICATION/05.4_Contact-Directory/MSSP-Client-Contacts.md` |
| Cross-Client Incident Procedure  | `09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Cross-Client-Incident-Procedure.md` |
| Evidence Collection SOP          | `06_EVIDENCE-AND-CHAIN-OF-CUSTODY/06.1_Evidence-Collection/Evidence-Collection-SOP.md` |
| Security Improvement Register    | `08_POST-INCIDENT/08.3_Improvement-Tracking/Security-Improvement-Register.xlsx` |
| TI IoC Handling SOP              | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-IoC-Handling-SOP.md` |

---

## 16. Revision History

| Version | Date        | Author                                  | Changes         |
| ------- | ----------- | --------------------------------------- | --------------- |
| 1.0     | 19-May-2026 | IR Team Lead / Vendor Management Lead   | Initial version |

---

## 17. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**