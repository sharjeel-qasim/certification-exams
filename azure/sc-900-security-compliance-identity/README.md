# SC-900: Microsoft Security, Compliance, and Identity Fundamentals — Practice Question Bank

[![Azure](https://img.shields.io/badge/Microsoft_Azure-0089D6?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/)
[![Exam](https://img.shields.io/badge/Exam-SC--900-blue?style=for-the-badge)](#table-of-contents)
[![Questions](https://img.shields.io/badge/Questions-50%20Verified%20Questions-success?style=for-the-badge)](#table-of-contents)
[![Cheat Sheet](https://img.shields.io/badge/Study_Guide-Cheat_Sheet-orange?style=for-the-badge)](CHEAT_SHEET.md)

Comprehensive practice question bank for the **Microsoft Certified: Security, Compliance, and Identity Fundamentals (SC-900)** exam. Verified against official Microsoft Learn practice assessments, official exam objectives, and domain guidelines.

> [!TIP]
> Preparing for the exam? Review the [SC-900 Last-Minute Cram Sheet](CHEAT_SHEET.md) for Zero Trust principles, Shared Responsibility matrix, Microsoft Defender XDR breakdown, Sentinel SIEM/SOAR components, and Purview compliance features.

---

## Table of Contents

- [Domain 1: Concepts of Security, Compliance, and Identity (Q1 – Q12)](#domain-1-concepts-of-security-compliance-and-identity)
- [Domain 2: Capabilities of Microsoft Entra (Identity & Access Management) (Q13 – Q25)](#domain-2-capabilities-of-microsoft-entra-identity--access-management)
- [Domain 3: Capabilities of Microsoft Security Solutions (Q26 – Q39)](#domain-3-capabilities-of-microsoft-security-solutions)
- [Domain 4: Capabilities of Microsoft Compliance Solutions (Q40 – Q50)](#domain-4-capabilities-of-microsoft-compliance-solutions)

---

## Domain 1: Concepts of Security, Compliance, and Identity

### Question 1
For each of the following statements about the guiding principles of Zero Trust, select **Yes** if the statement is true, otherwise select **No**:

| Statement | Answer |
| :--- | :---: |
| "Verify explicitly" is one of the guiding principles of Zero Trust. | **Yes** |
| "Assume breach" is one of the guiding principles of Zero Trust. | **Yes** |
| Zero Trust assumes that all traffic originating inside the corporate network is inherently trusted. | **No** |

> **Why:**
> - **Statement 1 (Yes):** "Verify explicitly" is the first core pillar (always authenticate and authorize based on all available data points).
> - **Statement 2 (Yes):** "Assume breach" is the third core pillar (minimize blast radius and segment access).
> - **Statement 3 (No):** Zero Trust fundamentally eliminates the concept of an "inherently trusted internal network."

---

### Question 2
What is the customer always responsible for securing across **all** cloud deployment models (IaaS, PaaS, and SaaS)?

- **A.** Operating system patching
- **B.** Physical datacenter security
- **C.** Data, user accounts, and identities
- **D.** Network virtualization and hypervisor security

**Correct answer:** C

> **Why:** Under the Shared Responsibility Model, the customer retains 100% responsibility for data governance, accounts, identities, and client devices regardless of whether IaaS, PaaS, or SaaS is used.

---

### Question 3
An organization evaluates a **Software as a Service (SaaS)** solution (such as Microsoft 365). Which security responsibility remains with the customer?

- **A.** Physical server hardware maintenance
- **B.** Managing user accounts, identities, and data access policies
- **C.** Operating system updates and patches
- **D.** Hypervisor virtualization management

**Correct answer:** B

> **Why:** In a SaaS model, the cloud provider manages infrastructure, operating systems, and application code. The customer remains solely responsible for managing their users, accounts, and access permissions.

---

### Question 4
Which security concept utilizes multiple layers of defensive controls (Physical, Identity, Perimeter, Network, Compute, Application, Data) so that if one layer fails, subsequent layers protect the asset?

- **A.** Single Sign-On (SSO)
- **B.** Defense in Depth
- **C.** Federation
- **D.** Asymmetric encryption

**Correct answer:** B

> **Why:** Defense in Depth implements layered security mechanisms across multiple rings of defense to slow down attackers and prevent unauthorized access.

---

### Question 5
When a user provides their username and password to log into a portal, which security process is taking place?

- **A.** Authorization
- **B.** Auditing
- **C.** Authentication
- **D.** Federation

**Correct answer:** C

> **Why:** Authentication is the process of proving that an identity is who they claim to be (verifying credentials). Authorization determines what resources the authenticated identity is permitted to access.

---

### Question 6
Which component of the CIA Triad ensures that sensitive financial data cannot be viewed or accessed by unauthorized individuals?

- **A.** Confidentiality
- **B.** Integrity
- **C.** Availability
- **D.** Non-repudiation

**Correct answer:** A

> **Why:** Confidentiality prevents unauthorized disclosure of information. Integrity prevents unauthorized modification, and Availability ensures authorized users have timely access.

---

### Question 7
Which type of cyber attack involves an attacker attempting common passwords against a large list of known usernames to avoid account lockout thresholds?

- **A.** Distributed Denial of Service (DDoS)
- **B.** Password Spraying
- **C.** Man-in-the-Middle (MitM)
- **D.** SQL Injection

**Correct answer:** B

> **Why:** Password spraying attempts a small number of commonly used passwords against many user accounts to bypass account lockout policies triggered by rapid brute-force attempts on a single account.

---

### Question 8
For each of the following statements about encryption, select **Yes** if the statement is true, otherwise select **No**:

| Statement | Answer |
| :--- | :---: |
| Symmetric encryption uses the same cryptographic key for both encryption and decryption. | **Yes** |
| Asymmetric encryption uses a public key to encrypt and a mathematically linked private key to decrypt. | **Yes** |
| Hashing is a two-way mathematical function that can be easily decrypted back to plaintext. | **No** |

> **Why:**
> - **Statement 1 (Yes):** Symmetric algorithms (e.g. AES) share a single secret key.
> - **Statement 2 (Yes):** Asymmetric algorithms (e.g. RSA) use public/private key pairs.
> - **Statement 3 (No):** Hashing (e.g. SHA-256) is strictly a one-way deterministic mathematical function used for integrity verification.

---

### Question 9
Which term refers to establishing a trust relationship between two distinct identity providers so that users can access resources across organizational boundaries using their existing corporate credentials?

- **A.** Role-Based Access Control (RBAC)
- **B.** Federation
- **C.** Symmetric encryption
- **D.** Multi-Factor Authentication

**Correct answer:** B

> **Why:** Federation links two independent identity systems (e.g. Entra ID and an on-premises AD FS or Google Workspace) through a trust relationship to enable cross-domain Single Sign-On (SSO).

---

### Question 10
In the Zero Trust model, which principle focuses on limiting user permissions to only what is required to perform a specific task for a limited time?

- **A.** Verify explicitly
- **B.** Use least privilege access
- **C.** Assume breach
- **D.** Perimeter defense

**Correct answer:** B

> **Why:** Least Privilege Access enforces Just-In-Time (JIT) and Just-Enough-Access (JEA) to minimize the risk of lateral movement and over-privileged credentials.

---

### Question 11
Which two industry standard security and compliance benchmarks are integrated into the Azure Security Benchmark?

*Choose 2 answers*

- **A.** Center for Internet Security (CIS) Controls
- **B.** ISO 9001 Quality Management
- **C.** Apache 2.0 Licensing Guidelines
- **D.** National Institute of Standards and Technology (NIST) SP 800-53

**Correct answers:** A, D

> **Why:** The Microsoft Cloud Security Benchmark is mapped directly to **CIS Controls** and **NIST SP 800-53** security frameworks.

---

### Question 12
For each of the following statements regarding threat intelligence and posture management, select **Yes** if true, otherwise select **No**:

| Statement | Answer |
| :--- | :---: |
| A security posture reflects an organization's overall cybersecurity readiness and defense health. | **Yes** |
| Vulnerability management identifies, evaluates, and remediates security weaknesses before attackers exploit them. | **Yes** |
| Security compliance guarantees that an organization is 100% immune to all zero-day cyber attacks. | **No** |

> **Why:**
> - **Statements 1 & 2 (Yes):** Posture measures readiness, and vulnerability management proactively patches security flaws.
> - **Statement 3 (No):** Compliance ensures adherence to standards and regulations, but cannot guarantee absolute immunity from zero-day exploits.

---

## Domain 2: Capabilities of Microsoft Entra (Identity & Access Management)

### Question 13
You need to provide temporary, time-bound administrator access to an engineer to troubleshoot an Azure production issue. The access must expire automatically after 4 hours and require justification upon activation. What should you use?

- **A.** Azure Role-Based Access Control (RBAC) permanent role assignment
- **B.** Microsoft Entra Privileged Identity Management (PIM)
- **C.** Microsoft Entra Password Protection
- **D.** Microsoft Entra Application Proxy

**Correct answer:** B

> **Why:** Microsoft Entra PIM provides Just-In-Time (JIT) privileged access management with time-limited activation (e.g. 4 hours), MFA requirements, approval workflows, and audit logging.

---

### Question 14
You need to configure an automated policy that requires users signing in from an untrusted location or high-risk IP address to perform Multi-Factor Authentication (MFA). Which Microsoft Entra capability should you configure?

- **A.** Conditional Access
- **B.** Access Reviews
- **C.** Self-Service Password Reset (SSPR)
- **D.** Entra Connect

**Correct answer:** A

> **Why:** Conditional Access analyzes real-time signals (user, location, device compliance, risk score) and enforces decisions (e.g. require MFA or block access).

---

### Question 15
What should you use to associate a single managed identity with **more than one** Azure virtual machine?

- **A.** A Microsoft Entra user account
- **B.** A system-assigned managed identity
- **C.** A service principal created in an on-premises domain controller
- **D.** A user-assigned managed identity

**Correct answer:** D

> **Why:** A **user-assigned managed identity** is created as an independent standalone Azure resource that can be assigned to multiple Azure VMs and resources simultaneously. System-assigned managed identities are tied to a single resource.

---

### Question 16
For each of the following statements about Microsoft Entra Managed Identities, select **Yes** if true, otherwise select **No**:

| Statement | Answer |
| :--- | :---: |
| System-assigned managed identities are automatically deleted when the associated Azure resource is deleted. | **Yes** |
| Managed identities eliminate the need for developers to manage credentials in application code. | **Yes** |
| User-assigned managed identities can only be assigned to a single Azure resource during their lifecycle. | **No** |

> **Why:**
> - **Statement 1 (Yes):** System-assigned identities share the lifecycle of the parent resource.
> - **Statement 2 (Yes):** Azure handles authentication token requests automatically via Entra ID, removing embedded secrets from source code.
> - **Statement 3 (No):** User-assigned identities can be assigned to multiple Azure resources.

---

### Question 17
Which tool should you use to synchronize on-premises Active Directory Domain Services (AD DS) user accounts, groups, and password hashes with Microsoft Entra ID?

- **A.** Microsoft Entra Connect (or Entra Cloud Sync)
- **B.** Microsoft Sentinel
- **C.** Azure Arc
- **D.** Active Directory Federation Services (AD FS)

**Correct answer:** A

> **Why:** Microsoft Entra Connect synchronizes identities, attributes, and password hashes between on-premises AD DS and cloud-based Microsoft Entra ID for hybrid identity.

---

### Question 18
Which passwordless authentication method provided by Microsoft Entra ID allows users to sign in using biometric authentication (face or fingerprint) tied to a specific Windows 11 hardware device?

- **A.** SMS text message verification
- **B.** Windows Hello for Business
- **C.** Email one-time passcode (OTP)
- **D.** Security Questions

**Correct answer:** B

> **Why:** Windows Hello for Business replaces passwords with strong two-factor authentication tied to a specific device using biometric verification or a PIN backed by a TPM chip.

---

### Question 19
What can be created and managed natively in on-premises **Active Directory Domain Services (AD DS)**?

- **A.** Computer accounts and organizational units (OUs)
- **B.** SaaS application connectors for third-party cloud apps
- **C.** Azure subscription role definitions
- **D.** Microsoft 365 group sensitivity labels

**Correct answer:** A

> **Why:** AD DS is a traditional on-premises directory service that manages domain-joined computer accounts, user accounts, security groups, and Organizational Units (OUs) using Kerberos and LDAP.

---

### Question 20
Which Microsoft Entra ID Governance feature allows administrators to periodically review and verify whether guest users and employees still require access to sensitive groups and applications?

- **A.** Microsoft Entra Access Reviews
- **B.** Conditional Access Named Locations
- **C.** Entra Password Protection
- **D.** Entra Verified ID

**Correct answer:** A

> **Why:** Access Reviews automate the recurring recertification of user and group memberships, ensuring that stale accounts or departed contractors lose unauthorized access.

---

### Question 21
What happens when a user attempts to sign into Microsoft Entra ID and their sign-in risk is evaluated as **High** by Microsoft Entra ID Protection?

- **A.** The user's password is automatically deleted.
- **B.** Conditional Access can trigger an automated block or force a secure password change via Multi-Factor Authentication.
- **C.** The user is granted administrator rights to investigate the incident.
- **D.** The Azure subscription is immediately placed into read-only mode.

**Correct answer:** B

> **Why:** Entra ID Protection feeds risk signals into Conditional Access to enforce automated remediation (such as requiring MFA + secure self-service password reset) or blocking high-risk sessions.

---

### Question 22
Which authentication protocol is standard for modern web application Single Sign-On (SSO) in Microsoft Entra ID?

- **A.** NTLM
- **B.** OpenID Connect (OIDC) / OAuth 2.0
- **C.** LDAP
- **D.** Telnet

**Correct answer:** B

> **Why:** Modern cloud identity platforms like Microsoft Entra ID use OpenID Connect (OIDC) for authentication and OAuth 2.0 for API authorization over HTTPS.

---

### Question 23
You need to prevent users in your organization from setting easily guessable passwords such as "Spring2026!" or common company names. Which Microsoft Entra ID feature should you implement?

- **A.** Entra Password Protection (Global & Custom Banned Password Lists)
- **B.** Microsoft Entra PIM
- **C.** Azure Bastion
- **D.** Entra External ID

**Correct answer:** A

> **Why:** Microsoft Entra Password Protection automatically blocks globally banned weak passwords and allows organizations to enforce custom banned wordlists across both cloud and on-premises AD.

---

### Question 24
What is the primary function of **Microsoft Entra External ID** (B2B and B2C collaboration)?

- **A.** To enable secure collaboration with external partners, suppliers, and customer accounts using their own identities.
- **B.** To format local hard drives on client workstations.
- **C.** To manage physical building turnstiles and badge scanners.
- **D.** To configure DNS records on cloud domain registrars.

**Correct answer:** A

> **Why:** Microsoft Entra External ID allows businesses to securely share internal applications and resources with external partners (B2B) or build consumer-facing applications (B2C/CIAM).

---

### Question 25
For each of the following statements about Microsoft Entra ID roles and Azure RBAC roles, select **Yes** if true, otherwise select **No**:

| Statement | Answer |
| :--- | :---: |
| Microsoft Entra roles (e.g. Global Administrator) control access to Microsoft Entra directory resources and Microsoft 365 services. | **Yes** |
| Azure RBAC roles (e.g. Owner, Contributor) control access to Azure infrastructure resources (VMs, Storage, Databases). | **Yes** |
| A Global Administrator in Entra ID automatically has permanent full Owner access to all Azure subscription resources by default. | **No** |

> **Why:**
> - **Statements 1 & 2 (Yes):** Entra roles manage tenant/identity objects; Azure RBAC roles manage Azure infrastructure resource hierarchies.
> - **Statement 3 (No):** Entra ID and Azure Resource Manager have distinct permission planes. A Global Admin does not have Azure subscription Owner permissions by default (they must explicitly elevate access to manage subscriptions if needed).

---

## Domain 3: Capabilities of Microsoft Security Solutions

### Question 26
Which cloud-native SIEM (Security Information and Event Management) and SOAR (Security Orchestration, Automated Response) service in Azure aggregates security data across the enterprise?

- **A.** Microsoft Defender for Endpoint
- **B.** Microsoft Sentinel
- **C.** Azure Key Vault
- **D.** Azure Network Watcher

**Correct answer:** B

> **Why:** Microsoft Sentinel is Azure's cloud-native SIEM and SOAR solution for intelligent security analytics, log ingestion, threat detection, hunting, and automated incident remediation.

---

### Question 27
In Microsoft Sentinel, which component provides automated, play-by-play incident response and remediation workflows powered by Azure Logic Apps?

- **A.** Workbooks
- **B.** Playbooks
- **C.** Data Connectors
- **D.** Jupyter Notebooks

**Correct answer:** B

> **Why:** Sentinel Playbooks are automated workflows built on Azure Logic Apps that execute automated response steps (e.g. isolating an infected VM, disabling a compromised user account).

---

### Question 28
Which service provides **Cloud Security Posture Management (CSPM)** and calculates the overall **Secure Score** across your Azure, AWS, and GCP subscriptions?

- **A.** Microsoft Defender for Cloud
- **B.** Microsoft Defender for Office 365
- **C.** Azure Bastion
- **D.** Azure Virtual Network NAT

**Correct answer:** A

> **Why:** Microsoft Defender for Cloud continuously monitors hybrid and multi-cloud infrastructure, assesses resources against security benchmarks, and displays the overall subscription **Secure Score**.

---

### Question 29
Which product within the Microsoft Defender XDR suite specifically provides **Endpoint Detection and Response (EDR)**, device vulnerability management, and **Microsoft Secure Score for Devices**?

- **A.** Microsoft Defender for Endpoint
- **B.** Microsoft Defender for Identity
- **C.** Microsoft Defender for Cloud Apps
- **D.** Azure DDoS Protection

**Correct answer:** A

> **Why:** Microsoft Defender for Endpoint protects client operating systems (Windows, macOS, Linux, Android, iOS) with antivirus, EDR, behavioral blocking, and device secure scoring.

---

### Question 30
You need to detect suspicious on-premises Active Directory reconnaissance activities, such as pass-the-hash and unauthorized domain controller replication. Which Microsoft Defender service should you deploy?

- **A.** Microsoft Defender for Identity
- **B.** Microsoft Defender for Office 365
- **C.** Azure Web Application Firewall
- **D.** Microsoft Defender for Storage

**Correct answer:** A

> **Why:** Microsoft Defender for Identity monitors on-premises Active Directory Domain Controllers to detect advanced threats, compromised credentials, and insider reconnaissance activities.

---

### Question 31
Which service in Microsoft Defender XDR provides discovery of Shadow IT applications, monitors user activities in third-party SaaS apps (like Salesforce and Box), and enforces app governance?

- **A.** Microsoft Defender for Cloud Apps (MDCA)
- **B.** Microsoft Defender for Endpoint
- **C.** Azure Bastion
- **D.** Azure Front Door

**Correct answer:** A

> **Why:** Defender for Cloud Apps is a Cloud Access Security Broker (CASB) that discovers shadow IT apps via firewall/endpoint log collectors and governs data in cloud applications.

---

### Question 32
To which type of resource can **Azure Bastion** provide secure, seamless RDP and SSH connectivity directly through a web browser without exposing public IP addresses?

- **A.** Azure App Service web apps
- **B.** Azure SQL Database
- **C.** Azure Virtual Machines
- **D.** Azure Storage Accounts

**Correct answer:** C

> **Why:** Azure Bastion is a fully managed PaaS service that provides secure browser-based TLS/RDP/SSH connectivity directly to Azure Virtual Machines inside a virtual network without public IPs on the VMs.

---

### Question 33
Which Azure security service provides centralized Layer 7 protection for web applications against common web vulnerabilities and exploits, such as SQL Injection (SQLi) and Cross-Site Scripting (XSS)?

- **A.** Azure Network Security Groups (NSGs)
- **B.** Azure Web Application Firewall (WAF)
- **C.** Azure Key Vault
- **D.** Azure ExpressRoute

**Correct answer:** B

> **Why:** Azure WAF protects web applications hosted behind Application Gateway, Azure Front Door, or Azure CDN from web vulnerabilities defined in OWASP Top 10 rulesets (SQLi, XSS).

---

### Question 34
What is the primary function of **Azure Key Vault**?

- **A.** To store and tightly control access to secrets, encryption keys, and SSL/TLS certificates.
- **B.** To inspect network traffic passing through virtual routers.
- **C.** To scan container images in Docker Hub for known vulnerabilities.
- **D.** To provide distributed database caching.

**Correct answer:** A

> **Why:** Azure Key Vault provides a secure, hardware-backed repository for storing and managing cryptographic keys, API tokens, database connection strings, and certificates.

---

### Question 35
For each of the following statements about Microsoft Sentinel, select **Yes** if true, otherwise select **No**:

| Statement | Answer |
| :--- | :---: |
| Microsoft Sentinel Data Connectors can ingest security logs from non-Microsoft environments, such as AWS CloudTrail and Syslog. | **Yes** |
| Sentinel Workbooks provide interactive visualizations and dashboards for analyzing log telemetry. | **Yes** |
| Sentinel requires an on-premises physical server appliance to be installed in every office datacenter. | **No** |

> **Why:**
> - **Statements 1 & 2 (Yes):** Sentinel is cloud-native, connects out-of-the-box to AWS/Syslog, and uses Workbooks for visualization.
> - **Statement 3 (No):** Microsoft Sentinel is 100% cloud-native serverless built on Azure Monitor Log Analytics.

---

### Question 36
Which two cards are available in the Microsoft Defender portal home dashboard to provide immediate security posture insight?

*Choose 2 answers*

- **A.** Users at risk
- **B.** Devices at risk
- **C.** Local weather forecast
- **D.** Printer spooler queue

**Correct answers:** A, B

> **Why:** The unified Microsoft Defender portal displays prioritized overview cards including **Users at risk**, **Devices at risk**, Incidents & alerts, and Secure Score.

---

### Question 37
What does a high **Secure Score** in Microsoft Defender for Cloud indicate?

- **A.** The subscription is experiencing high network latency.
- **B.** The organization has implemented a larger proportion of recommended security best practices and posture hardening actions.
- **C.** All virtual machines are utilizing maximum CPU power.
- **D.** The Azure bill is discounted.

**Correct answer:** B

> **Why:** Secure Score quantifies your security posture; completing prioritized improvement recommendations (e.g. enabling MFA, restricting ports) increases the score.

---

### Question 38
In Microsoft Sentinel, which tool allows security analysts to perform advanced, programmatic threat hunting and data exploration using Python and KQL?

- **A.** Jupyter Notebooks
- **B.** Paint 3D
- **C.** Windows Command Prompt
- **D.** Notepad

**Correct answer:** A

> **Why:** Microsoft Sentinel integrates with Azure ML **Jupyter Notebooks** to give threat hunters full programmatic access to query, visualize, and model security event data.

---

### Question 39
Which Azure network security feature controls inbound and outbound network traffic to Azure VM network interfaces and subnets using 5-tuple rules (Source, Source Port, Destination, Destination Port, Protocol)?

- **A.** Network Security Groups (NSGs)
- **B.** Azure Service Bus
- **C.** Azure Traffic Manager
- **D.** Azure API Management

**Correct answer:** A

> **Why:** NSGs filter Layer 4 network traffic across subnets and VM network interfaces using priority-based 5-tuple security rules.

---

## Domain 4: Capabilities of Microsoft Compliance Solutions

### Question 40
What is an **Assessment** in Microsoft Purview Compliance Manager?

- **A.** A software code review performed by an automated compiler.
- **B.** A structured evaluation that assesses an organization's compliance posture against a specific regulatory standard (such as GDPR, ISO 27001, or NIST).
- **C.** A hardware diagnostics check on physical hard drives.
- **D.** An exam taken by employees at the end of the year.

**Correct answer:** B

> **Why:** Assessments in Purview Compliance Manager group controls and improvement actions aligned to specific regulatory frameworks (e.g. ISO 27001, GDPR) to measure compliance.

---

### Question 41
Match the Microsoft Purview **Insider Risk Management** components to their appropriate operational descriptions:

| Component | Description |
| :--- | :--- |
| **Policies** | Define conditions, risk indicators (e.g. downloading sensitive files before leaving the company), and users to monitor. |
| **Alerts** | Generated automatically when user activity matches the thresholds defined in an insider risk policy. |
| **Cases** | Created by investigators to conduct formal investigations, review evidence, and track remediation workflows. |

> **Why:** Insider Risk Management operates in three stages: **Policies** set detection criteria, triggers generate **Alerts**, and confirmed risks are escalated into **Cases** for investigation.

---

### Question 42
An organization needs to classify sensitive emails and Word documents by automatically applying watermarks, header tags, and AES-256 encryption based on content. Which Microsoft Purview feature should be deployed?

- **A.** Sensitivity Labels (Microsoft Purview Information Protection)
- **B.** Azure Bastion
- **C.** Microsoft Defender for Identity
- **D.** Microsoft Sentinel Data Connectors

**Correct answer:** A

> **Why:** Sensitivity Labels classify and protect corporate data across Microsoft 365 apps by applying visual markings (watermarks/headers) and persistent encryption.

---

### Question 43
You need to prevent employees from accidentally copying credit card numbers and passport details into Microsoft Teams chat messages or sharing them with external recipients. What should you configure?

- **A.** Microsoft Purview Data Loss Prevention (DLP)
- **B.** Azure DDoS Protection
- **C.** Microsoft Entra Application Proxy
- **D.** Azure Bastion

**Correct answer:** A

> **Why:** Purview DLP identifies sensitive information types (e.g. credit card numbers) and applies policies to warn users or block transmission across Teams, Exchange, SharePoint, and OneDrive.

---

### Question 44
On which client operating systems can **Microsoft Purview Endpoint Data Loss Prevention (Endpoint DLP)** be deployed to monitor and restrict file actions (e.g. copying sensitive files to USB or printing)?

- **A.** Windows only
- **B.** Windows and Android only
- **C.** Windows and macOS
- **D.** Linux only

**Correct answer:** C

> **Why:** Endpoint DLP is natively supported on **Windows 10/11** and **macOS** devices (onboarded via Microsoft Defender for Endpoint or Intune).

---

### Question 45
For each of the following statements about Microsoft Purview eDiscovery, select **Yes** if true, otherwise select **No**:

| Statement | Answer |
| :--- | :---: |
| eDiscovery search results can be exported and downloaded for external legal review. | **Yes** |
| Legal holds can be placed on mailboxes and SharePoint sites to preserve content from deletion during ongoing litigation. | **Yes** |
| eDiscovery automatically permanently deletes all files that contain the word "confidential." | **No** |

> **Why:**
> - **Statements 1 & 2 (Yes):** eDiscovery is designed to search, place legal holds on, and export relevant electronic evidence for legal counsel.
> - **Statement 3 (No):** eDiscovery identifies and preserves data; it does not automatically delete records.

---

### Question 46
Which Microsoft Purview feature uses machine learning algorithms to detect toxic language, harassment, regulatory infractions, and sensitive data leakage across corporate communication channels (Teams, Exchange)?

- **A.** Communication Compliance
- **B.** Azure Key Vault
- **C.** Microsoft Defender for Storage
- **D.** Azure Firewall

**Correct answer:** A

> **Why:** Purview Communication Compliance analyzes organizational communications for policy violations, harassment, adult content, and unauthorized sharing of confidential data.

---

### Question 47
Where can an organization's compliance officer download independent third-party SOC 1, SOC 2, and ISO audit reports verifying Microsoft's cloud security and regulatory compliance?

- **A.** Microsoft Service Trust Portal
- **B.** Google Play Store
- **C.** Azure Virtual Machine Boot Diagnostics
- **D.** GitHub Marketplace

**Correct answer:** A

> **Why:** The **Service Trust Portal** is Microsoft's public repository for third-party compliance audit reports, ISO/SOC certifications, and implementation blueprints.

---

### Question 48
For each of the following statements about Microsoft Purview Data Lifecycle Management, select **Yes** if true, otherwise select **No**:

| Statement | Answer |
| :--- | :---: |
| Retention policies can be configured to keep content for a specified period (e.g. 7 years) and then delete it automatically. | **Yes** |
| Retention labels can be applied manually by end users or automatically based on sensitive info types. | **Yes** |
| Retention policies only apply to on-premises file servers and cannot be applied to Microsoft Teams. | **No** |

> **Why:**
> - **Statements 1 & 2 (Yes):** Retention policies and labels govern how long content must be preserved or when it must be purged.
> - **Statement 3 (No):** Purview Retention policies natively protect cloud workloads including Exchange, SharePoint, OneDrive, and Teams.

---

### Question 49
What is the primary objective of **Data Classification** in Microsoft Purview?

- **A.** To identify, label, and understand the sensitivity of data across the corporate estate so appropriate protection policies can be enforced.
- **B.** To compress files into smaller RAR archives.
- **C.** To convert SQL databases into plain text CSV files.
- **D.** To measure internet download speed.

**Correct answer:** A

> **Why:** Data classification scans and identifies sensitive info types (PII, financial, medical) across documents and databases to apply targeted protection and governance.

---

### Question 50
Which Microsoft privacy principle states that customer data in Microsoft cloud services will never be used for advertising purposes without explicit consent?

- **A.** You are in control of your data
- **B.** Transparency on data location and use
- **C.** Strong security protections
- **D.** Strict physical access controls

**Correct answer:** A

> **Why:** Microsoft's core privacy commitment guarantees that customers own their data, that Microsoft only uses data to provide agreed cloud services, and that data is never scanned or monetized for advertising.
