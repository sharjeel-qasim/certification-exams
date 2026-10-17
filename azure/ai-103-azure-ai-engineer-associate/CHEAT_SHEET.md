# ⚡ AI-103 / AI-102: Microsoft Azure AI Engineer Associate — Cram & Cheat Sheet

[![Azure](https://img.shields.io/badge/Microsoft_Azure-0089D6?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/)
[![Exam](https://img.shields.io/badge/Exam-AI--103%20%2F%20AI--102-blue?style=for-the-badge)](#-microsoft-foundry--agent-service-quick-reference)
[![Question Bank](https://img.shields.io/badge/Practice_Questions-64_MCQs-success?style=for-the-badge)](README.md)

High-yield, last-minute cram sheet for **Microsoft Certified: Azure AI Engineer Associate (AI-103 / AI-102)**. Covers Microsoft Foundry Agent Service, multi-agent orchestration, OpenAI multimodal/realtime/image/video APIs, AI Safety & Prompt Shields, Evaluators, Observability, Content Understanding, and Azure AI Search RAG pipelines.

---

## 🔵 Microsoft Foundry & Resource Governance

| Requirement / Scenario | Correct Azure / Foundry Configuration |
| :--- | :--- |
| **Single endpoint & key for multiple AI services (Speech + Language + Vision)** | Create a **Microsoft Foundry service** (multi-service Azure AI Services resource). |
| **Compare candidate models by quality, cost, and throughput without hosting weights** | Evaluate with **Model catalog leaderboards and metrics**; deploy using **Serverless deployment** (Models-as-a-Service). |
| **High throughput for burst traffic without reserved PTU capacity** | Use **Global Standard** deployment type. |
| **Prevent unexpected behavior changes from model updates** | Set version update policy to **Opt out of automatic model version upgrades** (or `Once the current version expires`). |
| **Keyless authentication from Agent to Azure Key Vault (Least Privilege)** | Enable a **System-assigned managed identity** and assign the **Key Vault Secrets User** RBAC role. |
| **Bicep Key Vault connection in Foundry using Managed Identity** | `category: 'AzureKeyVault'` and `authType: 'AccountManagedIdentity'`. |
| **Multiple client apps sharing the same keyless Azure AI Search config** | Configure an **Azure AI Search connection in the Foundry project** and reference it in each app. |
| **Restrict Foundry / Language service access to specific Azure VNet resources** | Enable a **Service Endpoint** in the VNet subnet and configure **Virtual Network rules** on the AI resource. |

---

## 🔵 Multi-Agent Orchestration & Tool Calling

### 1. Multi-Agent Orchestration Patterns
| Orchestration Pattern | How It Works | When to Use |
| :--- | :--- | :--- |
| **Workflow (YAML)** | Deterministic, step-based pipeline with shared state and conditional branching. | Triage -> Policy lookup -> Conditional ticket creation with minimal code; pausing for human approval via **`type: ask_question`**. |
| **Handoff** | Agents pass execution control directly to specialist peers without a central planner. | Triage agent routing to Billing or Technical specialist agents that can transfer back and forth as topics shift. |
| **Sequential** | Agents execute in a fixed linear order where each agent's output feeds the next. | Multi-stage pipelines (e.g., Draft -> Review -> Translate). |
| **Concurrent** | Multiple agents run in parallel on the same input and results are aggregated. | Brainstorming, ensemble voting, or independent parallel analysis. |
| **Magentic** | A manager/planner agent dynamically builds and updates a task ledger/plan. | Complex, open-ended problems with unknown steps beforehand. |

### 2. Agent Tool Calling & Security
- **Force deterministic tool invocation (e.g., MCP `kbsearch` or RAG retrieval):**
  - Pass **`tool_choice`** (`"required"` or specific tool name) in `project_client.agents.runs.create_and_process()`.
- **Isolated identity & audit tracing for published compliance agents:**
  - Set tool choice to **`required`** and authenticate using a **distinct agent identity** (isolated from the shared project identity).
- **OpenAPI 3.0 Tool returning `401 Unauthorized` (missing API key header):**
  - Define an **API key security scheme** (`type: apiKey`, `in: header`) in the OpenAPI spec **AND** explicitly **connect the OpenAPI tool to the Foundry project connection (`Connection1`)**.

---

## 🔵 Generative AI, Multimodal, Voice, Image & Video APIs

| Modality / Feature | Key API / Configuration | Exam Tip |
| :--- | :--- | :--- |
| **Deterministic Output + Max Reasoning** | `temperature=0`, `output_config={"effort": "high"}` | `temperature=0` stabilizes wording for automated validation; increasing `temperature` or `top_p` does **not** improve completeness. |
| **Improve Summary Completeness in Code** | **Add a retry evaluation before responses are returned** | Evaluates completeness in app logic and re-prompts before returning to the user. |
| **Multimodal Chat (Text + Image URL)** | `content: [{"type": "text", ...}, {"type": "image_url", ...}]` | Plain-text URLs inside a string are ignored as images; must use a structured content array. |
| **Foundry Agent Image Generation Tool** | Requires **`gpt-image-1`** deployment in the same project | Needed for agents to generate images during conversations. |
| **Image Inpainting (Masked Edit)** | `POST /openai/deployments/{deployment}/images/edits` | Send `image`, `mask`, and `prompt` as `multipart/form-data` (with `gpt-image-1` / `gpt-image-1.5`). |
| **Async Video Generation (OpenAI SDK)** | `client.videos.create(...)` & `client.videos.retrieve(video.id)` | Poll `video.status` until `"completed"`, `"failed"`, or `"cancelled"`. |
| **GPT Realtime Voice (~100 ms latency)** | **WebRTC** (for client/browser apps) | Use **WebRTC** for low-latency client audio streaming; use **Real-time STT + TTS** for turn-taking voice workflows. |
| **Semantic Similarity Vectors** | **Embeddings** model (`text-embedding-3-*`) | Returns numeric vectors representing document tokens. |

---

## 🔵 AI Safety, Guardrails, Evaluation & Observability

### 1. Azure AI Content Safety & Prompt Shields
| Threat / Scenario | Safety Feature to Configure |
| :--- | :--- |
| **Embedded malicious text in uploaded images / OCR output / PDFs** | **Prompt Shields for documents** (Indirect Prompt Injection detection). |
| **Treat third-party / untrusted document content as lower trust** | Prompt Shields (**Annotate and block**) + **Spotlighting** (delimiters/marking untrusted input). |
| **Classify and block uploaded user photos for harmful visual content** | **Image moderation** (severity levels across Hate, Violence, Sexual, Self-Harm). |

### 2. Microsoft Foundry Evaluators
| Evaluator Category | Metrics Included |
| :--- | :--- |
| **AI Quality (AI-Assisted)** | **Groundedness** (supported by context), **Relevance** (addresses query), **Coherence**, **Fluency**, **RAG Evaluator**. |
| **AI Quality (NLP)** | F1 Score, BLEU, GLEU, ROUGE, METEOR (lexical overlap against ground truth). |
| **Risk and Safety** | Harmful content (Violence, Sexual, Self-harm, Hate/Unfairness), **Protected Material**, **Content Safety** (sensitive/proprietary info). |

### 3. Observability & Tracing
- **External Python service calling Foundry Agent:** Use **OpenTelemetry** + **Application Insights**.
- **End-to-end visibility across Responses API + Content Safety connection:** **Enable application tracing in the Foundry project (`Project1`)**.
- **Diagnose sudden cost spike with unchanged traffic volume:** Inspect **Token usage** (input tokens vs. output tokens vs. tool usage).
- **Responsible AI Multi-Agent Auditing:**
  - Capture all nested operations across the agent run -> **Hierarchical spans**
  - Record tool invocation arguments and results -> **Tool call attributes**

---

## 🔵 Content Understanding, Document Intelligence & Azure AI Search (RAG)

### 1. Azure Content Understanding in Foundry Tools
| Scenario | Configuration / Feature |
| :--- | :--- |
| **High-volume, cost-effective standalone PDF invoices** | **Single-file task in standard mode** |
| **Cross-document validation with multi-step reasoning & reference data** | **Multi-file task in pro mode** |
| **Extract custom invoice fields (`invoiceNumber`, `totalAmount`) + route `< 0.80` confidence** | **Custom Content Understanding analyzer** defining required fields and returning confidence scores. |
| **Include per-field confidence score & bounding-box source grounding in PDF** | Enable **`estimateFieldSourceAndConfidence`**. |
| **Convert mixed scanned text, tables & multicolumn layouts to Markdown** | Configure an **Azure Content Understanding analyzer** first. |

### 2. Azure AI Search & Knowledge Mining
- **Vector Search Index Pipeline for PDFs:** Use **`Text Split`** skill (chunking) + **`Azure OpenAI Embedding`** skill (vectorization).
- **Search scanned invoice images in Blob Storage:** Add the **Optical Character Recognition (OCR)** built-in skill.
- **Knowledge Store Projections:**
  - Unstructured/structured JSON trees -> **Objects** projection
  - Extracted files / images / documents -> **Files** projection
  - Relational tabular data -> **Tables** projection

---

## 🔵 Vision, NLP, Speech & Containers Quick Reference

| Service / Topic | Key Exam Fact |
| :--- | :--- |
| **Azure Vision Spatial Analysis** | Monitors **real-time video feeds** at the edge and generates alerts when employees enter restricted/high-risk zones. |
| **Azure AI Custom Vision** | Train custom classification or object detection models from your own image library. Use **Classification + Multiclass + General** for single-label images (cat vs. dog). |
| **Export Custom Vision Model for Disconnected Network** | **1. Change Domain to `General (compact)`** -> **2. Retrain the model** -> **3. Export the model**. |
| **Azure Vision Image Analysis (Prebuilt)** | Use **Image descriptions** for captions and **Image type detection** to classify photograph vs. drawing/clip art. |
| **NLP `recognize_entities` vs. `recognize_linked_entities`** | `recognize_entities` extracts named entities (`London`, `Buckingham Palace`). `recognize_linked_entities` links entities to **Wikipedia URLs** (not Bing) and provides character locations in `matches`, but does **not** detect document language. |
| **Custom Speech REST API Invalid Project ID** | Set the `project` property to the **Custom Speech project ID** (not the Foundry project ID). |
| **Mixed-Language Live Call Transcripts in Translator** | Enable **automatic language detection** before sending segments to Azure Translator. |
| **Azure AI Docker Containers (On-Premises)** | **1. Pull image from MCR** -> **2. Provision on-premises K8s cluster with internet connectivity** (for billing telemetry) -> **3. Run container with `ApiKey` and `Billing` Endpoint URL**. Note: `/status` checks container health locally (does not validate API key against Azure); `/swagger` hosts API docs. |
