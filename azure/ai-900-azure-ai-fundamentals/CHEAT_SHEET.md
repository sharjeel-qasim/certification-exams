# ⚡ AI-900 / AI-901: Microsoft Azure AI Fundamentals — Cram & Cheat Sheet

[![Azure](https://img.shields.io/badge/Microsoft_Azure-0089D6?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/)
[![Exam](https://img.shields.io/badge/Exam-AI--900%20%2F%20AI--901-blue?style=for-the-badge)](#-high-frequency-exam-topics)

Quick-reference cheat sheet for **Microsoft Certified: Azure AI Fundamentals (AI-900 / AI-901)**. Covers the 6 Responsible AI Principles, Machine Learning models, Computer Vision tasks, Natural Language Processing (NLP), Speech services, Generative AI, and the Microsoft Foundry SDK.

---

## 🔵 The 6 Guiding Principles of Responsible AI (MEMORIZE THIS)

| Principle | Core Definition | Example / Scenario in Exam |
| :--- | :--- | :--- |
| **Fairness** | AI systems should treat all people fairly without demographic or gender bias. | Loan approval or hiring model must not discriminate against gender or ethnicity. |
| **Reliability & Safety** | AI systems should perform reliably, consistently, and safely under expected/unexpected conditions. | Autonomous vehicle or medical diagnosis AI must handle errors safely. |
| **Privacy & Security** | AI systems should be secure and respect data privacy throughout data lifecycle. | Anonymizing training data, protecting patient medical records from exposure. |
| **Inclusiveness** | AI systems should empower everyone and engage people regardless of physical ability. | Screen reader support, alt text for images, speech-to-text for hearing impaired. |
| **Transparency** | AI systems should be explainable, understandable, and users must know an AI is being used. | Providing clear explanations for why a credit limit was denied; AI disclaimers. |
| **Accountability** | People are ultimately accountable for how AI systems are governed and operated. | Designers and operators must adhere to governance frameworks and legal standards. |

---

## 🔵 Machine Learning Workloads Comparison

| Workload Type | Target / Prediction Type | Supervised / Unsupervised | Example |
| :--- | :--- | :--- | :--- |
| **Regression** | Continuous numeric value | Supervised (labeled numeric target) | Predicting house prices, temperature, stock trends |
| **Binary Classification** | Two discrete classes (Yes/No, True/False) | Supervised (labeled binary target) | Spam detection, disease diagnosis, loan approval |
| **Multiclass Classification**| Multiple discrete categories | Supervised (labeled category target) | Classifying animal species, email categories |
| **Clustering** | Grouping similar unlabelled data | **Unsupervised** (no label) | Customer segmentation, document grouping |
| **Anomaly Detection** | Identifying unusual patterns / outliers | Unsupervised / Semi-supervised | Credit card fraud detection, server failure warning |

---

## 🔵 Computer Vision Workload Capabilities

| Vision Capability | What It Detects / Returns | Common Azure Service |
| :--- | :--- | :--- |
| **Image Classification** | Assigns an entire image to a category / tag. | Azure AI Vision |
| **Object Detection** | Identifies specific objects **AND their bounding box coordinates** (`[x, y, w, h]`). | Azure AI Vision |
| **Semantic Segmentation** | Classifies **individual pixels** to identify exact object boundaries. | Azure AI Custom Vision |
| **Optical Character Recognition (OCR)** | Extracts printed or handwritten text from images/documents. | Azure Document Intelligence / Vision |
| **Spatial Analysis** | Tracks real-time movement and presence of people in video feeds. | Azure AI Vision Spatial Analysis |
| **Facial Detection & Analysis** | Detects human faces, facial attributes, and landmarks. | Azure AI Face |

---

## 🔵 NLP & Speech Services

| NLP / Speech Feature | What It Does | Primary Use Case |
| :--- | :--- | :--- |
| **Key Phrase Extraction** | Identifies the main talking points / themes in text. | Summarizing customer reviews or articles |
| **Entity Recognition (NER)** | Identifies specific entities (people, places, dates, organizations). | Extracting names and dates from legal contracts |
| **Sentiment Analysis** | Returns a sentiment score (`positive`, `neutral`, `negative`). | Analyzing social media feedback or survey responses |
| **Language Detection** | Identifies the spoken or written language (e.g. `en`, `es`, `de`). | Routing multilingual customer support tickets |
| **Speech-to-Text (STT)** | Transcribes spoken audio into text (`SpeechRecognizer`). | Real-time meeting transcripts, voice dictation |
| **Text-to-Speech (TTS)** | Synthesizes natural-sounding speech from text (`SpeechSynthesizer`). | Voice assistants, reading responses aloud |

---

## 🔵 Generative AI, Large Language Models (LLMs) & Agents

### Core Concepts & Components
- **Tokenization**: Breaking down raw text into smaller numerical units (tokens) for processing.
- **Embeddings**: Vector representations of tokens in a high-dimensional semantic space (e.g. Word2Vec) capturing contextual relationships.
- **Attention Mechanism**: Allows transformers to examine relationships between all tokens across long contexts dynamically.
- **System Prompt**: Top-level instructions that define the model's persona, boundaries, format rules, and safety guardrails.
- **Retrieval-Augmented Generation (RAG)**: Pattern that retrieves relevant external documents (via vector search) and injects them into the prompt before generation.

### Microsoft Foundry & SDK Quick Reference
- **Microsoft Foundry Portal**: Web portal for discovering models, configuring AI agents, and testing prompts in the playground.
- **`AIProjectClient`**: The primary entry point client in the Microsoft Foundry SDK for connecting to projects, executing completions, and calling agents.
- **Multimodal Models**: Vision-enabled models (like GPT-4o) accept messages containing both text and **base64-encoded image payloads** or image URLs.
