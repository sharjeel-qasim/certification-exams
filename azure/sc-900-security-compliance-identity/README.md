# SC-900: Microsoft Security, Compliance, and Identity Fundamentals — Practice Question Bank

[![Azure](https://img.shields.io/badge/Microsoft_Azure-0089D6?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/)
[![Exam](https://img.shields.io/badge/Exam-SC--900-blue?style=for-the-badge)](#table-of-contents)
[![Questions](https://img.shields.io/badge/Questions-50%20Verified%20Questions-success?style=for-the-badge)](#table-of-contents)
[![Cheat Sheet](https://img.shields.io/badge/Study_Guide-Cheat_Sheet-orange?style=for-the-badge)](CHEAT_SHEET.md)

Comprehensive practice question bank for the **Microsoft Certified: Security, Compliance, and Identity Fundamentals (SC-900)** exam. Verified against official Microsoft Learn practice assessments, official exam objectives, and domain guidelines.

> ⚡ **Quick Review:** Check out the [**SC-900 Exam Cheat Sheet**](./CHEAT_SHEET.md) for a high-yield summary of Microsoft Entra, Defender, Purview, and Zero Trust exam concepts before testing yourself below.

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

| Statement | Yes / No |
| :--- | :---: |
| 1. "Verify explicitly" is one of the guiding principles of Zero Trust. | Yes / No |
| 2. "Assume breach" is one of the guiding principles of Zero Trust. | Yes / No |
| 3. Zero Trust assumes that all traffic originating inside the corporate network is inherently trusted. | Yes / No |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** Statement 1: **Yes** | Statement 2: **Yes** | Statement 3: **No**

> **Why:**
> - **Statement 1 (Yes):** "Verify explicitly" is the first core pillar of Zero Trust—every access request must be authenticated and authorized using all available signals (user identity, location, device health, service workload, and data classification).
> - **Statement 2 (Yes):** "Assume breach" is the third core pillar of Zero Trust (alongside "Use least privilege access")—organizations operate as if an attacker is already present by minimizing blast radius, enforcing micro-segmentation, using end-to-end encryption, and continuously monitoring analytics.
> - **Statement 3 (No):** Traditional perimeter ("castle-and-moat") networks implicitly trusted internal traffic, whereas Zero Trust eliminates implicit trust regardless of whether a user is on the corporate LAN or a public network.

</details>

---

### Question 2
What is the customer always responsible for securing across **all** cloud deployment models (IaaS, PaaS, and SaaS)?

- **A.** Operating system patching
- **B.** Physical datacenter security
- **C.** Data, user accounts, and identities
- **D.** Network virtualization and hypervisor security

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** Under the Shared Responsibility Model, the customer always retains 100% responsibility for **data governance, endpoints/client devices, user accounts, and identities** across IaaS, PaaS, and SaaS. **A** (operating system patching) is only the customer's responsibility in IaaS (Microsoft manages the OS in PaaS and SaaS). **B** (physical datacenter security) and **D** (network virtualization and hypervisor security) are always the cloud provider's (Microsoft's) responsibility across all cloud models.

</details>

---

### Question 3
An organization evaluates a **Software as a Service (SaaS)** solution (such as Microsoft 365). Which security responsibility remains with the customer?

- **A.** Physical server hardware maintenance
- **B.** Managing user accounts, identities, and data access policies
- **C.** Operating system updates and patches
- **D.** Hypervisor virtualization management

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** In a **SaaS** deployment model, the customer remains solely responsible for **managing user accounts, identities, client endpoints, and data access policies**. **A** (physical server hardware), **C** (operating system updates), and **D** (hypervisor virtualization) are underlying infrastructure and platform layers managed entirely by Microsoft in SaaS.

</details>

---

### Question 4
Which security concept utilizes multiple layers of defensive controls (Physical, Identity, Perimeter, Network, Compute, Application, Data) so that if one layer fails, subsequent layers protect the asset?

- **A.** Single Sign-On (SSO)
- **B.** Defense in Depth
- **C.** Federation
- **D.** Asymmetric encryption

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **Defense in Depth** implements concentric layers of security controls (Physical, Identity & Access, Perimeter, Network, Compute, Application, and Data) so that if an attacker breaches one layer, the inner layers prevent unauthorized access to the core data. **A** (SSO) allows users to authenticate once to access multiple applications. **C** (Federation) establishes trust between separate identity realms. **D** (Asymmetric encryption) is a cryptographic technique using public/private key pairs rather than a multi-layered architectural model.

</details>

---

### Question 5
When a user provides their username and password to log into a portal, which security process is taking place?

- **A.** Authorization
- **B.** Auditing
- **C.** Authentication
- **D.** Federation

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **Authentication (AuthN)** is the process of verifying that an identity (user, service, or device) is who they claim to be by validating credentials. **A** (Authorization / AuthZ) occurs *after* authentication to determine what specific resources and actions the verified user is permitted to access. **B** (Auditing) records sign-in and resource access events for compliance and forensic analysis. **D** (Federation) enables cross-organization authentication across distinct identity providers.

</details>

---

### Question 6
Which component of the CIA Triad ensures that sensitive financial data cannot be viewed or accessed by unauthorized individuals?

- **A.** Confidentiality
- **B.** Integrity
- **C.** Availability
- **D.** Non-repudiation

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **Confidentiality** protects sensitive data from unauthorized disclosure through encryption, access control, and MFA. **B** (Integrity) ensures data remains accurate and untampered with in transit and at rest (e.g., via hashing and digital signatures). **C** (Availability) ensures systems and data remain accessible to authorized users when needed (e.g., via redundancy and DDoS protection). **D** (Non-repudiation) guarantees that a sender cannot deny having performed an action, and is not one of the three letters in the CIA Triad.

</details>

---

### Question 7
Which type of cyber attack involves an attacker attempting common passwords against a large list of known usernames to avoid account lockout thresholds?

- **A.** Distributed Denial of Service (DDoS)
- **B.** Password Spraying
- **C.** Man-in-the-Middle (MitM)
- **D.** SQL Injection

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **Password Spraying** tests a small number of commonly used passwords (e.g., `Password123!`) across many different user accounts simultaneously to evade standard account lockout policies that trigger after repeated failed attempts on a single account. **A** (DDoS) overwhelms network or application capacity to disrupt availability. **C** (MitM) intercepts and relays traffic between two communicating parties. **D** (SQL Injection) inserts malicious database queries into unvalidated web input fields.

</details>

---

### Question 8
For each of the following statements about encryption, select **Yes** if the statement is true, otherwise select **No**:

| Statement | Yes / No |
| :--- | :---: |
| 1. Symmetric encryption uses the same cryptographic key for both encryption and decryption. | Yes / No |
| 2. Asymmetric encryption uses a public key to encrypt and a mathematically linked private key to decrypt. | Yes / No |
| 3. Hashing is a two-way mathematical function that can be easily decrypted back to plaintext. | Yes / No |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** Statement 1: **Yes** | Statement 2: **Yes** | Statement 3: **No**

> **Why:**
> - **Statement 1 (Yes):** Symmetric encryption algorithms (such as AES) use a single shared secret key to both encrypt plaintext and decrypt ciphertext.
> - **Statement 2 (Yes):** Asymmetric encryption algorithms (such as RSA and ECC) use a mathematically linked key pair where data encrypted with the public key can only be decrypted with the corresponding private key (used in TLS, digital signatures, and SSH).
> - **Statement 3 (No):** Hashing (such as SHA-256) is strictly a **one-way** deterministic cryptographic function that generates a fixed-length digest to verify data integrity; it cannot be reversed or decrypted back to plaintext.

</details>

---

### Question 9
Which term refers to establishing a trust relationship between two distinct identity providers so that users can access resources across organizational boundaries using their existing corporate credentials?

- **A.** Role-Based Access Control (RBAC)
- **B.** Federation
- **C.** Symmetric encryption
- **D.** Multi-Factor Authentication

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **Federation** establishes a cryptographic trust relationship between two separate identity domains (such as Microsoft Entra ID and an external partner's identity provider or on-premises AD FS) so users can authenticate once in their home realm and access external resources via security tokens. **A** (RBAC) is an authorization model that assigns permissions via roles. **C** (Symmetric encryption) protects data confidentiality using a shared key. **D** (Multi-Factor Authentication) requires two or more verification factors during sign-in.

</details>

---

### Question 10
In the Zero Trust model, which principle focuses on limiting user permissions to only what is required to perform a specific task for a limited time?

- **A.** Verify explicitly
- **B.** Use least privilege access
- **C.** Assume breach
- **D.** Network micro-segmentation

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **Use least privilege access** is the second core guiding principle of Zero Trust, enforcing Just-In-Time (JIT) and Just-Enough-Access (JEA) alongside risk-based adaptive policies to limit standing permissions. **A** (Verify explicitly) focuses on authenticating and authorizing every request using all available signals. **C** (Assume breach) focuses on minimizing blast radius, verifying end-to-end encryption, and driving threat detection. **D** (Network micro-segmentation) is a technical implementation tactic under "Assume breach," not one of the three top-level Zero Trust principles.

</details>

---

### Question 11
Which two industry standard security and compliance benchmarks are integrated into the Microsoft Cloud Security Benchmark (formerly Azure Security Benchmark)?

*Choose 2 answers*

- **A.** Center for Internet Security (CIS) Controls
- **B.** Digital Millennium Copyright Act (DMCA)
- **C.** Open Systems Interconnection (OSI) Reference Model
- **D.** National Institute of Standards and Technology (NIST) SP 800-53

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answers:** A, D

> **Why:** The **Microsoft Cloud Security Benchmark (MCSB)** maps its security controls and recommendations directly to industry-standard cybersecurity frameworks including **Center for Internet Security (CIS) Controls** (**A**) and **NIST SP 800-53** (**D**) (as well as PCI-DSS). **B** (DMCA) is a US copyright law concerning digital media piracy, not a cloud infrastructure security benchmark. **C** (OSI Reference Model) is a conceptual 7-layer networking framework rather than a security compliance control standard.

</details>

---

### Question 12
For each of the following statements regarding threat intelligence and posture management, select **Yes** if true, otherwise select **No**:

| Statement | Yes / No |
| :--- | :---: |
| 1. A security posture reflects an organization's overall cybersecurity readiness and defense health. | Yes / No |
| 2. Vulnerability management identifies, evaluates, and remediates security weaknesses before attackers exploit them. | Yes / No |
| 3. Security compliance guarantees that an organization is 100% immune to all zero-day cyber attacks. | Yes / No |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** Statement 1: **Yes** | Statement 2: **Yes** | Statement 3: **No**

> **Why:**
> - **Statement 1 (Yes):** Security posture represents the overall strength of an organization's security controls, configurations, and ability to detect and respond to threats (measured in Azure via Secure Score).
> - **Statement 2 (Yes):** Vulnerability management continuously scans endpoints and cloud workloads to discover, prioritize, and patch software flaws and misconfigurations.
> - **Statement 3 (No):** Meeting regulatory compliance standards (e.g., ISO 27001, HIPAA) demonstrates adherence to baseline controls at a point in time, but never guarantees 100% immunity against novel or zero-day attacks.

</details>

---

## Domain 2: Capabilities of Microsoft Entra (Identity & Access Management)

### Question 13
You need to provide temporary, time-bound administrator access to an engineer to troubleshoot an Azure production issue. The access must expire automatically after 4 hours and require justification upon activation. What should you use?

- **A.** Azure Role-Based Access Control (RBAC) permanent role assignment
- **B.** Microsoft Entra Privileged Identity Management (PIM)
- **C.** Microsoft Entra Password Protection
- **D.** Microsoft Entra Application Proxy

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **Microsoft Entra Privileged Identity Management (PIM)** provides Just-In-Time (JIT) privileged access to Microsoft Entra roles and Azure RBAC roles, allowing users to be assigned as *Eligible* so they must activate the role with justification, MFA, approval, and an automatic expiration window (such as 4 hours). **A** (Permanent RBAC assignment) grants standing active privileges that do not automatically expire. **C** (Entra Password Protection) blocks weak and custom-banned passwords. **D** (Entra Application Proxy) publishes on-premises web applications for remote external access.

</details>

---

### Question 14
You need to configure an automated policy that requires users signing in from an untrusted location or high-risk IP address to perform Multi-Factor Authentication (MFA). Which Microsoft Entra capability should you configure?

- **A.** Conditional Access
- **B.** Access Reviews
- **C.** Self-Service Password Reset (SSPR)
- **D.** Entra Connect

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **Microsoft Entra Conditional Access** is the Zero Trust policy engine that evaluates real-time sign-in signals (`If` user/group, IP location, device compliance, application, and risk level) and enforces access controls (`Then` allow with MFA, require compliant device, or block access). **B** (Access Reviews) periodically audits whether users still need group or app access. **C** (SSPR) lets users reset or unlock their passwords without helpdesk assistance. **D** (Entra Connect) synchronizes on-premises Active Directory objects with Microsoft Entra ID.

</details>

---

### Question 15
What should you use to associate a single managed identity with **more than one** Azure virtual machine?

- **A.** A Microsoft Entra user account
- **B.** A system-assigned managed identity
- **C.** A service principal created in an on-premises domain controller
- **D.** A user-assigned managed identity

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** A **user-assigned managed identity** is created as a standalone Azure resource with its own independent lifecycle and can be shared across **multiple** Azure resources (such as a fleet of Virtual Machines needing identical access to a Key Vault or Storage account). **B** (System-assigned managed identity) is tightly coupled `1:1` to a single Azure resource and cannot be shared across multiple VMs. **A** (Entra user account) is designed for human interactive sign-in and requires manual credential management. **C** (On-premises domain controller account) is for local AD DS and is not an Azure managed identity.

</details>

---

### Question 16
For each of the following statements about Microsoft Entra Managed Identities, select **Yes** if true, otherwise select **No**:

| Statement | Yes / No |
| :--- | :---: |
| 1. System-assigned managed identities are automatically deleted when the associated Azure resource is deleted. | Yes / No |
| 2. Managed identities eliminate the need for developers to manage credentials in application code. | Yes / No |
| 3. User-assigned managed identities can only be assigned to a single Azure resource during their lifecycle. | Yes / No |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** Statement 1: **Yes** | Statement 2: **Yes** | Statement 3: **No**

> **Why:**
> - **Statement 1 (Yes):** System-assigned managed identities are tied directly to the lifecycle of the single Azure resource they are enabled on; deleting the resource automatically deletes the identity in Entra ID.
> - **Statement 2 (Yes):** Managed identities automatically handle token acquisition and credential rotation in the background via Microsoft Entra ID, eliminating hardcoded secrets or connection strings in code.
> - **Statement 3 (No):** User-assigned managed identities exist as independent Azure resources and can be assigned to **multiple** Azure resources simultaneously.

</details>

---

### Question 17
Which tool should you use to synchronize on-premises Active Directory Domain Services (AD DS) user accounts, groups, and password hashes with Microsoft Entra ID?

- **A.** Microsoft Entra Connect (or Entra Cloud Sync)
- **B.** Microsoft Sentinel
- **C.** Azure Arc
- **D.** Active Directory Federation Services (AD FS)

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **Microsoft Entra Connect** (and **Microsoft Entra Cloud Sync**) synchronizes user identities, group memberships, and password hashes (for Password Hash Synchronization) between on-premises AD DS and cloud-based Microsoft Entra ID. **B** (Microsoft Sentinel) is a cloud-native SIEM/SOAR platform for security analytics. **C** (Azure Arc) extends Azure resource governance and management to hybrid/multi-cloud servers and Kubernetes clusters. **D** (AD FS) provides federated claim-based authentication redirection rather than directory object and password hash synchronization.

</details>

---

### Question 18
Which passwordless authentication method provided by Microsoft Entra ID allows users to sign in using biometric authentication (face or fingerprint) tied to a specific Windows 11 hardware device?

- **A.** SMS text message verification
- **B.** Windows Hello for Business
- **C.** Email one-time passcode (OTP)
- **D.** Temporary Access Pass (TAP)

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **Windows Hello for Business** is Microsoft's passwordless authentication solution tied directly to a user's Windows device, using biometric sensors (facial recognition or fingerprint) or a device-specific PIN backed by cryptographic keys stored in the device's Trusted Platform Module (TPM) chip. **A** (SMS text message) and **C** (Email OTP) are phishable verification codes rather than biometric passwordless methods. **D** (Temporary Access Pass) is a time-limited passcode issued by an admin to help users onboard passwordless methods (like Windows Hello or FIDO2 keys) or recover access when they lose their device.

</details>

---

### Question 19
What can be created and managed natively in on-premises **Active Directory Domain Services (AD DS)**?

- **A.** Computer accounts and organizational units (OUs)
- **B.** SaaS application connectors for third-party cloud apps
- **C.** Azure subscription role definitions
- **D.** Microsoft 365 group sensitivity labels

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Traditional on-premises **Active Directory Domain Services (AD DS)** uses a hierarchical structure of forests, trees, domains, and **Organizational Units (OUs)** to manage domain-joined **computer accounts**, users, and Group Policy Objects (GPOs) via LDAP and Kerberos. **B** (SaaS application connectors) are configured in Microsoft Entra ID Enterprise Applications or Microsoft Defender for Cloud Apps. **C** (Azure subscription role definitions) are managed via Azure RBAC in Azure Resource Manager. **D** (Sensitivity labels) are created and published in Microsoft Purview Information Protection.

</details>

---

### Question 20
Which Microsoft Entra ID Governance feature allows administrators to periodically review and verify whether guest users and employees still require access to sensitive groups and applications?

- **A.** Microsoft Entra Access Reviews
- **B.** Conditional Access Named Locations
- **C.** Entra Password Protection
- **D.** Entra Verified ID

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **Microsoft Entra Access Reviews** (part of Microsoft Entra ID Governance) automates scheduled recertifications where group owners, managers, or users themselves attest whether internal employees and external B2B guests still need access—automatically revoking access for denied or expired memberships. **B** (Conditional Access Named Locations) defines trusted IP address ranges or countries/regions for sign-in policies. **C** (Entra Password Protection) prevents users from choosing weak or banned passwords. **D** (Entra Verified ID) issues and verifies decentralized digital credentials based on open W3C standards.

</details>

---

### Question 21
What happens when a user attempts to sign into Microsoft Entra ID and their sign-in risk is evaluated as **High** by Microsoft Entra ID Protection?

- **A.** Microsoft Entra Privileged Identity Management (PIM) permanently revokes the user's directory license.
- **B.** Conditional Access can trigger an automated block or force a secure password change via Multi-Factor Authentication.
- **C.** Microsoft Purview Data Loss Prevention (DLP) encrypts the user's on-premises hard drive.
- **D.** Azure Policy automatically deletes the user's hybrid Active Directory organizational unit.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **Microsoft Entra ID Protection** detects sign-in anomalies (such as anonymous IP usage, atypical travel, or leaked credentials) and feeds **Sign-in risk** and **User risk** signals into **Conditional Access**, which can automatically block access, require MFA, or require a secure self-service password reset. **A** is wrong because PIM manages JIT role activation rather than revoking licenses on risky sign-ins. **C** is wrong because Purview DLP prevents sensitive data leakage in transit/endpoints rather than encrypting full disks during sign-in. **D** is wrong because Azure Policy enforces cloud resource compliance rules in Azure Resource Manager, not on-premises AD OUs.

</details>

---

### Question 22
Which authentication protocol is standard for modern web application Single Sign-On (SSO) in Microsoft Entra ID?

- **A.** NTLM
- **B.** OpenID Connect (OIDC) / OAuth 2.0
- **C.** LDAP
- **D.** Kerberos

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **OpenID Connect (OIDC)** (built on top of **OAuth 2.0**) and **SAML 2.0** are the modern HTTP/HTTPS-based authentication and authorization protocols used natively by **Microsoft Entra ID** for cloud web application Single Sign-On (SSO). **A** (NTLM), **C** (LDAP), and **D** (Kerberos) are legacy or traditional on-premises directory and authentication protocols used by Active Directory Domain Services (AD DS) rather than modern cloud-native Entra web SSO.

</details>

---

### Question 23
You need to prevent users in your organization from setting easily guessable passwords such as "Spring2026!" or common company names. Which Microsoft Entra ID feature should you implement?

- **A.** Entra Password Protection (Global & Custom Banned Password Lists)
- **B.** Microsoft Entra PIM
- **C.** Azure Bastion
- **D.** Entra External ID

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **Microsoft Entra Password Protection** combines a Microsoft-maintained global banned password list with an organization's **custom banned password list** (to block company names, local sports teams, or seasonal patterns like `Spring2026!`, including character substitutions) across both Microsoft Entra ID and on-premises AD DS. **B** (Entra PIM) provides time-bound JIT privileged role elevation. **C** (Azure Bastion) provides browser-based RDP/SSH access to Azure VMs. **D** (Entra External ID) manages B2B guest collaboration and B2C customer identities.

</details>

---

### Question 24
What is the primary function of **Microsoft Entra External ID** (B2B and B2C collaboration)?

- **A.** To enable secure collaboration with external partners, suppliers, and customer accounts using their own identities.
- **B.** To synchronize on-premises Active Directory user objects and password hashes to the cloud.
- **C.** To provide Just-In-Time (JIT) elevation for Global Administrator role assignments.
- **D.** To enforce mobile device enrollment and application protection policies on corporate laptops.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **Microsoft Entra External ID** enables organizations to securely share internal apps and resources with external business partners/vendors via **B2B collaboration / B2B direct connect**, or publish customer-facing apps with customizable sign-up/sign-in experiences via **CIAM (B2C)** using external or social identities. **B** describes *Microsoft Entra Connect*. **C** describes *Microsoft Entra Privileged Identity Management (PIM)*. **D** describes *Microsoft Intune* mobile device and application management.

</details>

---

### Question 25
For each of the following statements about Microsoft Entra ID roles and Azure RBAC roles, select **Yes** if true, otherwise select **No**:

| Statement | Yes / No |
| :--- | :---: |
| 1. Microsoft Entra roles (e.g. Global Administrator) control access to Microsoft Entra directory resources and Microsoft 365 services. | Yes / No |
| 2. Azure RBAC roles (e.g. Owner, Contributor) control access to Azure infrastructure resources (VMs, Storage, Databases). | Yes / No |
| 3. A Global Administrator in Entra ID automatically has permanent full Owner access to all Azure subscription resources by default. | Yes / No |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** Statement 1: **Yes** | Statement 2: **Yes** | Statement 3: **No**

> **Why:**
> - **Statement 1 (Yes):** Microsoft Entra roles operate at the tenant/identity plane to govern directory objects (users, groups, enterprise apps) and Microsoft 365 admin centers.
> - **Statement 2 (Yes):** Azure RBAC operates through Azure Resource Manager (ARM) at Management Group, Subscription, Resource Group, and Resource scopes to control infrastructure (VMs, VNets, Storage).
> - **Statement 3 (No):** Microsoft Entra ID and Azure RBAC are separate permission systems. By default, a Global Administrator does **not** have standing access to Azure subscription resources (though they can temporarily toggle the *Access management for Azure resources* switch to grant themselves the *User Access Administrator* role if emergency recovery is needed).

</details>

---

## Domain 3: Capabilities of Microsoft Security Solutions

### Question 26
Which cloud-native SIEM (Security Information and Event Management) and SOAR (Security Orchestration, Automated Response) service in Azure aggregates security data across the enterprise?

- **A.** Microsoft Defender for Endpoint
- **B.** Microsoft Sentinel
- **C.** Azure Key Vault
- **D.** Azure Network Watcher

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **Microsoft Sentinel** is Microsoft's scalable, cloud-native **SIEM and SOAR** solution built on Azure Monitor Log Analytics, delivering central log aggregation, AI-driven threat detection, KQL hunting, and automated incident response across multi-cloud and hybrid estates. **A** (Defender for Endpoint) is an EDR and endpoint vulnerability solution for client/server devices. **C** (Azure Key Vault) stores cryptographic keys, secrets, and certificates. **D** (Azure Network Watcher) provides network-level diagnostics, packet capture, and flow logs rather than enterprise SIEM/SOAR correlation.

</details>

---

### Question 27
In Microsoft Sentinel, which component provides automated, play-by-play incident response and remediation workflows powered by Azure Logic Apps?

- **A.** Workbooks
- **B.** Playbooks
- **C.** Data Connectors
- **D.** Jupyter Notebooks

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **Playbooks** represent the **SOAR** (Security Orchestration, Automation, and Response) capability in Microsoft Sentinel—they are collections of automated remediation procedures built on **Azure Logic Apps** that can be triggered automatically by alerts/incidents (e.g., blocking an IP in Azure Firewall, isolating a device in Defender, or opening a ServiceNow ticket). **A** (Workbooks) provide customizable interactive dashboards for data visualization. **C** (Data Connectors) ingest telemetry from Microsoft and third-party sources. **D** (Jupyter Notebooks) provide an interactive Python/KQL environment for advanced threat hunting and machine learning.

</details>

---

### Question 28
Which service provides **Cloud Security Posture Management (CSPM)** and calculates the overall **Secure Score** across your Azure, AWS, and GCP subscriptions?

- **A.** Microsoft Defender for Cloud
- **B.** Microsoft Defender for Office 365
- **C.** Azure Bastion
- **D.** Azure Virtual Network NAT

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **Microsoft Defender for Cloud** provides both **CSPM** (Cloud Security Posture Management—calculating **Secure Score**, tracking regulatory compliance, and offering hardening recommendations) and **CWPP** (Cloud Workload Protection Platform—protecting VMs, databases, containers, and storage) across Azure, on-premises (via Azure Arc), AWS, and Google Cloud. **B** (Defender for Office 365) protects email and collaboration workspaces from phishing and malware. **C** (Azure Bastion) provides browser-based RDP/SSH access to VMs. **D** (Azure Virtual Network NAT) provides outbound internet SNAT connectivity for private virtual networks.

</details>

---

### Question 29
Which product within the Microsoft Defender XDR suite specifically provides **Endpoint Detection and Response (EDR)**, device vulnerability management, and **Microsoft Secure Score for Devices**?

- **A.** Microsoft Defender for Endpoint
- **B.** Microsoft Defender for Identity
- **C.** Microsoft Defender for Cloud Apps
- **D.** Azure DDoS Protection

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **Microsoft Defender for Endpoint** is an enterprise endpoint security platform protecting Windows, macOS, Linux, iOS, and Android devices with Threat & Vulnerability Management (**Microsoft Secure Score for Devices**), attack surface reduction, next-generation antivirus, and **Endpoint Detection and Response (EDR)**. **B** (Defender for Identity) monitors on-premises Active Directory Domain Controllers for identity attacks. **C** (Defender for Cloud Apps) is a CASB that governs SaaS applications and Shadow IT. **D** (Azure DDoS Protection) defends Azure public IP resources from volumetric and protocol network attacks.

</details>

---

### Question 30
You need to detect suspicious on-premises Active Directory reconnaissance activities, such as pass-the-hash and unauthorized domain controller replication. Which Microsoft Defender service should you deploy?

- **A.** Microsoft Defender for Identity
- **B.** Microsoft Defender for Office 365
- **C.** Azure Web Application Firewall
- **D.** Microsoft Defender for Storage

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **Microsoft Defender for Identity** (formerly Azure ATP) installs lightweight sensors on on-premises Active Directory Domain Controllers and AD FS/AD CS servers to analyze network traffic and Windows events—detecting reconnaissance, lateral movement (Pass-the-Hash, Pass-the-Ticket), Golden Ticket attacks, and malicious DC replication (DCSync). **B** (Defender for Office 365) protects Exchange Online, SharePoint, and Teams from phishing/malware. **C** (Azure WAF) protects web apps against Layer 7 HTTP exploits like SQLi and XSS. **D** (Defender for Storage) detects anomalous access and malware uploads in Azure Storage accounts.

</details>

---

### Question 31
Which service in Microsoft Defender XDR provides discovery of Shadow IT applications, monitors user activities in third-party SaaS apps (like Salesforce and Box), and enforces app governance?

- **A.** Microsoft Defender for Cloud Apps (MDCA)
- **B.** Microsoft Defender for Endpoint
- **C.** Azure Bastion
- **D.** Azure Front Door

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **Microsoft Defender for Cloud Apps** (formerly MCAS) is Microsoft's **Cloud Access Security Broker (CASB)** that discovers unsanctioned **Shadow IT** cloud apps, evaluates app risk scores, controls real-time session actions (such as blocking downloads on unmanaged devices), and protects sensitive information across Microsoft and third-party SaaS apps. **B** (Defender for Endpoint) secures client and server operating systems. **C** (Azure Bastion) provides secure RDP/SSH access to Azure VMs. **D** (Azure Front Door) is a global cloud CDN and Layer 7 application delivery network.

</details>

---

### Question 32
To which type of resource can **Azure Bastion** provide secure, seamless RDP and SSH connectivity directly through a web browser without exposing public IP addresses?

- **A.** Azure App Service web apps
- **B.** Azure SQL Database
- **C.** Azure Virtual Machines
- **D.** Azure Storage Accounts

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **Azure Bastion** is a fully managed PaaS jump-server service deployed inside an Azure Virtual Network that provides secure **RDP and SSH connectivity to Azure Virtual Machines** directly over TLS (port 443) in the Azure portal browser—removing the need to assign public IP addresses or open ports `3389`/`22` to the internet. **A** (Azure App Service), **B** (Azure SQL Database), and **D** (Azure Storage Accounts) are PaaS services managed via HTTPS APIs, SQL clients, or the Azure portal rather than interactive OS-level RDP/SSH sessions.

</details>

---

### Question 33
Which Azure security service provides centralized Layer 7 protection for web applications against common web vulnerabilities and exploits, such as SQL Injection (SQLi) and Cross-Site Scripting (XSS)?

- **A.** Azure Network Security Groups (NSGs)
- **B.** Azure Web Application Firewall (WAF)
- **C.** Azure Key Vault
- **D.** Azure ExpressRoute

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **Azure Web Application Firewall (WAF)** (integrated with Azure Application Gateway and Azure Front Door) inspects Layer 7 HTTP/HTTPS traffic using managed OWASP Core Rule Sets to block web application exploits including **SQL Injection (SQLi)**, **Cross-Site Scripting (XSS)**, and malicious bot scrapers. **A** (NSGs) operate at Layer 3/Layer 4 (IP, port, and protocol) and cannot inspect Layer 7 HTTP payloads. **C** (Azure Key Vault) stores secrets, keys, and certificates. **D** (Azure ExpressRoute) provides private dedicated fiber connectivity between on-premises networks and Azure.

</details>

---

### Question 34
What is the primary function of **Azure Key Vault**?

- **A.** To store and tightly control access to secrets, encryption keys, and SSL/TLS certificates.
- **B.** To filter inbound and outbound network traffic across Azure virtual networks using Layer 4 and Layer 7 rules.
- **C.** To assess multi-cloud resources against regulatory compliance benchmarks and calculate Secure Score.
- **D.** To synchronize on-premises Active Directory certificates and user identities with Microsoft Entra ID.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **Azure Key Vault** is a centralized cloud service backed by FIPS-validated Hardware Security Modules (HSMs) for safeguarding **secrets** (API keys, passwords, connection strings), **cryptographic keys** (for encryption), and **SSL/TLS certificates** (with automated lifecycle renewal). **B** describes *Azure Firewall*. **C** describes *Microsoft Defender for Cloud*. **D** describes *Microsoft Entra Connect*.

</details>

---

### Question 35
For each of the following statements about Microsoft Sentinel, select **Yes** if true, otherwise select **No**:

| Statement | Yes / No |
| :--- | :---: |
| 1. Microsoft Sentinel Data Connectors can ingest security logs from non-Microsoft environments, such as AWS CloudTrail and Syslog. | Yes / No |
| 2. Sentinel Workbooks provide interactive visualizations and dashboards for analyzing log telemetry. | Yes / No |
| 3. Sentinel requires an on-premises physical server appliance to be installed in every office datacenter. | Yes / No |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** Statement 1: **Yes** | Statement 2: **Yes** | Statement 3: **No**

> **Why:**
> - **Statement 1 (Yes):** Microsoft Sentinel includes out-of-the-box **Data Connectors** for Microsoft services as well as third-party clouds (AWS, GCP), firewalls, and standard protocols like Syslog, CEF, and TAXII.
> - **Statement 2 (Yes):** **Workbooks** (built on Azure Monitor Workbooks) provide customizable visual dashboards and KQL charts to monitor security trends and incident metrics.
> - **Statement 3 (No):** Microsoft Sentinel is 100% cloud-native and serverless in Azure—there is no physical hardware appliance to purchase or maintain in office datacenters.

</details>

---

### Question 36
Which two cards are available in the Microsoft Defender portal (`security.microsoft.com`) home dashboard to provide immediate security posture insight?

*Choose 2 answers*

- **A.** Users at risk
- **B.** Devices at risk
- **C.** Azure monthly billing and cost forecast
- **D.** Microsoft Purview eDiscovery legal hold cases

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answers:** A, B

> **Why:** The unified **Microsoft Defender portal** (`security.microsoft.com`) home dashboard aggregates real-time XDR telemetry into summary cards including **Users at risk** (**A**, powered by Entra ID Protection & Defender for Identity), **Devices at risk** (**B**, powered by Defender for Endpoint), Active incidents, and Microsoft Secure Score. **C** (Azure monthly billing and cost forecast) is located in *Microsoft Cost Management + Billing* in the Azure portal. **D** (eDiscovery legal hold cases) is managed inside the *Microsoft Purview compliance portal* (`compliance.microsoft.com`), not the Defender XDR home screen.

</details>

---

### Question 37
What does a high **Secure Score** in Microsoft Defender for Cloud indicate?

- **A.** The organization has experienced a higher volume of high-severity security incidents over the past 30 days.
- **B.** The organization has implemented a larger proportion of recommended security best practices and posture hardening actions.
- **C.** All Azure virtual machines have been migrated to on-premises Hyper-V hosts.
- **D.** The Azure subscription is automatically exempt from Microsoft Purview compliance audits.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **Secure Score** in Microsoft Defender for Cloud is a percentage-based KPI of your Cloud Security Posture Management (CSPM); a higher score means your organization has remediated more security recommendations aligned with the Microsoft Cloud Security Benchmark (such as enabling MFA, encrypting disks, and remediating vulnerabilities). **A** is wrong because active security incidents are tracked under Defender alerts/incidents rather than increasing your posture score. **C** is wrong because Secure Score evaluates both cloud and Azure Arc-enabled hybrid resources based on security controls, not workload location. **D** is wrong because a high Secure Score never exempts an organization from regulatory audits.

</details>

---

### Question 38
In Microsoft Sentinel, which tool allows security analysts to perform advanced, programmatic threat hunting and data exploration using Python and KQL?

- **A.** Jupyter Notebooks
- **B.** Microsoft Entra Connect Health
- **C.** Azure Bastion Session Manager
- **D.** Microsoft Purview Content Search

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Microsoft Sentinel integrates directly with Azure Machine Learning workspaces to run **Jupyter Notebooks** (supporting Python, KQL, and the `msticpy` security library) for advanced threat hunting, custom machine learning anomaly detection, and rich procedural investigation workflows. **B** (Entra Connect Health) monitors hybrid identity synchronization infrastructure. **C** (Azure Bastion) manages browser-based RDP/SSH sessions to Azure VMs. **D** (Purview Content Search) searches emails and documents across Microsoft 365 for compliance and eDiscovery rather than programmatic SIEM threat hunting.

</details>

---

### Question 39
Which Azure network security feature controls inbound and outbound network traffic to Azure VM network interfaces and subnets using 5-tuple rules (Source, Source Port, Destination, Destination Port, Protocol)?

- **A.** Network Security Groups (NSGs)
- **B.** Azure Bastion
- **C.** Azure DDoS Protection
- **D.** Microsoft Entra Application Proxy

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **Network Security Groups (NSGs)** act as stateful Layer 4 packet filters attached to Azure Virtual Network subnets or VM network interfaces (NICs), allowing or denying traffic based on priority-ordered **5-tuple rules** (Source IP, Source Port, Destination IP, Destination Port, and Protocol). **B** (Azure Bastion) provides browser-based RDP/SSH access to VMs without public IPs. **C** (Azure DDoS Protection) scrubs volumetric and protocol flood attacks targeting public IPs. **D** (Entra Application Proxy) publishes internal on-premises web applications to external users via Microsoft Entra ID.

</details>

---

## Domain 4: Capabilities of Microsoft Compliance Solutions

### Question 40
What is an **Assessment** in Microsoft Purview Compliance Manager?

- **A.** An automated penetration test executed against Azure Virtual Network firewalls.
- **B.** A structured evaluation that assesses an organization's compliance posture against a specific regulatory standard (such as GDPR, ISO 27001, or NIST).
- **C.** A real-time packet capture log generated by Azure Network Watcher.
- **D.** A temporary elevation request for Global Administrator privileges in Microsoft Entra PIM.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** In **Microsoft Purview Compliance Manager**, an **Assessment** groups technical controls and actionable **Improvement Actions** mapped to a specific regulation, industry standard, or law (such as GDPR, ISO/IEC 27001, NIST 800-53, or the baseline Data Protection Baseline), contributing to the organization's overall **Compliance Score**. **A** is wrong because Compliance Manager evaluates governance/configuration controls rather than running offensive network penetration tests. **C** describes network diagnostics in *Azure Network Watcher*. **D** describes Just-In-Time role activation in *Microsoft Entra PIM*.

</details>

---

### Question 41
Match the Microsoft Purview **Insider Risk Management** components (`Policies`, `Alerts`, `Cases`) to their appropriate operational descriptions:

1. Define conditions, risk indicators (e.g. downloading sensitive files before leaving the company), and users to monitor.
2. Generated automatically when user activity matches the thresholds defined in an insider risk policy.
3. Created by investigators to conduct formal investigations, review evidence, and track remediation workflows.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** 1: **Policies** | 2: **Alerts** | 3: **Cases**

| Component | Description |
| :--- | :--- |
| **Policies** | Define conditions, risk indicators (e.g. downloading sensitive files before leaving the company), and users to monitor. |
| **Alerts** | Generated automatically when user activity matches the thresholds defined in an insider risk policy. |
| **Cases** | Created by investigators to conduct formal investigations, review evidence, and track remediation workflows. |

> **Why:**
> - **Policies (1):** Built from predefined templates (e.g., *Data theft by departing users* or *Data leaks*) that specify which users/groups to monitor, which triggering events apply (such as an HR resignation date connector), and which risk indicators are scored.
> - **Alerts (2):** Automatically generated on the Alerts dashboard with a risk severity score (Low, Medium, High) when user activities cross policy thresholds, allowing analysts to triage whether the activity is benign or requires escalation.
> - **Cases (3):** When an alert is confirmed as suspicious, analysts escalate it to a **Case**, which provides tools like Content Explorer, Activity Explorer, pseudonymized user investigation, legal/HR collaboration notes, and escalation to eDiscovery.

</details>

---

### Question 42
An organization needs to classify sensitive emails and Word documents by automatically applying watermarks, header tags, and AES-256 encryption based on content. Which Microsoft Purview feature should be deployed?

- **A.** Sensitivity Labels (Microsoft Purview Information Protection)
- **B.** Azure Bastion
- **C.** Microsoft Defender for Identity
- **D.** Microsoft Sentinel Data Connectors

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **Sensitivity Labels** (part of **Microsoft Purview Information Protection**) classify and protect documents and emails by embedding persistent metadata, applying visual markings (headers, footers, watermarks), and enforcing Rights Management encryption that travels with the file even if shared outside the organization. **B** (Azure Bastion) provides browser-based RDP/SSH access to Azure VMs. **C** (Defender for Identity) detects identity-based threats against on-premises Active Directory. **D** (Sentinel Data Connectors) ingest security logs into a Log Analytics workspace.

</details>

---

### Question 43
You need to prevent employees from accidentally copying credit card numbers and passport details into Microsoft Teams chat messages or sharing them with external recipients. What should you configure?

- **A.** Microsoft Purview Data Loss Prevention (DLP)
- **B.** Azure DDoS Protection
- **C.** Microsoft Entra Application Proxy
- **D.** Azure Bastion

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **Microsoft Purview Data Loss Prevention (DLP)** continuously monitors content across Microsoft Teams chats/channels, Exchange Online emails, SharePoint sites, OneDrive accounts, and endpoints—detecting sensitive information types (such as credit card numbers, SSNs, or passport numbers) to display real-time Policy Tips or block unauthorized external sharing. **B** (Azure DDoS Protection) mitigates network flood attacks on Azure public IPs. **C** (Entra Application Proxy) provides remote access to internal web apps. **D** (Azure Bastion) provides RDP/SSH connectivity to Azure VMs.

</details>

---

### Question 44
On which client operating systems can **Microsoft Purview Endpoint Data Loss Prevention (Endpoint DLP)** be deployed to monitor and restrict file actions (e.g. copying sensitive files to USB or printing)?

- **A.** Windows only
- **B.** Windows and Android only
- **C.** Windows and macOS
- **D.** Linux only

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **Microsoft Purview Endpoint DLP** natively supports **Windows 10/11** and **macOS** client devices (onboarded to the Microsoft Purview compliance portal or Microsoft Defender for Endpoint) to audit and block exfiltration actions like copying sensitive files to removable USB drives, printing, uploading to unapproved cloud domains, or copying to the clipboard. **A** is wrong because macOS is also supported. **B** is wrong because Android and iOS mobile devices use *Microsoft Intune App Protection Policies (MAM)* rather than Endpoint DLP. **D** is wrong because Linux endpoints are not supported for Purview Endpoint DLP file-level exfiltration controls.

</details>

---

### Question 45
For each of the following statements about Microsoft Purview eDiscovery, select **Yes** if true, otherwise select **No**:

| Statement | Yes / No |
| :--- | :---: |
| 1. eDiscovery search results can be exported and downloaded for external legal review. | Yes / No |
| 2. Legal holds can be placed on mailboxes and SharePoint sites to preserve content from deletion during ongoing litigation. | Yes / No |
| 3. eDiscovery automatically permanently deletes all files that contain the word "confidential." | Yes / No |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** Statement 1: **Yes** | Statement 2: **Yes** | Statement 3: **No**

> **Why:**
> - **Statement 1 (Yes):** Microsoft Purview eDiscovery (Standard and Premium) allows legal investigators to search across Exchange, SharePoint, OneDrive, and Teams and export the collected evidence packages for review by external legal counsel.
> - **Statement 2 (Yes):** eDiscovery cases allow administrators to place an **eDiscovery Hold (Legal Hold)** on custodian mailboxes, OneDrive accounts, Teams messages, and SharePoint sites so immutable copies of data are preserved even if a user attempts to delete or alter them.
> - **Statement 3 (No):** eDiscovery is strictly a legal identification, preservation, and export tool; automated deletion based on age or labels is handled by **Microsoft Purview Data Lifecycle Management (Retention Policies/Labels)**, not eDiscovery.

</details>

---

### Question 46
Which Microsoft Purview feature uses machine learning algorithms to detect toxic language, harassment, regulatory infractions, and sensitive data leakage across corporate communication channels (Teams, Exchange)?

- **A.** Communication Compliance
- **B.** Azure Key Vault
- **C.** Microsoft Defender for Storage
- **D.** Azure Firewall

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **Microsoft Purview Communication Compliance** uses built-in trainable classifiers, optical character recognition (OCR), and machine learning to scan internal and external messages across Microsoft Teams, Exchange Online, Viva Engage, and third-party communications for code-of-conduct violations (harassment, profanity, threats) and regulatory compliance breaches (insider trading, unauthorized financial disclosures). **B** (Azure Key Vault) stores cryptographic secrets and keys. **C** (Defender for Storage) detects malware and unusual activity in Azure Storage accounts. **D** (Azure Firewall) filters Layer 4 and Layer 7 network traffic across Azure VNets.

</details>

---

### Question 47
Where can an organization's compliance officer download independent third-party SOC 1, SOC 2, and ISO audit reports verifying Microsoft's cloud security and regulatory compliance?

- **A.** Microsoft Service Trust Portal
- **B.** Microsoft Entra Admin Center
- **C.** Azure Advisor Recommendations Dashboard
- **D.** Microsoft Intune Endpoint Manager

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** The **Microsoft Service Trust Portal** (`servicetrust.microsoft.com`) is Microsoft's central portal providing public and NDA-protected access to independent third-party **SOC 1, SOC 2, SOC 3, FedRAMP, and ISO/IEC audit reports**, penetration test summaries, whitepapers, and regional compliance guides. **B** (Microsoft Entra Admin Center) manages identities, groups, and access policies. **C** (Azure Advisor) provides personalized recommendations for Azure cost, high availability, and performance. **D** (Microsoft Intune) manages endpoint device compliance and mobile applications.

</details>

---

### Question 48
For each of the following statements about Microsoft Purview Data Lifecycle Management, select **Yes** if true, otherwise select **No**:

| Statement | Yes / No |
| :--- | :---: |
| 1. Retention policies can be configured to keep content for a specified period (e.g. 7 years) and then delete it automatically. | Yes / No |
| 2. Retention labels can be applied manually by end users or automatically based on sensitive info types. | Yes / No |
| 3. Retention policies only apply to on-premises file servers and cannot be applied to Microsoft Teams. | Yes / No |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** Statement 1: **Yes** | Statement 2: **Yes** | Statement 3: **No**

> **Why:**
> - **Statement 1 (Yes):** Retention policies and labels in **Microsoft Purview Data Lifecycle Management** can enforce three actions: *Retain only*, *Delete only*, or *Retain for a specific period and then automatically delete* (e.g., retain financial records for 7 years, then purge).
> - **Statement 2 (Yes):** While **Retention Policies** apply broadly at the container level (an entire mailbox or SharePoint site), **Retention Labels** apply at the individual item/document level and can be applied manually by users or auto-applied based on keywords, sensitive information types, or trainable classifiers.
> - **Statement 3 (No):** Retention policies are cloud-native and protect Microsoft 365 workloads including **Microsoft Teams** chats and channel messages, Exchange mailboxes, SharePoint sites, OneDrive accounts, and Viva Engage.

</details>

---

### Question 49
What is the primary objective of **Data Classification** in Microsoft Purview?

- **A.** To identify, label, and understand the sensitivity of data across the corporate estate so appropriate protection policies can be enforced.
- **B.** To provision Just-In-Time (JIT) administrative access to Azure Virtual Machines.
- **C.** To balance incoming HTTP/HTTPS web traffic across multiple regional Azure App Services.
- **D.** To synchronize on-premises Active Directory group memberships with Microsoft Entra ID.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **Data Classification** in Microsoft Purview (using Sensitive Information Types, Exact Data Match, and Trainable Classifiers alongside Content Explorer and Activity Explorer) discovers and categorizes sensitive data across your estate ("Know your data") so downstream **Information Protection** labels, **DLP** policies, and **Data Lifecycle** retention rules can protect it effectively. **B** describes Just-In-Time VM access in *Microsoft Defender for Cloud* or *Entra PIM*. **C** describes *Azure Front Door* or *Azure Application Gateway*. **D** describes *Microsoft Entra Connect*.

</details>

---

### Question 50
Which Microsoft privacy principle states that customer data in Microsoft cloud services will never be used for advertising purposes without explicit consent?

- **A.** You are in control of your data
- **B.** Transparency on data location and use
- **C.** Strong security protections
- **D.** Defending customer data through legal protections

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Under Microsoft's six core privacy principles (**Control, Transparency, Security, Strong legal protections, No content-based targeting, and Benefits to you**), the **Control** (*You are in control of your data*) and **No content-based targeting** commitments guarantee that customers own their data and that Microsoft never scans commercial emails, chats, or files to build advertising profiles. **B** (Transparency) focuses on disclosing where customer data resides and who can access it. **C** (Security) focuses on technical encryption and defensive controls. **D** (Strong legal protections) focuses on challenging unlawful government requests for customer data in court.

</details>
