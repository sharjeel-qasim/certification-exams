# AI-103 / AI-102: Microsoft Azure AI Engineer Associate — Practice Question Bank

[![Azure](https://img.shields.io/badge/Microsoft_Azure-0089D6?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/)
[![Exam](https://img.shields.io/badge/Exam-AI--103%20%2F%20AI--102-blue?style=for-the-badge)](#table-of-contents)
[![Questions](https://img.shields.io/badge/Questions-64%20Verified%20Questions-success?style=for-the-badge)](#table-of-contents)
[![Cheat Sheet](https://img.shields.io/badge/Study_Guide-Cheat_Sheet-orange?style=for-the-badge)](CHEAT_SHEET.md)

Complete, cleaned, and verified Practice Question Bank for the **Microsoft Certified: Azure AI Engineer Associate (AI-103 / AI-102)** exam. Covers Microsoft Foundry Agent Service, multi-agent orchestration workflows, Azure OpenAI & multimodal models, AI safety & evaluations, Azure Content Understanding, Azure AI Search (RAG), Computer Vision, NLP, and Speech services.

> [!TIP]
> Before taking the exam, review the [AI-103 / AI-102 Last-Minute Cram & Cheat Sheet](CHEAT_SHEET.md) for quick-fire comparison tables on Agent Orchestration patterns, Prompt Shields, Foundry Evaluators, Content Understanding modes, and Azure AI Search skills.

---

## Table of Contents

- [Domain 1: Plan and Manage an Azure AI & Microsoft Foundry Solution (Q1 – Q10)](#domain-1-plan-and-manage-an-azure-ai--microsoft-foundry-solution)
- [Domain 2: Implement Generative AI, Multimodal & Azure OpenAI Solutions (Q11 – Q21)](#domain-2-implement-generative-ai-multimodal--azure-openai-solutions)
- [Domain 3: Design and Implement AI Agents & Multi-Agent Workflows (Q22 – Q29)](#domain-3-design-and-implement-ai-agents--multi-agent-workflows)
- [Domain 4: Implement AI Safety, Guardrails, Evaluation & Observability (Q30 – Q39)](#domain-4-implement-ai-safety-guardrails-evaluation--observability)
- [Domain 5: Document Intelligence, Content Understanding & Knowledge Mining (Q40 – Q48)](#domain-5-document-intelligence-content-understanding--knowledge-mining)
- [Domain 6: Computer Vision, Natural Language Processing & Speech (Q49 – Q57)](#domain-6-computer-vision-natural-language-processing--speech)
- [Domain 7: Case Study — Contoso, Ltd. (Q58 – Q64)](#domain-7-case-study--contoso-ltd)

---

## Domain 1: Plan and Manage an Azure AI & Microsoft Foundry Solution

### Question 1
You are developing an app that will use the Speech and Language APIs. You need to provision resources for the app. The solution must ensure that each service is accessed by using a single endpoint and credential.

Which type of resource should you create?

- **A.** Microsoft Foundry service
- **B.** Content Safety in Foundry Control Plane
- **C.** Azure Speech in Foundry Tools
- **D.** Azure Language in Foundry Tools

**Correct answer:** A

> **Why:** A multi-service **Microsoft Foundry service** (Azure AI Services) resource bundles multiple Foundry Tools APIs (including Speech, Language, Vision, and Translation) under a single unified endpoint and API key/credential.

---

### Question 2
You are building a web app named `App1` by using the Azure OpenAI SDK. You need to configure `App1` to connect to an Azure OpenAI resource named `AI1` and generate completions.

What information must you provide?

- **A.** the endpoint, key, and model name
- **B.** the endpoint, key, and model type
- **C.** the deployment name, key, and model name
- **D.** the deployment name, endpoint, and key

**Correct answer:** D

> **Why:** Connecting to an Azure OpenAI resource via the SDK requires the **resource endpoint**, the **authentication key** (or Microsoft Entra token), and the specific **deployment name** (not the generic base model name).

---

### Question 3
You have a Microsoft Foundry project for a support ticket triage app that reads ticket text from a database. You need to ensure that the app meets the following requirements:
- Compares candidate models by quality, cost, and throughput
- Prevents hosting model weights in the Azure subscription

What should you configure? To answer, select the appropriate options in the answer area.

| Configuration Area | Available Options | Selected Option |
| :--- | :--- | :--- |
| **Model evaluation** | • Configure private endpoint access<br>• Use deployment lists and license tabs<br>• Use tool catalog connections and run traces<br>• **Use model catalog leaderboards and metrics** | **Use model catalog leaderboards and metrics** |
| **Deployment option** | • Bring your own model<br>• Build a vector index<br>• **Use a serverless deployment**<br>• Use a managed compute deployment | **Use a serverless deployment** |

> **Why:**
> - **Model catalog leaderboards and metrics** allow side-by-side comparison of candidate foundation models across quality benchmarks, cost, and throughput/latency.
> - **Serverless deployments** (Models-as-a-Service / Standard pay-per-token APIs) expose models via managed endpoints without hosting model weights on dedicated compute VMs inside your Azure subscription.

---

### Question 4
You are building a solution in Azure that will use the Azure Language in Foundry Tools service to process sensitive customer data. You need to ensure that only specific Azure processes on a subnet can access the Language service. The solution must minimize administrative effort.

What should you include in the solution?

- **A.** virtual network rules
- **B.** Azure Application Gateway
- **C.** a virtual network gateway
- **D.** IPsec rules

**Correct answer:** A

> **Why:** Configuring **virtual network rules** (with Virtual Network service endpoints) on the Azure AI / Language resource restricts access directly to specific VNet subnets with minimal administrative overhead.

---

### Question 5
You have an Azure subscription that contains a Microsoft Foundry Service resource named `CSAccount1` and a virtual network named `VNet1`. `CSAccount1` is connected to `VNet1`.

You need to ensure that only specific resources can access `CSAccount1`. The solution must meet the following requirements:
- Prevent external access to `CSAccount1`.
- Minimize administrative effort.

Which two actions should you perform? Each correct answer presents part of the solution.

- **A.** In `VNet1`, create a virtual subnet.
- **B.** In `CSAccount1`, modify the virtual network settings.
- **C.** In `VNet1`, modify the virtual network settings.
- **D.** In `VNet1`, enable a service endpoint for `CSAccount1`.
- **E.** In `CSAccount1`, configure the Access control (IAM) settings.

**Correct answers:** B, D

> **Why:** Securing an Azure AI / Foundry resource to specific VNet resources requires **(D)** enabling the `Microsoft.CognitiveServices` service endpoint on the subnet in `VNet1` and **(B)** modifying the networking/firewall settings in `CSAccount1` to disable public network access and allow only the selected virtual network subnet.

---

### Question 6
You have a Microsoft Foundry project that contains an agent. The agent currently uses a stored access key to retrieve secrets from an Azure key vault, which violates a keyless credentials requirement.

You need to ensure that the agent can retrieve the secrets. The solution must follow the principle of least privilege.

What should you configure? To answer, select the appropriate options in the answer area.

| Configuration | Selected Option |
| :--- | :--- |
| **Managed identity scope** | **Assign a system-assigned managed identity to the agent / project** |
| **Key Vault authorization method** | **Assign the Key Vault Secrets User role to the managed identity** |

> **Why:**
> - Using a **managed identity** eliminates stored keys and satisfies keyless authentication requirements.
> - Granting the **Key Vault Secrets User** RBAC role follows the principle of least privilege by allowing only read access to secret contents (without permissions to modify secrets, keys, or certificates).

---

### Question 7
You plan to create a Microsoft Foundry project named `Project1` that will contain an agent and use an Azure key vault named `KV1`. The agent will use identity-based authentication to access `KV1`.

You need to configure a connection from `Project1` to `KV1`. How should you complete the Bicep code?

```bicep
resource existingKeyVault 'Microsoft.KeyVault/vaults@2024-11-01' existing = {
  name: 'KV1'
  scope: resourceGroup()
}

resource connection 'Microsoft.CognitiveServices/accounts/connections@2025-04-01-preview' = {
  name: '${aiFoundryName}-keyvault'
  parent: aiFoundry
  properties: {
    category: '<Dropdown 1>'
    target: existingKeyVault.id
    authType: '<Dropdown 2>'
    isSharedToAll: true
    metadata: {
      ApiType: 'Azure'
    }
  }
}
```

| Dropdown | Available Options | Correct Selection |
| :--- | :--- | :--- |
| **Dropdown 1 (`category`)** | `'AzureAIService'`, `'AzureKeyVault'`, `'AzureOpenAI'` | **`'AzureKeyVault'`** |
| **Dropdown 2 (`authType`)** | `'AccountKey'`, `'AccountManagedIdentity'`, `'ApiKey'` | **`'AccountManagedIdentity'`** |

> **Why:** For a keyless Azure Key Vault connection on a Microsoft Foundry resource in Bicep, `category` must be set to `'AzureKeyVault'` and `authType` must be set to `'AccountManagedIdentity'` (or `'ManagedIdentity'`).

---

### Question 8
You are building a web app named `App1` that generates responses by using a model deployed to a Microsoft Foundry project named `Project1`. `App1` is one of several client applications that will use the same Azure AI Search data source configuration before sending prompts to the model.

You need to integrate `Project1` and `App1`. The solution must meet the following requirements:
- All client applications must use the same search configuration.
- The solution must use keyless authentication.
- Administrative effort must be minimized.

What should you do?

- **A.** Create a custom HTTP connection in Foundry and manually configure Azure AI Search endpoints per application.
- **B.** Enable a managed identity for each application and call Azure AI Search directly.
- **C.** Configure an Azure AI Search connection in `Project1` and reference the connection in each application.
- **D.** Call Azure AI Search directly from each application by using Microsoft Entra authentication.

**Correct answer:** C

> **Why:** Configuring a centralized **Azure AI Search connection** (with managed identity / keyless authentication) inside `Project1` allows all client applications to reference the shared project connection without duplicating search configurations or managing per-app credentials.

---

### Question 9
You are building an app that will scan confidential documents and use the Azure Language in Foundry Tools service to analyze the contents. You provision a Microsoft Foundry Service resource.

You need to ensure that the app can make requests to the Azure Language in Foundry Tools service endpoint while ensuring that the confidential documents remain on-premises.

Which three actions should you perform in sequence?

**Available Actions:**
- Run the container and specify an App ID and Client Secret.
- Provision an Azure Kubernetes Service (AKS) resource.
- Provision an on-premises Kubernetes cluster that is isolated from the internet.
- Provision an on-premises Kubernetes cluster that has internet connectivity.
- Run the container and specify an API key and the Endpoint URL of the Azure AI resource.
- Pull an image from the Microsoft Container Registry (MCR).
- Pull an image from Docker Hub.

**Correct Sequence:**
1. **Pull an image from the Microsoft Container Registry (MCR).**
2. **Provision an on-premises Kubernetes cluster that has internet connectivity.**
3. **Run the container and specify an API key and the Endpoint URL of the Azure AI resource.**

> **Why:** Azure AI Docker containers are hosted in the **Microsoft Container Registry (MCR)**. Running the container on an **on-premises Kubernetes cluster** keeps document payloads local, while **internet connectivity** combined with the **API key and Endpoint URL** (`Billing` and `ApiKey` arguments) is required so the container can send billing and usage telemetry to Azure.

---

### Question 10
You run the following command to start an Azure AI Sentiment Analysis container:

```bash
docker run --rm -it -p 5000:5000 --memory 10g --cpus 2 \
mcr.microsoft.com/azure-cognitive-services/textanalytics/sentiment \
Eula=accept \
Billing={ENDPOINT_URI} \
ApiKey={API_KEY}
```

For each of the following statements, select **Yes** if the statement is true. Otherwise, select **No**.

| Statement | Answer |
| :--- | :---: |
| Going to `http://localhost:5000/status` will query the Azure endpoint to verify whether the API key used to start the container is valid. | **No** |
| The container logging provider will write log data. | **Yes** |
| Going to `http://localhost:5000/swagger` will provide the details to access the documentation for the available endpoints. | **Yes** |

> **Why:**
> - **Statement 1 (No):** `http://localhost:5000/status` only reports whether the local container service is running; it does not query Azure to validate the billing API key (use `/ready` or send a test API request to verify billing readiness).
> - **Statement 2 (Yes):** The container writes console/diagnostic logs via the standard Docker logging provider.
> - **Statement 3 (Yes):** `/swagger` renders the interactive OpenAPI/Swagger UI documenting all local container endpoints.

---

## Domain 2: Implement Generative AI, Multimodal & Azure OpenAI Solutions

### Question 11
You have an Azure subscription. You need to build an app that will compare documents for semantic similarity. The solution must meet the following requirements:
- Return numeric vectors that represent the tokens of each document.
- Minimize development effort.

Which Azure OpenAI model should you use?

- **A.** DALL-E
- **B.** GPT-3.5
- **C.** GPT-4
- **D.** embeddings

**Correct answer:** D

> **Why:** **Embeddings** models (such as `text-embedding-3-small`, `text-embedding-3-large`, or `text-embedding-ada-002`) convert text into high-dimensional floating-point vectors for semantic similarity comparison and vector search.

---

### Question 12
You have a Microsoft Foundry project that contains a deployed chat model. You have a Python service that sends API requests to the model. The service is integrated with an automated validation system that compares generated outputs against approved response patterns.

Stakeholders report that small wording differences are causing validation mismatches. You need to update the request parameters to improve output stability. The solution must maximize reasoning quality.

How should you complete the Python code?

```python
message = client.messages.create(
    model="deployment-name",
    messages=[
        {"role": "user", "content": "Summarize the release notes in 3 bullet points."}
    ],
    max_tokens=800,
    temperature=<Dropdown 1>,
    thinking={"type": "enabled"},
    output_config={"effort": "<Dropdown 2>"}
)
```

| Dropdown | Available Options | Correct Selection |
| :--- | :--- | :--- |
| **Dropdown 1 (`temperature`)** | `0`, `0.7`, `1.0` | **`0`** |
| **Dropdown 2 (`effort`)** | `"high"`, `"low"`, `"medium"` | **`"high"`** |

> **Why:** Setting `temperature=0` makes token selection greedy/deterministic to eliminate wording variations across runs, while setting `output_config={"effort": "high"}` allocates maximum reasoning compute for complex tasks.

---

### Question 13
You have a web app named `App1` that sends requests to a multimodal chat model deployment in a Microsoft Foundry project. User messages can contain both text and images.

Currently, `App1` includes image URLs as plain text inside the message content, so the model cannot recognize them as images. Traces show that the requests contain a single text message instead of a multimodal content array.

You need to send the message as a structured array that includes both the text portion and the image reference to ensure that the model can process the image correctly.

What should you do?

- **A.** Set the user message content array to include items that have `type: text` and `type: image_url`.
- **B.** Encode the image to base64 and include the encoded data inside the content string of the user message.
- **C.** Place the image URL inside the System Message and set `type` to `image_url`, so the model loads the image at initialization.
- **D.** Add the image URL to the request metadata section, so the model can resolve the processing issue automatically.

**Correct answer:** A

> **Why:** Multimodal chat models require the `content` field of the user message to be a structured JSON array containing typed content parts: `{"type": "text", "text": "..."}` and `{"type": "image_url", "image_url": {"url": "..."}}`.

---

### Question 14
You have a Microsoft Foundry Agent Service agent that uses a compatible orchestrator model. You need to configure the image generation tool so the agent can create images from text prompts during conversations.

Which model deployment must be available in the same Foundry project?

- **A.** `gpt-image-1`
- **B.** `gpt-4.1-mini`
- **C.** FLUX series image generation model
- **D.** `gpt-4o-mini`

**Correct answer:** A

> **Why:** The built-in image generation tool in Microsoft Foundry Agent Service requires an OpenAI image generation deployment such as **`gpt-image-1`** (or `gpt-image-1.5`) in the same Foundry project.

---

### Question 15
You have a Python application that calls a `gpt-image-1.5` deployment in Azure OpenAI by using the Image REST API. The application stores an existing product image as `Image1.png` and a valid mask as `Mask1.png`.

You need to send a POST request that replaces only the masked area of `Image1.png` with a new product label.

Which endpoint and request body should you use?

- **A.** `/openai/deployments/{deployment}/images/edits` with `image` and `prompt` as multipart form data
- **B.** `/openai/deployments/{deployment}/images/generations` with `prompt` and `image` as multipart form data
- **C.** `/openai/deployments/{deployment}/images/edits` with `image`, `mask`, and `prompt` as multipart form data
- **D.** `/openai/deployments/{deployment}/images/generations` with `prompt`, `mask`, and `size` in the JSON body

**Correct answer:** C

> **Why:** Inpainting (replacing only a masked region of an existing image) uses the **`/openai/deployments/{deployment}/images/edits`** endpoint with `multipart/form-data` containing the source `image`, the `mask` image, and the text `prompt`.

---

### Question 16
You are building a customer support web app named `App1` in Microsoft Foundry that uses a GPT realtime model. `App1` must support:
- Live, low-latency voice conversations that use Azure OpenAI
- Streaming audio input from users and playback audio responses

You need to configure a connection method that supports real-time audio streaming in a client application and targets approximately 100 ms latency.

Which connection method should you use?

- **A.** WebSocket
- **B.** RTMP
- **C.** SIP
- **D.** WebRTC

**Correct answer:** D

> **Why:** For browser and client-side voice applications using the GPT Realtime API, **WebRTC** is the recommended protocol because it provides dedicated media tracks, network jitter handling, and ultra-low latency (~100 ms), whereas WebSockets are primarily designed for server-to-server connections.

---

### Question 17
You are building an app that will provide users with definitions of common AI terms. You create the following Python code:

```python
openai.api_key = key
openai.api_base = endpoint
response = openai.ChatCompletion.create(
    engine=deployment_name,
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "What is an LLM?"}
    ]
)
print(response['choices'][0]['message']['content'])
```

For each of the following statements, select **Yes** if the statement is true. Otherwise, select **No**.

| Statement | Answer |
| :--- | :---: |
| The response will contain an explanation of large language models (LLMs) that has a high degree of certainty. | **Yes** *(or **No** if disambiguating from Master of Laws)* |
| Changing `"What is an LLM?"` to `"What is an LLM in the context of AI models?"` will produce the intended response. | **Yes** |
| Changing `"You are a helpful assistant."` to `"You must answer only within the context of AI language models."` will give a higher likelihood of producing the intended response. | **Yes** |

> **Why:**
> - Adding explicit domain context in either the user prompt (`"in the context of AI models"`) or the system prompt (`"answer only within the context of AI language models"`) disambiguates acronyms like `LLM` (Large Language Model vs. Master of Laws) and grounds the model's output.

---

### Question 18
You have a Microsoft Foundry project that contains an agent. The agent generates summaries from retrieved policy documents.

You need to improve response completeness. The solution must be implemented in the logic of the application code before responses are returned.

What should you do?

- **A.** Add a retry evaluation before the responses are returned.
- **B.** Replace the model with a smaller deployment.
- **C.** Decrease the value of the `max_tokens` parameter.
- **D.** Increase the value of the `presence_penalty` parameter.

**Correct answer:** A

> **Why:** Implementing a **retry evaluation loop** in application code evaluates the generated summary for completeness before returning it to the user and automatically re-prompts the agent when required clauses are missing.

---

### Question 19
> **Scenario Set (Questions 19–21):** Each question presents a unique solution to the same scenario. Determine whether the solution meets the stated goals.

You have a Microsoft Foundry project that contains an agent. The agent generates summaries from retrieved policy documents. Users report that some responses omit required regulatory clauses, even when the clauses are present in the retrieved content.

You need to improve response completeness.

**Solution:** You run an evaluation flow that scores responses for completeness and blocks responses that fall below a defined threshold.

Does this meet the goal?

- **A.** Yes
- **B.** No

**Correct answer:** B

> **Why:** Simply blocking responses below a threshold prevents incomplete outputs from being shown (resulting in errors/empty responses), but it does **not** improve the completeness of the generated summaries themselves (which requires prompt refinement or a retry-with-feedback loop).

---

### Question 20
You have a Microsoft Foundry project that contains an agent. The agent generates summaries from retrieved policy documents. Users report that some responses omit required regulatory clauses, even when the clauses are present in the retrieved content.

You need to improve response completeness.

**Solution:** You increase the value of the `temperature` parameter.

Does this meet the goal?

- **A.** Yes
- **B.** No

**Correct answer:** B

> **Why:** Increasing `temperature` increases token sampling randomness/creativity, which can reduce factual adherence and does not ensure required regulatory clauses are included.

---

### Question 21
You have a Microsoft Foundry project that contains an agent. The agent generates summaries from retrieved policy documents. Users report that some responses omit required regulatory clauses, even when the clauses are present in the retrieved content.

You need to improve response completeness.

**Solution:** You increase the value of the `top_p` parameter.

Does this meet the goal?

- **A.** Yes
- **B.** No

**Correct answer:** B

> **Why:** Increasing `top_p` (nucleus sampling) widens the pool of candidate tokens during generation, which increases variability rather than improving summary completeness.

---

## Domain 3: Design and Implement AI Agents & Multi-Agent Workflows

### Question 22
A multi-agent customer support solution built using the Microsoft Foundry Agent Service features a triage agent, a billing agent, and a technical agent. The triage agent evaluates the customer query and transfers control directly to the appropriate specialist. Each specialist can handle the conversation and pass it back or onward if the topic shifts. No central orchestrator or planner agent coordinates the steps.

Which agent orchestration pattern should you use?

- **A.** Sequential
- **B.** Concurrent
- **C.** Handoff
- **D.** Magentic

**Correct answer:** C

> **Why:** In the **Handoff** orchestration pattern, agents dynamically delegate and transfer execution control directly to specialist peers based on conversation context without relying on a central planner/orchestrator.

---

### Question 23
You have a Microsoft Foundry project that contains three agents as shown in the following table:

| Name | Description |
| :--- | :--- |
| `TriageAgent` | Classifies incoming customer requests |
| `PolicyAgent` | Answers policy questions by searching internal content |
| `ActionAgent` | Creates or updates tickets by calling an HTTP API |

You need to orchestrate the agents to ensure that the customer requests meet the following requirements:
- Support a deterministic, step-based process that uses conditional branching and shared state across the agents.
- Optionally trigger a ticket action based on the triage result.
- Minimize development effort.

What should you include in the solution?

- **A.** a workflow
- **B.** a multi-agent group chat session
- **C.** threads and runs without a workflow
- **D.** separate agent runs coordinated in the application code

**Correct answer:** A

> **Why:** Microsoft Foundry **workflows** declaratively define deterministic, step-based multi-agent pipelines with shared state and conditional branching without writing custom orchestration logic in application code.

---

### Question 24
You have a Microsoft Foundry project that contains an agent named `PaymentAgent`. `PaymentAgent` includes a function tool that issues customer refunds by using an external API.

You are creating a workflow in YAML. You need to ensure that the workflow pauses for human approval and continues with the refund step only after approval is granted.

How should you complete the workflow definition?

```yaml
steps:
  - id: propose_refund
    type: agent
    agent: PaymentAgent
  - id: approval
    type: <Dropdown 1>
  - id: execute_refund
    type: agent
    agent: PaymentAgent
    condition: <Dropdown 2>
```

| Dropdown | Available Options | Correct Selection |
| :--- | :--- | :--- |
| **Dropdown 1 (`type`)** | `ask_question`, `basic_chat`, `data_transformation` | **`ask_question`** |
| **Dropdown 2 (`condition`)** | Approval output evaluation expression | **`approval.output == 'approved'` *(or equivalent approval condition)*** |

> **Why:** In Foundry declarative YAML workflows, the **`ask_question`** step type pauses workflow execution to solicit interactive human input/approval, and the subsequent `execute_refund` step uses a **`condition`** expression checking that approval was granted.

---

### Question 25
You have a Microsoft Foundry project named `Project1` that contains the following:
- An OpenAPI tool that calls an external API
- A project connection named `Connection1` that stores the API key of the external API

When an agent calls the OpenAPI tool, the API returns a `401 Unauthorized` error, and traces show that the API key header is NOT being sent.

You need to ensure that the OpenAPI tool automatically includes the API key from `Connection1` on all requests.

What should you do?

- **A.** Add the API key header manually to the OpenAPI specification.
- **B.** Enable identity passthrough so that the tool uses the Microsoft Entra token of the caller.
- **C.** Configure the tool to use the default connection of `Project1`.
- **D.** Connect the tool to `Connection1`.

**Correct answer:** D

> **Why:** An OpenAPI tool in Microsoft Foundry only injects stored credentials into outgoing HTTP requests when the tool is explicitly **associated/connected with the project connection (`Connection1`)** configured for API key authentication.

---

### Question 26
You have a Microsoft Foundry project named `Project1` that contains an agent. The agent uses an OpenAPI 3.0 specification to call an external weather service.

The weather service requires a key to be passed in an HTTP header. The key value is stored as a connection in `Project1`.

You need to ensure that the key value from the connection is included automatically whenever the OpenAPI tool is invoked.

What should you configure in the OpenAPI specification?

- **A.** an API key security scheme
- **B.** a Bearer token security scheme
- **C.** a header parameter defined for each operation
- **D.** an Azure Key Vault connection

**Correct answer:** A

> **Why:** In an OpenAPI 3.0 specification, defining an **API key security scheme** (`type: apiKey`, `in: header`, `name: <Header-Name>`) under `components.securitySchemes` tells Foundry which HTTP header to populate with the key from the linked project connection.

---

### Question 27
You have a Microsoft Foundry project that contains an agent. The agent has a Model Context Protocol (MCP) tool named `kbsearch` that queries a knowledge base stored in Azure AI Search.

Some agent runs return answers from the base model without invoking the knowledge base, which results in responses without grounded citations.

You are provided with the following code snippet that runs the agent:

```python
run = project_client.agents.runs.create_and_process(
    thread_id=thread.id,
    agent_id=agent.id
)
```

You need to deterministically force the agent to invoke `kbsearch` on each run. What should you do?

- **A.** Add the `toolset` parameter to the `create_and_process()` method call.
- **B.** Replace the `create_and_process()` method with the `create_thread_and_process_run()` method.
- **C.** Add the `response_format` parameter to the `create_and_process()` method call.
- **D.** Add the `tool_choice` parameter to the `create_and_process()` method call.

**Correct answer:** D

> **Why:** Passing the **`tool_choice`** parameter (set to `"required"` or specifying the `kbsearch` tool explicitly) in `create_and_process()` forces the agent to invoke the tool rather than relying on the model's default `"auto"` decision.

---

### Question 28
You have a Microsoft Foundry project that contains an agent. The agent uses tools to retrieve internal content and call external APIs. The agent is currently configured to let the model decide when to call the tools.

You need to publish the agent for a compliance workflow. The solution must meet the following requirements:
- Each workflow run must include a retrieval step before generating a response.
- Tool calls must authenticate by using the published agent's own identity.
- Tool access must use an identity isolated from other project resources.
- Tool access must support audit tracing.

What should you do? To answer, select the appropriate options in the answer area.

| Configuration | Available Options | Selected Option |
| :--- | :--- | :--- |
| **Set tool choice to** | • `auto`<br>• `none`<br>• **`required`** | **`required`** |
| **Configure the tool to authenticate by** | • Storing API keys in prompts<br>• Using the shared project agent<br>• **Using a distinct agent identity** | **Using a distinct agent identity** |

> **Why:**
> - Setting **tool choice to `required`** guarantees that the agent executes a tool call (retrieval step) before producing a final response.
> - Configuring **a distinct agent identity** gives the published agent its own isolated managed identity separate from the shared project identity, enabling per-agent RBAC isolation and audit tracing.

---

### Question 29
You are creating an agent workflow in a Microsoft Foundry project to support natural voice interactions. The agent must receive continuous audio input, convert the input into text for reasoning, and then return spoken responses to a user.

The workflow must meet the following requirements:
- Support turn-taking dynamics, where the agent begins to generate the speech output before the user finishes speaking.
- Operate with low latency to maintain a conversational experience.

You need to enable both speech-to-text and text-to-speech for ongoing interactions between the user and the agent. What should you do?

- **A.** Use an embeddings model to encode the audio, and then decode the audio into text and speech.
- **B.** Use batch transcription to convert the audio input and return text responses from the agent.
- **C.** Use speech translation to convert the audio into another language and return the translated text.
- **D.** Use real-time speech to text for incoming audio and text to speech for agent responses.

**Correct answer:** D

> **Why:** Streaming **real-time speech-to-text (STT)** provides continuous partial transcripts for low-latency turn-taking, while streaming **text-to-speech (TTS)** synthesizes agent responses immediately as tokens are generated.

---

## Domain 4: Implement AI Safety, Guardrails, Evaluation & Observability

### Question 30
You have a Microsoft Foundry agent that processes refund requests by using a `gpt-4.1` deployment. The agent is configured to call a refund tool only when the user message and uploaded product image match an approved return policy.

The image preprocessing step extracts visible text from uploaded images and includes the text in the agent input. Some uploaded images contain text that asks the agent to create a refund case even when the photo evidence does not support one.

You need to detect this risk before the agent decides whether to call the refund tool. Which safety feature should you configure?

- **A.** Prompt Shields
- **B.** Groundedness detection
- **C.** Protected material detection
- **D.** Image moderation

**Correct answer:** A

> **Why:** **Prompt Shields** in Azure AI Content Safety detect both direct user jailbreaks and **indirect prompt injection attacks** hidden in external documents or OCR text extracted from images.

---

### Question 31
You have an app named `App1` that uses a Microsoft Foundry multimodal model deployment. `App1` runs optical character recognition (OCR) on uploaded images and appends the OCR output to the prompt as additional context.

Some uploaded images contain embedded text. You need to prevent potentially malicious instructions in that extracted text from being processed by the model.

What should you use?

- **A.** prompt shields for documents
- **B.** image moderation
- **C.** protected material text
- **D.** prompt shields for user prompts

**Correct answer:** A

> **Why:** Because the OCR output is appended as third-party/external context rather than typed directly by the user, it represents an indirect prompt injection vector and is protected by **prompt shields for documents** (Document Attack Detection).

---

### Question 32
You have a Microsoft Foundry project that contains an agent. The agent accepts user-uploaded screenshots and uses a multimodal chat model. Some screenshots contain potentially malicious embedded text.

You need to prevent a prompt injection attack and ensure that third-party content is treated as lower trust.

How should you configure prompt shields for document attacks?

| Configuration | Selected Option |
| :--- | :--- |
| **Prompt shields action** | **Annotate and block** |
| **Additional mitigation** | **Use spotlighting** |

> **Why:**
> - **Annotate and block** detects and blocks indirect prompt injection attempts in untrusted document/image inputs.
> - **Spotlighting** marks untrusted third-party inputs with special delimiters/encodings so the LLM distinguishes lower-trust external data from trusted system instructions.

---

### Question 33
You are deploying a support agent that enables users to upload photos. You need to automatically classify uploaded images for harmful content (Hate, Violence, Self-Harm, Sexual). The solution must block content based on severity levels.

What should you do?

- **A.** Enable prompt shields.
- **B.** Apply keyword scanning to optical character recognition (OCR) output by using Azure Vision in Foundry Tools.
- **C.** Implement image moderation.
- **D.** Use blocklists.

**Correct answer:** C

> **Why:** **Image moderation** in Azure AI Content Safety analyzes uploaded images across harm categories (Hate, Violence, Sexual, Self-Harm) and assigns severity scores (`0–6`) that can be filtered/blocked by threshold.

---

### Question 34
You have a Microsoft Foundry project that contains a Retrieval Augmented Generation (RAG) solution. You need to run a pre-production evaluation by using a labeled CSV dataset that contains the `query`, `context`, `response`, and `ground_truth`.

The evaluation must measure the following:
- Whether responses address the user query
- Whether responses are supported by the provided context
- Whether responses contain sensitive or proprietary information

Which AI quality evaluation metrics should you use?

| Requirement | Selected Evaluation Metric(s) |
| :--- | :--- |
| **To measure whether the responses are supported by the provided context and address the user query** | **Groundedness and Relevance** |
| **To measure whether responses contain sensitive or proprietary information** | **Content safety / Protected material detection** |

> **Why:**
> - **Groundedness** measures whether the generated response is factual with respect to the retrieved `context`, and **Relevance** measures how well the response answers the user `query`.
> - **Content safety / Protected material** evaluators detect sensitive, harmful, or proprietary/copyrighted content in model outputs.

---

### Question 35
You plan to configure an evaluation in Microsoft Foundry for a Retrieval Augmented Generation (RAG) chat app. You need to provide scores for groundedness, relevance, and harmful content categories.

Which two evaluation categories should you use?

- **A.** fluency evaluator
- **B.** AI quality (NLP) metrics
- **C.** similarity evaluators
- **D.** AI quality (AI-assisted) metrics
- **E.** risk and safety metrics

**Correct answers:** D, E *(Note: some practice keys list **B, E**, though in Microsoft Foundry Groundedness and Relevance are **D. AI quality (AI-assisted) metrics**, while BLEU/ROUGE/F1 are NLP metrics)*

> **Why:**
> - **AI quality (AI-assisted) metrics** use an LLM judge to score **Groundedness**, **Relevance**, **Coherence**, and **Fluency**.
> - **Risk and safety metrics** evaluate outputs across harmful content categories (Violence, Sexual, Self-harm, Hate and unfairness).

---

### Question 36
You have a Microsoft Foundry project that contains a prompt agent used by a customer support web app. The agent is invoked from a Python service that does NOT run in the Foundry portal.

You need to implement end-to-end tracing to capture latency breakdowns and exceptions across agent runs.

Which two components can you use? Each correct answer presents a complete solution.

- **A.** Microsoft Sentinel
- **B.** OpenTelemetry
- **C.** Application Insights
- **D.** a Log Analytics workspace
- **E.** the Azure Monitor Agent

**Correct answers:** B, C

> **Why:** End-to-end tracing for external Python applications calling Microsoft Foundry agents is instrumented using the **OpenTelemetry** SDK (`azure-core-tracing-opentelemetry`) and exported to **Azure Application Insights** for visualizing distributed traces, latency spans, and exceptions.

---

### Question 37
You have a web app named `App1` that processes user prompts by integrating with a Microsoft Foundry project named `Project1`. `App1` performs the following actions:
- Sends prompts directly to a model by using the Azure OpenAI Responses API
- Invokes the Azure AI Content Safety tool by using a Foundry connection within the same request

You need to configure end-to-end visibility into each step of the request workflow. What should you do?

- **A.** Enable logging by using Foundry Local.
- **B.** Enable application tracing in `Project1`.
- **C.** Enable logging by using the client SDK for Content Safety.
- **D.** Route requests through the Azure OpenAI endpoint.

**Correct answer:** B

> **Why:** Enabling **application tracing** in the Microsoft Foundry project (`Project1`) links Application Insights to the project and captures end-to-end distributed traces across model calls (Responses API) and connected Foundry tools (Content Safety).

---

### Question 38
You have a Microsoft Foundry project that contains a high-traffic agent. After a recent update, operational costs increase significantly. Monitoring confirms that the volume of user traffic to the agent remains unchanged.

You suspect that changes to the request or response characteristics are causing the increase. You need to identify whether the additional costs are driven by the model input size, the model output size, or expanded tool usage.

Which observability capability should you use?

- **A.** run success rate
- **B.** evaluation metrics
- **C.** latency
- **D.** token usage

**Correct answer:** D

> **Why:** **Token usage** observability breaks down prompt (input) tokens, completion (output) tokens, and tokens consumed by intermediate tool invocations, directly pinpointing the driver of increased LLM consumption costs.

---

### Question 39
You have a Microsoft Foundry project that contains a multi-agent solution. The agents use tool calling to query internal systems.

You need to implement responsible AI auditing to meet the following requirements:
- Capture all the nested operations across the entire agent run.
- Record tool invocation arguments and returned results as metadata.

What should you use for each requirement?

**Available Options:** `Hierarchical spans`, `A KQL query filter`, `Sampling`, `Tool call attributes`, `Trace sampling policy`

| Requirement | Selected Option |
| :--- | :--- |
| **Capture all the nested operations across the entire agent run** | **Hierarchical spans** |
| **Record tool invocation arguments and returned results as metadata** | **Tool call attributes** |

> **Why:**
> - **Hierarchical spans** in OpenTelemetry represent parent-child relationships across an entire multi-agent run (orchestrator -> sub-agent -> model call -> tool execution).
> - **Tool call attributes** attach structured key-value metadata (such as function name, input arguments, and output payload) to the tool execution span.

---

## Domain 5: Document Intelligence, Content Understanding & Knowledge Mining

### Question 40
You have a set of scanned files. You need to extract text from the files and perform sentiment analysis.

Which service should you use for each task?

| Task | Available Options | Selected Service |
| :--- | :--- | :--- |
| **Extract text** | `Azure AI Search`, `Azure Vision in Foundry Tools`, **`Azure Document Intelligence`** | **Azure Document Intelligence** |
| **Perform sentiment analysis** | `Azure AI Search`, `Azure AI Computer Vision`, **`Azure Language in Foundry Tools`** | **Azure Language in Foundry Tools** |

> **Why:** **Azure Document Intelligence** extracts text, tables, and structure from scanned documents using OCR, while **Azure Language in Foundry Tools** provides prebuilt **Sentiment Analysis** and opinion mining on the extracted text.

---

### Question 41
You have a Microsoft Foundry project that processes procurement documents submitted by suppliers. You need to implement two pipelines by using Azure Content Understanding in Foundry Tools.

The solution must meet the following requirements:
- Include a pipeline named `Pipeline1` that supports cost-effective, high-volume processing of standalone PDF invoices.
- Include a pipeline named `Pipeline2` that supports cross-document validation by using multi-step reasoning and reference data.

How should you configure each pipeline?

**Available Configurations:**
- `Multi-file task in pro mode`
- `Multi-file task in standard mode`
- `Single-file task in pro mode`
- `Single-file task in standard mode`

| Pipeline | Selected Configuration |
| :--- | :--- |
| **`Pipeline1`** | **Single-file task in standard mode** |
| **`Pipeline2`** | **Multi-file task in pro mode** |

> **Why:**
> - **Standard mode (`Single-file task in standard mode`)** is optimized for fast, cost-effective, high-volume extraction from individual documents like standalone invoices.
> - **Pro mode (`Multi-file task in pro mode`)** uses advanced multi-step reasoning across multiple files and reference documents for cross-document validation.

---

### Question 42
You have an application that processes scanned PDF invoices. The invoices have varied layouts and include multipage tables.

You have a pipeline that uses optical character recognition (OCR) and extracts totals and invoice numbers. The results are often incorrect because the document structure is ignored.

You need to implement a solution that provides OCR, layout analysis, and template-generalizing field extraction. The solution must NOT require training a custom model and must minimize administrative effort.

What should you include in the solution?

- **A.** Azure Content Understanding in Foundry Tools
- **B.** Azure Language in Foundry Tools
- **C.** an Azure Machine Learning model
- **D.** Azure Vision in Foundry Tools

**Correct answer:** A

> **Why:** **Azure Content Understanding in Foundry Tools** combines OCR, layout/table structure analysis, and generative schema-driven field extraction across varied invoice templates without requiring custom model training.

---

### Question 43
You have a Microsoft Foundry project that ingests scanned PDF invoices stored in Azure Blob Storage. Each invoice contains printed line items and has a table-based layout. Extracted results are stored as structured JSON and used as grounding data for an agent in a Retrieval Augmented Generation (RAG) solution.

You need to create a single analyzer that meets the following requirements:
- Extracts the invoice number, invoice date, vendor name, and total amount across varying templates
- Returns confidence scores so that results with confidence below `0.80` can be routed for supervisor review

What should you use?

- **A.** a custom Azure Content Understanding in Foundry Tools analyzer that defines the required fields as the extracted fields and returns confidence scores
- **B.** the Azure Content Understanding in Foundry Tools `prebuilt-layout` analyzer
- **C.** the Azure Content Understanding in Foundry Tools `prebuilt-documentSearch` analyzer and `search.score` from the Azure AI Search index
- **D.** a Foundry agent that has groundedness guardrails enabled to extract invoice fields and confidence scores

**Correct answer:** A

> **Why:** A **custom analyzer in Azure Content Understanding** lets you define a custom field schema (`invoiceNumber`, `invoiceDate`, `vendorName`, `totalAmount`) and outputs structured JSON with per-field **confidence scores** for human-in-the-loop routing (`< 0.80`), whereas `prebuilt-layout` only extracts layout elements without domain-specific invoice fields.

---

### Question 44
You have a Microsoft Foundry project that contains an agent. The knowledge source for the agent is a set of scanned PDF troubleshooting guides stored in Azure Blob Storage. The guide pages contain two-column layouts and tables.

You use Azure Content Understanding in Foundry Tools to process the PDFs. You plan to ingest the processed content into an index for Retrieval Augmented Generation (RAG) and store extracted fields for downstream automation.

Stakeholders must be able to verify where each extracted field value came from in the original PDF and route low-reliability extractions for manual review.

You need to ensure that the Content Understanding document analyzer output includes a per-field confidence score and source grounding to locations within the source document. What should you do?

- **A.** Configure the analyzer to use generative extraction for all fields.
- **B.** Provide labeled samples.
- **C.** Enable `estimateFieldSourceAndConfidence`.
- **D.** Set `enableSegment` to `true`.

**Correct answer:** C

> **Why:** Setting **`estimateFieldSourceAndConfidence`** to `true` in an Azure Content Understanding analyzer instructs the service to return both a per-field confidence score and bounding-box/page source grounding coordinates in the original PDF.

---

### Question 45
You have a Microsoft Foundry project that contains an agent. You need to process mixed-format documents that contain scanned text, tables, and multicolumn layouts. The extracted content must preserve the document structure and be converted into the Markdown format for downstream reasoning.

What should you configure first?

- **A.** an Azure OpenAI Responses API call that uses a multimodal model
- **B.** an Azure Language in Foundry Tools text analysis model deployment
- **C.** an Azure Content Understanding in Foundry Tools analyzer
- **D.** a generative chat completion request

**Correct answer:** C

> **Why:** **Azure Content Understanding in Foundry Tools** analyzers natively parse complex scanned text, tables, and multicolumn layouts and convert the structured document representation directly into **Markdown** for downstream LLM/RAG consumption.

---

### Question 46
You are building an Azure AI Search indexing pipeline named `Pipeline1` that ingests invoices stored in Azure Blob Storage. The invoices are stored as scanned images.

You need to enable users to search invoice data across the invoice fields.

Which built-in skill should you add to the skillset of `Pipeline1`?

- **A.** Text Split
- **B.** Image Analysis
- **C.** Text Translation
- **D.** optical character recognition (OCR)

**Correct answer:** D

> **Why:** The built-in **Optical Character Recognition (`#Microsoft.Skills.Vision.OcrSkill`)** skill extracts printed and handwritten text from scanned image blobs during indexing so the text can be indexed and searched in Azure AI Search.

---

### Question 47
You are creating an enrichment pipeline that will use Azure AI Search. The knowledge store contains unstructured JSON data and the text/files from scanned PDF documents.

Which projection type should you use for each data type in the Azure AI Search Knowledge Store?

| Data Type | Selected Projection Type |
| :--- | :--- |
| **JSON data** | **Objects** |
| **Extracted text / document data** | **Files** *(or **Tables** for tabular rows)* |

> **Why:** In an Azure AI Search Knowledge Store:
> - **Object projections (`Objects`)** store enriched document trees as structured JSON blobs in Azure Blob Storage.
> - **File projections (`Files`)** store binary files ornormalized images/documents in Azure Blob Storage (while **Table projections** store relational rows in Azure Table Storage).

---

### Question 48
You have a Microsoft Foundry project that contains an agent. The agent uses Azure AI Search for Retrieval Augmented Generation (RAG). You plan to ingest and index PDF product manuals.

You need to build a solution that supports semantic similarity matching. The solution must ensure that the agent retrieves relevant data when user questions use different wording than the product manuals.

Which indexing approach should you use?

- **A.** vector search
- **B.** semantic ranking
- **C.** suggesters
- **D.** analyzers

**Correct answer:** A

> **Why:** **Vector search** indexes embeddings of document chunks and queries them by cosine/vector similarity in semantic space, enabling retrieval of conceptually relevant passages even when user phrasing shares no exact keywords with the source manuals.

---

## Domain 6: Computer Vision, Natural Language Processing & Speech

### Question 49
You need to recommend a service that meets the following requirements:
- Generates alerts when employees enter high-risk areas
- Monitors video feeds in real time
- Minimizes development effort

What should you recommend?

- **A.** Azure AI Video Indexer
- **B.** Azure Vision in Foundry Tools Image Analysis
- **C.** Azure Vision in Foundry Tools Spatial Analysis
- **D.** Object detection in Azure Custom Vision

**Correct answer:** C

> **Why:** **Spatial Analysis** in Azure AI Vision processes real-time video streams (via containers on edge devices) to detect person movement, count occupancy, and trigger alerts when people cross lines or enter restricted zones (`personCrossingPolygon`).

---

### Question 50
You are designing an Azure AI solution to identify defective products on a production line. You have a real-time video feed and an image library of sample products that are approved or rejected manually.

You need to recommend a service that meets the following requirements:
- Monitors the video feed and identifies the defective products.
- Can train a new model by using the image library.
- Minimizes development effort.

What should you recommend?

- **A.** Azure Vision in Foundry Tools
- **B.** Azure AI Video Indexer
- **C.** Azure AI Custom Vision
- **D.** Azure Machine Learning

**Correct answer:** C

> **Why:** **Azure AI Custom Vision** allows you to train custom image classification or object detection models using your own labeled image library (approved vs. defective products) with minimal code and no manual deep-learning pipeline engineering.

---

### Question 51
You are building a Custom Vision model. You have images of cats and dogs. Each image contains either a cat or a dog.

You need to use the Azure Custom Vision service to detect whether the image is of a cat or a dog. How should you configure the project in the Azure Custom Vision portal?

| Setting | Available Options | Selected Option |
| :--- | :--- | :--- |
| **Project Types** | `Classification`, `Object Detection` | **`Classification`** |
| **Classification Types** | `Multiclass (Single tag per image)`, `Multilabel (Multiple tags per image)` | **`Multiclass (Single tag per image)`** |
| **Domains** | `Adult`, `Food`, `General`, `General (compact)`, `Landmarks`, `Retail` | **`General`** |

> **Why:** Categorizing a whole image as either a cat or a dog (mutually exclusive classes, without bounding boxes) requires a **Classification** project with **Multiclass (Single tag per image)** and the **General** domain.

---

### Question 52
You have an Azure Custom Vision service project that performs object detection. The project uses the `General` domain for classification and contains a trained model.

You need to export the model for use on a network that is disconnected from the internet.

Which three actions should you perform in sequence?

**Available Actions:**
- Change the classification type.
- Export the model.
- Change Domains to `General (compact)`.
- Create a new classification model.
- Retrain the model.

**Correct Sequence:**
1. **Change Domains to `General (compact)`.**
2. **Retrain the model.**
3. **Export the model.**

> **Why:** Only **compact domains** (such as `General (compact)`) can be exported to edge formats (ONNX, TensorFlow, CoreML, Dockerfile). When converting an existing project from `General` to `General (compact)`, you must **change the domain**, **retrain the model**, and then **export** the newly trained iteration.

---

### Question 53
You are building an app that will share user images. You need to configure the app to perform the following actions when a user uploads an image:
- Categorize the image as either a photograph or a drawing.
- Generate a caption for the image.

The solution must minimize development effort. Which two features should you include in the solution? Each correct answer presents part of the solution.

- **A.** image classification in Azure Custom Vision
- **B.** image descriptions in Azure Vision in Foundry Tools
- **C.** content tags in Azure Vision in Foundry Tools
- **D.** object detection in Azure Vision in Foundry Tools
- **E.** image type detection in Azure Vision in Foundry Tools

**Correct answers:** B, E

> **Why:** Prebuilt **Azure Vision in Foundry Tools** Image Analysis provides **(B) image descriptions/captions** (`Caption`) to generate natural-language descriptions and **(E) image type detection** (`ImageType`) to detect whether an image is clip art or a line drawing vs. a photograph.

---

### Question 54
You are building a solution that students will use to find references for essays. You use the following Python code:

```python
from azure.core.credentials import AzureKeyCredential
from azure.ai.textanalytics import TextAnalyticsClient

endpoint = os.environ["AZURE_TEXT_ANALYTICS_ENDPOINT"]
key = os.environ["AZURE_TEXT_ANALYTICS_KEY"]

text_analytics_client = TextAnalyticsClient(endpoint=endpoint, credential=AzureKeyCredential(key))
documents = [
    "Our tour guide took us up the Space Needle during our trip to Seattle last week."
]
result = text_analytics_client.recognize_linked_entities(documents)
```

For each of the following statements, select **Yes** if the statement is true. Otherwise, select **No**.

| Statement | Answer |
| :--- | :---: |
| The code will detect the language of documents. | **No** |
| The `url` attribute returned for each linked entity will be a Bing search link. | **No** |
| The `matches` attribute returned for each linked entity will provide the location in a document where the entity is referenced. | **Yes** |

> **Why:**
> - **Statement 1 (No):** `recognize_linked_entities` performs entity linking, not language detection (`detect_language` detects language).
> - **Statement 2 (No):** Entity linking disambiguates entities by returning a **Wikipedia URL** (e.g., `https://en.wikipedia.org/wiki/Space_Needle`), not a Bing search link.
> - **Statement 3 (Yes):** Each linked entity's `matches` collection includes `offset` and `length` properties specifying the exact character position in the document where the entity was mentioned.

---

### Question 55
You are developing a text processing solution. You have the following Python function:

```python
def get_key_words(textAnalyticsClient, text):
    response = textAnalyticsClient.recognize_entities(documents=[text])[0]
    print("Key Words:")
    for entity in response.entities:
        print("\t\t", entity.text)
```

You call the function and use the following string as the second argument:
`"Our tour of London included a visit to Buckingham Palace"`

What will be the output of the function?

- **A.** `London` and `Buckingham Palace` only
- **B.** `Tour` and `visit` only
- **C.** `Our tour of London included a visit to Buckingham Palace`
- **D.** `London` and `Tour` only

**Correct answer:** A

> **Why:** Despite the custom function name `get_key_words`, the code calls `recognize_entities()`, which performs **Named Entity Recognition (NER)** and extracts the named geographic/location entities **`London`** and **`Buckingham Palace`**.

---

### Question 56
You have a Microsoft Foundry project that contains an agent. The agent uses Azure Speech in Foundry Tools. You fine-tune a baseline speech-to-text model for the `en-US` locale and publish the model.

The agent calls the Speech-to-text REST API and returns an error message indicating that the project ID is invalid. You need to set the project property to the correct ID.

To what should you set the project property?

- **A.** the custom speech endpoint URL
- **B.** the Microsoft Foundry project URL
- **C.** the custom speech project ID
- **D.** the Microsoft Foundry project ID

**Correct answer:** C

> **Why:** When referencing a Custom Speech project in Speech API requests, the `project` property must be set to the **Custom Speech project ID** (rather than the parent Microsoft Foundry project ID or URL).

---

### Question 57
You have an application named `App1` that uses Azure Speech in Foundry Tools to transcribe live calls. Transcript segments often contain both English and Spanish. `App1` sends each segment to Azure Translator in Foundry Tools to translate to another language.

Sometimes, mixed-language segments result in incomplete or incorrect translations. You need to reduce translation errors. The solution must ensure that the entire transcript is translated successfully and minimize development effort.

What should you do before sending the segments to Translator?

- **A.** Enable automatic language detection for the translation request.
- **B.** Specify English as the source language in the translation request for all the segments.
- **C.** Split the mixed-language segments into single-language segments and translate each segment separately.
- **D.** Use document translation to translate the entire transcript as a single document.

**Correct answer:** A

> **Why:** Omitting the fixed `from` source language parameter enables **automatic language detection** in Azure Translator so each segment's dominant language is detected dynamically with minimal development effort.

---

## Domain 7: Case Study — Contoso, Ltd.

> [!NOTE]
> **Case Study Scenario Summary (Contoso, Ltd.):**
> - **Generative Environment:** Contoso has a Microsoft Foundry resource with two projects: `Project1` and `Project2`.
>   - **`Project1`:** Contains `Agent1`, which handles customer product inquiries.
>   - **`Project2`:** Contains a deployed video generation model used by the marketing department.
> - **Data Environment:** Product sheets are stored as PDF files in an Azure Storage account named `storage1` (containing both visual and textual product details). Finance department also reviews vendor invoices and contracts with complex visual/tabular layouts.
> - **Technical & Business Requirements:**
>   - `Agent1` must use product sheets from `storage1` via **semantic and vector search** so responses are grounded, complete, and accurate.
>   - `Agent1` must answer customer questions **only about Contoso products**.
>   - The model deployment used by `Agent1` must support burst/variable generative AI traffic **without requiring reserved capacity**, and the model version must produce **consistent responses** across time.
>   - Finance requires a multimodal solution to analyze both textual and visual content in invoices/contracts.

---

### Question 58 (Case Study 1/7)
You need to ensure that the marketing department can generate videos by using the model deployed to `Project2`.

How should you complete the Python code?

```python
import time
from openai import OpenAI

client = OpenAI(
    base_url="https://Contoso.openai.azure.com/openai/v1/",
    api_key=...
)

video = client.videos.<Dropdown 1>(
    model=deployment_name,
    prompt="A video of our products",
)

while video.status not in ["completed", "failed", "cancelled"]:
    time.sleep(20)
    video = client.videos.<Dropdown 2>(video.id)
    print(video.status)
```

| Dropdown | Correct Method |
| :--- | :--- |
| **Dropdown 1 (`client.videos.<Dropdown 1>`)** | **`create`** |
| **Dropdown 2 (`client.videos.<Dropdown 2>`)** | **`retrieve`** |

> **Why:** Video generation with the OpenAI SDK is asynchronous: `client.videos.create(...)` submits the video generation job, and `client.videos.retrieve(video.id)` polls the job status until it reaches `"completed"`.

---

### Question 59 (Case Study 2/7)
You need to recommend a solution to assess the responses generated by `Agent1` when the agent uses the product information stored in `storage1`. The solution must meet the technical requirements (verifying that responses are grounded, complete, and accurate).

What should you include in the recommendation?

- **A.** a custom guardrail
- **B.** a Retrieval Augmented Generation (RAG) evaluator
- **C.** model fine-tuning
- **D.** a coherence evaluator

**Correct answer:** B

> **Why:** A **Retrieval Augmented Generation (RAG) evaluator** in Microsoft Foundry measures retrieval quality, groundedness, completeness, and relevance of `Agent1`'s responses against the retrieved product documents from `storage1`.

---

### Question 60 (Case Study 3/7)
You need to configure an indexing pipeline for `Agent1` to retrieve the relevant product information in `storage1`. The solution must meet the technical requirements (semantic and vector search over PDF product sheets).

Which two built-in skills should you use? Each correct answer presents part of the solution.

- **A.** Entity Recognition
- **B.** Language Detection
- **C.** Key Phrase Extraction
- **D.** Text Split
- **E.** Azure OpenAI Embedding
- **F.** Merge

**Correct answers:** D, E

> **Why:** Building a vector search index over PDF documents in Azure AI Search requires **(D) the `Text Split` skill** to chunk documents into manageable passages and **(E) the `Azure OpenAI Embedding` skill** to generate vector embeddings for each chunk.

---

### Question 61 (Case Study 4/7)
You need to configure `Agent1` to answer customer questions about only the Contoso products. The solution must meet the business requirements.

What should you do?

- **A.** Apply top-p sampling.
- **B.** Add few-shot examples.
- **C.** Modify the system message instructions.
- **D.** Increase the value of the temperature parameter.

**Correct answer:** C

> **Why:** Modifying the **system message instructions** defines the agent's scope, persona, and topic boundaries (instructing `Agent1` to answer questions strictly about Contoso products and politely decline off-topic queries).

---

### Question 62 (Case Study 5/7)
You need to configure the model deployment for `Agent1` to meet the technical requirements:
- Support generative AI workloads and burst traffic without requiring reserved capacity.
- Ensure the model version used by `Agent1` produces consistent responses over time.

What should you configure?

| Setting | Available Options | Selected Option |
| :--- | :--- | :--- |
| **Deployment type** | `Standard`, **`Global Standard`**, `Global Provisioned` | **`Global Standard`** |
| **Version update policy** | `Once the current version expires`, **`Opt out of automatic model version upgrades`**, `Upgrade once a new default version becomes available` | **`Opt out of automatic model version upgrades`** *(or `Once the current version expires`)* |

> **Why:**
> - **Global Standard** provides high-throughput pay-per-token routing across global capacity for variable/burst traffic without purchasing reserved Provisioned Throughput Units (PTUs).
> - **Opting out of automatic model version upgrades** (pinning the model version until expiry) prevents silent model version changes from altering `Agent1`'s response behavior.

---

### Question 63 (Case Study 6/7)
You need to recommend a solution to support the planned changes and technical requirements for `Agent1` to use the product information stored in `storage1` (supporting both semantic and vector search).

What should you include in the recommendation?

- **A.** Grounding with Bing Search
- **B.** Azure AI Search
- **C.** Azure Document Intelligence in Foundry Tools
- **D.** Azure Translator in Foundry Tools

**Correct answer:** B

> **Why:** **Azure AI Search** is the knowledge retrieval engine that indexes content from `storage1` and provides hybrid **semantic and vector search** integration with Microsoft Foundry agents.

---

### Question 64 (Case Study 7/7)
You need to recommend an invoice review solution that resolves the issue reported by the finance department. The solution must support multimodal understanding of textual and visual document content.

What should you include in the recommendation?

- **A.** Azure Document Intelligence in Foundry Tools
- **B.** Azure Content Understanding in Foundry Tools
- **C.** chat completions
- **D.** Image Analysis

**Correct answer:** B

> **Why:** **Azure Content Understanding in Foundry Tools** provides multimodal document analysis combining OCR, visual layout/figure comprehension, and generative reasoning for complex invoices and contracts.
