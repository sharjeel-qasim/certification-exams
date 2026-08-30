# AI-900 / AI-901: Microsoft Azure AI Fundamentals — Comprehensive Question Bank

[![Azure](https://img.shields.io/badge/Microsoft_Azure-0089D6?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/)
[![Exam](https://img.shields.io/badge/Exam-AI--900%20%2F%20AI--901-blue?style=for-the-badge)](#table-of-contents)
[![Questions](https://img.shields.io/badge/Questions-45%20Verified%20Questions-success?style=for-the-badge)](#table-of-contents)
[![Cheat Sheet](https://img.shields.io/badge/Study_Guide-Cheat_Sheet-orange?style=for-the-badge)](CHEAT_SHEET.md)

Complete, cleaned, and verified Practice Question Bank for the **Microsoft Certified: Azure AI Fundamentals (AI-900 / AI-901)** exam. Curated directly from official Microsoft Learn assessments, practice exams, and training modules.

> [!TIP]
> Before practicing the questions, check out the [AI-900 / AI-901 Last-Minute Cram Sheet](CHEAT_SHEET.md) for quick-fire comparison tables on Responsible AI, Machine Learning algorithms, Vision tasks, and the Microsoft Foundry SDK.

---

## Table of Contents

- [Domain 1: Artificial Intelligence Workloads & Responsible AI (Q1 – Q8)](#domain-1-artificial-intelligence-workloads--responsible-ai)
- [Domain 2: Fundamental Principles of Machine Learning on Azure (Q9 – Q16)](#domain-2-fundamental-principles-of-machine-learning-on-azure)
- [Domain 3: Computer Vision & Multimodal Workloads on Azure (Q17 – Q22)](#domain-3-computer-vision--multimodal-workloads-on-azure)
- [Domain 4: Natural Language Processing (NLP) & Speech on Azure (Q23 – Q29)](#domain-4-natural-language-processing-nlp--speech-on-azure)
- [Domain 5: Generative AI, Large Language Models (LLMs) & AI Agents (Q30 – Q45)](#domain-5-generative-ai-large-language-models-llms--ai-agents)

---

## Domain 1: Artificial Intelligence Workloads & Responsible AI

### Question 1
When you design an AI system to assess whether loans should be approved, the factors used to make the decision should be explained to the applicant. Which Microsoft responsible AI principle does this address?

- **A.** Inclusiveness
- **B.** Transparency
- **C.** Fairness
- **D.** Reliability and safety

**Correct answer:** B

> **Why:** Transparency requires that AI systems are understandable and explainable so stakeholders and users know how conclusions, risk scores, and automated decisions are reached.

---

### Question 2
You have an AI-based loan approval system. During testing, you discover that the system exhibits demographic and gender bias in approving applications. Which responsible AI principle does this violate?

- **A.** Reliability and safety
- **B.** Fairness
- **C.** Transparency
- **D.** Accountability

**Correct answer:** B

> **Why:** Fairness requires AI systems to treat all people impartially without demographic, gender, racial, or socioeconomic discrimination.

---

### Question 3
You are building an AI system. Which task should you include to help the service meet the Microsoft **Inclusiveness** principle for responsible AI?

- **A.** Ensure that training datasets are representative of the entire population.
- **B.** Provide documentation to help developers debug code.
- **C.** Ensure that all visuals and user interfaces have associated text and alt-tags readable by screen readers.
- **D.** Enable autoscaling to ensure that the service scales based on load.

**Correct answer:** C

> **Why:** Inclusiveness ensures AI systems empower everyone and engage people of all physical and cognitive abilities, including users relying on screen readers and assistive technology.

---

### Question 4
The Microsoft responsible AI principle of **Reliability and Safety** requires AI systems to:

- **A.** Enable continuous human manual approval for every single operation.
- **B.** Ensure equitable demographic distribution of outcomes.
- **C.** Perform consistently and safely under expected operational conditions and handle errors gracefully.
- **D.** Provide clear technical architecture explanations to end users.

**Correct answer:** C

> **Why:** Reliability and Safety ensures AI solutions operate robustly, consistently, and securely across intended scenarios while preventing harm during unforeseen failures.

---

### Question 5
Which Microsoft responsible AI principle states that human beings must remain ultimately answerable for how an AI system is governed and operated?

- **A.** Accountability
- **B.** Transparency
- **C.** Inclusiveness
- **D.** Fairness

**Correct answer:** A

> **Why:** Accountability establishes that human developers, data scientists, and organizations are responsible for designing, deploying, and governing AI systems within ethical and legal boundaries.

---

### Question 6
For each of the following statements about data protection in AI systems, select **Yes** if the statement is true, otherwise select **No**:

| Statement | Answer |
| :--- | :---: |
| Restricting users to authorized data reduces the risk of sensitive data exposure when they use AI systems. | **Yes** |
| Sharing personal user data openly improves collaboration and supports responsible AI practices. | **No** |
| Protecting personal data and complying with data privacy regulations are key considerations in responsible AI. | **Yes** |

> **Why:**
> - **Statement 1 (Yes):** Applying the principle of least privilege ensures users only see data they are authorized to access, preventing sensitive data leakage.
> - **Statement 2 (No):** Unrestricted sharing of personal user data violates privacy principles and privacy regulations like GDPR.
> - **Statement 3 (Yes):** Protecting personally identifiable information (PII) and regulatory compliance are essential tenets of the Privacy and Security principle.

---

### Question 7
You are designing an AI system that will generate insurance quotes automatically. Match each requirement to the corresponding Microsoft responsible AI principle:

| Requirement | Responsible AI Principle |
| :--- | :--- |
| The decision-making process must be recorded so that staff can identify the reasoning behind a particular quote. | **Transparency** |
| A customer's personal information must be visible only to staff who are involved in the decision-making process. | **Privacy and security** |
| The system must be accessible to customers who use screen readers or assistive technology. | **Inclusiveness** |

> **Why:**
> - Auditability of reasoning and explainability map to **Transparency**.
> - Restricting customer personal information to authorized personnel maps to **Privacy and security**.
> - Accessibility via screen readers and assistive technology maps to **Inclusiveness**.

---

### Question 8
For each of the following statements regarding inclusiveness in AI systems, select **Yes** if the statement is true, otherwise select **No**:

| Statement | Answer |
| :--- | :---: |
| Designing an AI system for a typical user profile alone is sufficient to support inclusiveness. | **No** |
| A high number of active users guarantees an AI system provides an inclusive experience. | **No** |
| Providing accessible interfaces and multilingual language options helps support inclusiveness in an AI system. | **Yes** |

> **Why:**
> - **Statement 1 (No):** Designing solely for the "typical" user excludes people with disabilities or diverse needs.
> - **Statement 2 (No):** A large volume of active users does not mean the system is accessible or inclusive.
> - **Statement 3 (Yes):** Offering accessible controls, screen-reader support, and multiple languages actively fosters inclusiveness.

---

## Domain 2: Fundamental Principles of Machine Learning on Azure

### Question 9
You need to predict the selling price of a used car based on its mileage, age, make, and engine size. Which type of machine learning model should you train?

- **A.** Regression
- **B.** Binary Classification
- **C.** Multiclass Classification
- **D.** Clustering

**Correct answer:** A

> **Why:** Regression is a supervised learning technique used to predict continuous numeric quantities (such as prices, temperatures, or probabilities).

---

### Question 10
Natural language processing can be used in machine learning to:

- **A.** Classify email messages as work-related or personal.
- **B.** Predict the number of future car rentals based on weather.
- **C.** Predict which website visitors will make a financial transaction.
- **D.** Stop a factory assembly line when extremely high temperatures are recorded.

**Correct answer:** A

> **Why:** Text classification is an NLP capability that assigns text documents into categories (e.g. work vs. personal). Predicting numerical car rentals is regression; sensor-based emergency stops are rule-based systems.

---

### Question 11
Asking a chatbot whether it will rain tomorrow and being provided with a weather probability report is an example of:

- **A.** Computer vision
- **B.** Image generation
- **C.** Prediction and forecasting
- **D.** Optical character recognition

**Correct answer:** C

> **Why:** Estimating future meteorological outcomes based on historical patterns is a predictive forecasting machine learning workload.

---

### Question 12
A retail marketing team wants to group customers into distinct segments based on purchasing behavior and visit frequency without using prior labeled categories. Which machine learning approach should they use?

- **A.** Regression
- **B.** Supervised classification
- **C.** Clustering
- **D.** Time series forecasting

**Correct answer:** C

> **Why:** Clustering is an unsupervised machine learning method that partitions unlabeled data points into natural groupings based on feature similarity.

---

### Question 13
An email service needs to automatically classify incoming messages as either **Spam** or **Not Spam**. Which type of machine learning workload is this?

- **A.** Regression
- **B.** Binary Classification
- **C.** Clustering
- **D.** Anomaly Detection

**Correct answer:** B

> **Why:** Binary classification predicts one of two mutually exclusive discrete label classes (Spam vs. Not Spam, Yes vs. No).

---

### Question 14
In natural language processing and machine learning, what is the primary purpose of **Tokenization**?

- **A.** To translate text into another human language.
- **B.** To convert text into binary code for network transmission.
- **C.** To break down raw text into smaller discrete units (words, sub-words, or characters) represented as numerical IDs.
- **D.** To correct spelling and grammatical mistakes.

**Correct answer:** C

> **Why:** Tokenization segments text into tokens (words or sub-word fragments), allowing models to map text into numerical vectors that neural networks can process.

---

### Question 15
What are **Vector Embeddings** in machine learning?

- **A.** Compressed image thumbnails stored in cloud storage.
- **B.** Vector-based numerical representations of tokens in a multi-dimensional space that capture semantic meaning and contextual relationships.
- **C.** Static rule-based decision trees compiled into binary code.
- **D.** Audio frequencies stored in MP3 format.

**Correct answer:** B

> **Why:** Embeddings represent words, sentences, or documents as dense numerical vectors where mathematically close vectors share similar semantic meanings.

---

### Question 16
Which feature representation captures contextual semantic similarity between words rather than just statistical occurrence counts?

- **A.** Term Frequency-Inverse Document Frequency (TF-IDF)
- **B.** Word2Vec (Dense Vector Embeddings)
- **C.** Bag of Words
- **D.** One-Hot Encoding

**Correct answer:** B

> **Why:** Word2Vec generates dense continuous vector embeddings where semantically related words occupy nearby coordinates, whereas TF-IDF only measures statistical frequency across documents.

---

## Domain 3: Computer Vision & Multimodal Workloads on Azure

### Question 17
Information extraction solutions that detect and read text in scanned documents and images rely on:

- **A.** Computer vision
- **B.** Image generation
- **C.** Sentiment analysis
- **D.** Speech synthesis

**Correct answer:** A

> **Why:** Optical Character Recognition (OCR) and document text extraction are foundational capabilities of computer vision.

---

### Question 18
Which type of computer vision solution detects specific items in an image and provides **bounding box coordinates** for each detected item?

- **A.** Image Classification
- **B.** Object Detection
- **C.** Optical Character Recognition (OCR)
- **D.** Facial Analysis

**Correct answer:** B

> **Why:** Object Detection identifies the category of items in an image and returns rectangular bounding box coordinates (`x`, `y`, `width`, `height`) locating each item.

---

### Question 19
You are developing an application that extracts fields from PDFs by using Azure Content Understanding in Foundry Tools. How should you initiate the analysis and retrieve the results asynchronously?

- **A.** Call `get_results()` immediately after uploading the file.
- **B.** Execute a synchronous SQL query against the document blob.
- **C.** Send an HTTP GET request to the root endpoint.
- **D.** Call `begin_analyze()`, and then call `poller.result()` to retrieve the results.

**Correct answer:** D

> **Why:** Long-running document and media processing operations in Azure SDKs follow the Poller pattern: `begin_analyze()` starts the asynchronous job and returns a poller, and `poller.result()` awaits completion and retrieves extracted fields.

---

### Question 20
You are developing an application that analyzes uploaded video files by using Azure Content Understanding in Foundry Tools. Which API should you use?

- **A.** The Translator API
- **B.** The Custom Text API
- **C.** The Analyze API in Content Understanding
- **D.** The Text Analytics for Health API

**Correct answer:** C

> **Why:** The Content Understanding Analyze API processes multimodal media (video, audio, documents) to extract metadata, visual scenes, and structured insights.

---

### Question 21
You have a Microsoft Foundry project that contains a vision-enabled model deployment (such as GPT-4o). You need to develop an application that sends a message containing an image to the model. How should the request message be structured?

- **A.** A user message that includes both a text item and an image item (as a base64-encoded string or HTTPS URL) in the content array.
- **B.** An email attachment containing the image file path.
- **C.** A plain text message containing the image's raw binary bytes in ASCII.
- **D.** A multi-part form upload directed to a relational database.

**Correct answer:** A

> **Why:** Multimodal vision models in Microsoft Foundry / OpenAI expect a `user` role message with a structured `content` array containing objects of type `text` and `image_url` (with HTTPS URL or base64 data URI).

---

### Question 22
For each of the following statements about Image Analysis capabilities in Microsoft Foundry Tools, select **Yes** if the statement is true, otherwise select **No**:

| Statement | Answer |
| :--- | :---: |
| Image analysis capabilities can perform optical character recognition (OCR). | **Yes** |
| Image analysis capabilities can generate captions and descriptive tags for images. | **Yes** |
| Image analysis capabilities are designed primarily to create new images from text prompts. | **No** |

> **Why:**
> - **Statement 1 (Yes):** Image Analysis includes OCR text detection.
> - **Statement 2 (Yes):** Image Analysis extracts descriptive tags, objects, and captions.
> - **Statement 3 (No):** Creating new images from text prompts is done by image *generation* models (e.g. DALL-E 3), not image analysis.

---

## Domain 4: Natural Language Processing (NLP) & Speech on Azure

### Question 23
You are developing an application that continuously transcribes speech from a default microphone by using Azure Speech in Microsoft Foundry Tools. Which class from the Azure Speech SDK should you use?

- **A.** `SpeechSynthesizer`
- **B.** `AudioConfig`
- **C.** `SpeechRecognizer`
- **D.** `ConversationTranscriber`

**Correct answer:** C

> **Why:** `SpeechRecognizer` is the primary Azure Speech SDK class for capturing microphone audio and recognizing spoken words in real time.

---

### Question 24
A voice-activated security key system that verifies a spoken passphrase is an example of:

- **A.** Speech recognition
- **B.** Speech synthesis
- **C.** Sentiment analysis
- **D.** Key phrase extraction

**Correct answer:** A

> **Why:** Converting acoustic vocal signals into digital text or command tokens is speech recognition (speech-to-text).

---

### Question 25
You need to develop an application that converts recorded audio to text, and then reads the generated responses aloud. What should you use?

- **A.** Azure Language in Foundry Tools
- **B.** Azure Translator in Foundry Tools
- **C.** Azure Document Intelligence in Foundry Tools
- **D.** Azure Speech in Foundry Tools

**Correct answer:** D

> **Why:** Azure Speech provides both Speech-to-Text (STT) for audio transcription and Text-to-Speech (TTS) for synthesizing voice audio.

---

### Question 26
What activity happens during the pre-processing stage of speech recognition?

- **A.** Background noise is added to the audio signal.
- **B.** Feature vectors (acoustic spectrogram features) are extracted from the audio waveform.
- **C.** Text is translated to a foreign language.
- **D.** Sentences are converted into SQL queries.

**Correct answer:** B

> **Why:** Pre-processing filters noise, segments waveforms, and extracts acoustic feature vectors for neural acoustic modeling.

---

### Question 27
You have a website that includes customer reviews in French, German, and Spanish. You need to store the reviews in English and present the reviews to users in their preferred local language. Which Azure AI capability should you use?

- **A.** Azure AI Translator (Translation)
- **B.** Key phrase extraction
- **C.** Entity recognition
- **D.** Sentiment analysis

**Correct answer:** A

> **Why:** Azure AI Translator provides automatic bidirectional machine translation across languages.

---

### Question 28
You are building an application to extract corporate names, commercial products, dates, and locations from news articles. Which Azure Language feature should you use?

- **A.** Language detection
- **B.** Key phrase extraction
- **C.** Named Entity Recognition (NER)
- **D.** Text translation

**Correct answer:** C

> **Why:** Named Entity Recognition identifies and classifies real-world entities into predefined categories (Person, Location, Organization, DateTime).

---

### Question 29
You are developing a Python application that summarizes customer comments by using Azure Language in Foundry Tools. Which client library package should you install?

- **A.** `azure-ai-textanalytics` (or `azure-ai-language-text`)
- **B.** `azure-storage-blob`
- **C.** `azure-identity`
- **D.** `azure-cognitiveservices-vision`

**Correct answer:** A

> **Why:** The `azure-ai-textanalytics` package provides client APIs for summarization, key phrase extraction, sentiment analysis, and entity recognition.

---

## Domain 5: Generative AI, Large Language Models (LLMs) & AI Agents

### Question 30
Which is the most accurate description of **Generative AI**?

- **A.** Generative AI uses a language model or foundation neural network to create original content in response to a prompt.
- **B.** Generative AI is an older form of statistical regression superseded by decision trees.
- **C.** Generative AI is a database indexing protocol.
- **D.** Generative AI is a hardware virtualization architecture.

**Correct answer:** A

> **Why:** Generative AI generates novel, contextually relevant content (text, code, imagery, synthetic audio) conditioned on natural language inputs.

---

### Question 31
What is a **Large Language Model (LLM)**?

- **A.** A type of AI model designed to understand and generate natural language based on vast training datasets and billions of parameters.
- **B.** A small database query script.
- **C.** A hardware graphics card.
- **D.** A rule-based grammar checker.

**Correct answer:** A

> **Why:** LLMs are massive transformer-based neural networks trained on broad text corpora to perform language understanding, synthesis, and reasoning.

---

### Question 32
What is an **AI Agent** in the context of modern artificial intelligence?

- **A.** An autonomous AI application that can reason, use external tools/APIs, and perform multi-step tasks on behalf of a user.
- **B.** A human customer support agent who uses computers.
- **C.** An antivirus background scanner.
- **D.** A static spreadsheet macro.

**Correct answer:** A

> **Why:** AI Agents leverage language models as reasoning engines combined with memory, planning, and tool execution to accomplish complex user goals.

---

### Question 33
What is the purpose of a **System Prompt** in generative AI applications?

- **A.** To provide overarching instructions, behavioral constraints, persona rules, and response formats that govern how the model responds to user queries.
- **B.** To reboot the Azure virtual machine.
- **C.** To allocate RAM on the user's local PC.
- **D.** To compile C# source code.

**Correct answer:** A

> **Why:** System prompts define the persona, boundaries, permitted actions, and formatting guidelines for generative models.

---

### Question 34
In transformer-based language models, what is the role of the **Attention Mechanism**?

- **A.** It forces the computer monitor to remain on during processing.
- **B.** It dynamically calculates mathematical weights between each token and all other tokens in the context window to capture long-range contextual relationships.
- **C.** It filters swear words from user input.
- **D.** It compresses text into ZIP archives.

**Correct answer:** B

> **Why:** Self-attention computes dynamic relational weights across all tokens in an input sequence, allowing models to understand context regardless of word distance.

---

### Question 35
After a generative AI model is deployed in Microsoft Foundry, how do client applications send inference requests to the model?

- **A.** By sending HTTP POST requests to the deployment's Endpoint URL with authentication headers.
- **B.** By modifying the server's BIOS settings.
- **C.** By emailing the prompts to Microsoft support.
- **D.** By mounting an NFS drive.

**Correct answer:** A

> **Why:** Deployed models expose a secure REST Endpoint URL that client applications call with API keys or Entra ID bearer tokens.

---

### Question 36
When developing a lightweight chat application by using the **Microsoft Foundry SDK**, which client class is instantiated to connect to your project?

- **A.** `AIProjectClient`
- **B.** `BlobServiceClient`
- **C.** `SpeechClient`
- **D.** `TableClient`

**Correct answer:** A

> **Why:** `AIProjectClient` is the core Foundry SDK entry point used to authenticate, access deployments, run prompts, and manage agents.

---

### Question 37
You are developing a simple application that uses the Microsoft Foundry SDK to call an AI model. Which three elements must you provide in code or environment variables to run the application?

*Choose 3 answers*

- **A.** The model deployment name
- **B.** The endpoint URL
- **C.** Credentials (API key or Token)
- **D.** The user's home Wi-Fi password
- **E.** The physical server MAC address

**Correct answers:** A, B, C

> **Why:** Connecting to and calling a model deployment requires the **Endpoint URL**, the **Model Deployment Name**, and **Authentication Credentials** (API Key or `DefaultAzureCredential`).

---

### Question 38
You are developing a lightweight application that will call an agent programmatically by using the Microsoft Foundry SDK. How can you quickly retrieve the required connection variables from the portal?

- **A.** In the Foundry playground, select Code, and view the `.env` variables and code sample.
- **B.** Download the entire server operating system image.
- **C.** Run `ipconfig` on your local laptop.
- **D.** Check Windows Event Viewer.

**Correct answer:** A

> **Why:** In Microsoft Foundry Playground, clicking the **View Code** button displays pre-configured code snippets and the `.env` configuration keys (project connection string, deployment names).

---

### Question 39
Which type of Azure AI workload should you use to create original artistic illustrations based on the text description of an article?

- **A.** Azure Document Intelligence
- **B.** Azure AI Language
- **C.** Azure AI Vision OCR
- **D.** Generative AI (e.g. DALL-E / Image Generation Model)

**Correct answer:** D

> **Why:** Creating novel images from textual descriptions is performed by Generative AI image generation models (such as DALL-E 3).

---

### Question 40
You need to build an AI solution that responds to user queries with detailed written explanations, step-by-step reasoning, and summaries. Which type of AI model should you use?

- **A.** An embedding model
- **B.** An image generation model
- **C.** A text generation model (LLM)
- **D.** A speech recognition model

**Correct answer:** C

> **Why:** Text generation models (e.g. GPT-4o, GPT-3.5) generate descriptive, coherent textual explanations and answers.

---

### Question 41
You create an agent named Agent1 in the Microsoft Foundry portal. When you open the Foundry playground to test Agent1, what does the playground use to ensure that the tests reflect production behavior?

- **A.** The local web browser cache.
- **B.** A mock offline emulator.
- **C.** The user's personal desktop settings.
- **D.** The exact configuration, instructions, and tools assigned to Agent1 in the project.

**Correct answer:** D

> **Why:** The Foundry Playground directly invokes the deployed agent instance using its configured model, system instructions, temperature, and attached tools.

---

### Question 42
For each of the following statements about managing agents in Microsoft Foundry, select **Yes** if the statement is true, otherwise select **No**:

| Statement | Answer |
| :--- | :---: |
| Saving an agent in the Microsoft Foundry portal creates a version that can be tested in the Agents playground. | **Yes** |
| An agent can only call tools that are written in C++. | **No** |
| Publishing an agent allows client applications to interact with it via SDK and REST APIs. | **Yes** |

> **Why:**
> - **Statement 1 (Yes):** Saving creates a testable version in the playground.
> - **Statement 2 (No):** Agents can call OpenAPI tools, Azure Functions, and custom Python/C# scripts.
> - **Statement 3 (Yes):** Publishing exposes secure API endpoints for client SDKs and applications.

---

### Question 43
What is the primary benefit of **Retrieval-Augmented Generation (RAG)** in enterprise AI applications?

- **A.** It eliminates the need for computer monitors.
- **B.** It dynamically retrieves relevant domain knowledge from enterprise data stores via vector search to ground model responses in real-time, reducing hallucinations without model retraining.
- **C.** It translates all English text to binary numbers.
- **D.** It allows AI models to run without electricity.

**Correct answer:** B

> **Why:** RAG supplements prompt context with domain-specific knowledge retrieved from vector indexes, delivering factual, up-to-date responses without model fine-tuning.

---

### Question 44
An application needs to accept spoken customer questions through a mobile device and synthesize vocal responses. Which two Azure AI capabilities are combined?

- **A.** Speech-to-Text and Text-to-Speech
- **B.** Computer Vision and OCR
- **C.** Facial Recognition and Translation
- **D.** Document Intelligence and Language Detection

**Correct answer:** A

> **Why:** Speech-to-Text transcribes the user's spoken audio into text, and Text-to-Speech converts generated text answers back into natural audible speech.

---

### Question 45
Which implementation best aligns with the Microsoft **Transparency** principle for an AI diagnostic recommendation tool?

- **A.** Displaying a confidence score and a summary of the clinical indicators that led to the recommendation.
- **B.** Hiding the AI logic to prevent user confusion.
- **C.** Restricting all tool access to administrators only.
- **D.** Allowing the tool to make autonomous decisions without doctor review.

**Correct answer:** A

> **Why:** Transparency requires providing understandable explanations, rationale, and confidence indicators so users can evaluate AI recommendations appropriately.
