# 🎓 Certification Exams & Question Banks

[![GitHub License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Certifications](https://img.shields.io/badge/Certifications-4%20Available-success.svg)](#-available-certifications)
[![Format](https://img.shields.io/badge/Format-MCQs_%2B_Verified_Answers_%2B_Explanations-orange.svg)](#-question-bank-format--structure)
[![Contribution](https://img.shields.io/badge/Contributions-Welcome-brightgreen.svg)](#-how-to-contribute--add-exams)

Welcome to the **Certification Exams & Question Banks** repository! This repository is a curated, high-quality knowledge base of verified sample exam questions, multiple-choice options, correct answer keys, and concise technical explanations for professional software engineering, cloud, database, and infrastructure certifications.

---

## 🌟 Available Certifications

| Technology / Category | Certification Exam | Questions & Study Material | Status | Direct Link |
| :--- | :--- | :---: | :---: | :--- |
| **🔴 Redis** | [Redis for .NET Developers](redis/redis-for-dotnet-developers/README.md) | **65 MCQs** | ✅ Verified | [View Question Bank →](redis/redis-for-dotnet-developers/README.md) |
| **☁️ Microsoft Azure** | [DP-900: Azure Data Fundamentals](azure/dp-900-azure-data-fundamentals/README.md) | **50 MCQs** + [Cram Sheet](azure/dp-900-azure-data-fundamentals/CHEAT_SHEET.md) | ✅ Verified | [View Question Bank →](azure/dp-900-azure-data-fundamentals/README.md) |
| **🤖 Microsoft Azure** | [AI-900 / AI-901: Azure AI Fundamentals](azure/ai-900-azure-ai-fundamentals/README.md) | **45 MCQs** + [Cram Sheet](azure/ai-900-azure-ai-fundamentals/CHEAT_SHEET.md) | ✅ Verified | [View Question Bank →](azure/ai-900-azure-ai-fundamentals/README.md) |
| **🔒 Microsoft Azure** | [SC-900: Security, Compliance & Identity](azure/sc-900-security-compliance-identity/README.md) | **50 MCQs** + [Cram Sheet](azure/sc-900-security-compliance-identity/CHEAT_SHEET.md) | ✅ Verified | [View Question Bank →](azure/sc-900-security-compliance-identity/README.md) |
| **☁️ Cloud & DevOps** | *(Upcoming: AWS, GCP, CKA, Terraform)* | — | ⏳ In Planning | *Coming soon* |
| **☕ Backend & Frameworks** | *(Upcoming: Spring, .NET, Node.js)* | — | ⏳ In Planning | *Coming soon* |

---

## 🧠 Question Bank Format & Structure

Each question in this repository is presented in a clean, exam-ready format:

1. **Question & Scenario**: The exact question statement, scenarios, and code snippets.
2. **Options / Answer Area**: Clear multiple-choice options (**A**, **B**, **C**, **D**) or dedicated **Answer Area Tables** for Yes/No statements and matching drills.
3. **Correct Answer Key**: Clearly specified correct option(s) (e.g. `Correct answers: A, C` or `Correct answer: B`).
4. **Brief Technical Explanation (`Why`)**: Clear, concise reasoning explaining why the answer is correct and resolving edge cases.

---

## 📂 Repository Structure

```text
certification-exams/
├── .gitignore
├── README.md                                    # Root repository index & guidelines
│
├── redis/                                       # Redis Certifications
│   └── redis-for-dotnet-developers/             # Redis for .NET Developers Exam
│       └── README.md                            # 65 MCQs + Verified Answers + Explanations
│
├── azure/                                       # Microsoft Azure Certifications
│   ├── dp-900-azure-data-fundamentals/          # DP-900 Exam Guide & Question Bank
│   │   ├── README.md                            # 50 MCQs organized by 4 Official Domains
│   │   └── CHEAT_SHEET.md                       # Last-Minute Cram Sheet & Comparison Matrices
│   │
│   ├── ai-900-azure-ai-fundamentals/            # AI-900 / AI-901 Exam Guide & Question Bank
│   │   ├── README.md                            # 45 MCQs on Generative AI, LLMs, Vision, NLP
│   │   └── CHEAT_SHEET.md                       # Responsible AI, ML & Foundry SDK Cram Sheet
│   │
│   └── sc-900-security-compliance-identity/     # SC-900 Exam Guide & Question Bank
│       ├── README.md                            # 50 MCQs on Zero Trust, Entra, Defender, Purview
│       └── CHEAT_SHEET.md                       # High-Yield Cram Sheet & Product Comparisons
│
└── [category]/                                  # Future certification categories
    └── [exam-name]/
        └── README.md
```

---

## 🚀 How to Add New Exams

This repository is structured to seamlessly scale to new exams across different domains (Cloud, Databases, Kubernetes, Programming Languages).

When adding a new certification:

1. Create a dedicated directory under the relevant category folder:
   ```text
   <technology>/<certification-name>/README.md
   ```
2. Follow the established MCQ formatting template:
   - **Question Statement**: Scenario description, code blocks, and number of answers to select.
   - **Options**: Clear bulleted list of choices `A`, `B`, `C`, `D` or direct Answer Area table for Yes/No statements.
   - **Correct Answer(s)**: `**Correct answer(s):** <Letter(s)>`
   - **Brief Explanation**: `> **Why:** <Concise explanation of the underlying concept>`
3. Update the [Available Certifications](#-available-certifications) table in this root `README.md`.

---

## 📄 License & Disclaimer

- The study guides and explanations in this repository are created for educational and certification preparation purposes.
- Content is provided under the [MIT License](LICENSE).
