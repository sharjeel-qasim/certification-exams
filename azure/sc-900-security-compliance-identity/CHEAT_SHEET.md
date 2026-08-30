# ⚡ SC-900: Microsoft Security, Compliance, and Identity Fundamentals — Cram & Cheat Sheet

[![Azure](https://img.shields.io/badge/Microsoft_Azure-0089D6?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/)
[![Exam](https://img.shields.io/badge/Exam-SC--900-blue?style=for-the-badge)](#-high-frequency-exam-topics)

Quick-reference cram sheet for **Microsoft Certified: Security, Compliance, and Identity Fundamentals (SC-900)**. Covers Zero Trust principles, Shared Responsibility, Microsoft Entra ID, Microsoft Defender XDR, Microsoft Sentinel, and Microsoft Purview.

---

## 🔵 1. Zero Trust Architecture (MEMORIZE THIS)

Zero Trust operates on the core assumption that threats exist both inside and outside the network perimeter.

| Guiding Principle | Definition | Exam Scenario |
| :--- | :--- | :--- |
| **Verify Explicitly** | Always authenticate and authorize based on all available data points (user identity, location, device health, service or workload, data classification, anomalies). | Evaluating Conditional Access signals before granting access to an app. |
| **Use Least Privilege Access** | Limit user access with Just-In-Time and Just-Enough-Access (JIT/JEA), risk-based adaptive policies, and data protection. | Activating an administrator role for 2 hours via Privileged Identity Management (PIM). |
| **Assume Breach** | Minimize blast radius and segment access. Verify end-to-end encryption and use analytics to get visibility, drive threat detection, and improve defenses. | Using micro-segmentation with Network Security Groups (NSGs) and assuming attackers are already in the network. |

---

## 🔵 2. Shared Responsibility Model

| Responsibility Area | On-Premises | IaaS (VMs) | PaaS (App Services, SQL DB) | SaaS (M365, Salesforce) |
| :--- | :---: | :---: | :---: | :---: |
| **Data & Information** | Customer | Customer | Customer | **Customer** |
| **User Accounts & Identities** | Customer | Customer | Customer | **Customer** |
| **Devices (Mobile, PC)** | Customer | Customer | Customer | **Customer** |
| **Applications** | Customer | Customer | Shared | Microsoft |
| **Operating System (OS)** | Customer | **Customer** | Microsoft | Microsoft |
| **Network Controls** | Customer | Shared | Microsoft | Microsoft |
| **Physical Datacenter / Hosts** | Customer | Microsoft | Microsoft | Microsoft |

> [!IMPORTANT]
> **Golden Rule**: In ALL cloud deployment models (IaaS, PaaS, SaaS), the **customer is ALWAYS responsible** for **Data**, **Identities/Accounts**, and **Access Management**.

---

## 🔵 3. Microsoft Entra ID (Identity & Access)

### Managed Identities
- **System-Assigned**: Tied directly to a single Azure resource lifecycle (e.g. one VM). Deleted automatically when the resource is deleted.
- **User-Assigned**: Standalone Azure resource that can be shared across **multiple Azure VMs / resources**.

### Privileged Identity Management (PIM)
- Provides **Just-In-Time (JIT)** time-bound role activation (e.g. 1–8 hours).
- Enforces approval workflows, MFA verification, and justification logging upon activation.
- Generates access reviews to audit over-privileged users.

### Conditional Access
- **Signals** (Who, Where, Device State, Risk Score) ➔ **Decision** (Allow, Block, Require MFA) ➔ **Enforcement**.

---

## 🔵 4. Microsoft Defender XDR & Security Solutions

| Service | Primary Protection Scope | Key Capabilities |
| :--- | :--- | :--- |
| **Microsoft Defender for Endpoint** | Laptops, desktops, servers, mobile devices | Endpoint Detection and Response (EDR), **Secure Score for Devices**, automated remediation |
| **Microsoft Defender for Office 365** | Emails, Teams chats, SharePoint, OneDrive | Anti-phishing, Safe Attachments, Safe Links |
| **Microsoft Defender for Identity** | On-premises Active Directory Domain Controllers | Detects pass-the-hash, pass-the-ticket, reconnaissance, lateral movement |
| **Microsoft Defender for Cloud Apps (MDCA)** | SaaS applications & cloud shadow IT | Cloud Discovery via log collectors, OAuth app governance, app connectors |
| **Microsoft Defender for Cloud** | Multi-cloud & hybrid infrastructure (Azure, AWS, GCP) | **Cloud Security Posture Management (CSPM)**, subscription **Secure Score**, CWPP |

---

## 🔵 5. Microsoft Sentinel (SIEM & SOAR)

- **SIEM (Security Information & Event Management)**: Centralizes, aggregates, and analyzes logs/telemetry from across the entire enterprise.
- **SOAR (Security Orchestration, Automated Response)**: Automates incident response and remediation using **Playbooks** (powered by Azure Logic Apps).
- **Core Components**:
  - **Data Connectors**: Ingest logs from Microsoft services, AWS, firewalls, and Syslog.
  - **Workbooks**: Interactive visualization dashboards.
  - **Analytics Rules**: Generate actionable security incidents from raw events using KQL.
  - **Jupyter Notebooks**: Advanced programmatic threat hunting and exploratory analysis.

---

## 🔵 6. Microsoft Purview & Compliance Solutions

| Compliance Feature | Primary Function |
| :--- | :--- |
| **Compliance Manager** | Calculates an organizational **Compliance Score** and provides prioritized **Improvement Actions** against regulatory standards (ISO 27001, GDPR, NIST). |
| **Sensitivity Labels** | Classifies and protects data across documents and emails with encryption, watermarks, and access restrictions. |
| **Data Loss Prevention (DLP)** | Prevents accidental sharing of sensitive data (credit cards, SSNs) across Exchange, SharePoint, OneDrive, Teams, and **Endpoints** (Windows/macOS). |
| **Insider Risk Management** | Detects malicious or inadvertent insider risks (data theft by departing employees, IP leaks) through **Policies**, **Alerts**, and **Cases**. |
| **eDiscovery (Standard/Premium)** | Identifies, preserves (legal holds), collects, and exports content for legal discovery and investigations. |
| **Communication Compliance** | Monitors organizational communications for regulatory violations, profanity, and sensitive data leakage. |
