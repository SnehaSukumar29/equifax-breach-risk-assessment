# 5. Risk Analysis — Likelihood, Impact & Risk Matrix (Step 2)

[← Threat & Vulnerability Analysis](04-threat-vulnerability-analysis.md) · [Next: Risk Register & Treatment →](06-risk-register-and-treatment.md)

Risk score = **Likelihood × Impact**, using the [scoring criteria](02-methodology.md#scoring-criteria).

## 5.1 Likelihood & Impact Determination

| Risk | L | Likelihood Justification | I | Impact Justification | Score | Rating |
|------|:-:|--------------------------|:-:|----------------------|:-----:|:------:|
| **R1** | 5 | Public exploit code was available within a day of disclosure; US-CERT notified Equifax directly; ACIS was internet-facing with no WAF or virtual patch | 5 | RCE gave full control of the entry point, affecting C, I and A, and opened the path to ~147.9M consumer records | **25** | 🔴 Critical |
| **R2** | 4 | Highly likely once R1 was exploited: PII unencrypted, no DLP or egress filtering, monitoring inactive. Rated 4 (not 5) because it depends on R1 first | 5 | ~147.9M records including SSNs and DOBs exfiltrated over 76 days. Catastrophic confidentiality impact; $575M+ settlement | **20** | 🔴 Critical |
| **R3** | 5 | Once inside ACIS, little skill was needed to use plaintext credentials on an accessible file share, and the flat network imposed no barriers | 4 | Enabled access to 48 unrelated databases, massively expanding the breach beyond the initially compromised system | **20** | 🔴 Critical |
| **R4** | 5 | The certificate had already been expired for over a year before the breach began — the failure was pre-existing and certain, with no compensating control | 5 | IDS and IPS were ineffective for the entire 76-day intrusion. Total loss of monitoring capability allowed every other risk to go undetected | **25** | 🔴 Critical |
| **R5** | 4 | Absent MFA made unauthorised access highly likely once the attacker held internal credentials. Rated 4 because it depends on R3 first | 5 | 209,000 payment card records exfiltrated. PCI DSS exposure, FTC action and class action litigation | **20** | 🔴 Critical |

## 5.2 Inherent Risk Matrix

|  | **Impact 1** | **Impact 2** | **Impact 3** | **Impact 4** | **Impact 5** |
|---|:---:|:---:|:---:|:---:|:---:|
| **Likelihood 5** | 🟢 | 🟡 | 🟠 | 🔴 **R3** | 🔴 **R1, R4** |
| **Likelihood 4** | 🟢 | 🟡 | 🟠 | 🟠 | 🔴 **R2, R5** |
| **Likelihood 3** | 🟢 | 🟡 | 🟡 | 🟠 | 🟠 |
| **Likelihood 2** | 🟢 | 🟢 | 🟡 | 🟡 | 🟡 |
| **Likelihood 1** | 🟢 | 🟢 | 🟢 | 🟢 | 🟢 |

🟢 Low (1–5) · 🟡 Medium (6–10) · 🟠 High (11–16) · 🔴 Critical (17–25)

## 5.3 Summary

| Risk | Likelihood | Impact | Score | Rating |
|------|------------|--------|:-----:|:------:|
| R1 | 5 – Almost Certain | 5 – Severe | 25 | 🔴 Critical |
| R2 | 4 – Likely | 5 – Severe | 20 | 🔴 Critical |
| R3 | 5 – Almost Certain | 4 – Major | 20 | 🔴 Critical |
| R4 | 5 – Almost Certain | 5 – Severe | 25 | 🔴 Critical |
| R5 | 4 – Likely | 5 – Severe | 20 | 🔴 Critical |

**All five risks are Critical.** Notably, R2, R3 and R5 are *chained* — each depends on the one before it — which is why breaking the chain at R1 (patching) and detecting it via R4 (monitoring) are the highest-value treatments.
