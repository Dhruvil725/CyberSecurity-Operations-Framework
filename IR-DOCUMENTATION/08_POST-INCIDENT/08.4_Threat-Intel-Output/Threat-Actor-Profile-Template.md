# Threat Actor Profile Template

---

# 1. Document Control

| Field          | Value                                            |
| -------------- | ------------------------------------------------ |
| Document Name  | Template – Threat Actor Profile                  |
| Document ID    | TI-TAP-001                                       |
| Version        | 1.0                                              |
| Effective Date | 30-May-2026                                      |
| Owner          | Threat Intel Lead / SOC Manager                  |
| Approved By    | CISO                                             |
| Classification | Internal – Confidential (TLP varies per profile) |
| Review Cycle   | Semi-Annually (or upon significant new intel)    |

---

# 2. Purpose

This template provides the standardized **Threat Actor Profile** format used to document, analyze, and operationalize intelligence about specific threat actors (APT groups, cybercriminal groups, hacktivists, insiders) relevant to the organization or MSSP clients.

A formal threat actor profile is critical because:

- understanding adversaries is foundational to NIST CSF Identify (ID.RA) and threat-informed defense
- ISO 27001 Annex A.5.7 requires threat intelligence as a control
- RBI Cyber Security Framework expects threat intelligence capability and adversary awareness
- profiles enable proactive defense (detection engineering, hunt hypotheses, controls prioritization)
- attribution analysis requires structured actor knowledge
- briefings to executive leadership and the board require actor-level intelligence
- MSSP clients in regulated industries expect threat-actor-specific reporting
- threat actor TTPs evolve; profiles must be living documents
- profiles inform tabletop exercises, red team scenarios, and purple team simulations
- audit trail required for threat intelligence program maturity

This template ensures:

- consistent structure across all threat actor profiles
- evidence-based attribution with confidence ratings
- MITRE ATT&CK alignment for TTPs
- linkage to IoCs, incidents, and intelligence reports
- TLP-classified content for appropriate sharing
- audit-ready evidence of threat intelligence capability
- support for strategic, operational, and tactical decision-making

Reference alignment:
`04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Platform-Usage-Guide.md`
`08_POST-INCIDENT/08.4_Threat-Intel-Output/IoC-Output-Register.md`
`08_POST-INCIDENT/08.4_Threat-Intel-Output/TTP-Intelligence-Report.md`

---

# 3. Scope

This template is used to profile:

| Actor Type                        | Examples                                             |
| --------------------------------- | ---------------------------------------------------- |
| **Nation-State / APT**            | APT28, APT29, Lazarus Group, APT41                   |
| **Cybercriminal Groups**          | FIN7, Conti, LockBit, Cl0p                           |
| **Ransomware Groups**             | BlackCat/ALPHV, Royal, Akira                         |
| **Hacktivists**                   | Anonymous, KillNet, named hacktivist groups          |
| **Initial Access Brokers (IABs)** | Named or unnamed brokers                             |
| **Insider Threats**               | Documented insider categories (malicious, negligent) |
| **Unknown/Emerging Actors**       | Newly observed actors pending attribution            |
| **Industry-Specific Threats**     | Actors targeting BFSI/Healthcare/Critical Infra      |
| **Geographic-Specific Threats**   | Actors targeting India/APAC/specific regions         |

Profile creation triggers:

| Trigger                  | Examples                                  |
| ------------------------ | ----------------------------------------- |
| Active campaign observed | Actor targeting organization or industry  |
| Incident attribution     | Actor identified during incident          |
| External intelligence    | CERT-In, vendor reports, ISAC alerts      |
| Strategic priority       | Board/CISO interest in specific actors    |
| Tabletop scenario        | Profile needed for exercise               |
| Compliance               | Regulatory expectation (e.g., RBI alerts) |

Out of scope:

- Generic threat narratives without specific actor attribution (use TTP Intelligence Report)
- Single-IoC entries (use IoC Output Register)
- Tactical incident-specific intel (use incident report)

---

# 4. Definitions

| Term              | Definition                                                                |
| ----------------- | ------------------------------------------------------------------------- |
| Threat Actor      | Individual, group, or organization conducting malicious cyber activity    |
| APT               | Advanced Persistent Threat – typically nation-state aligned               |
| Attribution       | Process of identifying the actor behind an attack                         |
| TTPs              | Tactics, Techniques, and Procedures (MITRE ATT&CK framework)              |
| Diamond Model     | Adversary, Capability, Infrastructure, Victim analysis framework          |
| Kill Chain        | Lockheed Martin Cyber Kill Chain (Reconnaissance → Actions on Objectives) |
| Pyramid of Pain   | Hierarchy of indicators (Hash → IP → Domain → Tools → TTPs)               |
| Confidence Level  | Analytical confidence in assessment (High/Medium/Low)                     |
| Aliases           | Alternative names used by different vendors/intel providers               |
| Operational Tempo | Frequency and intensity of actor activity                                 |
| Targeting         | Industries, geographies, organizations of interest to actor               |

---

# 5. Roles and Responsibilities

| Role                     | Responsibilities                                                |
| ------------------------ | --------------------------------------------------------------- |
| Threat Intel Lead        | Owns profile library; ensures quality; approves publication     |
| Threat Intel Analyst     | Creates and maintains profiles; conducts research               |
| L3 Analyst               | Provides forensic findings supporting attribution               |
| SOC Manager              | Approves strategic profiles; reviews quarterly                  |
| CISO                     | Reviews high-priority actor profiles; approves external sharing |
| Detection Engineer       | Operationalizes actor TTPs into detection rules                 |
| Red/Purple Team          | Uses profiles for adversary emulation                           |
| Tabletop Facilitator     | Uses profiles for exercise scenarios                            |
| Compliance Lead          | Validates regulatory-aligned actor coverage                     |
| MSSP SDM (if applicable) | Coordinates client-specific actor relevance                     |

---

# 6. Threat Actor Profile Principles (Mandatory)

| Principle        | Description                                                 |
| ---------------- | ----------------------------------------------------------- |
| Evidence-based   | All assertions must be supported by sources                 |
| Confidence-rated | Use analytical confidence (High/Medium/Low)                 |
| Sourced          | Every claim must cite source (open-source/closed-source)    |
| MITRE-aligned    | TTPs mapped to ATT&CK                                       |
| Diamond Model    | Use Diamond Model for attribution analysis                  |
| TLP-classified   | Profile content has TLP classification                      |
| Living document  | Updated as new intelligence emerges                         |
| Sanitization     | Sensitive sources/methods protected in shared versions      |
| Actionable       | Profile must inform defensive actions                       |
| Objective        | Avoid speculation; clearly distinguish assessment from fact |

---

# 7. Confidence Rating Definitions (Mandatory)

Use ICD-203 confidence language:

| Confidence            | Definition                                                                |
| --------------------- | ------------------------------------------------------------------------- |
| **High Confidence**   | Well-corroborated information from multiple sources; consistent over time |
| **Medium Confidence** | Credibly sourced and plausible; some information gaps                     |
| **Low Confidence**    | Limited sources; significant gaps; contradictory information              |

Use estimative language (per ICD-203):

| Probability                  | Language                       |
| ---------------------------- | ------------------------------ |
| Almost no chance (1–5%)      | Remote, highly unlikely        |
| Very unlikely (5–20%)        | Very unlikely                  |
| Unlikely (20–45%)            | Unlikely, probably not         |
| Roughly even chance (45–55%) | Roughly even chance            |
| Likely (55–80%)              | Likely, probably               |
| Very likely (80–95%)         | Very likely, highly likely     |
| Almost certain (95–99%)      | Almost certain, nearly certain |

---

# 8. Threat Actor Profile Template (Copy/Paste)

## 8.1 Profile Metadata (Mandatory)

| Field                     | Value                                      |
| ------------------------- | ------------------------------------------ |
| Profile ID                | `TAP-YYYY-####`                            |
| Profile Name              | Primary actor name (e.g., APT29)           |
| Aliases                   | Comma-separated list of known aliases      |
| Profile Version           | v1.0 / v1.1 / etc.                         |
| Date Created (UTC)        |                                            |
| Last Updated (UTC)        |                                            |
| Next Review Date (UTC)    |                                            |
| Author / Analyst          |                                            |
| Reviewed By               |                                            |
| Approved By               |                                            |
| TLP Classification        | RED / AMBER+STRICT / AMBER / GREEN / CLEAR |
| Distribution              | Internal SOC / MSSP / Client / External    |
| Client/Tenant (MSSP only) | Client ID / Name (if client-specific)      |

---

## 8.2 Executive Summary (Mandatory)

> Provide a 3–5 sentence summary suitable for executive consumption.

**Summary:**

`[Brief actor description, primary targeting, key TTPs, relevance to organization]`

**Relevance to Organization:**

| Aspect                  | Assessment                             |
| ----------------------- | -------------------------------------- |
| Industry Targeting      | Direct / Indirect / Adjacent / None    |
| Geographic Targeting    | Direct / Indirect / None               |
| Likelihood of Targeting | High / Medium / Low                    |
| Potential Impact        | Critical / High / Medium / Low         |
| Recommended Posture     | Active Defense / Vigilance / Awareness |

---

## 8.3 Actor Identification (Mandatory)

### 8.3.1 Names and Aliases

| Source                                   | Name/Alias |
| ---------------------------------------- | ---------- |
| MITRE ATT&CK                             |            |
| CrowdStrike                              |            |
| Mandiant / FireEye                       |            |
| Microsoft (Threat Actor Naming Taxonomy) |            |
| Kaspersky                                |            |
| Talos / Cisco                            |            |
| ESET                                     |            |
| Trend Micro                              |            |
| Recorded Future                          |            |
| Government (e.g., CISA, NCSC)            |            |
| Internal Designation (if any)            |            |

### 8.3.2 Actor Type and Motivation

| Field                          | Value                                                         | Confidence |
| ------------------------------ | ------------------------------------------------------------- | ---------- |
| Actor Type                     | Nation-state / Cybercriminal / Hacktivist / Insider / Unknown |            |
| Primary Motivation             | Espionage / Financial / Disruption / Hacktivism / Mixed       |            |
| Secondary Motivation           |                                                               |            |
| Suspected Affiliation          | Country/Region (if attributed)                                |            |
| Estimated First Observed (UTC) |                                                               |            |
| Operational Status             | Active / Dormant / Disrupted / Defunct                        |            |
| Operational Tempo              | High / Medium / Low                                           |            |

---

## 8.4 Attribution Analysis (Mandatory)

### 8.4.1 Diamond Model Analysis

```
            ADVERSARY
        [Actor: APT##]
              |
              |
   CAPABILITY ─┼─ INFRASTRUCTURE
   [Tools,   ]    [C2, Domains,
    Malware]      Servers]
              |
              |
            VICTIM
       [Targets, Industries]
```

| Diamond Vertex     | Details                                                 |
| ------------------ | ------------------------------------------------------- |
| **Adversary**      | Actor identity, suspected affiliation, motivation       |
| **Capability**     | Malware families, exploit kits, custom tooling          |
| **Infrastructure** | C2 servers, domains, hosting providers, ASNs            |
| **Victim**         | Industries, geographies, organization profiles targeted |

### 8.4.2 Attribution Confidence

| Attribution Claim             | Confidence | Supporting Evidence |
| ----------------------------- | ---------- | ------------------- |
| Actor identity                |            |                     |
| Nation-state affiliation      |            |                     |
| Specific campaign attribution |            |                     |
| Motivation                    |            |                     |

---

## 8.5 Targeting Analysis (Mandatory)

### 8.5.1 Industry Targeting

| Industry                  | Confirmed / Suspected | Examples |
| ------------------------- | --------------------- | -------- |
| Financial Services / BFSI |                       |          |
| Government                |                       |          |
| Healthcare                |                       |          |
| Energy / Utilities        |                       |          |
| Telecommunications        |                       |          |
| Defense / Aerospace       |                       |          |
| Technology                |                       |          |
| Manufacturing             |                       |          |
| Retail / E-commerce       |                       |          |
| Critical Infrastructure   |                       |          |
| Other                     |                       |          |

### 8.5.2 Geographic Targeting

| Region        | Confirmed / Suspected | Notes |
| ------------- | --------------------- | ----- |
| North America |                       |       |
| Europe        |                       |       |
| Asia-Pacific  |                       |       |
| India         |                       |       |
| Middle East   |                       |       |
| Latin America |                       |       |
| Africa        |                       |       |

### 8.5.3 Target Organization Profile

| Attribute                | Typical Target                                |
| ------------------------ | --------------------------------------------- |
| Organization size        | Large enterprise / SMB / Government           |
| Revenue range            |                                               |
| Strategic value          | Data type / IP / Financial / Disruption value |
| Notable victims (public) |                                               |

---

## 8.6 TTPs (Tactics, Techniques, Procedures) – MITRE ATT&CK Mapping (Mandatory)

### 8.6.1 ATT&CK Tactic Coverage

| Tactic                        | Techniques Used | Notes |
| ----------------------------- | --------------- | ----- |
| Reconnaissance (TA0043)       |                 |       |
| Resource Development (TA0042) |                 |       |
| Initial Access (TA0001)       |                 |       |
| Execution (TA0002)            |                 |       |
| Persistence (TA0003)          |                 |       |
| Privilege Escalation (TA0004) |                 |       |
| Defense Evasion (TA0005)      |                 |       |
| Credential Access (TA0006)    |                 |       |
| Discovery (TA0007)            |                 |       |
| Lateral Movement (TA0008)     |                 |       |
| Collection (TA0009)           |                 |       |
| Command and Control (TA0011)  |                 |       |
| Exfiltration (TA0010)         |                 |       |
| Impact (TA0040)               |                 |       |

### 8.6.2 Detailed Technique Inventory

| Technique ID | Technique Name | Sub-Technique | Description (Actor's Usage) | Confidence |
| ------------ | -------------- | ------------- | --------------------------- | ---------- |
| T####        |                |               |                             | High       |
| T####        |                |               |                             | Medium     |
| T####        |                |               |                             | High       |

### 8.6.3 Notable Procedures

> Document specific procedures observed (more granular than techniques).

| Procedure | Description | Detection Opportunity |
| --------- | ----------- | --------------------- |
|           |             |                       |

---

## 8.7 Capabilities (Tools, Malware, Exploits) – Mandatory

### 8.7.1 Malware Families

| Malware Name | Type                                                   | Description | First Observed | Notes |
| ------------ | ------------------------------------------------------ | ----------- | -------------- | ----- |
|              | RAT / Ransomware / Loader / Wiper / Backdoor / Stealer |             |                |       |

### 8.7.2 Exploit Kits / Vulnerabilities Exploited

| CVE / Vulnerability | Affected Product | Notes |
| ------------------- | ---------------- | ----- |
|                     |                  |       |

### 8.7.3 Custom Tools

| Tool Name | Function | Description |
| --------- | -------- | ----------- |
|           |          |             |

### 8.7.4 Living-Off-the-Land Binaries (LOLBins)

| Binary | Usage | Detection Approach |
| ------ | ----- | ------------------ |
|        |       |                    |

### 8.7.5 Open-Source Tools (Cobalt Strike, Metasploit, etc.)

| Tool | Usage | Notes |
| ---- | ----- | ----- |
|      |       |       |

---

## 8.8 Infrastructure (C2, Hosting, Domains) – Mandatory

### 8.8.1 C2 Infrastructure Patterns

| Aspect                       | Pattern                       |
| ---------------------------- | ----------------------------- |
| C2 communication protocol    | HTTPS / DNS / Custom          |
| C2 domain patterns           | DGA / Typosquat / Compromised |
| Hosting providers preferred  |                               |
| Geographic concentration     |                               |
| Bullet-proof hosting usage   |                               |
| Fast-flux / Domain shadowing |                               |

### 8.8.2 Known Infrastructure (Reference IoC Register)

| Infrastructure Type       | Reference       | TLP |
| ------------------------- | --------------- | --- |
| Active C2 IPs             | `IOC-YYYY-####` |     |
| Active C2 Domains         | `IOC-YYYY-####` |     |
| Historical infrastructure | `IOC-YYYY-####` |     |

Reference:
`08_POST-INCIDENT/08.4_Threat-Intel-Output/IoC-Output-Register.md`

---

## 8.9 Notable Campaigns (Mandatory)

| Campaign Name | Date Range | Target | Outcome | Source |
| ------------- | ---------- | ------ | ------- | ------ |
|               |            |        |         |        |

---

## 8.10 Observed Activity Against Organization (Mandatory if Applicable)

| Date | Incident ID | Activity Type                           | Outcome | Notes |
| ---- | ----------- | --------------------------------------- | ------- | ----- |
|      | INC-####    | Targeting / Compromise / Reconnaissance |         |       |

---

## 8.11 Defensive Recommendations (Mandatory)

### 8.11.1 Detection Recommendations

| Detection Area | Recommendation | Tool          | Priority         |
| -------------- | -------------- | ------------- | ---------------- |
| Network        |                | SIEM / NDR    | High / Med / Low |
| Endpoint       |                | EDR           |                  |
| Email          |                | Email Gateway |                  |
| Identity       |                | UEBA / IAM    |                  |
| Cloud          |                | CSPM / CWPP   |                  |

### 8.11.2 Preventive Recommendations

| Control Area         | Recommendation | Priority |
| -------------------- | -------------- | -------- |
| Patching             |                |          |
| MFA                  |                |          |
| Network Segmentation |                |          |
| Email Filtering      |                |          |
| Endpoint Hardening   |                |          |
| User Awareness       |                |          |

### 8.11.3 Hunt Hypotheses

| Hunt Hypothesis | Data Sources | MITRE Technique |
| --------------- | ------------ | --------------- |
|                 |              | T####           |

Reference:
`03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Threat-Hunting-Procedures.md`

### 8.11.4 Tabletop / Red Team Scenarios

| Scenario | Purpose                                | Reference                       |
| -------- | -------------------------------------- | ------------------------------- |
|          | Detection validation / Process testing | `10_TRAINING-AND-EXERCISES/...` |

---

## 8.12 Recent Activity and Trends (Mandatory)

### 8.12.1 Recent Operations (Last 6 Months)

| Date | Activity | Target | Source |
| ---- | -------- | ------ | ------ |
|      |          |        |        |

### 8.12.2 Trend Analysis

- **Operational tempo change:** `Increasing / Stable / Decreasing`
- **TTP evolution:** `New techniques adopted, old techniques abandoned`
- **Target shift:** `New industries/geographies of interest`
- **Tooling changes:** `New malware, retired tools`
- **Public exposure:** `Recent vendor reports, government attribution`

---

## 8.13 Source Material (Mandatory)

### 8.13.1 Internal Sources

| Source                    | Reference | Date | Confidence |
| ------------------------- | --------- | ---- | ---------- |
| Internal incident         |           |      |            |
| Internal hunt             |           |      |            |
| Internal malware analysis |           |      |            |

### 8.13.2 External Sources (Open-Source)

| Source                             | URL / Reference | Date | Confidence |
| ---------------------------------- | --------------- | ---- | ---------- |
| Vendor report (CrowdStrike)        |                 |      |            |
| Vendor report (Mandiant)           |                 |      |            |
| Microsoft Threat Intel             |                 |      |            |
| MITRE ATT&CK                       |                 |      |            |
| Government advisory (CISA/CERT-In) |                 |      |            |
| Academic research                  |                 |      |            |
| News articles                      |                 |      |            |
| Conference presentations           |                 |      |            |

### 8.13.3 External Sources (Closed-Source / Subscription)

| Source             | Reference | TLP | Confidence |
| ------------------ | --------- | --- | ---------- |
| Commercial TI feed |           |     |            |
| ISAC sharing       |           |     |            |
| Trusted partner    |           |     |            |

---

## 8.14 Intelligence Gaps and Outstanding Questions

| Gap / Question | Priority         | Collection Plan |
| -------------- | ---------------- | --------------- |
|                | High / Med / Low |                 |

---

## 8.15 Related Profiles

| Related Actor | Relationship                                     | Reference     |
| ------------- | ------------------------------------------------ | ------------- |
|               | Sub-group / Affiliate / Successor / Tool-sharing | TAP-YYYY-#### |

---

## 8.16 Linked Intelligence Products

| Product                  | Reference        |
| ------------------------ | ---------------- |
| IoC Sets                 | `IOC-YYYY-####`  |
| TTP Intelligence Reports | `TTP-YYYY-####`  |
| Incident Reports         | `INC-YYYY-####`  |
| Hunt Reports             | `HUNT-YYYY-####` |
| Malware Analysis Reports | `MA-YYYY-####`   |

---

# 9. Visual Reference – Pyramid of Pain (Standard Reference)

When operationalizing actor intelligence, focus on higher-pain indicators:

```
                  ▲
                 ╱ ╲           ← Hardest for actor to change
                ╱TTP╲          ← MAXIMUM PAIN (focus here)
               ╱─────╲
              ╱ TOOLS ╲
             ╱─────────╲
            ╱ARTIFACTS  ╲
           ╱─────────────╲
          ╱  DOMAINS      ╲
         ╱─────────────────╲
        ╱   IP ADDRESSES    ╲
       ╱─────────────────────╲
      ╱      HASH VALUES      ╲
     ─────────────────────────── ← Easiest for actor to change
```

Detection rules and hunts should prioritize:

1. TTPs (behaviors) – highest value
2. Tools – high value
3. Artifacts (registry keys, named pipes) – medium value
4. Domains – medium value
5. IPs – low value (frequently rotated)
6. Hashes – low value (trivially changed)

---

# 10. Profile Lifecycle (Mandatory)

| Phase           | Activities                             | Owner                | Frequency     |
| --------------- | -------------------------------------- | -------------------- | ------------- |
| **Creation**    | New actor identified, profile drafted  | Threat Intel Analyst | On trigger    |
| **Validation**  | Sources verified, attribution assessed | Threat Intel Lead    | At creation   |
| **Approval**    | TLP, distribution approved             | SOC Manager / CISO   | At creation   |
| **Publication** | Profile shared per TLP                 | Threat Intel Lead    | At creation   |
| **Monitoring**  | Active monitoring for new activity     | Threat Intel Analyst | Continuous    |
| **Update**      | New intel incorporated                 | Threat Intel Analyst | As needed     |
| **Review**      | Periodic full review                   | Threat Intel Lead    | Semi-annually |
| **Archival**    | Profile archived if actor defunct      | Threat Intel Lead    | As applicable |

---

# 11. Distribution and Sharing (Mandatory)

## 11.1 Internal Distribution

| Audience               | Format                         | Frequency                 |
| ---------------------- | ------------------------------ | ------------------------- |
| SOC L2/L3              | Full profile                   | At creation + on update   |
| Detection Engineering  | Full profile + TTP highlights  | At creation + on update   |
| Threat Hunters         | Full profile + hunt hypotheses | At creation + on update   |
| Incident Response Team | Full profile                   | At creation + on incident |
| Management             | Executive summary              | Quarterly briefing        |
| CISO / Board           | Strategic summary              | Quarterly briefing        |

## 11.2 External Distribution (per TLP)

| Recipient                | TLP Limit   | Format        | Approval           |
| ------------------------ | ----------- | ------------- | ------------------ |
| MSSP Clients (relevant)  | AMBER       | Sanitized PDF | SOC Manager        |
| ISACs                    | GREEN/AMBER | STIX/MISP     | SOC Manager        |
| CERT-In                  | GREEN       | PDF/Email     | SOC Manager + CISO |
| Trusted Partners         | AMBER       | PDF           | SOC Manager        |
| Public (blog/whitepaper) | CLEAR       | Markdown/PDF  | CISO               |

---

# 12. Quality Checklist (Per Profile)

Before publishing a profile:

- [ ] Metadata complete (ID, version, dates, author, TLP)
- [ ] Executive summary written (3–5 sentences)
- [ ] Relevance to organization assessed
- [ ] All known aliases documented
- [ ] Actor type and motivation assessed with confidence
- [ ] Diamond Model analysis completed
- [ ] Targeting (industry/geo) documented
- [ ] MITRE ATT&CK tactic coverage mapped
- [ ] Detailed technique inventory completed
- [ ] Capabilities (malware/tools/exploits) inventoried
- [ ] Infrastructure patterns documented
- [ ] Notable campaigns listed
- [ ] Observed activity against org documented (if any)
- [ ] Defensive recommendations provided (detection/prevention/hunt)
- [ ] Recent activity and trends summarized
- [ ] Source material cited with confidence
- [ ] Intelligence gaps documented
- [ ] Related profiles linked
- [ ] Linked intelligence products referenced
- [ ] Confidence ratings applied throughout
- [ ] TLP classification assigned
- [ ] Reviewed by Threat Intel Lead
- [ ] Approved per distribution requirements
- [ ] MSSP: tenant scoping verified (if applicable)

---

# 13. Review Process (Mandatory)

## 13.1 Continuous Monitoring

Threat Intel Analyst:

- Monitors open-source intelligence on profiled actors
- Tracks vendor reports and government advisories
- Identifies new TTPs, malware, infrastructure
- Updates profile as significant new intel emerges

## 13.2 Semi-Annual Review

Threat Intel Lead reviews each profile:

- TTPs current with MITRE ATT&CK latest
- Infrastructure references valid
- Recent activity section updated
- Confidence ratings still valid
- Defensive recommendations still relevant
- Source material current

## 13.3 Quarterly Strategic Review

CISO + Threat Intel Lead review:

- Top 5–10 actors most relevant to organization
- Coverage gaps (industries/geographies/actors)
- Detection coverage against actor TTPs
- Hunt program alignment with actor TTPs
- Tabletop/red team scenario alignment

---

# 14. MSSP Considerations (If Applicable)

For MSSP-managed clients:

- Master profiles maintained at MSSP level
- Client-specific relevance assessments per profile
- Client-tailored versions sanitized of MSSP-confidential sources
- Each client receives **relevant actor profiles** based on industry/geo
- Client-confidential observed activity stays in tenant-scoped profile
- Cross-client TTP observations sanitized before inclusion in master profile
- Client briefings on top actors per their industry
- Joint hunt programs informed by profiles
- Tabletop scenarios using client-relevant actors

References:
`09_MSSP-SPECIFIC/09.3_Multi-Tenant-Procedures/Client-Data-Segregation-Policy.md`
`07_REPORTING/07.3_MSSP-Client-Reports/MSSP-Executive-Briefing-Template.md`

---

# 15. Integration with Other Processes

| Process               | Integration Point                         |
| --------------------- | ----------------------------------------- |
| IoC Management        | Profile references actor IoCs             |
| Detection Engineering | Profile TTPs feed detection rules         |
| Threat Hunting        | Profile hypotheses feed hunts             |
| Incident Response     | Profile used during attribution analysis  |
| Red/Purple Team       | Profiles inform adversary emulation       |
| Tabletop Exercises    | Profiles drive realistic scenarios        |
| Executive Briefings   | Profiles support strategic communications |
| Compliance            | Actor coverage demonstrates TI maturity   |
| Risk Assessment       | Actor relevance informs risk scoring      |

---

# 16. Common Pitfalls to Avoid

| Pitfall                     | Mitigation                                      |
| --------------------------- | ----------------------------------------------- |
| Speculation as fact         | Use confidence language; cite sources           |
| Single-source attribution   | Require multi-source corroboration              |
| Outdated profiles           | Semi-annual review mandatory                    |
| Vendor-name confusion       | Document all aliases                            |
| Over-classification         | Use TLP appropriately; avoid TLP:RED by default |
| Under-classification        | Sensitive sources/methods must be protected     |
| No actionable output        | Always include detection/hunt recommendations   |
| MITRE drift                 | Re-map to latest ATT&CK version annually        |
| Forgotten profiles          | Maintain active profile list with review dates  |
| Cross-tenant leakage (MSSP) | Strict tenant scoping                           |

---

# 17. Related Documents

| Document                         | Path                                                                            |
| -------------------------------- | ------------------------------------------------------------------------------- |
| IoC Output Register              | `08_POST-INCIDENT/08.4_Threat-Intel-Output/IoC-Output-Register.md`              |
| TTP Intelligence Report          | `08_POST-INCIDENT/08.4_Threat-Intel-Output/TTP-Intelligence-Report.md`          |
| TI Feed Management               | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Feed-Management.md`        |
| TI Platform Usage Guide          | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Platform-Usage-Guide.md`   |
| TI Reporting Template            | `04_TOOLS-AND-TECHNOLOGY/04.4_Threat-Intelligence/TI-Reporting-Template.md`     |
| L3 Threat Intel Integration      | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Threat-Intel-Integration.md`      |
| L3 Attribution Analysis          | `03_SOC-TIER-PROCEDURES/03.3_L3-Procedures/L3-Attribution-Analysis.md`          |
| L2 Threat Hunting Procedures     | `03_SOC-TIER-PROCEDURES/03.2_L2-Procedures/L2-Threat-Hunting-Procedures.md`     |
| APT Playbook (Master)            | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-Master.md`                              |
| APT Attribution Analysis         | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-Attribution-Analysis.md`                |
| APT Threat Intel Integration     | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-ThreatIntel-Integration.md`             |
| MITRE ATT&CK Quick Reference     | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/MITRE-ATT&CK-Quick-Reference.md` |
| Attack Technique Reference       | `10_TRAINING-AND-EXERCISES/10.4_Knowledge-Base/Attack-Technique-Reference.md`   |
| Detection Improvement Log        | `08_POST-INCIDENT/08.3_Improvement-Tracking/Detection-Improvement-Log.md`       |
| Purple Team Exercise Guide       | `10_TRAINING-AND-EXERCISES/10.3_Drills/Purple-Team-Exercise-Guide.md`           |
| MSSP Executive Briefing Template | `07_REPORTING/07.3_MSSP-Client-Reports/MSSP-Executive-Briefing-Template.md`     |

---

# 18. Revision History

| Version | Date        | Author                          | Changes         |
| ------- | ----------- | ------------------------------- | --------------- |
| 1.0     | 30-May-2026 | Threat Intel Lead / SOC Manager | Initial version |

---

# 19. Approval

Approved by:

Name: ____________________
Title: ____________________
Date: ____________________

---

**End of Document**
