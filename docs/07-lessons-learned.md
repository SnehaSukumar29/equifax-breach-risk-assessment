# 7. Discussion & Lessons Learned

[← Risk Register & Treatment](06-risk-register-and-treatment.md) · [References →](references.md)

## Would a Risk Assessment Have Prevented the Breach?

Very likely, yes. A structured NIST SP 800-30 assessment carried out before May 2017 would have turned two known, preventable failures into prioritised actions with owners and deadlines:

- **R1 (unpatched Struts)** would have scored **25 — Critical**, triggering immediate patching well before exploitation began on 13 May 2017.
- **R4 (expired certificate)** would have been flagged as a **Critical** monitoring failure. Had the certificate been renewed, the malicious queries and data transfers would have been visible within days rather than going unnoticed for 76.

## The Highest-Value Control

**Automated patch management with verification (NIST SI-2 Flaw Remediation).** Without the initial exploitation of CVE-2017-5638, risks R2–R5 never materialise. Research on vulnerability prioritisation (Kasturi et al., 2024) supports focusing remediation on internet-facing, high-CVSS vulnerabilities first.

## Organisational, Not Just Technical

Equifax had the right tools — a scanning programme, a patch notification process, an IDS and an inspection appliance — but no governance structure to ensure they worked as intended. Macnish and van der Ham (2020) frame the breach as fundamentally an ethical and governance failure, while Sadok, Alter and Bednar (2020) show how security is often treated as "someone else's job", which helps explain why the patch email of 9 March 2017 was never acted on.

## Key Lessons

| # | Lesson | In practice |
|:-:|--------|-------------|
| 1 | **Knowing about a vulnerability is not the same as fixing it** | Patch management must include automated verification that remediation actually happened |
| 2 | **Security tooling needs lifecycle management too** | Certificates, licences and sensor health must be inventoried and monitored — if monitoring goes dark, the organisation is blind |
| 3 | **Segmentation limits the blast radius** | One compromised web app should never reach 48 unrelated databases |
| 4 | **Accountability turns awareness into action** | A risk assessment assigns criticality, owners and deadlines to issues that would otherwise sit in an inbox |

## Conclusion

The 2017 Equifax breach was caused by failing to apply a known critical patch to an internet-facing application despite direct notification from US-CERT, compounded by an expired SSL certificate that disabled network monitoring and prevented detection of the intrusion. This assessment identified five Critical risks using NIST SP 800-30 — every one of them arising from known and preventable conditions.

The most important proactive step any organisation can take is to conduct a structured risk assessment *before* a breach: assigning criticality scores, ownership and remediation deadlines to convert passive awareness into accountable action.
