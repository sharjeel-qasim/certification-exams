# AI-900 / AI-901: Microsoft Azure AI Fundamentals — Question Bank

[![Azure](https://img.shields.io/badge/Microsoft_Azure-0089D6?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/)
[![Exam](https://img.shields.io/badge/Exam-AI--900%20%2F%20AI--901-blue?style=for-the-badge)](#table-of-contents)
[![Questions](https://img.shields.io/badge/Questions-Comprehensive%20MCQs-success?style=for-the-badge)](#table-of-contents)
[![Cheat Sheet](https://img.shields.io/badge/Study_Guide-Cheat_Sheet-orange?style=for-the-badge)](CHEAT_SHEET.md)

Comprehensive Multiple Choice Question (MCQ) Practice Bank for the **Microsoft Certified: Azure AI Fundamentals (AI-900 / AI-901)** exam. Aligned to the latest Microsoft Learn exam objectives, covering Generative AI, Large Language Models (LLMs), Microsoft Foundry SDK, AI Agents, Computer Vision, NLP, and Responsible AI principles.

> [!TIP]
> Preparing for the exam? Review the [AI-900 / AI-901 Last-Minute Cram Sheet](CHEAT_SHEET.md) for the 6 Responsible AI Principles, Machine Learning models comparison, and Computer Vision task matrices.

---

## Table of Contents

- [Domain 1: Describe Artificial Intelligence Workloads & Considerations (Responsible AI)](#domain-1-describe-artificial-intelligence-workloads--considerations-responsible-ai)
- [Domain 2: Fundamental Principles of Machine Learning on Azure](#domain-2-fundamental-principles-of-machine-learning-on-azure)
- [Domain 3: Features of Computer Vision Workloads on Azure](#domain-3-features-of-computer-vision-workloads-on-azure)
- [Domain 4: Features of Natural Language Processing (NLP) & Speech Workloads on Azure](#domain-4-features-of-natural-language-processing-nlp--speech-workloads-on-azure)
- [Domain 5: Generative AI, Large Language Models & AI Agents on Azure](#domain-5-generative-ai-large-language-models--ai-agents-on-azure)

---

## Domain 1: Describe Artificial Intelligence Workloads & Considerations (Responsible AI)

### Question 1
When you design an AI system to assess whether loans should be approved, the factors used to make the decision should be explained to the applicant. Which Microsoft responsible AI principle does this address?

- **A.** Inclusiveness
- **B.** Transparency
- **C.** Fairness
- **D.** Reliability and safety

**Correct answer:** B

> **Why:** Transparency requires that AI systems are understandable and explainable so that stakeholders and users know how conclusions and automated decisions are reached.

---

### Question 2
You have an AI-based loan approval system. During testing, you discover that the system exhibits demographic and gender bias in approving applications. Which responsible AI principle was violated?

- **A.** Inclusiveness
- **B.** Fairness
- **C.** Reliability and safety
- **D.** Accountability

**Correct answer:** B

> **Why:** The Fairness principle states that AI systems should treat all people fairly and without discrimination across gender, race, ethnicity, or demographic groups.

---

### Question 3
You are designing an AI system. Which task should you include to help the service meet the Microsoft **Inclusiveness** principle for responsible AI?

- **A.** Publish a detailed technical architecture whitepaper explaining how neural networks operate.
- **B.** Anonymize user records before training the model.
- **C.** Ensure that all visuals and user interfaces have associated text and alt-tags readable by screen readers.
- **D.** Run stress testing to verify consistent response times under peak traffic.

**Correct answer:** C

> **Why:** Inclusiveness ensures that AI solutions empower everyone and engage people of all abilities, including users with visual, auditory, or physical disabilities (e.g. providing screen-reader compatible text).

---

### Question 4
The Microsoft responsible AI principle of **Reliability and Safety** requires that an AI system must:

- **A.** Expose all underlying training data to the public.
- **B.** Require multi-factor authentication for every query.
- **C.** Perform consistently and safely under both expected operational conditions and edge cases.
- **D.** Never use pre-trained third-party foundation models.

**Correct answer:** C

> **Why:** Reliability and Safety requires that AI systems operate consistently and robustly as intended, minimizing risks and handling unexpected situations safely.

---

### Question 5
Which Microsoft responsible AI principle states that people must remain ultimately answerable for how an AI system is governed and operated?

- **A.** Accountability
- **B.** Transparency
- **C.** Inclusiveness
- **D.** Fairness

**Correct answer:** A

> **Why:** Accountability establishes that human developers, data scientists, and organizations are responsible for designing, deploying, and governing AI systems within legal and ethical standards.

---

### Question 6
An organization trains an AI model on sensitive hospital patient records. To adhere to Microsoft's **Privacy and Security** principle, what should the team do?

- **A.** Make the training datasets publicly accessible to ensure transparency.
- **B.** Ensure that personally identifiable health information (PHI) is encrypted, access-controlled, and anonymized during training and inference.
- **C.** Disable logging to prevent monitoring.
- **D.** Store model weights in an unauthenticated blob container.

**Correct answer:** B

> **Why:** Privacy and Security mandates that AI systems respect personal data rights and safeguard confidential information against exposure or unauthorized access throughout the data lifecycle.

---

## Domain 2: Fundamental Principles of Machine Learning on Azure

### Question 7
You need to predict the selling price of a used car based on its mileage, age, make, and engine size. Which type of machine learning model should you train?

- **A.** Regression
- **B.** Binary Classification
- **C.** Multiclass Classification
- **D.** Clustering

**Correct answer:** A

> **Why:** Regression is a supervised learning technique used to predict continuous numeric values (such as prices, temperatures, or sales).

---

### Question 8
An email service needs to automatically classify incoming messages as either **Spam** or **Not Spam**. Which type of machine learning workload is this?

- **A.** Regression
- **B.** Binary Classification
- **C.** Clustering
- **D.** Anomaly Detection

**Correct answer:** B

> **Why:** Binary classification predicts one of two mutually exclusive discrete outcomes (e.g. Yes/No, Spam/Not Spam, True/False).

---

### Question 9
A retail marketing team wants to group customers into segments based on purchasing behavior and visit frequency without using prior labeled categories. Which machine learning approach should they use?

- **A.** Regression
- **B.** Supervised classification
- **C.** Clustering
- **D.** Time series forecasting

**Correct answer:** C

> **Why:** Clustering is an unsupervised machine learning method that partitions unlabeled data points into natural groupings based on feature similarity.

---

### Question 10
In natural language processing and machine learning, what is the primary purpose of **Tokenization**?

- **A.** To translate text into another human language.
- **B.** To encrypt sentences for secure storage in database columns.
- **C.** To break down raw text into smaller discrete units (words, sub-words, or characters) represented as numerical IDs.
- **D.** To check grammatical spelling mistakes in a document.

**Correct answer:** C

> **Why:** Tokenization splits text sequences into tokens (words or sub-word fragments), allowing models to map text into numerical vectors that neural networks can process.

---

### Question 11
What are **Vector Embeddings** in machine learning?

- **A.** Compressed image thumbnails stored in cloud storage.
- **B.** Vector-based numerical representations of tokens in a multi-dimensional space that capture semantic meaning and relationships.
- **C.** Rule-based decision trees compiled into binary code.
- **D.** Audio frequencies stored in MP3 format.

**Correct answer:** B

> **Why:** Embeddings represent words, sentences, or documents as dense numerical vectors where mathematically close vectors share similar semantic meanings (e.g., Word2Vec, Ada embeddings).

---

## Domain 3: Features of Computer Vision Workloads on Azure

### Question 12
Which type of computer vision solution detects specific items in an image and provides **bounding box coordinates** for each detected item?

- **A.** Image Classification
- **B.** Object Detection
- **C.** Optical Character Recognition (OCR)
- **D.** Facial Analysis

**Correct answer:** B

> **Why:** Object Detection identifies the category of items in an image and returns rectangular bounding box coordinates (`x`, `y`, `width`, `height`) locating each item.

---

### Question 13
You need to extract typed and handwritten text from scanned invoices and receipts. Which Azure AI capability should you use?

- **A.** Optical Character Recognition (OCR) / Azure Document Intelligence
- **B.** Semantic Segmentation
- **C.** Image Classification
- **D.** Face Recognition

**Correct answer:** A

> **Why:** Optical Character Recognition (OCR), available through Azure AI Vision and Azure Document Intelligence, extracts printed and handwritten text from physical documents and images into structured digital text.

---

### Question 14
You are developing an application that analyzes video files to extract insights and structured fields using Azure Content Understanding. How should you initiate the analysis and retrieve the results asynchronously?

- **A.** Call `get_results()` immediately after uploading the file.
- **B.** Execute a synchronous SQL query against the video blob.
- **C.** Call `begin_analyze()`, and then call `poller.result()` to await and retrieve the analysis results.
- **D.** Use the Speech SDK's `RecognizeOnceAsync()` method.

**Correct answer:** C

> **Why:** Large media and document analysis in Azure Content Understanding / Document Intelligence uses a long-running asynchronous operation pattern: `begin_analyze()` starts the operation and returns a poller, and `poller.result()` waits for completion.

---

### Question 15
When using the Azure OpenAI Responses API with a vision-enabled model (such as GPT-4o) to analyze a locally captured image, how should the image data be provided in the request payload?

- **A.** As a base64-encoded image string or image URL within the user message content array.
- **B.** As an attachment in an email protocol.
- **C.** As a raw CSV file containing RGB pixel integers.
- **D.** By saving the file to local disk and passing the local Windows file path.

**Correct answer:** A

> **Why:** Multimodal vision models in Azure OpenAI accept images formatted as either accessible HTTPS image URLs or base64-encoded data URIs (`data:image/jpeg;base64,...`) in the message content payload.

---

## Domain 4: Features of Natural Language Processing (NLP) & Speech Workloads on Azure

### Question 16
You have a website that contains customer reviews written in multiple languages (Spanish, German, French). You need to store all reviews in English and present them to users in their preferred language. Which Azure AI service feature should you implement?

- **A.** Azure AI Translator (Translation)
- **B.** Key Phrase Extraction
- **C.** Entity Recognition
- **D.** Sentiment Analysis

**Correct answer:** A

> **Why:** Azure AI Translator provides real-time automated text translation across dozens of supported languages.

---

### Question 17
You are developing an application that extracts key named elements such as company names, dates, financial amounts, and physical locations from legal contracts. Which NLP feature should you use?

- **A.** Language Detection
- **B.** Sentiment Analysis
- **C.** Named Entity Recognition (NER)
- **D.** Speech Synthesis

**Correct answer:** C

> **Why:** Named Entity Recognition (NER) identifies and categorizes specific entities (people, places, organizations, dates, quantities) in unstructured text.

---

### Question 18
You are developing a .NET application that continuously captures audio from a microphone and transcribes spoken words into real-time text using Azure Speech. Which class in the Azure Speech SDK should you instantiate?

- **A.** `SpeechSynthesizer`
- **B.** `TranslationRecognizer`
- **C.** `SpeechRecognizer`
- **D.** `AudioDataStream`

**Correct answer:** C

> **Why:** `SpeechRecognizer` is the primary class in the Azure AI Speech SDK used for speech-to-text transcription from microphone audio inputs or audio files.

---

### Question 19
Which Azure AI service should you use to convert typed textual responses into natural, human-sounding synthesized voice output?

- **A.** Azure AI Speech (Text-to-Speech)
- **B.** Azure AI Language (NER)
- **C.** Azure AI Vision
- **D.** Azure AI Search

**Correct answer:** A

> **Why:** Text-to-Speech (speech synthesis) in Azure AI Speech converts written text into synthesized audible spoken audio using neural voices.

---

## Domain 5: Generative AI, Large Language Models & AI Agents on Azure

### Question 20
Which is the most accurate description of **Generative AI**?

- **A.** An older form of statistical AI that has been completely superseded by rule-based expert systems.
- **B.** AI models that use large language models and foundation neural networks to generate original content (text, code, images, audio) in response to natural language prompts.
- **C.** An algorithm designed exclusively for sorting relational database records.
- **D.** A hardware chip used for accelerating network packet routing.

**Correct answer:** B

> **Why:** Generative AI refers to deep learning models trained on vast amounts of data that can generate new, original content (text, code, images, audio) based on user prompts.

---

### Question 21
What is an **AI Agent** in modern artificial intelligence systems?

- **A.** An autonomous software entity that can perceive its environment, reason using language models, utilize tools/APIs, and execute multi-step tasks on behalf of a user.
- **B.** A human customer support representative who monitors AI systems.
- **C.** A simple static HTML web page.
- **D.** A hardware sensor attached to a robotic arm.

**Correct answer:** A

> **Why:** AI Agents combine language models with reasoning, memory, and tool-calling capabilities to autonomously execute actions and workflows to achieve specific goals.

---

### Question 22
What is the primary purpose of a **System Prompt** when configuring a generative AI model?

- **A.** To provide foundational instructions, behavioral boundaries, persona definitions, and response constraints to guide the model's output before user prompts are evaluated.
- **B.** To format the computer's hard drive before running Python scripts.
- **C.** To compress the model weights into an encrypted ZIP file.
- **D.** To measure the CPU temperature of the GPU cluster.

**Correct answer:** A

> **Why:** System prompts establish the instructions, tone, behavioral guardrails, and role definitions for generative models across conversations.

---

### Question 23
When developing a lightweight generative application using the **Microsoft Foundry SDK**, which client class is used as the central entry point to connect to your project and deploy agents?

- **A.** `AIProjectClient`
- **B.** `BlobServiceClient`
- **C.** `SqlConnection`
- **D.** `HttpClientHandler`

**Correct answer:** A

> **Why:** `AIProjectClient` is the primary client in the Microsoft Foundry SDK used to authenticate, manage project connections, deploy agents, and run inference.

---

### Question 24
What is the primary benefit of **Retrieval-Augmented Generation (RAG)** architecture?

- **A.** It allows models to generate content without using any tokens.
- **B.** It dynamically grounds model responses in private, up-to-date enterprise knowledge bases and documents retrieved via vector search, reducing hallucinations without requiring expensive fine-tuning.
- **C.** It replaces neural networks with relational SQL databases.
- **D.** It forces models to run completely offline without internet connectivity.

**Correct answer:** B

> **Why:** RAG retrieves relevant excerpts from external enterprise documents and injects them into the model prompt, ensuring accurate, fresh, and grounded responses without model retraining.
