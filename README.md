# 🎓 Certification Exams & Question Banks

[![GitHub License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Certifications](https://img.shields.io/badge/Certifications-7%20Available-success.svg)](#-available-certifications)
[![Format](https://img.shields.io/badge/Format-MCQs_%2B_Verified_Answers_%2B_Explanations-orange.svg)](#-question-bank-format--structure)
[![Contribution](https://img.shields.io/badge/Contributions-Welcome-brightgreen.svg)](#-how-to-contribute--add-exams)

Welcome to the **Certification Practice Exams & Study Guides** repository! This repository is a curated, high-quality knowledge base of verified practice exam questions, multiple-choice options, correct answer keys, and concise technical explanations for professional software engineering, cloud, database, and infrastructure certifications.

---

## 🌟 Available Certifications

| Technology / Category | Certification Exam | Practice Questions | Study Guide | Status | Direct Link |
| :--- | :--- | :---: | :---: | :---: | :--- |
| **🔴 Redis** | [Redis for .NET Developers](redis/redis-for-dotnet-developers/README.md) | **65 MCQs** | [⚡ Cheat Sheet](redis/redis-for-dotnet-developers/CHEAT_SHEET.md) | ✅ Verified | [View Questions →](redis/redis-for-dotnet-developers/README.md) |
| **🔴 Redis** | [Redis for JavaScript Developers](redis/redis-for-javascript-developers/README.md) | **45 MCQs** | [⚡ Cheat Sheet](redis/redis-for-javascript-developers/CHEAT_SHEET.md) | ✅ Verified | [View Questions →](redis/redis-for-javascript-developers/README.md) |
| **🔴 Redis** | [Redis Associate Cloud Operator](redis/redis-associate-cloud-operator/README.md) | **65 MCQs** | [⚡ Cheat Sheet](redis/redis-associate-cloud-operator/CHEAT_SHEET.md) | ✅ Verified | [View Questions →](redis/redis-associate-cloud-operator/README.md) |
| **☁️ Microsoft Azure** | [DP-900: Microsoft Azure Data Fundamentals](azure/dp-900-azure-data-fundamentals/README.md) | **50 MCQs** | [⚡ Cheat Sheet](azure/dp-900-azure-data-fundamentals/CHEAT_SHEET.md) | ✅ Verified | [View Questions →](azure/dp-900-azure-data-fundamentals/README.md) |
| **🤖 Microsoft Azure** | [AI-900: Microsoft Azure AI Fundamentals](azure/ai-900-azure-ai-fundamentals/README.md) | **45 MCQs** | [⚡ Cheat Sheet](azure/ai-900-azure-ai-fundamentals/CHEAT_SHEET.md) | ✅ Verified | [View Questions →](azure/ai-900-azure-ai-fundamentals/README.md) |
| **🧠 Microsoft Azure** | [AI-103: Developing AI Apps and Agents on Azure](azure/ai-103-developing-ai-apps-and-agents/README.md) | **64 MCQs** | [⚡ Cheat Sheet](azure/ai-103-developing-ai-apps-and-agents/CHEAT_SHEET.md) | ✅ Verified | [View Questions →](azure/ai-103-developing-ai-apps-and-agents/README.md) |
| **🔒 Microsoft Azure** | [SC-900: Microsoft Security, Compliance, and Identity Fundamentals](azure/sc-900-security-compliance-identity/README.md) | **50 MCQs** | [⚡ Cheat Sheet](azure/sc-900-security-compliance-identity/CHEAT_SHEET.md) | ✅ Verified | [View Questions →](azure/sc-900-security-compliance-identity/README.md) |

---

## 🧠 Question Bank Format & Structure

Each question in this repository is designed for **active recall** and deep technical understanding:

1. **Question & Scenario**: Real-world exam scenarios, architecture tradeoffs, and code snippets.
2. **Realistic Exam Options / Answer Area**: Multiple-choice options (**A**, **B**, **C**, **D**) with authentic exam-grade distractors, or dedicated **Answer Area Tables** for Yes/No statements and matching drills.
3. **Interactive Spoiler Toggle (`<details>`)**: Answers are hidden behind a click-to-reveal **`💡 View Answer & Explanation`** toggle so you can test yourself without accidentally seeing the answer first.
4. **Correct Answer + Distractor Breakdown (`Why`)**: Explains both **why the correct answer works** and **why the wrong options (exam traps) fail**, helping you master multiple concepts from every single question.
5. **Last-Minute Cram Sheet (`CHEAT_SHEET.md`)**: Every certification includes a dedicated high-yield cheat sheet with comparison tables, CLI/SDK references, and common exam traps.

---

## 📂 Repository Structure

```text
certification-exams/
├── .gitignore
├── README.md                                    # Root repository index & guidelines
│
├── redis/                                       # Redis Certifications
│   ├── redis-for-dotnet-developers/             # Redis for .NET Developers
│   │   ├── README.md                            # 65 MCQs + Active-Recall Spoilers + Explanations
│   │   └── CHEAT_SHEET.md                       # Data structures, C# patterns & Cram Sheet
│   │
│   ├── redis-for-javascript-developers/         # Redis for JavaScript Developers
│   │   ├── README.md                            # 45 MCQs on node-redis, Streams, Geo, JSON
│   │   └── CHEAT_SHEET.md                       # Node.js patterns, Pub/Sub & Cram Sheet
│   │
│   └── redis-associate-cloud-operator/          # Redis Associate Cloud Operator
│       ├── README.md                            # 65 MCQs on Pro vs Essentials, HA, Private Link, IaC
│       └── CHEAT_SHEET.md                       # Architecture, Networking & Prometheus Cram Sheet
│
└── azure/                                       # Microsoft Azure Certifications
    ├── dp-900-azure-data-fundamentals/          # DP-900: Microsoft Azure Data Fundamentals
    │   ├── README.md                            # 50 MCQs organized by 4 Official Domains
    │   └── CHEAT_SHEET.md                       # Last-Minute Cram Sheet & Comparison Matrices
    │
    ├── ai-900-azure-ai-fundamentals/            # AI-900: Microsoft Azure AI Fundamentals
    │   ├── README.md                            # 45 MCQs on Generative AI, LLMs, Vision, NLP
    │   └── CHEAT_SHEET.md                       # Responsible AI, ML & Foundry SDK Cram Sheet
    │
    ├── ai-103-developing-ai-apps-and-agents/    # AI-103: Developing AI Apps and Agents on Azure
    │   ├── README.md                            # 64 MCQs on Foundry Agents, RAG, Multimodal, Safety
    │   └── CHEAT_SHEET.md                       # Orchestration, Evaluators & Search Cram Sheet
    │
    └── sc-900-security-compliance-identity/     # SC-900: Microsoft Security, Compliance, and Identity Fundamentals
        ├── README.md                            # 50 MCQs on Zero Trust, Entra, Defender, Purview
        └── CHEAT_SHEET.md                       # High-Yield Cram Sheet & Product Comparisons
```

---

## 🚀 How to Add New Exams

This repository is structured to seamlessly scale to new exams across different domains (Cloud, Databases, Kubernetes, Programming Languages).

When adding a new certification:

1. Create a dedicated directory under the relevant category folder:
   ```text
   <technology>/<certification-name>/README.md
   <technology>/<certification-name>/CHEAT_SHEET.md
   ```
2. Follow the established MCQ formatting template:
   - **Question Statement**: Scenario description, code blocks, and number of answers to select.
   - **Options**: Clear bulleted list of choices `A`, `B`, `C`, `D` or direct Answer Area table for Yes/No statements.
   - **Collapsible Answer & Explanation**:
     ```markdown
     <details>
     <summary>💡 <b>View Answer & Explanation</b></summary>

     **Correct answer:** <Letter(s)>

     > **Why:** <Explanation of why the correct option is right AND why the wrong options are incorrect>

     </details>
     ```
3. Update the [Available Certifications](#-available-certifications) table in this root `README.md`.

---

## 📄 License & Disclaimer

- The study guides and explanations in this repository are created for educational and certification preparation purposes.
- Content is provided under the [MIT License](LICENSE).
