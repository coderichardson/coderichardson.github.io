---
title: "ISO, SOC, NIST And Other Common Cybersecurity Compliance Requirements"
date: 2020-09-14 00:20:00 +0000
tags:
  - "Compliance"
---

Depending on your industry your company may be subject to adhere to many, one, or no compliance requirements. Even for companies that have no compliance requirements, following the associated guidance and controls often results in a more secure and better documented environment.

Today I'll be covering a high-level overview of some of the most common compliance requirements we run into in information security -- what they're used for, how they're different, and who they might apply to. This list is far from exhaustive, so if I've excluded any you think should be here please comment and let me know.

Disclaimer: Do not take the information provided here as definitive or current to your or your organization's compliance status or situation. Consult the appropriate legal and/or regulatory guidance for your situation.

## ISO 27001

ISO 27000 is a family of standards published by the [International Organization for Standardization](https://www.iso.org/home.html). The most popular of these (at least within infosec) is [ISO 27001](https://www.iso.org/isoiec-27001-information-security.html). ISO 270001 focuses on an organization's Information Security Management System (ISMS), and can be supplemented with other ISO standards.

Organizations can become ISO 27001 certified through an audit conducted by an accredited third party. The organization defines the scope of the audit, but certain requirements must be met within that scope. For example, an organization must have certain policies and procedures surrounding information security management, and a dedicated committee or group that meets to discuss the ISMS. ISO provides a copy of the standard documentation [on their website](https://www.iso.org/obp/ui/#iso:std:iso-iec:27001:ed-2:v1:en).

## SOC (1, 2, 3)

System and Organization Controls (SOC) compliance is not a regulation or specific set of standards, but an auditing report created by the [American Institute of Certified Public Accountants](https://www.aicpa.org/interestareas/frc/assuranceadvisoryservices/serviceorganization-smanagement.html) (AICPA). SOC reports ultimately prove that *an organization is doing what they say they're doing*. The content and depth of the audit depends on the SOC audit selected (SOC 1, 2, or 3), as well as the sub-type (Type 1 or Type 2). Many sites will draw a clear-cut difference between these but some overlap especially around operational practices does exist. Nonetheless, different reports are often requested by potential customers with specific expectations in mind.

|  |
| --- |
|  |
| Source: <https://www.otava.com/blog/soc-1-soc-2-soc-3-report-comparison/> |

  

The difference between Type 1 and Type 2 for these reports (excluding SOC 3 as it does not have different types) is time. Type 1 audits use a "point in time" scope for the audit, while Type 2 audits review a span of time -- typically 12 months. This means providing evidence that an organization follows the stated practices over the selected span of time, and therefore Type 2 for either a SOC 1 or SOC 2 report is more thorough.

## PCI

Payment Card Industry Data Security Standard (PCI DSS) is a set of security standards that apply to all companies that handle credit cards. PCI DSS is not a regulation, but part of an agreement merchants enter into when accepting credit card payments and handling what is referred to as "cardholder data". These standards are designed to assist companies in the secure acceptance, processing, and storage of credit card information. PCI applies to all companies that accept, transmit, or store credit cards regardless of company size or number of transactions. PCI was created by American Express, Mastercard, Visa, Discover, and other major credit card companies to protect transactions in 2004, and has been updated several times since.

Unlike a SOC audit, PCI audits include a specific list of expectations an organization must meet. This can include items such as:

- Firewall with listed configurations.
- Network diagrams.
- Change records/management for all firewall modifications.
- Technical consistency between documentation and appliance configuration.
- Administrative logins to appliances require strong encryption methods.

An organization will fall into one of four levels based on transaction amount. The merchant level determines the stringency of the PCI DSS audit and are broken down as follows:

**Level 1 -** Any merchant processing over 6 million Visa transactions per year (regardless of channel).

**Level 2 -**Any merchant processing 1 million to 6 million Visa transactions per year (regardless of channel).

**Level 3 -**Any merchant processing 20,000 to 1 million Visa e-commerce transactions per year.

**Level 4 -**Any merchant processing fewer than 20,000 Visa e-commerce transactions per year, and all other merchants processing up to 1 million Visa transactions per year (regardless of channel).

Source: <https://www.pcicomplianceguide.org/faq/#4>

Failure to comply with the required standards (depending on level) can result in major fines in the event of a data breach or other event triggering a PCI DSS audit.

## GDPR

General Data Protection Regulation (GDPR) is a regulation created in 2016 and enforced in 2018 by the European Parliament for the European Union (EU). The primary goal of GDPR is to protect personal data and privacy rights of individuals. The regulation includes seven principles covering data protection and 8 covering privacy rights to accomplish this. Failure to comply with the regulation results in hefty fines up to €20 million or 4% of global revenue (whichever is higher).

Any organization that processes personal data of people in the EU must comply with GDPR. This means companies outside the EU must also comply in the event they process such data.

The [gdpr.eu](http://gdpr.eu) has a great [checklist](https://gdpr.eu/checklist/) and [FAQ](https://gdpr.eu/faq/) covering the principles and general information mentioned above.

## CIS

The Center for Internet Security (CIS) is a nonprofit organization dedicated to developing and promoting security best practices for organizations. The CIS was founded by organizations such as the SANS Institute, ISC2, IIA, AICPA, and ISACA. The CIS is arguably most famous for:

1. Benchmarks applicable to various operating systems and applications.
2. The 20 critical security controls.

Membership to the CIS can be purchased which will allow detailed access to the various benchmarks, controls, and other information gathered and published by CIS. Generalized information is available for free from [cisecurity.org](https://www.cisecurity.org/). Together, the controls and benchmarks provide a security framework and implementation guidelines for technologies that can apply to organizations in most industries.

The full list of the 20 critical security controls are listed below:

**Basic CIS Controls**

1. Inventory and Control of Hardware Assets
2. Inventory and Control of Software Assets
3. Continuous Vulnerability Management
4. Controlled Use of Administrative Privileges
5. Secure Configuration for Hardware and Software on Mobile Devices, Laptops, Workstations and Servers
6. Maintenance, Monitoring and Analysis of Audit Logs

**Foundational CIS Controls**

7. Email and Web Browser Protection.

8. Malware Defenses

9. Limitation and Control of Network Ports, Protocols and Services

10. Data Recovery Capabilities

11. Secure Configuration for Network Devices, such as Firewalls, Routers and Switches

12. Boundary Defense

13. Data Protection

14. Controlled Access Based on the Need to Know

15. Wireless Access Control

16. Account Monitoring and Control

**Organizational CIS Controls**

17. Implement a Security Awareness and Training Program

18. Application Software Security

19. Incident Response and Management

20. Penetration Tests and Red Team Exercises

## NIST

The National Institute of Standards and Technology (NIST) is an agency of the US Department of Commerce that, among other things, provides guidance and a set of standards for government agencies and private organizations to follow. In the case of government requirements, NIST publishes standards for agencies to be compliant with the Federal Information Security Management Act (FISMA). In the case of private organizations, there is no requirement to follow the standards (unless you do business with federal agencies), but they act as a series of best practices that can apply to most organizations.

The most famous of the NIST publications is [NIST SP 800-53](https://nvd.nist.gov/800-53/Rev4) due to its direct relationship with FISMA compliance. NIST SP 800-53 defines the security controls that must be implemented [to become FISMA compliant](https://www.varonis.com/blog/fisma-compliance/#:~:text=FISMA%20stands%20for%20the%20Federal,plans%20to%20protect%20sensitive%20data.). These controls are organized into three Minimum Security Controls (low, moderate, and high baseline controls) which fall under one of 18 Control Families (e.g. Access Control, Incident Response, Risk Assessment).

I won't be covering FISMA as it's own entity here, but it is worth mentioning another popular requirement in FISMA that NIST has a publication for -- [FIPS 140-2](https://csrc.nist.gov/publications/detail/fips/140/2/final) ([FIPS 140-3](https://csrc.nist.gov/publications/detail/fips/140/3/final) will become the current standard later this month 2020-09-22). This publication is a computer security standard used to approve cryptographic modules. Password vaults and other storage applications/appliances will often be involved with FIPS 140-2/3 compliance.

A great overview of the NIST cybersecurity publications can be found at the [NIST Computer Security Resource Center](https://csrc.nist.gov/publications). These are divided into the following:

- **[FIPS](https://csrc.nist.gov/publications/fips)** - Federal Information Processing Standards | Security standards.
- **[SP](https://csrc.nist.gov/publications/sp)**- NIST Special Publications | Guidelines, technical specifications, recommendations and reference materials.

- **[SP 800](https://csrc.nist.gov/publications/sp800) -** Computer security
- **[SP 1800](https://csrc.nist.gov/publications/sp1800) -** Cybersecurity practice guides
- **[SP 500](https://csrc.nist.gov/publications/sp500) -** Information technology (relevant documents)

- [NISTIR](https://csrc.nist.gov/publications/nistir)- NIST Internal or Interagency Reports Reports of research findings, including background information for FIPS and SPs.
- **[ITL Bulletin](https://csrc.nist.gov/publications/itl-bulletin)**- NIST Information Technology Laboratory (ITL) Bulletins. Monthly overviews of NIST's security and privacy publications, programs and projects.

Source: <https://csrc.nist.gov/publications>

## HIPAA

The Health Insurance Portability and Accountability Act of 1996 (HIPAA) covers more than information security regulations, but the Security and Privacy rules fulfill the act's requirement to protect the privacy and security of certain health information.

The HIPAA Security Rule applies to health plans, health care clearinghouses, and any health care provider that transmits health information in electronic form. The information protected falls under the Privacy Rule and refers to Protected Health Information (PHI), while the Security Rule defines the safeguards that must be met. Covered Entities (as opposed to Business Associates or Healthcare Clearinghouses which I won't delve into here) must:

1. Ensure the confidentiality, integrity, and availability of all e-PHI they create, receive, maintain or transmit;
2. Identify and protect against reasonably anticipated threats to the security or integrity of the information;
3. Protect against reasonably anticipated, impermissible uses or disclosures; and
4. Ensure compliance by their workforce.

Source: <https://www.hhs.gov/hipaa/for-professionals/security/laws-regulations/index.html>

So what qualifies as PHI? Any health information combined with Personally Identifiable Information (PII). What qualifies as PII? That depends on state law when referring to just PII, but from a HIPAA perspective it is defined as having a "reasonable basis to believe the information can be used to identify the individual." For example, if an organization sends an email to someone with a health condition, containing information regarding that health condition, this is considered considered PHI. In these cases the PII is referred to as an "identifier" -- the information that links the medical information to an individual. If this information is removed (a process called "de-identification") it is no longer considered PHI.

Some examples of these identifiers are:

1. Name
2. Address (including subdivisions smaller than state such as street address, city, county, or zip code)
3. Any dates (except years) that are directly related to an individual, including birthday, date of admission or discharge, date of death, or the exact age of individuals older than 89
4. Telephone number
5. Fax number
6. Email address
7. Social Security number
8. Medical record number
9. Health plan beneficiary number
10. Account number
11. Certificate/license number
12. Vehicle identifiers, serial numbers, or license plate numbers
13. Device identifiers or serial numbers
14. Web URLs
15. IP address
16. Biometric identifiers such as fingerprints or voice prints
17. Full-face photos
18. Any other unique identifying numbers, characteristics, or codes

Source: <https://compliancy-group.com/protected-health-information-understanding-phi/>  
<https://www.hhs.gov/hipaa/for-professionals/privacy/special-topics/de-identification/index.html>

Penalties for HIPAA non-compliance can result in fines of $100 to $50,000 per incident or even jail time depending on the type of non-compliance ("Reasonable Cause" or "Willful Neglect").

## Summary

I hope this has been an informative high-level overview of these sometimes confusing standards. Even if they don't apply to your industry, or you only follow a subset of one of these, it can be good to know where compliance requirements and guidance exist and what those requirements apply to. Especially if you apply to work for a federal government contractor healthcare clearinghouse that processes credit card transactions. 😁