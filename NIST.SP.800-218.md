# NIST Special Publication 800-218

Secure Software Development Framework (SSDF) Version 1.1: Recommendations for Mitigating the Risk of Software Vulnerabilities

- Murugiah Souppaya
- Karen Scarfone
- Donna Dodson

This publication is available free of charge from: https://doi.org/10.6028/NIST.SP.800-218

NIST Special Publication 800-218

Secure Software Development Framework (SSDF) Version 1.1: Recommendations for Mitigating the Risk of Software Vulnerabilities

Murugiah Souppaya

Computer Security Division
Information Technology Laboratory

Karen Scarfone

Scarfone Cybersecurity
Clifton, VA

Donna Dodson*

* Former NIST employee; all work for this publication was done while at NIST.

 February 2022

U.S. Department of Commerce

Gina M. Raimondo, Secretary

National Institute of Standards and Technology
James K. Olthoff, Performing the Non-Exclusive Functions and Duties of the Under Secretary of Commerce
for Standards and Technology & Director, National Institute of Standards and Technology

Authority
This publication has been developed by NIST in accordance with its statutory responsibilities under the
Federal Information Security Modernization Act (FISMA) of 2014, 44 U.S.C. § 3551 et seq., Public Law
(P.L.) 113-283. NIST is responsible for developing information security standards and guidelines, including
minimum requirements for federal information systems, but such standards and guidelines shall not apply
to national security systems without the express approval of appropriate federal officials exercising policy
authority over such systems. This guideline is consistent with the requirements of the Office of Management
and Budget (OMB) Circular A-130.
Nothing in this publication should be taken to contradict the standards and guidelines made mandatory and
binding on federal agencies by the Secretary of Commerce under statutory authority. Nor should these
guidelines be interpreted as altering or superseding the existing authorities of the Secretary of Commerce,
Director of the OMB, or any other federal official. This publication may be used by nongovernmental
organizations on a voluntary basis and is not subject to copyright in the United States. Attribution would,
however, be appreciated by NIST.
National Institute of Standards and Technology Special Publication 800-218
Natl. Inst. Stand. Technol. Spec. Publ. 800-218, 36 pages (February 2022)
CODEN: NSPUE2

This publication is available free of charge from:
https://doi.org/10.6028/NIST.SP.800-218

Certain commercial entities, equipment, or materials may be identified in this document in order to describe an
experimental procedure or concept adequately. Such identification is not intended to imply recommendation or
endorsement by NIST, nor is it intended to imply that the entities, materials, or equipment are necessarily the best
available for the purpose.
There may be references in this publication to other publications currently under development by NIST in accordance
with its assigned statutory responsibilities. The information in this publication, including concepts and methodologies,
may be used by federal agencies even before the completion of such companion publications. Thus, until each
publication is completed, current requirements, guidelines, and procedures, where they exist, remain operative. For
planning and transition purposes, federal agencies may wish to closely follow the development of these new
publications by NIST.
Organizations are encouraged to review all draft publications during public comment periods and provide feedback to
NIST. Many NIST cybersecurity publications, other than the ones noted above, are available at
https://csrc.nist.gov/publications.
Submit comments on this publication to: ssdf@nist.gov
National Institute of Standards and Technology
Attn: Computer Security Division, Information Technology Laboratory
100 Bureau Drive (Mail Stop 8930) Gaithersburg, MD 20899-8930

All comments are subject to release under the Freedom of Information Act (FOIA).

Reports on Computer Systems Technology


The Information Technology Laboratory (ITL) at the National Institute of Standards and
Technology (NIST) promotes the U.S. economy and public welfare by providing technical
leadership for the Nation’s measurement and standards infrastructure. ITL develops tests, test
methods, reference data, proof of concept implementations, and technical analyses to advance
the development and productive use of information technology. ITL’s responsibilities include the
development of management, administrative, technical, and physical standards and guidelines for
the cost-effective security and privacy of other than national security-related information in
federal information systems. The Special Publication 800-series reports on ITL’s research,
guidelines, and outreach efforts in information system security, and its collaborative activities
with industry, government, and academic organizations.
Abstract

Few software development life cycle (SDLC) models explicitly address software security in
detail, so secure software development practices usually need to be added to each SDLC model
to ensure that the software being developed is well-secured. This document recommends the
Secure Software Development Framework (SSDF) – a core set of high-level secure software
development practices that can be integrated into each SDLC implementation. Following such
practices should help software producers reduce the number of vulnerabilities in released
software, reduce the potential impact of the exploitation of undetected or unaddressed
vulnerabilities, and address the root causes of vulnerabilities to prevent future recurrences.
Because the framework provides a common vocabulary for secure software development,
software acquirers can also use it to foster communications with suppliers in acquisition
processes and other management activities.
Keywords
secure software development; Secure Software Development Framework (SSDF); secure
software development practices; software acquisition; software development; software
development life cycle (SDLC); software security.
Trademark Information
All registered trademarks or trademarks belong to their respective organizations.

## Acknowledgments
The authors thank all of the organizations and individuals who provided input for this update to
the SSDF. In response to Section 4 of Executive Order (EO) 14028 on “Improving the Nation’s
Cybersecurity,” NIST held a June 2021 workshop and received over 150 position papers, many
of which suggested secure software development practices, tasks, examples of implementations,
and references for consideration for this SSDF update. The authors appreciate all of those
suggestions, as well as the input from those who spoke at or attended the workshop and shared
their thoughts during or after the workshop.


Additionally, the authors appreciate the public comments submitted by dozens of organizations
and individuals and wish to acknowledge the particularly helpful feedback from Amazon Web
Services, Apiiro, Blackberry, BSA | The Software Alliance, the Enterprise Cloud Coalition, the
General Services Administration (GSA), Google, IBM, Medical Imaging & Technology Alliance
(MITA), Microsoft, Oracle, the Software Assurance Forum for Excellence in Code (SAFECode),
Synopsis, the U.S. Navy, Xoomworks, and Robert Grupe. Representatives of Siemens Energy
and Synopsis contributed mappings to new references.
The authors thank all of their NIST colleagues for their support throughout the SSDF update,
especially Curt Barker, Paul Black, Jon Boyens, Jim Foti, Barbara Guttman, Mat Heyman,
Nicole Keller, Matt Scholl, Adam Sedgewick, Kevin Stine, and Isabel Van Wyk.
The authors also wish to thank all of the individuals and organizations who provided comments
on drafts of the original version of the SSDF, including the Administrative Offices of the U.S.
Courts, The Aerospace Corporation, BSA | The Software Alliance, Capitis Solutions, the
Consortium for Information & Software Quality (CISQ), HackerOne, Honeycomb Secure
Systems, iNovex, Ishpi Information Technologies, the Information Security and Privacy
Advisory Board (ISPAB), Juniper Networks, Microsoft, MITA, Naval Sea Systems Command
(NAVSEA), NIST, Northrop Grumman, the Office of the Undersecretary of Defense for
Research and Engineering, Red Hat, SAFECode, and the Software Engineering Institute (SEI).

## Audience

There are two primary audiences for this document. The first is software producers (e.g.,
commercial-off-the-shelf [COTS] product vendors, government-off-the-shelf [GOTS] software
developers, custom software developers, internal development teams) regardless of size, sector,
or level of maturity. The second is software acquirers – both federal agencies and other
organizations. Readers of this document are not expected to be experts in secure software
development in order to understand it, but such expertise is required to implement its
recommended practices.

Personnel within the following Workforce Categories and Specialty Areas from the National
Initiative for Cybersecurity Education (NICE) Cybersecurity Workforce Framework [SP800181]
are most likely to find this publication of interest:

- Securely Provision (SP)
  - Risk Management (RSK)
  - Software Development (DEV)
  - Systems Requirements Planning (SRP)
  - Test and Evaluation (TST)
  - Systems Development (SYS)
- Operate and Maintain (OM)
  - Systems Analysis (ANA)
- Oversee and Govern (OV)
  - Training, Education, and Awareness (TEA)
  - Cybersecurity Management (MGT)
  - Executive Cyber Leadership (EXL)
  - Program/Project Management (PMA) Acquisition
- Protect and Defend (PR)
  - Incident Response (CIR)
  - Vulnerability Assessment and Management (VAM)
- Analyze (AN)
  - Threat Analysis (TWA)
  - Exploitation Analysis (EXP)

### Note to Readers

We encourage you to provide feedback on the SSDF at any time, especially as you implement
the SSDF within your own organization and software development efforts. Having inputs from a
variety of software producers will be particularly helpful to us in refining and revising the SSDF.

The publication will be updated periodically to reflect your inputs and feedback.

If you are from a standards-developing organization or another organization that has produced a
set of secure practices and you would like to map your secure software development standard or
guidance to the SSDF, please contact us at ssdf@nist.gov. We would like to introduce you to the
National Online Informative References Program (OLIR) so that you can submit your mapping
there to augment the existing set of informative references.

### Patent Disclosure Notice
NOTICE: The Information Technology Laboratory (ITL) has requested that holders of patent claims
whose use may be required for compliance with the guidance or requirements of this publication
disclose such patent claims to ITL. However, holders of patents are not obligated to respond to ITL
calls for patents and ITL has not undertaken a patent search in order to identify which, if any,
patents may apply to this publication.

As of the date of publication and following call(s) for the identification of patent claims whose use
may be required for compliance with the guidance or requirements of this publication, no such
patent claims have been identified to ITL.
No representation is made or implied by ITL that licenses are not required to avoid patent
infringement in the use of this publication.

## Executive Summary
This document describes a set of fundamental, sound practices for secure software development called the Secure Software Development Framework (SSDF). Organizations should integrate the
SSDF throughout their existing software development practices, express their secure software development requirements to third-party suppliers using SSDF conventions, and acquire
software that meets the practices described in the SSDF. Using the SSDF helps organizations to meet the following secure software development recommendations:

- Organizations should ensure that their people, processes, and technology are prepared to
perform secure software development.

- Organizations should protect all components of their software from tampering and
unauthorized access.

- Organizations should produce well-secured software with minimal security
vulnerabilities in its releases.

- Organizations should identify residual vulnerabilities in their software releases and
respond appropriately to address those vulnerabilities and prevent similar ones from
occurring in the future.

The SSDF does not prescribe how to implement each practice. The focus is on the outcomes of
the practices rather than on the tools, techniques, and mechanisms to do so. This means that the
SSDF can be used by organizations in any sector or community, regardless of size or
cybersecurity sophistication. It can also be used for any type of software development, regardless
of technology, platform, programming language, or operating environment.

The SSDF defines only a high-level subset of what organizations may need to do, so
organizations should consult the references and other resources for additional information on
implementing the practices. Not all practices are applicable to all use cases; organizations should
adopt a risk-based approach to determine what practices are relevant, appropriate, and effective
to mitigate the threats to their software development practices.
Organizations can communicate how they are addressing the clauses from Section 4 of the
President’s Executive Order (EO) on “Improving the Nation’s Cybersecurity (14028)” by
referencing the SSDF practices and tasks described in Appendix A.


### Table of Contents

- Executive Summary
- Introduction
- The Secure Software Development Framework
- References 
- The SSDF and Executive Order 14028
- Acronyms
- Change Log

### List of Tables

Table 1: The Secure Software Development Framework (SSDF) Version 1.1

Table 2: SSDF Practices Corresponding to EO 14028 Clauses


## Introduction

A software development life cycle (SDLC) 1 is a formal or informal methodology for designing,
creating, and maintaining software (including code built into hardware). There are many models
for SDLCs, including waterfall, spiral, agile, and – in particular – agile combined with software
development and IT operations (DevOps) practices. Few SDLC models explicitly address
software security in detail, so secure software development practices usually need to be added to
and integrated into each SDLC model. Regardless of which SDLC model is used, secure
software development practices should be integrated throughout it for three reasons: to reduce
the number of vulnerabilities in released software, to reduce the potential impact of the
exploitation of undetected or unaddressed vulnerabilities, and to address the root causes of
vulnerabilities to prevent recurrences. Vulnerabilities include not just bugs caused by coding
flaws, but also weaknesses caused by security configuration settings, incorrect trust assumptions,
and outdated risk analysis. [IR7864]

Most aspects of security can be addressed multiple times within an SDLC, but in general, the
earlier in the SDLC that security is addressed, the less effort and cost is ultimately required to
achieve the same level of security. This principle, known as shifting left, is critically important
regardless of the SDLC model. Shifting left minimizes any technical debt that would require
remediating early security flaws late in development or after the software is in production.
Shifting left can also result in software with stronger security and resiliency.
There are many existing documents on secure software development practices, including those
listed in the References section. This document does not introduce new practices or define new
terminology. Instead, it describes a set of high-level practices based on established standards,
guidance, and secure software development practice documents. These practices, collectively
called the Secure Software Development Framework (SSDF), are intended to help the target
audiences achieve secure software development objectives. Many of the practices directly
involve the software itself, while others indirectly involve it (e.g., securing the development
environment).

Future work may expand on this publication and potentially cover topics such as how the SSDF
may apply to and vary for particular software development methodologies and associated
practices like DevOps, how an organization can transition from their current software
development practices to also incorporating the SSDF practices, and how the SSDF could be
applied in the context of open-source software. Future work will likely take the form of use cases
so that the insights will be more readily applicable to specific types of development
environments, and it will likely include collaboration with the open-source community and other
groups and organizations.

Note that SDLC is also widely used for “system development life cycle.” All usage of “SDLC” in this document is
referencing software, not systems.

This document identifies secure software development practices but does not prescribe how to
implement them. The focus is on the outcomes of the practices to be implemented rather than on the tools, techniques, and mechanisms used to do so. Advantages of specifying the practices at a
high level include the following:

- Can be used by organizations in any sector or community, regardless of size or
cybersecurity sophistication
- Can be applied to software developed to support information technology (IT), industrial
control systems (ICS), cyber-physical systems (CPS), or the Internet of Things (IoT)
- Can be integrated into any existing software development workflow and automated
toolchain; should not negatively affect organizations that already have robust secure
software development practices in place
- Makes the practices broadly applicable, not specific to particular technologies, platforms,
programming languages, SDLC models, development environments, operating
environments, tools, etc.
- Can help an organization document its secure software development practices today and
define its future target practices as part of its continuous improvement process
- Can assist an organization currently using a classic software development model in
transitioning its secure software development practices for use with a modern software
development model (e.g., agile, DevOps)
- Can assist organizations that are procuring and using software to understand secure
software development practices employed by their suppliers

This document provides a common language to describe fundamental secure software
development practices. This is similar to the approach taken by the Framework for Improving
Critical Infrastructure Cybersecurity, also known as the NIST Cybersecurity Framework
[NISTCSF]. 2 Expertise in secure software development is not required to understand the
practices. The common language helps facilitate communications about secure software practices
among both internal and external organizational stakeholders, such as:

- Business owners, software developers, project managers and leads, cybersecurity
professionals, and operations and platform engineers within an organization who need to
clearly communicate with each other about secure software development
- Software acquirers, including federal agencies and other organizations, that want to
define required or desired characteristics for software in their acquisition processes in
order to have higher-quality software (particularly with fewer significant security
vulnerabilities) 3

The SSDF practices may help support the NIST Cybersecurity Framework Functions, Categories, and Subcategories, but the
SSDF practices do not map to them and are typically the responsibility of different parties. Developers can adopt SSDF
practices, and the outcomes of their work could help organizations with their operational security in support of the
Cybersecurity Framework.

Future work may provide more practical guidance for software acquirers on how they can leverage the SSDF in specific use
cases.


Software producers (e.g., commercial-off-the-shelf [COTS] product vendors,
government-off-the-shelf [GOTS] software developers, software developers working
within or on behalf of software acquirer organizations) that want to integrate secure
software development practices throughout their SDLCs, express their secure software
practices to their customers, or define requirements for their suppliers


This document’s practices are not based on the assumption that all organizations have the same
security objectives and priorities. Rather, the recommendations reflect that each software
producer may have unique security assumptions, and each software acquirer may have unique
security needs and requirements. While the aim is for each software producer to follow all
applicable practices, the expectation is that the degree to which each practice is implemented and
the formality of the implementation will vary based on the producer’s security assumptions. The
practices provide flexibility for implementers, but they are also clear to avoid leaving too much
open to interpretation.

Although most of these practices are relevant to any software development effort, some are not.
For example, if developing a particular piece of software does not involve using a compiler,
there would be no need to follow a practice on configuring the compiler to improve executable
security. Some practices are foundational, while others are more advanced and depend on certain
foundational practices already being in place. Also, practices are not all equally important for all
cases.

Factors such as risk, cost, feasibility, and applicability should be considered when deciding
which practices to use and how much time and resources to devote to each practice. 4
Automatability is also an important factor to consider, especially for implementing practices at
scale. The practices, tasks, and implementation examples represent a starting point to consider;
they are meant to be changed and customized, and they are not prioritized. Any stated frequency
for performing practices is notional. The intention of the SSDF is not to create a checklist to
follow, but to provide a basis for planning and implementing a risk-based approach to adopting
secure software development practices.
The responsibility for implementing the practices may be distributed among different
organizations based on the delivery of the software and services (e.g., infrastructure as a service,
software as a service, platform as a service, container as a service, serverless). In these situations,
it likely follows a shared responsibility model involving the platform/service providers and the
tenant organization that is consuming those platforms/services. The tenant organization should
establish an agreement with the providers that specifies which party is responsible for each
practice and task and how each provider will attest to their conformance with the agreement.

Organizations seeking guidance on how to get started with secure software development can consult many publicly available
references, such as “SDL That Won’t Break the Bank” by Steve Lipner from SAFECode (https://i.blackhat.com/us-18/ThuAugust-9/us-18-Lipner-SDL-For-The-Rest-Of-Us.pdf), “Application Software Security and the CIS Controls: A Reference
Paper” by Steve Lipner and Stacy Simpson from SAFECode (https://safecode.org/resource-publications/cis-controls/), and
“Simplified Implementation of the Microsoft SDL” by Microsoft (https://www.microsoft.com/enus/download/details.aspx?id=12379).


## The Secure Software Development Framework

This document defines version 1.1 of the Secure Software Development Framework (SSDF)
with fundamental, sound, and secure recommended practices based on established secure
software development practice documents. The practices are organized into four groups:

1. Prepare the Organization (PO): Organizations should ensure that their people,
processes, and technology are prepared to perform secure software development at the
organization level. Many organizations will find some PO practices to also be applicable
to subsets of their software development, like individual development groups or projects.
2. Protect the Software (PS): Organizations should protect all components of their
software from tampering and unauthorized access.
3. Produce Well-Secured Software (PW): Organizations should produce well-secured
software with minimal security vulnerabilities in its releases.
4. Respond to Vulnerabilities (RV): Organizations should identify residual vulnerabilities
in their software releases and respond appropriately to address those vulnerabilities and
prevent similar ones from occurring in the future.

Each practice definition includes the following elements:
- Practice
  - The name of the practice and a unique identifier, followed by a brief
  explanation of what the practice is and why it is beneficial
- Tasks
  - One or more actions that may be needed to perform a practice
- Notional Implementation Examples
  - One or more notional examples of types of tools,
  processes, or other methods that could be used to help implement a task. No examples or
  combination of examples are required, and the stated examples are not the only feasible
  options. Some examples may not be applicable to certain organizations and situations.
- References
  - Pointers to one or more established secure development practice documents
  and their mappings to a particular task. Not all references will apply to all instances of
  software development.

Table 1 defines the practices. They are only a subset of what an organization may need to do.
The information in the table is space constrained; much more information on each practice can
be found in the references. Note that the order of the practices, tasks, and notional
implementation examples in the table is not intended to imply the sequence of implementation or
the relative importance of any practice, task, or example.
The table uses terms like “sensitive data,” “qualified person,” and “well-secured,” which are not
defined in this publication. Organizations adopting the SSDF should define these terms in the
context of their own environments and use cases. The same is true for the names of
environments, like “development,” “build,” “staging,” “integration,” “test,” “production,” and
“distribution,” which vary widely among organizations and projects. Enumerating your
environments is necessary in order to secure them properly, and especially to prevent lateral
movement of attackers from environment to environment.

Table 1: The Secure Software Development Framework (SSDF) Version 1.1

See [nist-ssdf-practices.md](nist-ssdf-practices.md)

## References

This publication is available free of charge from: https://doi.org/10.6028/NIST.SP.800-218

[BSAFSS]

BSA (2020) The BSA Framework for Secure Software: A New Approach to
Securing the Software Lifecycle, Version 1.1. Available at
https://www.bsa.org/files/reports/bsa_framework_secure_software_update
_2020.pdf

[BSIMM]

Migues S, Erlikhman E, Ewers J, Nassery K (2021) BSIMM12 2021
Foundations Report. Available at
https://www.bsimm.com/content/dam/bsimm/reports/bsimm12foundations.pdf

[CNCFSSCP]

Cloud Native Computing Foundation (2021) Software Supply Chain Best
Practices. Available at https://github.com/cncf/tagsecurity/tree/main/supply-chain-security/supply-chain-security-paper

[EO14028]

Executive Order 14028 (2021) Improving the Nation’s Cybersecurity. (The
White House, Washington, DC), DCPD-202100401, May 12, 2021.
https://www.govinfo.gov/app/details/DCPD-202100401

[IDASOAR]

Hong Fong EK, Wheeler D, Henninger A (2016) State-of-the-Art
Resources (SOAR) for Software Vulnerability Detection, Test, and
Evaluation 2016. (Institute for Defense Analyses [IDA], Alexandria, VA),
IDA Paper P-8005. Available at https://www.ida.org/research-andpublications/publications/all/s/st/stateoftheart-resources-soar-for-softwarevulnerability-detection-test-and-evaluation-2016

[IEC62443]

International Electrotechnical Commission (IEC), Security for industrial
automation and control systems – Part 4-1: Secure product development
lifecycle requirements, IEC 62443-4-1, 2018. Available at
https://webstore.iec.ch/publication/33615

[IR7692]

Waltermire DA, Scarfone KA, Casipe M (2011) Specification for the Open
Checklist Interactive Language (OCIL) Version 2.0. (National Institute of
Standards and Technology, Gaithersburg, MD), NIST Interagency or
Internal Report (IR) 7692. https://doi.org/10.6028/NIST.IR.7692

[IR7864]

LeMay E, Scarfone KA, Mell PM (2012) The Common Misuse Scoring
System (CMSS): Metrics for Software Feature Misuse Vulnerabilities.
(National Institute of Standards and Technology, Gaithersburg, MD), NIST
Interagency or Internal Report (IR) 7864.
https://doi.org/10.6028/NIST.IR.7864

[IR8397]

Black P, Guttman B, Okun V (2021) Guidelines on Minimum Standards
for Developer Verification of Software. (National Institute of Standards
and Technology, Gaithersburg, MD), NIST Interagency or Internal Report
(IR) 8397. https://doi.org/10.6028/NIST.IR.8397

[ISO27034]

International Organization for Standardization (ISO)/International
Electrotechnical Commission (IEC), Information technology – Security
techniques – Application security – Part 1: Overview and concepts,
ISO/IEC 27034-1:2011, 2011. Available at
https://www.iso.org/standard/44378.html

[ISO29147]

International Organization for Standardization (ISO)/International
Electrotechnical Commission (IEC), Information technology – Security
techniques – Vulnerability disclosure, ISO/IEC 29147:2018, 2018.
Available at https://www.iso.org/standard/72311.html

[ISO30111]

International Organization for Standardization (ISO)/International
Electrotechnical Commission (IEC), Information technology – Security
techniques – Vulnerability handling processes, ISO/IEC 30111:2019, 2019.
Available at https://www.iso.org/standard/69725.html

[MSSDL]

Microsoft (2021) Security Development Lifecycle. Available at
https://www.microsoft.com/en-us/securityengineering/sdl/

[NISTCSF]

National Institute of Standards and Technology (2018) Framework for
Improving Critical Infrastructure Cybersecurity, Version 1.1. (National
Institute of Standards and Technology, Gaithersburg, MD).
https://doi.org/10.6028/NIST.CSWP.04162018

[NISTLABEL]

Ogata M, Haney J, Merkel W, Phelps A (2022) Recommended Criteria for
Cybersecurity Labeling of Consumer Software. (National Institute of
Standards and Technology, Gaithersburg, MD). Available at
https://www.nist.gov/itl/executive-order-improving-nations-cybersecurity

[NTIASBOM]

National Telecommunications and Information Administration (NTIA)
(2021) The Minimum Elements For a Software Bill of Materials (SBOM).
Available at https://www.ntia.doc.gov/report/2021/minimum-elementssoftware-bill-materials-sbom

[OWASPASVS]

Open Web Application Security Project (2021) OWASP Application
Security Verification Standard 4.0.3. Available at
https://github.com/OWASP/ASVS

[OWASPMASVS] Open Web Application Security Project (2021) OWASP Mobile
Application Security Verification Standard, Version 1.4.2. Available at
https://github.com/OWASP/owasp-masvs/releases
[OWASPSAMM]

Open Web Application Security Project (2017) Software Assurance
Maturity Model Version 1.5. Available at
https://www.owasp.org/index.php/OWASP_SAMM_Project

[OWASPSCVS]

Open Web Application Security Project (2020) OWASP Software
Component Verification Standard, Version 1.0. Available at
https://github.com/OWASP/Software-Component-Verification-Standard

[PCISSLC]

Payment Card Industry (PCI) Security Standards Council (2021) Secure
Software Lifecycle (Secure SLC) Requirements and Assessment Procedures
Version 1.1. Available at
https://www.pcisecuritystandards.org/document_library?category=sware_s
ec#results

[SCAGILE]

Software Assurance Forum for Excellence in Code (2012) Practical
Security Stories and Security Tasks for Agile Development Environments.
Available at
http://www.safecode.org/publication/SAFECode_Agile_Dev_Security0712
.pdf

[SCFPSSD]

Software Assurance Forum for Excellence in Code (2018) Fundamental
Practices for Secure Software Development: Essential Elements of a
Secure Development Lifecycle Program, Third Edition. Available at
https://safecode.org/wpcontent/uploads/2018/03/SAFECode_Fundamental_Practices_for_Secure_
Software_Development_March_2018.pdf

[SCSIC]

Software Assurance Forum for Excellence in Code (2010) Software
Integrity Controls: An Assurance-Based Approach to Minimizing Risks in
the Software Supply Chain. Available at
http://www.safecode.org/publication/SAFECode_Software_Integrity_Cont
rols0610.pdf

[SCTPC]

Software Assurance Forum for Excellence in Code (2017) Managing
Security Risks Inherent in the Use of Third-Party Components. Available
at https://www.safecode.org/wpcontent/uploads/2017/05/SAFECode_TPC_Whitepaper.pdf

[SCTTM]

Software Assurance Forum for Excellence in Code (2017) Tactical Threat
Modeling. Available at https://www.safecode.org/wpcontent/uploads/2017/05/SAFECode_TM_Whitepaper.pdf

[SP80053]

Joint Task Force (2020) Security and Privacy Controls for Information
Systems and Organizations. (National Institute of Standards and
Technology, Gaithersburg, MD), NIST Special Publication (SP) 800-53,
Rev. 5. Includes updates as of December 10, 2020.
https://doi.org/10.6028/NIST.SP.800-53r5

[SP800160]

Ross R, McEvilley M, Oren J (2016) Systems Security Engineering:
Considerations for a Multidisciplinary Approach in the Engineering of
Trustworthy Secure Systems. (National Institute of Standards and
Technology, Gaithersburg, MD), NIST Special Publication (SP) 800-160,
Volume 1. Includes updates as of March 21, 2018.
https://doi.org/10.6028/NIST.SP.800-160v1

[SP800161]

Boyens J, Smith A, Bartol N, Winkler K, Holbrook A, Fallon M (2021)
Cybersecurity Supply Chain Risk Management Practices for Systems and
Organizations. (National Institute of Standards and Technology,
Gaithersburg, MD), Second Draft NIST Special Publication (SP) 800-161,
Rev. 1. https://doi.org/10.6028/NIST.SP.800-161r1-draft2

[SP800181]

Newhouse W, Keith S, Scribner B, Witte G (2017) National Initiative for
Cybersecurity Education (NICE) Cybersecurity Workforce Framework.
(National Institute of Standards and Technology, Gaithersburg, MD), NIST
Special Publication (SP) 800-181. https://doi.org/10.6028/NIST.SP.800181

[SP800216]

Schaffer K, Mell P, Trinh H (2021) Recommendations for Federal
Vulnerability Disclosure Guidelines. (National Institute of Standards and
Technology, Gaithersburg, MD), Draft NIST Special Publication (SP) 800216. https://doi.org/10.6028/NIST.SP.800-216-draft

## Appendix A - The SSDF and Executive Order 14028 

Removed in this Markdown Version, please see original

## Appendix B - Acronyms

Selected acronyms and abbreviations used in this document are defined below.


BSIMM - Building Security In Maturity Model

CISQ - Consortium for Information & Software Quality

CNCF - Cloud Native Computing Foundation

COTS - Commercial-Off-the-Shelf

CPS - Cyber-Physical System

DevOps - Development and Operations

EO - Executive Order

GOTS - Government-Off-the-Shelf

GSA - General Services Administration

ICS - Industrial Control System

IDA - Institute for Defense Analyses

IEC - International Electrotechnical Commission

IoT - Internet of Things

IR - Interagency or Internal Report

ISO - International Organization for Standardization

ISPAB - Information Security and Privacy Advisory Board

IT - Information Technology

ITL - Information Technology Laboratory

KPI - Key Performance Indicator

KRI - Key Risk Indicator

MITA - Medical Imaging & Technology Alliance

NAVSEA - Naval Sea Systems Command

NICE - National Initiative for Cybersecurity Education

NIST - National Institute of Standards and Technology

NTIA - National Telecommunications and Information Administration

OLIR - National Online Informative References Program

OWASP - Open Web Application Security Project

PCI - Payment Card Industry

PSIRT - Product Security Incident Response Team

SAFECode - Software Assurance Forum for Excellence in Code

SAMM - Software Assurance Maturity Model

SBOM - Software Bill of Materials

SDL - [Microsoft] Security Development Lifecycle

SDLC - Software Development Life Cycle

SEI - Software Engineering Institute

SLC - Software Lifecycle

