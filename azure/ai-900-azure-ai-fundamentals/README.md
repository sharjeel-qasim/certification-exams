# AI-900: Microsoft Azure AI Fundamentals — Practice Question Bank

[![Azure](https://img.shields.io/badge/Microsoft_Azure-0089D6?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/)
[![Exam](https://img.shields.io/badge/Exam-AI--900-blue?style=for-the-badge)](#table-of-contents)
[![Questions](https://img.shields.io/badge/Questions-45%20Verified%20Questions-success?style=for-the-badge)](#table-of-contents)
[![Cheat Sheet](https://img.shields.io/badge/Study_Guide-Cheat_Sheet-orange?style=for-the-badge)](CHEAT_SHEET.md)

Complete, cleaned, and verified Practice Question Bank for the **Microsoft Certified: Azure AI Fundamentals (AI-900)** exam. Curated directly from official Microsoft Learn assessments, practice exams, and training modules.

> ⚡ **Quick Review:** Check out the [**AI-900 Exam Cheat Sheet**](./CHEAT_SHEET.md) for a high-yield summary of core Azure AI concepts, workloads, and exam traps before testing yourself below.

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **Transparency** (B) requires that AI systems are understandable and explainable so stakeholders and users know how conclusions, risk scores, and automated decisions are reached. **Inclusiveness** (A) focuses on empowering people of all physical and cognitive abilities (e.g., accessibility features). **Fairness** (C) ensures equitable treatment across demographic groups without bias, while **Reliability and safety** (D) ensures consistent, safe system operation under expected and unexpected conditions.

</details>

---

### Question 2
You have an AI-based loan approval system. During testing, you discover that the system exhibits demographic and gender bias in approving applications. Which responsible AI principle does this violate?

- **A.** Reliability and safety
- **B.** Fairness
- **C.** Transparency
- **D.** Accountability

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **Fairness** (B) requires AI systems to treat all people impartially without demographic, gender, racial, or socioeconomic discrimination. **Reliability and safety** (A) addresses consistent operational stability and error handling. **Transparency** (C) addresses explainability of model behavior and limitations, while **Accountability** (D) establishes human oversight, governance, and legal/ethical responsibility for the system.

</details>

---

### Question 3
You are building an AI system. Which task should you include to help the service meet the Microsoft **Inclusiveness** principle for responsible AI?

- **A.** Ensure that training datasets are representative of the entire population.
- **B.** Provide documentation to help developers debug code.
- **C.** Ensure that all visuals and user interfaces have associated text and alt-tags readable by screen readers.
- **D.** Enable autoscaling to ensure that the service scales based on load.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **Inclusiveness** (C) ensures AI systems empower everyone and engage people of all physical and cognitive abilities, including users relying on screen readers and assistive technology. Ensuring representative training datasets (A) primarily addresses **Fairness** by reducing sampling bias. Providing developer documentation (B) supports **Transparency** and engineering governance, and enabling autoscaling (D) supports cloud infrastructure availability and **Reliability and safety**.

</details>

---

### Question 4
The Microsoft responsible AI principle of **Reliability and Safety** requires AI systems to:

- **A.** Enable continuous human manual approval for every single operation.
- **B.** Ensure equitable demographic distribution of outcomes.
- **C.** Perform consistently and safely under expected operational conditions and handle errors gracefully.
- **D.** Provide clear technical architecture explanations to end users.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **Reliability and Safety** (C) ensures AI solutions operate robustly, consistently, and safely across intended scenarios while responding gracefully to unanticipated conditions. Requiring human oversight and governance (A) aligns with **Accountability** (and does not mandate manual approval for every single inference). Equitable demographic outcomes (B) aligns with **Fairness**, and explaining how a system works to users (D) aligns with **Transparency**.

</details>

---

### Question 5
Which Microsoft responsible AI principle states that human beings must remain ultimately answerable for how an AI system is governed and operated?

- **A.** Accountability
- **B.** Transparency
- **C.** Inclusiveness
- **D.** Fairness

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **Accountability** (A) establishes that human developers, data scientists, and organizations remain ultimately answerable for designing, deploying, and governing AI systems within ethical, legal, and organizational norms. **Transparency** (B) focuses on making AI behavior and decision factors understandable, **Inclusiveness** (C) focuses on accessibility for users of all abilities, and **Fairness** (D) focuses on eliminating discriminatory bias.

</details>

---

### Question 6
For each of the following statements about data protection in AI systems, select **Yes** if the statement is true, otherwise select **No**:

| Statement | Answer |
| :--- | :---: |
| Restricting users to authorized data reduces the risk of sensitive data exposure when they use AI systems. | Yes / No |
| Sharing personal user data openly improves collaboration and supports responsible AI practices. | Yes / No |
| Protecting personal data and complying with data privacy regulations are key considerations in responsible AI. | Yes / No |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** Statement 1: **Yes** | Statement 2: **No** | Statement 3: **Yes**

> **Why:**
> - **Statement 1 (Yes):** Applying role-based access control (RBAC) and the principle of least privilege ensures users and AI models only access authorized data, directly supporting the **Privacy and security** principle (selecting *No* ignores the risk of unauthorized data leakage in prompts and completions).
> - **Statement 2 (No):** Unrestricted sharing of personal user data violates the **Privacy and security** principle and data protection laws such as GDPR and HIPAA (selecting *Yes* would expose personally identifiable information to misuse).
> - **Statement 3 (Yes):** Safeguarding personally identifiable information (PII), securing data in transit/at rest, and complying with privacy regulations are foundational requirements of **Privacy and security** in responsible AI.

</details>

---

### Question 7
You are designing an AI system that will generate insurance quotes automatically. Match each requirement to the corresponding Microsoft responsible AI principle (*Transparency*, *Privacy and security*, or *Inclusiveness*):

| Requirement | Responsible AI Principle |
| :--- | :--- |
| 1. The decision-making process must be recorded so that staff can identify the reasoning behind a particular quote. | ? |
| 2. A customer's personal information must be visible only to staff who are involved in the decision-making process. | ? |
| 3. The system must be accessible to customers who use screen readers or assistive technology. | ? |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** 1: **Transparency** | 2: **Privacy and security** | 3: **Inclusiveness**

> **Why:**
> - **Requirement 1 → Transparency:** Recording and exposing the factors behind automated insurance quotes makes the model's reasoning auditable and explainable (unlike *Accountability*, which defines who governs the system, or *Fairness*, which measures demographic parity).
> - **Requirement 2 → Privacy and security:** Restricting access to customer PII solely to authorized staff enforces data confidentiality and least-privilege access control.
> - **Requirement 3 → Inclusiveness:** Supporting screen readers and assistive technologies ensures customers with visual or physical impairments can equally use the system.

</details>

---

### Question 8
For each of the following statements regarding inclusiveness in AI systems, select **Yes** if the statement is true, otherwise select **No**:

| Statement | Answer |
| :--- | :---: |
| Designing an AI system for a typical user profile alone is sufficient to support inclusiveness. | Yes / No |
| A high number of active users guarantees an AI system provides an inclusive experience. | Yes / No |
| Providing accessible interfaces and multilingual language options helps support inclusiveness in an AI system. | Yes / No |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** Statement 1: **No** | Statement 2: **No** | Statement 3: **Yes**

> **Why:**
> - **Statement 1 (No):** Designing only for an "average" or "typical" user profile overlooks edge cases and systematically excludes individuals with permanent or temporary disabilities (violating **Inclusiveness**).
> - **Statement 2 (No):** High adoption or traffic volume measures popularity, not whether people with visual, auditory, motor, or cognitive impairments can effectively use the system.
> - **Statement 3 (Yes):** Offering screen-reader compatibility, voice-to-text controls, high-contrast UI, and multilingual support directly removes barriers and fulfills the **Inclusiveness** principle.

</details>

---

## Domain 2: Fundamental Principles of Machine Learning on Azure

### Question 9
You need to predict the selling price of a used car based on its mileage, age, make, and engine size. Which type of machine learning model should you train?

- **A.** Regression
- **B.** Binary Classification
- **C.** Multiclass Classification
- **D.** Clustering

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **Regression** (A) is a supervised machine learning technique used to predict a continuous numerical label (such as a car's selling price, home value, or temperature). **Binary Classification** (B) predicts one of two discrete categories (e.g., *will sell* vs. *won't sell*). **Multiclass Classification** (C) predicts one of three or more discrete categories (e.g., classifying vehicle body type as *Sedan*, *SUV*, or *Truck*), and **Clustering** (D) is an unsupervised technique that groups unlabeled data points by similarity.

</details>

---

### Question 10
Natural language processing can be used in machine learning to:

- **A.** Classify email messages as work-related or personal.
- **B.** Predict the number of future car rentals based on weather.
- **C.** Predict which website visitors will make a financial transaction.
- **D.** Stop a factory assembly line when extremely high temperatures are recorded.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Classifying unstructured email text as work-related or personal (A) is a **Natural Language Processing (NLP)** text classification task. Predicting the numerical count of future car rentals from weather features (B) is a tabular **Regression** workload. Predicting whether a visitor will complete a transaction (Yes/No) from clickstream logs (C) is tabular **Binary Classification**, and halting an assembly line based on numeric temperature thresholds (D) is rule-based automation or numeric **Anomaly Detection**.

</details>

---

### Question 11
Asking a chatbot whether it will rain tomorrow and being provided with a weather probability report is an example of:

- **A.** Computer vision
- **B.** Image generation
- **C.** Prediction and forecasting
- **D.** Optical character recognition

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** Estimating future meteorological outcomes and probabilities from historical atmospheric data is an example of **Prediction and forecasting** (C). **Computer vision** (A) interprets visual inputs such as photos or video streams. **Image generation** (B) synthesizes new images from text prompts (e.g., DALL-E), and **Optical character recognition (OCR)** (D) detects and extracts printed or handwritten text from images and scanned documents.

</details>

---

### Question 12
A retail marketing team wants to group customers into distinct segments based on purchasing behavior and visit frequency without using prior labeled categories. Which machine learning approach should they use?

- **A.** Regression
- **B.** Supervised classification
- **C.** Clustering
- **D.** Time series forecasting

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **Clustering** (C) (such as K-Means) is an *unsupervised* machine learning technique that discovers natural groupings in unlabeled data based on feature similarity. **Regression** (A) and **Supervised classification** (B) are *supervised* techniques that require historical data with known ground-truth labels (`y`) during training. **Time series forecasting** (D) predicts future numerical trends over sequential time intervals rather than segmenting unlabeled customer profiles.

</details>

---

### Question 13
An email service needs to automatically classify incoming messages as either **Spam** or **Not Spam**. Which type of machine learning workload is this?

- **A.** Regression
- **B.** Binary Classification
- **C.** Clustering
- **D.** Anomaly Detection

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **Binary Classification** (B) is a supervised learning workload that assigns items into one of two mutually exclusive discrete classes (`Spam` vs. `Not Spam`, `True` vs. `False`). **Regression** (A) predicts continuous numeric values. **Clustering** (C) groups unlabeled items without predefined categories, and **Anomaly Detection** (D) identifies rare statistical outliers in time-series telemetry rather than performing supervised two-class categorization.

</details>

---

### Question 14
In natural language processing and machine learning, what is the primary purpose of **Tokenization**?

- **A.** To translate text into another human language.
- **B.** To assign a positive, neutral, or negative sentiment score to an entire document.
- **C.** To break down raw text into smaller discrete units (words, sub-words, or characters) represented as numerical IDs.
- **D.** To extract named entities such as people, organizations, and locations from unstructured text.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **Tokenization** (C) splits raw input text into discrete units called tokens (words, sub-words, or punctuation) and maps them to integer IDs so language models can process them mathematically. Translating text between languages (A) is **Machine Translation** (Azure AI Translator). Assigning positive/neutral/negative polarity scores (B) is **Sentiment Analysis**, and identifying people, places, and organizations (D) is **Named Entity Recognition (NER)** in Azure AI Language.

</details>

---

### Question 15
What are **Vector Embeddings** in machine learning?

- **A.** Discrete integer IDs assigned sequentially to words based on alphabetical order in a vocabulary.
- **B.** Vector-based numerical representations of tokens in a multi-dimensional space that capture semantic meaning and contextual relationships.
- **C.** Predefined regular expression patterns used by Azure AI Document Intelligence to extract form fields.
- **D.** Bounding box coordinate arrays returned by an Azure AI Vision object detection model.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **Vector Embeddings** (B) represent tokens, sentences, or documents as dense arrays of floating-point numbers in a multi-dimensional space where semantically similar concepts have close geometric distance (e.g., cosine similarity). Sequential alphabetical integer IDs (A) represent simple vocabulary indexing without capturing semantic similarity. Regular expression rules (C) are static string-matching patterns, and bounding box arrays (D) represent 2D pixel coordinates (`x`, `y`, `width`, `height`) in **Object Detection**.

</details>

---

### Question 16
Which feature representation captures contextual semantic similarity between words rather than just statistical occurrence counts?

- **A.** Term Frequency-Inverse Document Frequency (TF-IDF)
- **B.** Word2Vec (Dense Vector Embeddings)
- **C.** Bag of Words
- **D.** One-Hot Encoding

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **Word2Vec (Dense Vector Embeddings)** (B) trains neural networks to place words appearing in similar contexts close together in continuous vector space, capturing semantic relationships (e.g., *king* − *man* + *woman* ≈ *queen*). **TF-IDF** (A) and **Bag of Words** (C) only measure word frequency and document occurrence statistics without understanding word meaning or synonyms. **One-Hot Encoding** (D) represents each vocabulary word as a sparse binary vector where all words are equidistant and orthogonal.

</details>

---

## Domain 3: Computer Vision & Multimodal Workloads on Azure

### Question 17
Information extraction solutions that detect and read text in scanned documents and images rely on:

- **A.** Computer vision
- **B.** Image generation
- **C.** Sentiment analysis
- **D.** Speech synthesis

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Detecting and reading text from scanned documents and photographs (Optical Character Recognition / OCR) is a core capability of **Computer vision** (A), powering both Azure AI Vision and Azure AI Document Intelligence. **Image generation** (B) creates new visual artwork from text prompts (e.g., DALL-E). **Sentiment analysis** (C) is an NLP feature that evaluates emotional tone in text, and **Speech synthesis** (D) is an Azure AI Speech capability that converts text into spoken audio (Text-to-Speech).

</details>

---

### Question 18
Which type of computer vision solution detects specific items in an image and provides **bounding box coordinates** for each detected item?

- **A.** Image Classification
- **B.** Object Detection
- **C.** Optical Character Recognition (OCR)
- **D.** Facial Analysis

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **Object Detection** (B) identifies multiple individual objects within an image, returning a class label, confidence score, and rectangular **bounding box coordinates** (`x`, `y`, `width`, `height`) for each item. **Image Classification** (A) assigns a single category label to the entire image without locating where objects are. **Optical Character Recognition (OCR)** (C) extracts written or printed text rather than classifying physical objects, and **Facial Analysis** (D) specifically detects human faces and facial landmarks rather than general object categories.

</details>

---

### Question 19
You are developing an application that extracts fields from PDFs by using Azure Content Understanding in Foundry Tools. How should you initiate the analysis and retrieve the results asynchronously?

- **A.** Call `get_results()` immediately after uploading the file.
- **B.** Call `analyze_document_sync()` and read the response headers directly.
- **C.** Stream the PDF bytes to `ChatCompletionsClient.complete()` using a synchronous callback.
- **D.** Call `begin_analyze()`, and then call `poller.result()` to retrieve the results.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** Document and media extraction in Azure Content Understanding and Azure AI Document Intelligence are asynchronous long-running operations (LRO) that use the SDK Poller pattern: calling **`begin_analyze()`** (D) starts the background job and returns an `LROPoller` object, and **`poller.result()`** waits for completion and returns the extracted schema fields. Calling `get_results()` without initiating an analysis job (A) or calling a non-existent synchronous method (B) fails, and `ChatCompletionsClient.complete()` (C) is used for LLM chat completions rather than structured Content Understanding extraction pipelines.

</details>

---

### Question 20
You are developing an application that analyzes uploaded video files by using Azure Content Understanding in Foundry Tools. Which API should you use?

- **A.** The Translator API
- **B.** The Custom Text API
- **C.** The Analyze API in Content Understanding
- **D.** The Text Analytics for Health API

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **The Analyze API in Content Understanding** (C) is a multimodal service in Microsoft Foundry Tools that ingests documents, images, audio, and video files to extract scenes, transcripts, keyframes, and structured fields. **The Translator API** (A) translates text strings across languages. **The Custom Text API** (B) trains custom text classifiers in Azure AI Language, and **The Text Analytics for Health API** (D) extracts clinical entities (medications, diagnoses, symptoms) from medical text.

</details>

---

### Question 21
You have a Microsoft Foundry project that contains a vision-enabled model deployment (such as GPT-4o). You need to develop an application that sends a message containing an image to the model. How should the request message be structured?

- **A.** A user message that includes both a text item and an image item (as a base64-encoded string or HTTPS URL) in the content array.
- **B.** A `system` message containing a local file system path (`C:\images\photo.png`) in the `prompt` parameter.
- **C.** A separate `function` role message that passes raw unencoded binary bytes in the HTTP query string.
- **D.** An `assistant` role message containing only the image's EXIF metadata headers.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Vision-enabled multimodal chat models (such as GPT-4o in Microsoft Foundry) require a **`user` role message whose `content` property is an array** containing both a `text` object (the question/prompt) and an `image_url` object (containing either a public HTTPS URL or a base64-encoded data URI) (A). Cloud APIs cannot read local client file paths like `C:\...` in a `system` message (B). Raw binary bytes cannot be sent in HTTP query strings or `function` role messages (C), and `assistant` messages represent prior model outputs while EXIF metadata lacks the actual image pixels (D).

</details>

---

### Question 22
For each of the following statements about Image Analysis capabilities in Microsoft Foundry Tools, select **Yes** if the statement is true, otherwise select **No**:

| Statement | Answer |
| :--- | :---: |
| Image analysis capabilities can perform optical character recognition (OCR). | Yes / No |
| Image analysis capabilities can generate captions and descriptive tags for images. | Yes / No |
| Image analysis capabilities are designed primarily to create new images from text prompts. | Yes / No |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** Statement 1: **Yes** | Statement 2: **Yes** | Statement 3: **No**

> **Why:**
> - **Statement 1 (Yes):** Azure AI Vision Image Analysis (`Read` capability) performs Optical Character Recognition (OCR) to extract printed and handwritten text from images.
> - **Statement 2 (Yes):** Image Analysis can generate human-readable natural language captions (`Caption` and `Dense Captions`) as well as content tags (`Tags`) describing objects and scenery in an image.
> - **Statement 3 (No):** Image Analysis *interprets existing images*; generating brand-new images from text prompts is performed by **Generative AI image generation models** such as **DALL-E 3**.

</details>

---

## Domain 4: Natural Language Processing (NLP) & Speech on Azure

### Question 23
You are developing an application that continuously transcribes speech from a default microphone by using Azure Speech in Microsoft Foundry Tools. Which class from the Azure Speech SDK should you use?

- **A.** `SpeechSynthesizer`
- **B.** `AudioConfig`
- **C.** `SpeechRecognizer`
- **D.** `ConversationTranscriber`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **`SpeechRecognizer`** (C) is the Azure AI Speech SDK client class that performs Speech-to-Text (STT) transcription from an audio input source (such as a microphone or audio file). **`SpeechSynthesizer`** (A) performs the opposite task: Text-to-Speech (TTS) audio generation. **`AudioConfig`** (B) is a helper class that specifies which microphone or audio file to use, but cannot transcribe speech on its own. **`ConversationTranscriber`** (D) is specialized for multi-channel/multi-speaker meeting transcription with speaker diarization rather than standard single-user microphone recognition.

</details>

---

### Question 24
A voice-activated security key system that verifies a spoken passphrase is an example of:

- **A.** Speech recognition
- **B.** Speech synthesis
- **C.** Sentiment analysis
- **D.** Key phrase extraction

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Converting spoken acoustic audio into text to verify a passphrase relies on **Speech recognition** (Speech-to-Text) (A). **Speech synthesis** (B) converts written text into spoken audio (Text-to-Speech). **Sentiment analysis** (C) evaluates positive, neutral, or negative emotional tone in text, and **Key phrase extraction** (D) identifies the main talking points in a written document using Azure AI Language.

</details>

---

### Question 25
You need to develop an application that converts recorded audio to text, and then reads the generated responses aloud. What should you use?

- **A.** Azure Language in Foundry Tools
- **B.** Azure Translator in Foundry Tools
- **C.** Azure Document Intelligence in Foundry Tools
- **D.** Azure Speech in Foundry Tools

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** **Azure Speech in Foundry Tools** (D) provides both **Speech-to-Text** (for transcribing recorded audio into text) and **Text-to-Speech** (for synthesizing spoken audio responses). **Azure Language** (A) analyzes text (sentiment, entities, summarization) but does not process raw audio waveforms. **Azure Translator** (B) performs text-to-text translation between languages, and **Azure Document Intelligence** (C) extracts text and structure from visual documents and forms.

</details>

---

### Question 26
What activity happens during the pre-processing stage of speech recognition?

- **A.** Synthesized voice prosody and pitch contours are applied to generate an MP3 output stream.
- **B.** Feature vectors (acoustic spectrogram features) are extracted from the audio waveform.
- **C.** Named entities and key phrases are extracted from the transcribed paragraph.
- **D.** A language model generates a conversational reply using Retrieval-Augmented Generation (RAG).

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** During the acoustic **pre-processing** stage of speech recognition (B), raw analog/digital audio waveforms are denoised, segmented into short time frames, and converted into time-frequency **spectrogram feature vectors** for the acoustic model. Applying voice prosody and pitch to generate audio (A) happens during **Text-to-Speech synthesis**. Extracting named entities and key phrases (C) is a downstream **NLP text analysis** task performed *after* transcription, and generating a RAG reply (D) is a **Generative AI** workflow.

</details>

---

### Question 27
You have a website that includes customer reviews in French, German, and Spanish. You need to store the reviews in English and present the reviews to users in their preferred local language. Which Azure AI capability should you use?

- **A.** Azure AI Translator (Translation)
- **B.** Key phrase extraction
- **C.** Entity recognition
- **D.** Sentiment analysis

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **Azure AI Translator** (A) provides neural machine translation to convert text between source languages (French, German, Spanish) and target languages (English and local user languages). **Key phrase extraction** (B) identifies main concepts within text in its current language. **Entity recognition** (C) classifies nouns into categories like Person, Location, or Organization, and **Sentiment analysis** (D) determines whether a review is positive, neutral, or negative without translating it.

</details>

---

### Question 28
You are building an application to extract corporate names, commercial products, dates, and locations from news articles. Which Azure Language feature should you use?

- **A.** Language detection
- **B.** Key phrase extraction
- **C.** Named Entity Recognition (NER)
- **D.** Text translation

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **Named Entity Recognition (NER)** (C) identifies specific words or phrases in unstructured text and categorizes them into predefined entity types such as `Organization` (corporate names), `Product`, `DateTime`, `Location`, and `Person`. **Language detection** (A) only identifies the language in which the article is written (e.g., `"en"`). **Key phrase extraction** (B) returns a flat list of main talking points without classifying them by entity type, and **Text translation** (D) converts text from one language to another.

</details>

---

### Question 29
You are developing a Python application that summarizes customer comments by using Azure Language in Foundry Tools. Which client library package should you install?

- **A.** `azure-ai-textanalytics` (or `azure-ai-language-text`)
- **B.** `azure-storage-blob`
- **C.** `azure-identity`
- **D.** `azure-cognitiveservices-vision`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** The **`azure-ai-textanalytics`** (or **`azure-ai-language-text`**) package (A) is the official Azure Python SDK for Azure AI Language capabilities including extractive/abstractive summarization, sentiment analysis, key phrase extraction, and NER. **`azure-storage-blob`** (B) is used to upload and manage files in Azure Blob Storage. **`azure-identity`** (C) provides Microsoft Entra ID authentication classes (such as `DefaultAzureCredential`) but contains no NLP methods, and **`azure-cognitiveservices-vision`** (D) is used for computer vision tasks rather than text summarization.

</details>

---

## Domain 5: Generative AI, Large Language Models (LLMs) & AI Agents

### Question 30
Which is the most accurate description of **Generative AI**?

- **A.** Generative AI uses a language model or foundation neural network to create original content in response to a prompt.
- **B.** Generative AI exclusively classifies labeled tabular data into predefined binary categories using logistic regression.
- **C.** Generative AI is an unsupervised clustering algorithm that groups numeric data points without generating new content.
- **D.** Generative AI is a rule-based optical character recognition (OCR) engine that extracts static text from scanned receipts.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **Generative AI** (A) uses deep learning foundation models (such as Large Language Models and diffusion models) to synthesize original, contextually relevant content—including text, code, images, and audio—in response to natural language prompts. Classifying tabular records into two categories (B) describes supervised **Binary Classification**. Grouping unlabeled numeric points (C) describes unsupervised **Clustering**, and extracting text from scanned receipts (D) describes **Optical Character Recognition (OCR)** / **Azure AI Document Intelligence**.

</details>

---

### Question 31
What is a **Large Language Model (LLM)**?

- **A.** A type of AI model designed to understand and generate natural language based on vast training datasets and billions of parameters.
- **B.** A supervised regression algorithm used exclusively to forecast numeric time-series metrics such as stock prices.
- **C.** A computer vision model trained solely to return bounding box coordinates around objects in video streams.
- **D.** A deterministic, rule-based lookup table that matches exact keyword strings without statistical training.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** A **Large Language Model (LLM)** (A) is a deep learning transformer neural network trained on massive text corpora with billions of parameters to understand context, reason, and generate human-like text by predicting subsequent tokens. Forecasting continuous numeric values over time (B) is **Time-Series Regression**. Returning bounding box coordinates for objects in video (C) is **Object Detection** in Computer Vision, and matching exact keywords via static lookup tables (D) describes legacy **rule-based systems** rather than neural language models.

</details>

---

### Question 32
What is an **AI Agent** in the context of modern artificial intelligence?

- **A.** An autonomous AI application that can reason, use external tools/APIs, and perform multi-step tasks on behalf of a user.
- **B.** A static embedding model that only converts text strings into fixed-length numerical vectors.
- **C.** A prebuilt Azure AI Translator endpoint that only converts text between source and target languages.
- **D.** An automated data-labeling tool in Azure AI Custom Vision that draws bounding boxes around training images.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** An **AI Agent** (A) combines a Large Language Model (as its reasoning and planning engine) with system instructions, conversation state/memory, and external **tools** (such as OpenAPI endpoints, Azure Functions, or Azure AI Search) to autonomously execute multi-step workflows. Converting text into numerical vectors (B) is the function of an **Embedding Model**. Translating text between languages (C) is a single-purpose **Azure AI Translator** call, and drawing bounding boxes on training images (D) is data labeling in **Azure AI Custom Vision**.

</details>

---

### Question 33
What is the purpose of a **System Prompt** in generative AI applications?

- **A.** To provide overarching instructions, behavioral constraints, persona rules, and response formats that govern how the model responds to user queries.
- **B.** To permanently update the neural network's internal weights through gradient descent backpropagation.
- **C.** To provision additional GPU compute nodes in the Azure Machine Learning cluster.
- **D.** To convert unstructured audio files into acoustic spectrogram feature vectors for speech synthesis.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** A **System Prompt** (A) (passed in the `system` role message) sets the AI assistant's persona, tone, behavioral guardrails, safety boundaries, and output formatting rules for the conversation. Permanently updating neural network weights via backpropagation (B) describes **Model Training / Fine-Tuning**, whereas system prompts guide the model via in-context learning without altering weights. Provisioning GPU nodes (C) is **infrastructure scaling**, and converting audio to spectrograms (D) is **Azure AI Speech pre-processing**.

</details>

---

### Question 34
In transformer-based language models, what is the role of the **Attention Mechanism**?

- **A.** It randomly drops 50% of input tokens from the prompt to reduce API token billing costs.
- **B.** It dynamically calculates mathematical weights between each token and all other tokens in the context window to capture long-range contextual relationships.
- **C.** It blocks harmful, hateful, or violent user prompts at the API gateway before they reach the model.
- **D.** It converts every word into a sparse one-hot encoded binary vector based on alphabetical order.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** The **Self-Attention Mechanism** (B) in transformer architectures evaluates how strongly each token in a sequence relates to every other token in the context window, enabling the model to resolve ambiguous words (e.g., whether *"bank"* means a river bank or financial institution) based on surrounding context. It does not randomly drop input tokens to reduce billing (A). Blocking harmful or violent prompts at the API layer (C) is performed by **Azure AI Content Safety** filters, and creating sparse binary vectors without context (D) describes **One-Hot Encoding**.

</details>

---

### Question 35
After a generative AI model is deployed in Microsoft Foundry, how do client applications send inference requests to the model?

- **A.** By sending HTTP POST requests to the deployment's Endpoint URL with authentication headers.
- **B.** By executing a direct T-SQL `SELECT` query against the model's underlying GPU memory.
- **C.** By uploading prompts as CSV files to an unauthenticated public DNS server.
- **D.** By connecting via Remote Desktop Protocol (RDP) to the underlying Microsoft Foundry host virtual machine.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Deployed models in Microsoft Foundry expose a managed HTTPS **Endpoint URL**; client applications (or the Foundry / OpenAI SDKs) invoke inference by sending authenticated **HTTP POST** requests containing the JSON payload and an API key or Microsoft Entra ID bearer token (A). Models are neural network APIs rather than relational databases queried with T-SQL (B), DNS servers resolve domain names rather than processing AI prompts (C), and Microsoft Foundry is a managed PaaS service that does not expose underlying host VMs via RDP (D).

</details>

---

### Question 36
When developing a lightweight chat application by using the **Microsoft Foundry SDK**, which client class is instantiated to connect to your project?

- **A.** `AIProjectClient`
- **B.** `BlobServiceClient`
- **C.** `SpeechClient`
- **D.** `TableClient`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **`AIProjectClient`** (A) (from the `azure-ai-projects` library) is the primary Microsoft Foundry SDK class used to connect to a Foundry project using its project endpoint and credentials, retrieve chat clients, and interact with deployed models and agents. **`BlobServiceClient`** (B) manages Azure Blob Storage containers and files. **`SpeechClient` / `SpeechRecognizer`** (C) interacts with Azure AI Speech services, and **`TableClient`** (D) queries NoSQL key-attribute tables in Azure Table Storage or Azure Cosmos DB.

</details>

---

### Question 37
You are developing a simple application that uses the Microsoft Foundry SDK to call an AI model. Which three elements must you provide in code or environment variables to run the application?

*Choose 3 answers*

- **A.** The model deployment name
- **B.** The endpoint URL
- **C.** Credentials (API key or Token)
- **D.** The training dataset's original hyperparameter learning rate
- **E.** The internal neural network architecture weight matrix file (`.safetensors`)

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A, B, C

> **Why:** To authenticate and route inference calls to a deployed model using the Microsoft Foundry SDK, your application must specify the **Model Deployment Name** (A) (e.g., `"gpt-4o"`), the **Endpoint URL** (B) of the Foundry project or resource, and **Authentication Credentials** (C) (an API key or Microsoft Entra ID token via `DefaultAzureCredential`). Training hyperparameters such as the learning rate (D) are only used during model training or fine-tuning, and the model's weight files (E) are hosted and managed server-side by Azure rather than provided by the client application.

</details>

---

### Question 38
You are developing a lightweight application that will call an agent programmatically by using the Microsoft Foundry SDK. How can you quickly retrieve the required connection variables from the portal?

- **A.** In the Foundry playground, select Code, and view the `.env` variables and code sample.
- **B.** Export the model's neural network weights from Azure Blob Storage and decompile the binary.
- **C.** Query the Azure Activity Log using Kusto Query Language (KQL) for client IP addresses.
- **D.** Open the Azure Cost Management billing blade and inspect the invoice PDF.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** In the Microsoft Foundry portal playground, selecting **View Code** (or **Sample code**) provides ready-to-use Python, C#, and JavaScript snippets pre-populated with your project endpoint, agent ID, model deployment name, and `.env` variable templates (A). Model weights are not exported or decompiled to find connection strings (B). Azure Activity Logs (C) record control-plane management operations rather than SDK snippets, and Azure Cost Management (D) tracks cloud spending and invoices rather than API endpoints.

</details>

---

### Question 39
Which type of Azure AI workload should you use to create original artistic illustrations based on the text description of an article?

- **A.** Azure Document Intelligence
- **B.** Azure AI Language
- **C.** Azure AI Vision OCR
- **D.** Generative AI (e.g. DALL-E / Image Generation Model)

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** Creating original visual illustrations from natural language text prompts requires a **Generative AI image generation model** such as **DALL-E 3** in Microsoft Foundry / Azure OpenAI (D). **Azure Document Intelligence** (A) extracts text, tables, and key-value fields from existing forms and invoices. **Azure AI Language** (B) analyzes and summarizes written text without producing images, and **Azure AI Vision OCR** (C) reads text out of existing images rather than generating new artwork.

</details>

---

### Question 40
You need to build an AI solution that responds to user queries with detailed written explanations, step-by-step reasoning, and summaries. Which type of AI model should you use?

- **A.** An embedding model
- **B.** An image generation model
- **C.** A text generation model (LLM)
- **D.** A speech recognition model

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **A text generation model (Large Language Model / LLM)** (C) such as GPT-4o or Phi-3 is designed to generate coherent natural language explanations, multi-step reasoning, and text summaries. **An embedding model** (A) (such as `text-embedding-3-large`) converts text into numerical vectors for semantic search and cannot generate conversational prose. **An image generation model** (B) (such as DALL-E 3) produces images from text prompts, and **A speech recognition model** (D) transcribes spoken audio into text without generating reasoned answers.

</details>

---

### Question 41
You create an agent named Agent1 in the Microsoft Foundry portal. When you open the Foundry playground to test Agent1, what does the playground use to ensure that the tests reflect production behavior?

- **A.** An unconfigured base foundation model that ignores Agent1's custom instructions and knowledge sources.
- **B.** A static rule-based mock responder that returns hardcoded JSON strings without calling the LLM.
- **C.** A fine-tuning job that retrains the base model's weights on every test message.
- **D.** The exact configuration, instructions, and tools assigned to Agent1 in the project.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** The Microsoft Foundry Agents Playground runs live inference against **Agent1's exact configuration**—including its selected model deployment, system instructions, temperature parameters, connected grounding knowledge (such as Azure AI Search), and action tools (D)—so playground tests accurately mirror production API behavior. It does not strip away custom instructions (A) or return hardcoded mock strings (B), and testing in the playground uses real-time inference rather than retraining model weights via fine-tuning (C).

</details>

---

### Question 42
For each of the following statements about managing agents in Microsoft Foundry, select **Yes** if the statement is true, otherwise select **No**:

| Statement | Answer |
| :--- | :---: |
| Saving an agent in the Microsoft Foundry portal creates a version that can be tested in the Agents playground. | Yes / No |
| An agent can only call tools that are written in C++. | Yes / No |
| Publishing an agent allows client applications to interact with it via SDK and REST APIs. | Yes / No |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** Statement 1: **Yes** | Statement 2: **No** | Statement 3: **Yes**

> **Why:**
> - **Statement 1 (Yes):** Saving an agent configuration in the Microsoft Foundry portal persists its instructions, model selection, and attached tools so it can be immediately tested in the Agents playground.
> - **Statement 2 (No):** Microsoft Foundry agents are language-agnostic when invoking tools; they can call OpenAPI 3.0 REST endpoints, Azure Functions, Azure Logic Apps, Code Interpreter (Python), and Azure AI Search indexes regardless of the backend implementation language.
> - **Statement 3 (Yes):** Deployed/published agents in a Microsoft Foundry project are accessible programmatically to external client applications using the `AIProjectClient` SDK or REST APIs.

</details>

---

### Question 43
What is the primary benefit of **Retrieval-Augmented Generation (RAG)** in enterprise AI applications?

- **A.** It permanently modifies the foundation model's internal neural network weights through supervised fine-tuning.
- **B.** It dynamically retrieves relevant domain knowledge from enterprise data stores via vector search to ground model responses in real-time, reducing hallucinations without model retraining.
- **C.** It increases the model's parameter count automatically every time a user submits a prompt.
- **D.** It replaces the Large Language Model entirely with an unsupervised K-Means clustering algorithm.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **Retrieval-Augmented Generation (RAG)** (B) queries an external knowledge index (such as **Azure AI Search** using vector or hybrid search) at runtime and injects the most relevant document chunks into the prompt context, grounding the LLM's response in up-to-date enterprise data and reducing hallucinations without expensive retraining. Permanently modifying model weights (A) describes **Fine-Tuning**, not RAG. A model's parameter count is fixed by its neural architecture and never grows during inference (C), and RAG still uses an **LLM** to synthesize natural language answers rather than replacing it with **K-Means clustering** (D).

</details>

---

### Question 44
An application needs to accept spoken customer questions through a mobile device and synthesize vocal responses. Which two Azure AI capabilities are combined?

- **A.** Speech-to-Text and Text-to-Speech
- **B.** Computer Vision and OCR
- **C.** Facial Recognition and Translation
- **D.** Document Intelligence and Language Detection

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Accepting spoken audio questions and reading responses aloud combines **Speech-to-Text** (speech recognition to transcribe the customer's voice into text) and **Text-to-Speech** (speech synthesis to convert the AI's text reply into natural audio) in **Azure AI Speech** (A). **Computer Vision and OCR** (B) analyze images and printed text. **Facial Recognition and Translation** (C) identify faces in images and translate written text across languages, and **Document Intelligence and Language Detection** (D) parse structured forms and identify the language code of text documents.

</details>

---

### Question 45
Which implementation best aligns with the Microsoft **Transparency** principle for an AI diagnostic recommendation tool?

- **A.** Displaying a confidence score and a summary of the clinical indicators that led to the recommendation.
- **B.** Encrypting the patient database at rest using Azure Key Vault managed keys.
- **C.** Implementing role-based access control (RBAC) so only licensed clinicians can sign in to the portal.
- **D.** Deploying the diagnostic model across multiple Azure Availability Zones for 99.99% uptime.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** Displaying confidence scores and the underlying clinical features that influenced the recommendation (A) directly supports **Transparency** (interpretability and explainability), helping clinicians understand *why* the model made a specific suggestion and assess its certainty. Encrypting patient data at rest (B) and restricting portal sign-in via RBAC (C) address the **Privacy and security** principle, while deploying across multiple Availability Zones for high uptime (D) addresses infrastructure resiliency and the **Reliability and safety** principle.

</details>
