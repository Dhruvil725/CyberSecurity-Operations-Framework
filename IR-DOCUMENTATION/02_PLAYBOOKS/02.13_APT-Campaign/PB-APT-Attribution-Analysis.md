# Playbook: APT Campaign – Attribution Analysis

---

## 1. Document Control

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Document Name  | Playbook – APT Campaign (Attribution Analysis)               |
| Document ID    | IR-PB-APT-005                                                |
| Version        | 1.0                                                          |
| Effective Date | 21-May-2026                                                  |
| Owner          | Threat Intelligence Lead / IR Team Lead                      |
| Approved By    | CISO                                                         |
| Classification | Internal – Confidential                                      |
| Review Cycle   | Quarterly and after any confirmed APT investigation          |

---

## 2. Purpose

This document defines the structured methodology for performing attribution analysis during Advanced Persistent Threat (APT) investigations.

Attribution analysis is the process of evaluating whether observed attacker behavior can be reasonably associated with a known threat actor, campaign, criminal group, or nation-state operation.

APT attribution is inherently complex because attackers frequently:

- Reuse public tools
- Mimic other threat actors
- Use compromised infrastructure
- Operate through multiple proxy layers
- Purchase third-party malware kits
- Intentionally plant misleading artifacts (false flags)

Because of this, attribution must always be:

- Evidence-based
- Confidence-rated
- Technically defensible
- Reviewed by multiple analysts
- Clearly separated from assumptions or speculation

This playbook establishes:

- Attribution methodology
- Confidence scoring framework
- Evidence categories
- Infrastructure correlation procedures
- TTP-based actor mapping
- False-flag assessment
- Reporting standards
- Legal and executive communication guidance

---

## 3. Scope

Applies to attribution analysis involving:

- Nation-state APT groups
- Financially motivated advanced actors
- Organized cybercrime groups
- Long-term intrusion campaigns
- Supply chain campaigns
- Multi-stage espionage operations
- Hybrid cloud/on-prem campaigns
- MSSP cross-client investigations

---

## 4. Attribution Principles (IMPORTANT)

### 4.1 Attribution Is Probabilistic, Not Absolute

Attribution should never be stated as absolute fact unless supported by:

- Multiple corroborating evidence categories
- Strong infrastructure overlap
- Malware code lineage
- Consistent TTP patterns
- Reliable intelligence source validation

---

### 4.2 Technical Evidence Takes Priority

The following are stronger attribution indicators:

- Malware code similarity
- Infrastructure reuse
- Encryption routines
- Compile-time patterns
- Unique TTP combinations
- Persistence mechanisms
- Tooling overlap

The following are weak indicators alone:

- IP geolocation
- Language artifacts
- Timezone alone
- Public rumors
- Single malware family overlap

---

### 4.3 False Flag Awareness

APT actors may intentionally:

- Use another actor’s malware
- Reuse known public infrastructure
- Insert misleading language artifacts
- Mimic another group’s TTPs

All attribution assessments must include false-flag evaluation.

---

## 5. Attribution Workflow

| Phase | Objective | Owner |
|-------|-----------|-------|
| Phase 1 | Collect attribution evidence | L3 / TI |
| Phase 2 | Correlate infrastructure | TI Team |
| Phase 3 | Compare malware/tooling | Malware Analyst |
| Phase 4 | Compare ATT&CK TTP patterns | TI Analyst |
| Phase 5 | Evaluate targeting patterns | TI Lead |
| Phase 6 | Assess false-flag indicators | TI + IR |
| Phase 7 | Assign confidence level | TI Lead |
| Phase 8 | Produce attribution report | TI Team |

---

# 6. Phase 1 – Attribution Evidence Collection

APT attribution requires collection of multiple evidence categories.

---

## 6.1 Required Evidence Categories

| Evidence Type | Examples |
|---------------|----------|
| Infrastructure | IPs, domains, hosting providers |
| Malware | Hashes, loaders, implants |
| Network Patterns | JA3, beacon intervals |
| TTPs | MITRE ATT&CK mapping |
| Persistence | Services, tasks, registry |
| Authentication | Credential use patterns |
| Cloud Activity | API behavior |
| Language Artifacts | Error strings, comments |

---

## 6.2 Attribution Evidence Table

| Evidence | Source | Related Actor? | Confidence |
|----------|--------|----------------|-----------|
|          |        |                |           |

---

# 7. Phase 2 – Infrastructure Correlation (CRITICAL)

APT actors often reuse infrastructure patterns across campaigns.

---

## 7.1 Infrastructure Correlation Activities

- Identify ASN overlap
- Compare hosting providers
- Compare TLS certificates
- Review passive DNS history
- Review registrar overlap
- Analyze domain naming conventions
- Compare WHOIS registration patterns
- Identify IP reuse across campaigns

---

## 7.2 Infrastructure Reuse Indicators

| Indicator | Significance |
|-----------|-------------|
| Reused certificate fingerprint | Strong |
| Same registrar and naming scheme | Medium |
| Same VPS provider only | Weak |
| Shared ASN | Weak/Medium |
| Same domain pattern structure | Medium |

---

## 7.3 Infrastructure Mapping Table

| Indicator | Historical Match | Associated Actor | Confidence |
|-----------|-----------------|-----------------|-----------|
|           |                 |                 |           |

---

# 8. Phase 3 – Malware and Tooling Analysis

APT groups often reuse or modify tooling.

---

## 8.1 Malware Comparison Areas

| Category | Example |
|----------|---------|
| Encryption routines | Custom XOR/AES usage |
| Beacon intervals | Consistent timing |
| Persistence style | Same scheduled task naming |
| Compiler artifacts | PDB paths |
| Network protocol structure | Same packet formatting |
| Mutex naming | Shared patterns |
| Service names | Operational consistency |

---

## 8.2 Tooling Correlation Matrix

| Malware/Tool | Known Actor Usage | Match Confidence |
|--------------|------------------|-----------------|
|              |                  |                 |

---

## 8.3 Public Tool Caveat (IMPORTANT)

Many APT actors use:

- Cobalt Strike
- Mimikatz
- Sliver
- Metasploit
- PsExec

These tools alone are NOT sufficient for attribution.

Attribution requires:
- Customization overlap
- Operational patterns
- Infrastructure correlation
- TTP consistency

---

# 9. Phase 4 – TTP Correlation (IMPORTANT)

MITRE ATT&CK mapping is central to attribution.

---

## 9.1 TTP Correlation Objectives

Compare:

- Initial access methods
- Lateral movement style
- Persistence techniques
- Defense evasion patterns
- Exfiltration methods
- C2 protocol usage
- Operational timing

---

## 9.2 ATT&CK Correlation Table

| Technique | Observed? | Known Actor Usage | Confidence |
|-----------|-----------|------------------|------------|
|           |           |                  |            |

Reference:
`PB-APT-MITRE-Mapping.md`

---

## 9.3 Behavioral Consistency Indicators

Strong indicators:

- Same sequence of TTPs
- Same operational cadence
- Same exfiltration pattern
- Same persistence naming convention
- Same anti-forensic behavior

Weak indicators:

- Single ATT&CK overlap
- Generic phishing behavior
- Generic PowerShell usage

---

# 10. Phase 5 – Targeting Analysis

APT campaigns often target specific industries or geographies.

---

## 10.1 Targeting Factors

| Factor | Example |
|--------|---------|
| Industry targeting | BFSI, telecom, government |
| Geographic targeting | Specific region focus |
| Technology targeting | Specific vendor stack |
| Political timing | Elections, sanctions |
| Financial timing | Earnings reports |

---

## 10.2 Campaign Alignment Questions

| Question | Assessment |
|----------|------------|
| Does targeting match known actor interests? | |
| Does timing align with known campaigns? | |
| Does victim profile align historically? | |
| Does malware overlap with previous victimology? | |

---

# 11. Phase 6 – False Flag Assessment (CRITICAL)

False flags are common in advanced campaigns.

---

## 11.1 False Flag Indicators

| Indicator | Meaning |
|-----------|---------|
| Sudden language artifact insertion | Deliberate deception |
| Public malware reused unchanged | Misleading overlap |
| TTP inconsistency | Possible mimicry |
| Infrastructure mismatch | Operational inconsistency |
| Compile timezone mismatch | Potential manipulation |

---

## 11.2 False Flag Evaluation Questions

- Does malware sophistication match claimed actor?
- Are operational patterns consistent?
- Is infrastructure professionally managed?
- Is tooling reused naturally or artificially?
- Are overlaps superficial or deep?

---

# 12. Attribution Confidence Model

---

## 12.1 Confidence Levels

| Confidence | Meaning |
|------------|--------|
| Low | Limited overlap or circumstantial evidence |
| Medium | Multiple corroborating indicators |
| High | Strong infrastructure, malware, and TTP overlap |

---

## 12.2 Confidence Requirements

### Low Confidence
- One or two weak overlaps
- Limited infrastructure match
- Generic malware overlap

### Medium Confidence
- Multiple TTP correlations
- Infrastructure overlap
- Historical targeting consistency

### High Confidence
- Strong malware lineage
- Infrastructure reuse
- Consistent operational behavior
- Reliable TI corroboration

---

# 13. Attribution Reporting

Attribution reports must include:

- Evidence summary
- Confidence level
- Supporting indicators
- Contradictory indicators
- False-flag assessment
- Known actor profile summary
- ATT&CK comparison
- Infrastructure map

---

## 13.1 Attribution Statement Format

Example:

"The observed activity demonstrates medium-confidence overlap with Threat Actor Group X based on infrastructure reuse, malware similarities, and ATT&CK technique alignment. However, no single indicator independently confirms attribution."

---

# 14. Executive Communication Guidance

Executives must understand:

- Attribution is confidence-based
- Attribution may evolve over time
- Public attribution carries legal and reputational risk
- False positives are possible
- Technical evidence drives conclusions

Never state:

- Definitive nation-state attribution without strong evidence
- Public accusations without legal review
- Unsupported actor naming

---

# 15. MSSP Attribution Considerations

For MSSP environments:

- Avoid cross-client assumptions
- Separate attribution evidence per tenant
- Protect client confidentiality
- Correlate carefully across shared infrastructure
- Coordinate legal review for multi-client campaigns

---

# 16. Attribution Escalation Criteria

Escalate to executive leadership if:

- Nation-state involvement suspected
- Multiple clients affected
- Critical infrastructure targeted
- Regulatory or geopolitical implications exist
- Public disclosure likely

---

# 17. Documentation Requirements

| Requirement | Status |
|------------|--------|
| Infrastructure correlation completed | ☐ |
| Malware comparison completed | ☐ |
| ATT&CK mapping completed | ☐ |
| False flag assessment completed | ☐ |
| Confidence assigned | ☐ |
| Executive summary prepared | ☐ |

---

# 18. Common Attribution Mistakes

| Mistake | Risk |
|---------|------|
| Relying on IP geolocation | Misattribution |
| Overconfidence in public reports | Incorrect conclusions |
| Ignoring false flags | Strategic error |
| Using malware family alone | Weak attribution |
| Public disclosure without legal review | Legal exposure |

---

## 19. Related Documents

| Document | Path |
|----------|------|
| APT Master | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-Master.md` |
| APT L3 Forensics | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-L3-Forensics.md` |
| APT Threat Intel Integration | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-ThreatIntel-Integration.md` |
| APT Long-Term Monitoring | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-LongTerm-Monitoring.md` |
| APT MITRE Mapping | `02_PLAYBOOKS/02.13_APT-Campaign/PB-APT-MITRE-Mapping.md` |
| Threat Actor Profile Template | `08_POST-INCIDENT/08.4_Threat-Intel-Output/Threat-Actor-Profile-Template.md` |

---

## 20. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 21-May-2026 | Threat Intelligence Lead | Initial version |

---

## 21. Approval

Approved by:

Name: ____________________  
Title: ____________________  
Date: ____________________

---

**End of Document**