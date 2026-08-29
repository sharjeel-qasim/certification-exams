# 🎓 Certification Exams & Question Banks

[![GitHub License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Certifications](https://img.shields.io/badge/Certifications-Available-success.svg)](#-available-certifications)
[![Format](https://img.shields.io/badge/Format-MCQs_%2B_Verified_Answers_%2B_Explanations-orange.svg)](#-study-guide-design--methodology)
[![Contribution](https://img.shields.io/badge/Contributions-Welcome-brightgreen.svg)](#-how-to-contribute--add-exams)

Welcome to the **Certification Exams & Question Banks** repository! This repository is a curated, high-quality knowledge base of verified sample exam questions, multiple-choice options, correct answer keys, and concise technical explanations for professional software engineering, cloud, database, and infrastructure certifications.

---

## 🌟 Available Certifications

| Technology / Category | Certification Exam | Questions | Status | Direct Link |
| :--- | :--- | :---: | :---: | :--- |
| **🔴 Redis** | [Redis for .NET Developers](redis/redis-for-dotnet-developers/README.md) | **65 Questions** | ✅ Verified | [View Question Bank →](redis/redis-for-dotnet-developers/README.md) |
| **☁️ Cloud & DevOps** | *(Upcoming: AWS, Azure, GCP, CKA)* | — | ⏳ In Planning | *Coming soon* |
| **☕ Backend & Frameworks** | *(Upcoming: Spring, .NET, Node.js)* | — | ⏳ In Planning | *Coming soon* |

---

## 🧠 Question Bank Format & Structure

Each question in this repository is presented in a clean, exam-ready format:

1. **Question & Scenario**: The exact question statement, scenarios, and code snippets.
2. **Options**: All multiple choice options (**A**, **B**, **C**, **D**, **E**).
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
   - **Options**: Clear bulleted list of choices `A`, `B`, `C`, `D`.
   - **Correct Answer(s)**: `**Correct answer(s):** <Letter(s)>`
   - **Brief Explanation**: `> **Why:** <Concise explanation of the underlying concept>`
3. Update the [Available Certifications](#-available-certifications) table in this root `README.md`.

---

## 📄 License & Disclaimer

- The study guides and explanations in this repository are created for educational and certification preparation purposes.
- Content is provided under the [MIT License](LICENSE).
