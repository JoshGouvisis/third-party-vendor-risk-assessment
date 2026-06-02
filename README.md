# Third-Party Vendor Risk Assessment: CloudVault HR

## Meridian Financial Group

**Assessment Date:** June 2026
**Assessor:** Josh Gouvisis
**Vendor:** CloudVault HR
**Classification:** Internal Use Only

---

## Executive Summary

Meridian Financial Group is evaluating CloudVault HR, a cloud-based SaaS platform, to replace its current on-premises HR system. The vendor will handle extremely sensitive employee data including Social Security numbers, bank account details, salary information, and health insurance records, making this a high-sensitivity engagement with significant regulatory implications under SEC, FINRA, and SOX. CloudVault HR demonstrates a reasonably mature security posture for a company of its size, with SOC 2 Type II certification, strong encryption standards, annual penetration testing, and a documented business continuity plan. However, two meaningful gaps require resolution before onboarding: MFA is not enforced by default, which is unacceptable given the sensitivity of data involved, and the SOC 2 report does not cover the Confidentiality or Privacy trust service criteria, leaving the most relevant data protection assurances unvalidated by an independent auditor. **Overall Risk Rating: Medium. Conditional approval is recommended pending satisfaction of the conditions outlined in this report.**

---

## Vendor Profile

| Attribute | Detail |
|-----------|--------|
| Vendor Name | CloudVault HR |
| Service Type | SaaS — Human Resources Management Platform |
| Founded | 2019 |
| Headquarters | Austin, TX |
| Company Size | ~120 employees |
| Customers | ~800 mid-market companies |
| Hosting | AWS (us-east-1 and us-west-2) |
| Data Accessed | Employee SSNs, salary data, bank account details (direct deposit), health insurance information, performance records |
| Data Residency | US only. No international data transfer. |
| Regulatory Relevance | Data handled is subject to SEC, FINRA, SOX, and state privacy regulations |
| Subprocessors | Stripe (payment processing), AWS (infrastructure), SendGrid (transactional email) |
| Compliance Status | SOC 2 Type II (Security and Availability). ISO 27001 in progress, expected Q3 2026. |

---

## Risk Rating

| Rating | Definition |
|--------|-----------|
| Low | Vendor meets or exceeds security requirements. Minimal residual risk. Approve. |
| **Medium** | **Vendor meets most requirements but has gaps that should be addressed. Approve with conditions.** |
| High | Vendor has significant security gaps. Do not approve until gaps are remediated. |
| Critical | Vendor poses unacceptable risk. Do not onboard. |

**Assigned Rating: Medium**

CloudVault HR has meaningful security controls in place and a generally mature posture for a company founded in 2019. The rating is not High because the identified gaps are addressable through configuration changes and contractual requirements rather than fundamental security failures. The rating is not Low because the MFA enforcement gap and incomplete SOC 2 coverage represent genuine residual risk for a financial services firm handling this category of data.

---

## Findings

| # | Area | Finding | Risk Level | Recommendation |
|---|------|---------|------------|----------------|
| 1 | Multi-Factor Authentication | MFA is available and recommended but not enforced by default. Enforcement is configurable by the customer. In a financial services environment handling SSNs and bank account data, optional MFA is not acceptable. | High | Require Meridian to enforce MFA for all users as a condition of onboarding. Document MFA enforcement configuration in the vendor contract. Verify enforcement before go-live. |
| 2 | SOC 2 Coverage | SOC 2 Type II report covers Security and Availability only. Confidentiality and Privacy trust service criteria are not included. Given that CloudVault HR will process highly sensitive PII and financial data, the absence of independent assurance over Confidentiality and Privacy is a meaningful gap. | Medium | Request CloudVault HR's roadmap for expanding SOC 2 coverage to include Confidentiality and Privacy. Require notification if SOC 2 scope changes. Consider requiring expanded coverage as a condition of contract renewal. |
| 3 | ISO 27001 Certification | ISO 27001 is in progress with expected certification in Q3 2026. SOC 2 Type II provides reasonable assurance in the interim, but ISO 27001 would provide a broader internationally recognized control framework validation. | Low | Track certification progress. Require CloudVault HR to notify Meridian if certification is delayed or scope changes. Request copy of certification upon completion. |
| 4 | Subprocessor Risk: SendGrid | SendGrid handles transactional email. Depending on platform configuration, notification emails may contain employee names, partial account details, or HR action confirmations. This represents a data flow through a third party that is not covered by CloudVault HR's SOC 2 report. | Medium | Request documentation of what employee data is included in SendGrid-processed emails. Confirm SendGrid's data handling agreements are flowed down from CloudVault HR. Verify SendGrid is listed in the DPA as a covered subprocessor. |
| 5 | Subprocessor Risk: Stripe | Stripe handles payment processing. Bank account details for direct deposit may flow through Stripe depending on architecture. Stripe is PCI-DSS compliant, which provides assurance, but data flow should be confirmed. | Medium | Request clarification on exactly what financial data flows through Stripe and under what conditions. Confirm Stripe's inclusion and coverage in CloudVault HR's DPA. |
| 6 | 2024 Staging Environment Incident | In 2024, an unauthorized party accessed a staging environment containing test data. No production data was exposed. CloudVault HR disclosed publicly and remediated within 72 hours. | Low | This is evaluated as a net positive indicator rather than a red flag. Transparent public disclosure and rapid remediation demonstrate a functioning incident response process. However, Meridian should request the post-incident report under NDA to confirm test data did not include any real customer data and to review remediation steps taken. |
| 7 | Data Deletion | Customer data is deleted within 30 days of contract termination upon written request. Deletion is not automatic. | Low | Ensure the data processing agreement (DPA) includes a mandatory deletion clause and timeline. Require written confirmation of deletion upon contract termination. |
| 8 | MFA Scope for Employees | CloudVault HR provides annual security awareness training for its own employees but the questionnaire does not address whether MFA is enforced internally for CloudVault HR staff accessing customer data. | Medium | Request confirmation that CloudVault HR enforces MFA for all internal staff with access to production customer data. This should be verifiable through the SOC 2 report or a supplemental control attestation. |

---

## Strengths

CloudVault HR demonstrates several practices that provide meaningful confidence for a vendor of this size and age:

**SOC 2 Type II Completed.** A completed Type II report covering Security and Availability means an independent auditor has validated that controls were operating effectively over a period of time, not just documented on paper. This is a meaningful baseline for a company founded in 2019.

**Strong Encryption Standards.** AES-256 at rest and TLS 1.2+ in transit are current industry standards. No concerns here.

**Annual Third-Party Penetration Testing.** The November 2025 pentest produced no critical findings and two high findings that were remediated within 30 days. The willingness to conduct and share pentest results under NDA is a positive signal.

**Documented and Tested Business Continuity.** RPO of 4 hours and RTO of 8 hours with a tested plan as of Q4 2025 is a reasonable posture. BCP documentation and testing demonstrate operational maturity.

**Transparent Incident Disclosure.** The 2024 staging environment incident was publicly disclosed and remediated within 72 hours. Transparency is a strong indicator of a security culture that does not hide problems.

**SAML SSO Support.** Support for SAML SSO allows Meridian to integrate CloudVault HR into its existing identity management infrastructure, centralizing access control and simplifying deprovisioning.

**US-Only Data Residency.** No international data transfer simplifies regulatory compliance and eliminates cross-border data transfer risk.

**Customer-Configurable RBAC.** Role-based access control managed by the customer means Meridian can enforce least-privilege access internally without depending on the vendor to do it.

---

## Gaps and Concerns

**MFA Not Enforced by Default.** This is the most significant gap. A platform handling SSNs, bank account numbers, and health insurance data should enforce MFA at the platform level, not leave it as a customer configuration option. The risk is that a Meridian administrator could fail to enable it, leaving accounts protected only by passwords. In a financial services context, this is not an acceptable default posture.

**SOC 2 Does Not Cover Confidentiality or Privacy.** The trust service criteria most directly relevant to what CloudVault HR does, protecting the confidentiality of employee data and handling personal information appropriately, are not independently audited. Security and Availability cover system uptime and access controls at a high level, but they do not specifically validate that CloudVault HR handles sensitive PII with appropriate controls and data minimization practices.

**Subprocessor Data Flows Are Not Fully Documented.** Stripe and SendGrid are listed, but the questionnaire does not specify what data actually flows through each. For a platform handling payroll and bank account data, understanding exactly what Stripe receives and under what circumstances is important, not assumed.

**ISO 27001 Not Yet Certified.** This is a lower concern given the SOC 2 Type II, but ISO 27001 would provide a broader control framework validation. The "expected Q3 2026" timeline has not been independently verified and should be tracked.

**Annual Employee Security Training Only.** Annual training is a baseline, but given the sensitivity of the data CloudVault HR handles, monthly or quarterly phishing simulations and more frequent touchpoints would be a stronger posture.

---

## Conditions for Approval

The following conditions must be satisfied before Meridian onboards CloudVault HR:

1. **MFA Enforcement Required at Go-Live.** Meridian must configure and enforce MFA for all user accounts within the CloudVault HR platform before any employee data is migrated. This must be verified by Meridian IT prior to go-live and documented in the onboarding checklist.

2. **DPA Review and Execution.** Meridian's legal and compliance team must review and execute a data processing agreement that explicitly covers: data categories processed, subprocessor obligations, breach notification timelines (72 hours as stated), data deletion requirements, and audit rights.

3. **SOC 2 Report Review Under NDA.** Meridian must obtain and review the full SOC 2 Type II report prior to onboarding to validate the scope and confirm no exceptions were noted in the auditor's opinion.

4. **Subprocessor Data Flow Clarification.** CloudVault HR must provide written documentation of exactly what employee data flows through Stripe and SendGrid and under what conditions, prior to contract execution.

5. **2024 Incident Post-Mortem Request.** Meridian should request the post-incident report from the 2024 staging environment incident under NDA to confirm no real customer data was involved and to review the remediation steps taken.

6. **Internal MFA Confirmation.** CloudVault HR must confirm in writing that all internal staff with access to production customer data are required to use MFA.

---

## Ongoing Monitoring Recommendations

Onboarding is not the end of vendor risk management. Meridian should implement the following ongoing oversight activities:

**Annual Vendor Reassessment.** Conduct a full reassessment of CloudVault HR's security posture each year, including a refreshed questionnaire and review of any changes to their environment, certifications, or subprocessors.

**SOC 2 Report Review.** Request and review the updated SOC 2 Type II report annually. Pay attention to any new exceptions, changes in scope, or changes in the auditor's opinion. Note whether Confidentiality and Privacy criteria are added in future reporting periods.

**ISO 27001 Certification Tracking.** Follow up on the expected Q3 2026 certification. If CloudVault HR achieves certification, request a copy. If certification is delayed, document the reason and assess whether it changes the risk posture.

**Incident Notification Monitoring.** Confirm that CloudVault HR's 72-hour breach notification commitment is reflected in the executed DPA. Establish an internal point of contact at Meridian responsible for receiving and triaging vendor incident notifications.

**Access Reviews.** Conduct quarterly reviews of which Meridian employees have access to CloudVault HR and at what permission level. Revoke access promptly for terminated employees. Verify that RBAC configurations remain aligned with least-privilege principles.

**Subprocessor Change Notifications.** Require CloudVault HR to notify Meridian in advance of any changes to their subprocessor list. Review new subprocessors before changes take effect.

**Contract Renewal Review.** At each contract renewal, revisit the risk rating and conditions. Reassess whether the SOC 2 scope has expanded and whether the risk posture has improved or deteriorated.

---

## What I Learned

Going into this I thought vendor risk assessment was mostly about collecting answers to a questionnaire and checking whether the vendor had the right certifications. What I realized pretty quickly is that the answers themselves are only the starting point. CloudVault HR answered every question, and most of the answers were positive. The real work was figuring out what the answers didn't cover and what that meant for Meridian specifically.

The MFA finding was straightforward once I thought about it in context. "Available but not enforced" sounds reasonable in isolation, but when you put it next to the fact that this vendor will hold employee SSNs and bank account numbers for a financial services firm, it stopped sounding reasonable fast. That was the first time I really understood what it means to evaluate a control against the specific risk environment, not just against a generic standard.

The SOC 2 coverage gap took me longer to catch. I initially read "SOC 2 Type II completed" and moved on like it was a green light. It wasn't until I looked at which trust service criteria were actually covered that I realized the two most relevant ones, Confidentiality and Privacy, weren't in scope at all. That taught me to read certifications carefully instead of treating them as blanket assurance.

The 2024 incident was the part I found most interesting to think through. My instinct was that any breach history should count against the vendor. But when I worked through what actually happened and how they responded, I landed in a different place. I don't think I would have gotten there without having a framework to evaluate it against instead of just reacting to it.
