# 3. System Characterisation (Step 1)

[← Methodology](02-methodology.md) · [Next: Threat & Vulnerability Analysis →](04-threat-vulnerability-analysis.md)

## Assessment Scope

| Element | Definition |
|---------|------------|
| **Purpose** | Assess the information security risks in Equifax's consumer data infrastructure at the time of the 2017 breach, and recommend the mitigations that should have been in place to prevent it |
| **Scope** | ACIS dispute portal (web application), application servers (×2), web servers (×2), SSL/TLS traffic inspection systems, database servers, internal network infrastructure |
| **Boundaries** | Includes production IT systems in Equifax data centres handling consumer data. Excludes third-party payment processors' internal systems and physical office security |
| **Time horizon** | September 2016 – September 2017 (12 months before public disclosure) |

### Out of Scope
1. HR systems unrelated to consumer data
2. Physical security of data centres
3. Third-party processors
4. External credit reporting systems (Experian, TransUnion)
5. Insider threats
6. Post-breach remediation systems implemented after September 2017
7. Social engineering and phishing

### Assumptions
1. Equifax's network architecture remained unchanged throughout the assessment period
2. The threat landscape reflects 2017 conditions
3. No major system design changes occurred during the assessment period
4. ACIS was a legacy system with high architectural complexity (based on congressional testimony)
5. The March 2017 vulnerability scan is assumed accurate at the time it ran

### Constraints
Limited to publicly available documentation — the US House Oversight Committee report, GAO report GAO-18-559, and the FTC complaint against Equifax. No penetration testing data or direct access to Equifax internal systems was available.

---

## Asset Register

C / I / A scored 1–5 using the [scoring criteria](02-methodology.md#scoring-criteria).

| ID | Asset | Type | Business Function / Role in Breach | C | I | A | Regulatory Impact | Criticality |
|----|-------|------|------------------------------------|:-:|:-:|:-:|:-:|:-:|
| A01 | Consumer PII Database | Data | Names, SSNs, DOBs, addresses and driver's licence numbers of ~147.9M US consumers | 5 | 5 | 2 | 5 | 🔴 Critical |
| A02 | Apache Struts Web Application (ACIS) | Application | Customer-facing credit dispute portal; confirmed entry point via CVE-2017-5638 | 4 | 5 | 5 | 4 | 🔴 Critical |
| A03 | Payment Card Database | Data | Payment card numbers and expiry dates of 209,000 US consumers | 5 | 4 | 2 | 5 | 🔴 Critical |
| A04 | Internal Credentials File | Data | Usernames and passwords stored unencrypted in a configuration file on a mounted file share; gave attackers access to 48 databases | 4 | 5 | 3 | 4 | 🔴 Critical |
| A05 | SSL/TLS Inspection Appliance (SSLV) | Security system | Inspects encrypted traffic for malicious activity; certificate expired January 2016, leaving IDS/IPS ineffective for ~19 months | 1 | 2 | 5 | 4 | 🟠 High |
| A06 | Internal Network | Infrastructure | Connects internal systems; lack of segmentation allowed movement from ACIS to 48 unrelated databases | 3 | 4 | 3 | 3 | 🟠 High |
| A07 | Dispute Documents Database | Data | Scanned identity documents and correspondence of 182,000 US consumers | 4 | 4 | 2 | 4 | 🟠 High |
| A08 | Employee User Accounts | Identity | Internal accounts used to authenticate to databases; attackers impersonated authorised users to run ~9,000 queries undetected | 4 | 3 | 2 | 4 | 🟠 High |
| A09 | Security Certificate Inventory | Operational | Organisation-wide SSL/TLS certificate inventory; 300+ certificates had expired, including 79 on business-critical monitoring devices | 2 | 3 | 5 | 3 | 🟠 High |

> A machine-readable version is available in [`data/asset-register.csv`](../data/asset-register.csv).
