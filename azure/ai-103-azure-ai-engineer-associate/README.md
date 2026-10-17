# AI-103 / AI-102: Microsoft Azure AI Engineer Associate — Practice Question Bank

[![Azure](https://img.shields.io/badge/Microsoft_Azure-0089D6?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/)
[![Exam](https://img.shields.io/badge/Exam-AI--103%20%2F%20AI--102-blue?style=for-the-badge)](#table-of-contents)
[![Questions](https://img.shields.io/badge/Questions-64%20Verified%20Questions-success?style=for-the-badge)](#table-of-contents)
[![Cheat Sheet](https://img.shields.io/badge/Study_Guide-Cheat_Sheet-orange?style=for-the-badge)](./CHEAT_SHEET.md)

Complete, cleaned, and verified Practice Question Bank for the **Microsoft Certified: Azure AI Engineer Associate (AI-103 / AI-102)** exam. Covers Microsoft Foundry Agent Service, multi-agent orchestration workflows, Azure OpenAI & multimodal models, AI safety & evaluations, Azure Content Understanding, Azure AI Search (RAG), Computer Vision, NLP, and Speech services.

> ⚡ **Quick Review:** Check out the [**AI-103 / AI-102 Exam Cheat Sheet**](./CHEAT_SHEET.md) for a high-yield summary of Azure OpenAI, RAG, Agent Framework, Vision, Speech, and Document Intelligence before testing yourself below.

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **A** is correct because a multi-service **Microsoft Foundry service** (Azure AI Services) resource bundles multiple Foundry Tools APIs (including Speech, Language, Vision, and Translation) under a single unified endpoint and API key/credential. **B** is wrong because Content Safety only provides content moderation and prompt shield capabilities, not Speech or Language APIs. **C** and **D** are wrong because they are single-service resources that expose only Speech or only Language respectively, requiring separate endpoints and credentials.

</details>

---

### Question 2
You are building a web app named `App1` by using the Azure OpenAI SDK. You need to configure `App1` to connect to an Azure OpenAI resource named `AI1` and generate completions.

What information must you provide?

- **A.** the endpoint, key, and model name
- **B.** the endpoint, key, and model type
- **C.** the deployment name, key, and model name
- **D.** the deployment name, endpoint, and key

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** **D** is correct because connecting to an Azure OpenAI resource via the SDK requires the **resource endpoint**, the **authentication key** (or Microsoft Entra token), and the specific **deployment name** created in that resource. **A** and **B** are wrong because Azure OpenAI inference calls target a specific **deployment name** rather than a generic base `model name` or `model type`. **C** is wrong because it omits the **endpoint** URL needed to locate the `AI1` resource.

</details>

---

### Question 3
You have a Microsoft Foundry project for a support ticket triage app that reads ticket text from a database. You need to ensure that the app meets the following requirements:
- Compares candidate models by quality, cost, and throughput
- Prevents hosting model weights in the Azure subscription

What should you configure? To answer, select the appropriate options in the answer area.

| Configuration Area | Available Options |
| :--- | :--- |
| **Model evaluation** | • Configure private endpoint access<br>• Use deployment lists and license tabs<br>• Use tool catalog connections and run traces<br>• Use model catalog leaderboards and metrics |
| **Deployment option** | • Bring your own model<br>• Build a vector index<br>• Use a serverless deployment<br>• Use a managed compute deployment |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** **Model evaluation:** Use model catalog leaderboards and metrics | **Deployment option:** Use a serverless deployment

> **Why:**
> - **Model evaluation:** **Use model catalog leaderboards and metrics** is correct because it allows side-by-side comparison of candidate foundation models across quality benchmarks, cost, and throughput/latency. *Configure private endpoint access* is for network isolation; *Use deployment lists and license tabs* only shows existing deployments and licensing terms; and *Use tool catalog connections and run traces* is for runtime agent debugging rather than pre-deployment model comparison.
> - **Deployment option:** **Use a serverless deployment** (Models-as-a-Service / Standard pay-per-token APIs) is correct because it exposes models via Microsoft-managed endpoints without hosting model weights on dedicated compute VMs inside your Azure subscription. *Use a managed compute deployment* and *Bring your own model* are wrong because they host model weights on compute instances in your subscription, and *Build a vector index* is used for RAG data retrieval rather than model hosting.

</details>

---

### Question 4
You are building a solution in Azure that will use the Azure Language in Foundry Tools service to process sensitive customer data. You need to ensure that only specific Azure processes on a subnet can access the Language service. The solution must minimize administrative effort.

What should you include in the solution?

- **A.** virtual network rules
- **B.** Azure Application Gateway
- **C.** a virtual network gateway
- **D.** IPsec rules

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **A** is correct because configuring **virtual network rules** (with Virtual Network service endpoints) on the Azure AI / Language resource restricts access directly to specific VNet subnets with minimal administrative overhead. **B** (`Azure Application Gateway`) is a Layer-7 web traffic load balancer/WAF that adds unnecessary cost and configuration complexity. **C** (`a virtual network gateway`) is used for site-to-site or ExpressRoute hybrid connectivity, and **D** (`IPsec rules`) secures host-to-host IP traffic rather than restricting access to an Azure PaaS endpoint by subnet.

</details>

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B, D

> **Why:** **B** and **D** are correct because securing an Azure AI / Foundry resource to specific VNet resources requires enabling the `Microsoft.CognitiveServices` **service endpoint** on the subnet in `VNet1` (**D**) and modifying the **virtual network/firewall settings** in `CSAccount1` to disable public network access and allow only the selected virtual network subnet (**B**). **A** is wrong because `CSAccount1` is already connected to `VNet1` and creating a new subnet alone does not block external access. **C** is wrong because VNet-level settings do not restrict public access to `CSAccount1`. **E** is wrong because Access control (IAM) manages identity role assignments (RBAC), not network-level access restrictions.

</details>

---

### Question 6
You have a Microsoft Foundry project that contains an agent. The agent currently uses a stored access key to retrieve secrets from an Azure key vault, which violates a keyless credentials requirement.

You need to ensure that the agent can retrieve the secrets. The solution must follow the principle of least privilege.

What should you configure? To answer, select the appropriate options in the answer area.

| Configuration | Available Options |
| :--- | :--- |
| **Managed identity scope** | • Assign a system-assigned managed identity to the agent / project<br>• Create a service principal with a client secret<br>• Store a Key Vault access key in environment variables |
| **Key Vault authorization method** | • Assign the Key Vault Secrets User role to the managed identity<br>• Assign the Key Vault Administrator role to the managed identity<br>• Assign the Key Vault Secrets Officer role to the managed identity |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** **Managed identity scope:** Assign a system-assigned managed identity to the agent / project | **Key Vault authorization method:** Assign the Key Vault Secrets User role to the managed identity

> **Why:**
> - **Managed identity scope:** **Assign a system-assigned managed identity to the agent / project** is correct because it eliminates stored keys or secrets and satisfies the keyless authentication requirement. *Creating a service principal with a client secret* or *storing a Key Vault access key in environment variables* still relies on static secret credentials.
> - **Key Vault authorization method:** **Assign the Key Vault Secrets User role** is correct because it follows the principle of least privilege by granting read-only access to secret contents. *Key Vault Administrator* and *Key Vault Secrets Officer* are wrong because they grant unnecessary permissions to create, modify, or delete secrets and manage vault access policies.

</details>

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

| Dropdown | Available Options |
| :--- | :--- |
| **Dropdown 1 (`category`)** | `'AzureAIService'`, `'AzureKeyVault'`, `'AzureOpenAI'` |
| **Dropdown 2 (`authType`)** | `'AccountKey'`, `'AccountManagedIdentity'`, `'ApiKey'` |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** **Dropdown 1 (`category`):** `'AzureKeyVault'` | **Dropdown 2 (`authType`):** `'AccountManagedIdentity'`

> **Why:**
> - **Dropdown 1 (`category`):** **`'AzureKeyVault'`** is correct because the connection targets an Azure Key Vault resource (`KV1`). `'AzureAIService'` and `'AzureOpenAI'` are wrong because they are used for connecting AI model endpoints rather than Key Vaults.
> - **Dropdown 2 (`authType`):** **`'AccountManagedIdentity'`** is correct because the scenario requires keyless, identity-based authentication. `'AccountKey'` and `'ApiKey'` are wrong because they authenticate using static keys rather than a managed identity.

</details>

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **C** is correct because configuring a centralized **Azure AI Search connection** (with managed identity / keyless authentication) inside `Project1` allows all client applications to reference the shared project connection without duplicating search configurations or managing per-app credentials. **A** is wrong because manually configuring endpoints per application via a custom HTTP connection increases administrative effort and does not use the native keyless AI Search integration. **B** and **D** are wrong because calling Azure AI Search directly from each client application forces every app to duplicate the search configuration and manage its own RBAC assignments.

</details>

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:**
1. **Pull an image from the Microsoft Container Registry (MCR).**
2. **Provision an on-premises Kubernetes cluster that has internet connectivity.**
3. **Run the container and specify an API key and the Endpoint URL of the Azure AI resource.**

> **Why:**
> 1. **Pull an image from the Microsoft Container Registry (MCR):** Official Azure AI containers are distributed via MCR (`mcr.microsoft.com`), whereas *Pull an image from Docker Hub* is wrong because Microsoft no longer hosts current Azure AI container images on Docker Hub.
> 2. **Provision an on-premises Kubernetes cluster that has internet connectivity:** Running on-premises keeps confidential document payloads local, while internet connectivity is required to report billing usage to Azure. *Provision an AKS resource* is wrong because it processes documents in the cloud, and *an on-premises cluster isolated from the internet* is wrong because standard Azure AI containers cannot start or run without outbound connectivity to the Azure billing endpoint.
> 3. **Run the container and specify an API key and the Endpoint URL:** Azure AI containers require `Eula=accept`, `Billing={ENDPOINT_URI}`, and `ApiKey={API_KEY}` to authenticate billing telemetry, whereas *specifying an App ID and Client Secret* alone omits the mandatory billing endpoint URL.

</details>

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

| Statement | Options |
| :--- | :---: |
| 1. Going to `http://localhost:5000/status` will query the Azure endpoint to verify whether the API key used to start the container is valid. | Yes / No |
| 2. The container logging provider will write log data. | Yes / No |
| 3. Going to `http://localhost:5000/swagger` will provide the details to access the documentation for the available endpoints. | Yes / No |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** Statement 1: **No**, Statement 2: **Yes**, Statement 3: **Yes**

> **Why:**
> - **Statement 1 (No):** `http://localhost:5000/status` only reports whether the local container HTTP service is running; it does not query the Azure billing endpoint to verify whether the API key is valid (whereas `/ready` or an actual API request checks readiness/billing validation).
> - **Statement 2 (Yes):** Running the container in interactive mode outputs operational and diagnostic logs through the standard Docker container logging provider.
> - **Statement 3 (Yes):** Navigating to `http://localhost:5000/swagger` renders the interactive OpenAPI/Swagger UI documenting all available local container endpoints.

</details>

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** **D** is correct because **embeddings** models (such as `text-embedding-3-small`, `text-embedding-3-large`, or `text-embedding-ada-002`) convert text into high-dimensional floating-point vectors designed for semantic similarity comparison and vector search. **A** (`DALL-E`) is wrong because it generates images from text prompts. **B** (`GPT-3.5`) and **C** (`GPT-4`) are wrong because they are generative chat/text completion models that return text tokens rather than numeric vector representations.

</details>

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

| Dropdown | Available Options |
| :--- | :--- |
| **Dropdown 1 (`temperature`)** | `0`, `0.7`, `1.0` |
| **Dropdown 2 (`effort`)** | `"high"`, `"low"`, `"medium"` |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** **Dropdown 1 (`temperature`):** `0` | **Dropdown 2 (`effort`):** `"high"`

> **Why:**
> - **Dropdown 1 (`temperature`):** **`0`** is correct because it uses greedy/deterministic token selection to eliminate random wording variations across runs. `0.7` and `1.0` are wrong because higher temperatures increase sampling randomness and cause validation mismatches.
> - **Dropdown 2 (`effort`):** **`"high"`** is correct because it allocates maximum reasoning compute to maximize reasoning quality. `"low"` and `"medium"` are wrong because they trade off reasoning depth for lower latency and token cost.

</details>

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **A** is correct because multimodal chat models require the `content` field of the user message to be a structured JSON array containing typed content parts: `{"type": "text", "text": "..."}` and `{"type": "image_url", "image_url": {"url": "..."}}`. **B** is wrong because pasting a base64 string inside a plain text `content` string is still parsed as raw text rather than an image object (base64 images must still be passed as a data URI inside a `type: image_url` array item). **C** is wrong because user-supplied images must be sent in the `user` role message array rather than the `system` message. **D** is wrong because request `metadata` is only used for logging/filtering and is ignored by the vision processor.

</details>

---

### Question 14
You have a Microsoft Foundry Agent Service agent that uses a compatible orchestrator model. You need to configure the image generation tool so the agent can create images from text prompts during conversations.

Which model deployment must be available in the same Foundry project?

- **A.** `gpt-image-1`
- **B.** `gpt-4.1-mini`
- **C.** FLUX series image generation model
- **D.** `gpt-4o-mini`

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **A** is correct because the built-in image generation tool in Microsoft Foundry Agent Service requires an Azure OpenAI image generation deployment such as **`gpt-image-1`** (or `gpt-image-1.5`) in the same Foundry project. **B** (`gpt-4.1-mini`) and **D** (`gpt-4o-mini`) are wrong because they are chat/vision-input models that generate text responses rather than serving as the dedicated image generation model deployment. **C** (`FLUX series`) is wrong because the built-in Foundry Agent image generation tool specifically integrates with Azure OpenAI `gpt-image-*` models rather than third-party FLUX catalog deployments.

</details>

---

### Question 15
You have a Python application that calls a `gpt-image-1.5` deployment in Azure OpenAI by using the Image REST API. The application stores an existing product image as `Image1.png` and a valid mask as `Mask1.png`.

You need to send a POST request that replaces only the masked area of `Image1.png` with a new product label.

Which endpoint and request body should you use?

- **A.** `/openai/deployments/{deployment}/images/edits` with `image` and `prompt` as multipart form data
- **B.** `/openai/deployments/{deployment}/images/generations` with `prompt` and `image` as multipart form data
- **C.** `/openai/deployments/{deployment}/images/edits` with `image`, `mask`, and `prompt` as multipart form data
- **D.** `/openai/deployments/{deployment}/images/generations` with `prompt`, `mask`, and `size` in the JSON body

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **C** is correct because inpainting (replacing only a masked region of an existing image) uses the **`/openai/deployments/{deployment}/images/edits`** endpoint with `multipart/form-data` containing the source `image`, the `mask` image (`Mask1.png`), and the text `prompt`. **A** is wrong because omitting `mask` modifies the entire image rather than restricting edits to the masked area. **B** and **D** are wrong because `/images/generations` creates new images from scratch from a JSON text prompt and does not accept an input `image` or `mask` for editing.

</details>

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** **D** is correct because for browser and client-side voice applications using the GPT Realtime API, **WebRTC** is the recommended protocol, providing dedicated UDP audio media tracks, built-in jitter/packet-loss handling, and ultra-low latency (~100 ms). **A** (`WebSocket`) is wrong because WebSockets are designed primarily for server-to-server integrations over TCP and have higher latency for direct browser audio streaming. **B** (`RTMP`) is wrong because it is a legacy media streaming protocol not supported by the Azure OpenAI Realtime API. **C** (`SIP`) is wrong because SIP is a telephony signaling protocol for phone networks rather than a web app client streaming protocol.

</details>

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

| Statement | Options |
| :--- | :---: |
| 1. The response will contain an explanation of large language models (LLMs) that has a high degree of certainty. | Yes / No |
| 2. Changing `"What is an LLM?"` to `"What is an LLM in the context of AI models?"` will produce the intended response. | Yes / No |
| 3. Changing `"You are a helpful assistant."` to `"You must answer only within the context of AI language models."` will give a higher likelihood of producing the intended response. | Yes / No |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** Statement 1: **No**, Statement 2: **Yes**, Statement 3: **Yes**

> **Why:**
> - **Statement 1 (No):** Asking `"What is an LLM?"` with zero domain context (`"You are a helpful assistant."`) is ambiguous because `LLM` can refer to either a *Large Language Model* (AI) or a *Master of Laws (LL.M.)* (legal degree). Therefore, a response specifically about AI large language models does not have high certainty unless additional context (Statement 2) or grounding/system instructions (Statement 3) are provided.
> - **Statement 2 (Yes):** Adding `"in the context of AI models"` to the user prompt explicitly disambiguates the acronym and ensures the model defines large language models.
> - **Statement 3 (Yes):** Constraining the system prompt to `"You must answer only within the context of AI language models."` grounds the assistant's domain scope and significantly increases the likelihood of returning the intended AI definition.

</details>

---

### Question 18
You have a Microsoft Foundry project that contains an agent. The agent generates summaries from retrieved policy documents.

You need to improve response completeness. The solution must be implemented in the logic of the application code before responses are returned.

What should you do?

- **A.** Add a retry evaluation before the responses are returned.
- **B.** Replace the model with a smaller deployment.
- **C.** Decrease the value of the `max_tokens` parameter.
- **D.** Increase the value of the `presence_penalty` parameter.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **A** is correct because implementing a **retry evaluation loop** in application code evaluates the generated summary for completeness before returning it to the user and automatically re-prompts the agent when required policy details are missing. **B** is wrong because replacing the model with a smaller deployment reduces reasoning capability and typically increases omissions. **C** is wrong because decreasing `max_tokens` shortens the maximum allowed output length, truncating responses and reducing completeness. **D** is wrong because increasing `presence_penalty` penalizes repeating tokens that have already appeared, which does not verify or enforce summary completeness.

</details>

---

### Question 19
> **Scenario Set (Questions 19–21):** Each question presents a unique solution to the same scenario. Determine whether the solution meets the stated goals.

You have a Microsoft Foundry project that contains an agent. The agent generates summaries from retrieved policy documents. Users report that some responses omit required regulatory clauses, even when the clauses are present in the retrieved content.

You need to improve response completeness.

**Solution:** You run an evaluation flow that scores responses for completeness and blocks responses that fall below a defined threshold.

Does this meet the goal?

- **A.** Yes
- **B.** No

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **B** (`No`) is correct because simply blocking responses below a threshold prevents incomplete outputs from being returned (resulting in blocked/failed requests), but it does **not** improve the completeness of the generated summaries themselves. **A** (`Yes`) is wrong because improving completeness requires refining the prompt instructions or adding a retry-with-feedback loop rather than merely blocking output.

</details>

---

### Question 20
You have a Microsoft Foundry project that contains an agent. The agent generates summaries from retrieved policy documents. Users report that some responses omit required regulatory clauses, even when the clauses are present in the retrieved content.

You need to improve response completeness.

**Solution:** You increase the value of the `temperature` parameter.

Does this meet the goal?

- **A.** Yes
- **B.** No

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **B** (`No`) is correct because increasing `temperature` increases token sampling randomness/creativity, which reduces factual adherence and makes the model more likely to drift or omit required regulatory clauses. **A** (`Yes`) is wrong because `temperature` controls output randomness, not structural completeness.

</details>

---

### Question 21
You have a Microsoft Foundry project that contains an agent. The agent generates summaries from retrieved policy documents. Users report that some responses omit required regulatory clauses, even when the clauses are present in the retrieved content.

You need to improve response completeness.

**Solution:** You increase the value of the `top_p` parameter.

Does this meet the goal?

- **A.** Yes
- **B.** No

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **B** (`No`) is correct because increasing `top_p` (nucleus sampling) widens the pool of candidate tokens considered during generation, which increases wording variability rather than ensuring required regulatory clauses are included. **A** (`Yes`) is wrong because adjusting `top_p` does not enforce domain completeness.

</details>

---

## Domain 3: Design and Implement AI Agents & Multi-Agent Workflows

### Question 22
A multi-agent customer support solution built using the Microsoft Foundry Agent Service features a triage agent, a billing agent, and a technical agent. The triage agent evaluates the customer query and transfers control directly to the appropriate specialist. Each specialist can handle the conversation and pass it back or onward if the topic shifts. No central orchestrator or planner agent coordinates the steps.

Which agent orchestration pattern should you use?

- **A.** Sequential
- **B.** Concurrent
- **C.** Handoff
- **D.** Magentic

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **C** is correct because in the **Handoff** orchestration pattern, agents dynamically delegate and transfer execution control directly to specialist peers based on conversation context without relying on a central planner/orchestrator. **A** (`Sequential`) is wrong because it chains agents in a fixed linear pipeline regardless of topic shifts. **B** (`Concurrent`) is wrong because it runs multiple agents simultaneously in parallel on the same input rather than transferring conversation ownership between specialists. **D** (`Magentic`) is wrong because it uses a central manager agent to build and coordinate a dynamic task ledger.

</details>

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **A** is correct because Microsoft Foundry **workflows** declaratively define deterministic, step-based multi-agent pipelines with shared state and conditional branching without writing custom orchestration code. **B** (`a multi-agent group chat session`) is wrong because group chat relies on open-ended conversational turn-taking rather than deterministic step-by-step branching. **C** (`threads and runs without a workflow`) is wrong because standalone threads and runs operate on a single agent without built-in multi-agent state sharing or conditional branching. **D** (`separate agent runs coordinated in the application code`) is wrong because manually coding state management and branching logic in the client application does not minimize development effort.

</details>

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

| Dropdown | Available Options |
| :--- | :--- |
| **Dropdown 1 (`type`)** | `ask_question`, `basic_chat`, `data_transformation` |
| **Dropdown 2 (`condition`)** | `approval.output == 'approved'`, `propose_refund.output != null`, `always` |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** **Dropdown 1 (`type`):** `ask_question` | **Dropdown 2 (`condition`):** `approval.output == 'approved'`

> **Why:**
> - **Dropdown 1 (`type`):** **`ask_question`** is correct because in Foundry declarative YAML workflows, the `ask_question` step pauses execution to wait for human input/approval. `basic_chat` is wrong because it invokes an LLM completion without pausing for human approval, and `data_transformation` is wrong because it only transforms existing state variables.
> - **Dropdown 2 (`condition`):** **`approval.output == 'approved'`** is correct because it gates the `execute_refund` step on the human approver's decision. `propose_refund.output != null` and `always` are wrong because they would execute the refund regardless of whether human approval was granted.

</details>

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** **D** is correct because an OpenAPI tool in Microsoft Foundry only injects stored credentials into outgoing HTTP requests when the tool is explicitly **linked/connected to the project connection (`Connection1`)**. **A** is wrong because hardcoding the API key value directly inside the OpenAPI spec exposes credentials in plain text instead of retrieving them from `Connection1`. **B** is wrong because the external API authenticates via an API key stored in `Connection1`, not a Microsoft Entra bearer token. **C** is wrong because OpenAPI tools require explicit binding to the target custom connection ID rather than a generic project default connection.

</details>

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **A** is correct because in an OpenAPI 3.0 specification, defining an **API key security scheme** (`type: apiKey`, `in: header`, `name: <Header-Name>`) under `components.securitySchemes` tells Foundry which HTTP header to populate with the key from the linked project connection. **B** (`a Bearer token security scheme`) is wrong because it formats the credential as `Authorization: Bearer <token>` rather than populating the custom API key header expected by the weather service. **C** (`a header parameter defined for each operation`) is wrong because operation parameters are expected to be supplied by the model at runtime rather than injected from the project connection. **D** (`an Azure Key Vault connection`) is wrong because Azure connections are configured in the Foundry resource/project, not inside an OpenAPI 3.0 specification document.

</details>

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** **D** is correct because passing the **`tool_choice`** parameter (set to `"required"` or specifying the `kbsearch` tool explicitly) in `create_and_process()` forces the agent to invoke the tool rather than relying on the model's default `"auto"` decision. **A** (`toolset`) is wrong because it only registers which tools are available to the run without forcing invocation. **B** (`create_thread_and_process_run()`) is wrong because it merely combines thread creation and run execution into one call while still defaulting to optional (`"auto"`) tool usage. **C** (`response_format`) is wrong because it controls output formatting (such as JSON schema), not tool invocation behavior.

</details>

---

### Question 28
You have a Microsoft Foundry project that contains an agent. The agent uses tools to retrieve internal content and call external APIs. The agent is currently configured to let the model decide when to call the tools.

You need to publish the agent for a compliance workflow. The solution must meet the following requirements:
- Each workflow run must include a retrieval step before generating a response.
- Tool calls must authenticate by using the published agent's own identity.
- Tool access must use an identity isolated from other project resources.
- Tool access must support audit tracing.

What should you do? To answer, select the appropriate options in the answer area.

| Configuration | Available Options |
| :--- | :--- |
| **Set tool choice to** | • `auto`<br>• `none`<br>• `required` |
| **Configure the tool to authenticate by** | • Storing API keys in prompts<br>• Using the shared project agent<br>• Using a distinct agent identity |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** **Set tool choice to:** `required` | **Configure the tool to authenticate by:** Using a distinct agent identity

> **Why:**
> - **Set tool choice to:** **`required`** is correct because it guarantees that the agent executes a tool call (the mandatory retrieval step) before generating a final response. `auto` is wrong because the model can choose to skip tool invocation, and `none` is wrong because it prevents the agent from calling any tools.
> - **Configure the tool to authenticate by:** **Using a distinct agent identity** is correct because a published agent gets its own dedicated managed identity isolated from other project resources, enabling least-privilege access and per-agent audit tracing. *Using the shared project agent* identity violates the isolation requirement, and *Storing API keys in prompts* is insecure and does not use identity-based authentication.

</details>

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** **D** is correct because streaming **real-time speech-to-text (STT)** provides continuous partial transcripts for low-latency turn-taking, while streaming **text-to-speech (TTS)** synthesizes spoken agent responses immediately as tokens are generated. **A** is wrong because embeddings models convert inputs into numeric vectors for similarity search and cannot transcribe or synthesize speech. **B** is wrong because batch transcription processes pre-recorded audio files asynchronously (high latency) and returns text rather than spoken audio. **C** is wrong because speech translation converts speech from one language to another rather than transcribing audio for same-language agent reasoning and speech synthesis.

</details>

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **A** is correct because **Prompt Shields** in Azure AI Content Safety detect both direct user jailbreaks and **indirect prompt injection attacks** hidden in external documents or OCR text extracted from images before the model acts on them. **B** (`Groundedness detection`) is wrong because it checks whether generated model outputs are faithful to source documents after generation, not whether input text contains malicious instructions. **C** (`Protected material detection`) is wrong because it scans model outputs for copyrighted text or code. **D** (`Image moderation`) is wrong because it evaluates visual harm categories (Hate, Violence, Sexual, Self-Harm) rather than adversarial text instructions extracted via OCR.

</details>

---

### Question 31
You have an app named `App1` that uses a Microsoft Foundry multimodal model deployment. `App1` runs optical character recognition (OCR) on uploaded images and appends the OCR output to the prompt as additional context.

Some uploaded images contain embedded text. You need to prevent potentially malicious instructions in that extracted text from being processed by the model.

What should you use?

- **A.** prompt shields for documents
- **B.** image moderation
- **C.** protected material text
- **D.** prompt shields for user prompts

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **A** is correct because the OCR output is appended as external/third-party context rather than typed directly as the user prompt, making it an indirect prompt injection vector that is scanned by **prompt shields for documents** (Document Attack Detection). **B** (`image moderation`) is wrong because it classifies visual harm severity (Hate, Violence, Sexual, Self-Harm) in images rather than adversarial text commands. **C** (`protected material text`) is wrong because it detects copyrighted text in model outputs. **D** (`prompt shields for user prompts`) is wrong because it scans direct user jailbreak inputs (`userPrompt`) rather than untrusted third-party document/OCR context (`documents`).

</details>

---

### Question 32
You have a Microsoft Foundry project that contains an agent. The agent accepts user-uploaded screenshots and uses a multimodal chat model. Some screenshots contain potentially malicious embedded text.

You need to prevent a prompt injection attack and ensure that third-party content is treated as lower trust.

How should you configure prompt shields for document attacks?

| Configuration | Available Options |
| :--- | :--- |
| **Prompt shields action** | • Annotate only<br>• Annotate and block<br>• Disable |
| **Additional mitigation** | • Use spotlighting<br>• Increase temperature<br>• Enable protected material detection |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** **Prompt shields action:** Annotate and block | **Additional mitigation:** Use spotlighting

> **Why:**
> - **Prompt shields action:** **Annotate and block** is correct because it actively blocks requests when an indirect prompt injection attack is detected in untrusted document/image inputs. *Annotate only* and *Disable* are wrong because they allow malicious prompt injections to proceed to the model without blocking them.
> - **Additional mitigation:** **Use spotlighting** is correct because it marks untrusted third-party inputs with special delimiters/encodings so the LLM distinguishes lower-trust external data from trusted system instructions. *Increase temperature* and *Enable protected material detection* are wrong because they affect sampling randomness and copyright detection, not input trust isolation.

</details>

---

### Question 33
You are deploying a support agent that enables users to upload photos. You need to automatically classify uploaded images for harmful content (Hate, Violence, Self-Harm, Sexual). The solution must block content based on severity levels.

What should you do?

- **A.** Enable prompt shields.
- **B.** Apply keyword scanning to optical character recognition (OCR) output by using Azure Vision in Foundry Tools.
- **C.** Implement image moderation.
- **D.** Use blocklists.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **C** is correct because **image moderation** in Azure AI Content Safety analyzes uploaded images across the four harm categories (Hate, Violence, Sexual, Self-Harm) and assigns severity scores (`0–6`) that can be blocked by threshold. **A** (`Enable prompt shields`) is wrong because Prompt Shields detect text-based jailbreak and prompt injection attacks, not harmful visual imagery. **B** (keyword scanning on OCR output) and **D** (`Use blocklists`) are wrong because they only match text strings/keywords and cannot detect harmful visual content in photos that contain no text.

</details>

---

### Question 34
You have a Microsoft Foundry project that contains a Retrieval Augmented Generation (RAG) solution. You need to run a pre-production evaluation by using a labeled CSV dataset that contains the `query`, `context`, `response`, and `ground_truth`.

The evaluation must measure the following:
- Whether responses address the user query
- Whether responses are supported by the provided context
- Whether responses contain sensitive or proprietary information

Which AI quality evaluation metrics should you use?

| Requirement | Available Evaluation Metrics |
| :--- | :--- |
| **To measure whether the responses are supported by the provided context and address the user query** | • Fluency and Coherence<br>• Groundedness and Relevance<br>• BLEU and ROUGE |
| **To measure whether responses contain sensitive or proprietary information** | • Content safety / Protected material detection<br>• Similarity and F1 score<br>• Retrieval score |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** **Supported by context and address query:** Groundedness and Relevance | **Sensitive or proprietary information:** Content safety / Protected material detection

> **Why:**
> - **Groundedness and Relevance:** **Groundedness** measures whether the generated response is factual with respect to the retrieved `context`, and **Relevance** measures how well the response answers the user `query`. *Fluency and Coherence* are wrong because they only evaluate linguistic readability and sentence flow, and *BLEU and ROUGE* are wrong because they measure lexical n-gram overlap against `ground_truth` rather than context groundedness.
> - **Content safety / Protected material detection:** These evaluators detect sensitive, harmful, or proprietary/copyrighted content in model outputs. *Similarity and F1 score* and *Retrieval score* are wrong because they measure answer accuracy and search context quality rather than sensitive or proprietary content leakage.

</details>

---

### Question 35
You plan to configure an evaluation in Microsoft Foundry for a Retrieval Augmented Generation (RAG) chat app. You need to provide scores for groundedness, relevance, and harmful content categories.

Which two evaluation categories should you use?

- **A.** fluency evaluator
- **B.** AI quality (NLP) metrics
- **C.** similarity evaluators
- **D.** AI quality (AI-assisted) metrics
- **E.** risk and safety metrics

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D, E

> **Why:** **D** and **E** are correct because in Microsoft Foundry, **AI quality (AI-assisted) metrics** (**D**) use an LLM judge to score **Groundedness** and **Relevance**, while **risk and safety metrics** (**E**) evaluate outputs across harmful content categories (Violence, Sexual, Self-harm, Hate and unfairness). **A** (`fluency evaluator`) is wrong because it only scores grammatical quality and readability, not groundedness, relevance, or safety. **B** (`AI quality (NLP) metrics`) is wrong because traditional NLP metrics (BLEU, ROUGE, METEOR, F1) calculate lexical overlap with reference text rather than LLM-judged groundedness/relevance or safety harms. **C** (`similarity evaluators`) is wrong because similarity only compares semantic closeness between the response and ground truth, without evaluating context groundedness or harmful content.

</details>

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B, C

> **Why:** **B** and **C** are correct because end-to-end tracing for external Python applications calling Microsoft Foundry agents is instrumented using the **OpenTelemetry** SDK (`azure-core-tracing-opentelemetry`) (**B**) and exported to **Azure Application Insights** (**C**) for visualizing distributed traces, latency spans, and exceptions. **A** (`Microsoft Sentinel`) is wrong because it is a security information and event management (SIEM) tool for threat detection, not distributed APM tracing. **D** (`a Log Analytics workspace`) is the backend log store rather than the tracing instrumentation/APM component. **E** (`the Azure Monitor Agent`) is wrong because it collects OS-level telemetry from virtual machines, not application-level SDK traces.

</details>

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **B** is correct because enabling **application tracing** in the Microsoft Foundry project (`Project1`) links Application Insights to the project and captures correlated, end-to-end distributed traces across both model calls (Responses API) and connected Foundry tools (Content Safety). **A** is wrong because Foundry Local runs local models on edge/developer hardware and does not trace cloud Foundry project workflows. **C** is wrong because logging only in the Content Safety client SDK does not capture or correlate the Azure OpenAI Responses API steps. **D** is wrong because routing requests through the Azure OpenAI endpoint alone does not enable distributed tracing across project tool connections.

</details>

---

### Question 38
You have a Microsoft Foundry project that contains a high-traffic agent. After a recent update, operational costs increase significantly. Monitoring confirms that the volume of user traffic to the agent remains unchanged.

You suspect that changes to the request or response characteristics are causing the increase. You need to identify whether the additional costs are driven by the model input size, the model output size, or expanded tool usage.

Which observability capability should you use?

- **A.** run success rate
- **B.** evaluation metrics
- **C.** latency
- **D.** token usage

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** **D** is correct because **token usage** observability breaks down prompt (input) tokens, completion (output) tokens, and tokens consumed by intermediate tool invocations, directly pinpointing the driver of increased LLM consumption costs. **A** (`run success rate`) is wrong because it tracks the ratio of successful vs. failed runs, not billing consumption. **B** (`evaluation metrics`) is wrong because it measures AI quality and safety scores rather than token counts. **C** (`latency`) is wrong because it measures execution duration rather than whether input size, output size, or tool calls drove the cost spike.

</details>

---

### Question 39
You have a Microsoft Foundry project that contains a multi-agent solution. The agents use tool calling to query internal systems.

You need to implement responsible AI auditing to meet the following requirements:
- Capture all the nested operations across the entire agent run.
- Record tool invocation arguments and returned results as metadata.

What should you use for each requirement?

**Available Options:** `Hierarchical spans`, `A KQL query filter`, `Sampling`, `Tool call attributes`, `Trace sampling policy`

| Requirement | Available Options |
| :--- | :--- |
| **Capture all the nested operations across the entire agent run** | `Hierarchical spans`, `A KQL query filter`, `Sampling`, `Tool call attributes`, `Trace sampling policy` |
| **Record tool invocation arguments and returned results as metadata** | `Hierarchical spans`, `A KQL query filter`, `Sampling`, `Tool call attributes`, `Trace sampling policy` |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** **Capture all nested operations:** Hierarchical spans | **Record tool invocation arguments and results:** Tool call attributes

> **Why:**
> - **Hierarchical spans** is correct because OpenTelemetry parent-child spans represent all nested operations across an entire multi-agent run (orchestrator -> sub-agent -> model call -> tool execution).
> - **Tool call attributes** is correct because span attributes attach structured key-value metadata (function name, input arguments, and returned output payload) to the tool execution span.
> - **Why the other options are wrong:** *Sampling* and *Trace sampling policy* drop a percentage of traces to reduce ingestion volume (which violates the requirement to capture *all* nested operations for auditing), and *A KQL query filter* queries already-collected logs rather than recording spans or metadata during execution.

</details>

---

## Domain 5: Document Intelligence, Content Understanding & Knowledge Mining

### Question 40
You have a set of scanned files. You need to extract text from the files and perform sentiment analysis.

Which service should you use for each task?

| Task | Available Options |
| :--- | :--- |
| **Extract text** | `Azure AI Search`, `Azure Vision in Foundry Tools`, `Azure Document Intelligence` |
| **Perform sentiment analysis** | `Azure AI Search`, `Azure AI Computer Vision`, `Azure Language in Foundry Tools` |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** **Extract text:** Azure Document Intelligence | **Perform sentiment analysis:** Azure Language in Foundry Tools

> **Why:**
> - **Extract text:** **Azure Document Intelligence** is correct because it is purpose-built to extract text, layout, and structure from scanned documents using OCR. *Azure AI Search* is a search indexing engine rather than a standalone document OCR service, and *Azure Vision in Foundry Tools* is tuned for general images rather than multi-page scanned document files.
> - **Perform sentiment analysis:** **Azure Language in Foundry Tools** is correct because it provides prebuilt Sentiment Analysis and opinion mining on text. *Azure AI Search* and *Azure AI Computer Vision* do not provide standalone NLP sentiment classification APIs.

</details>

---

### Question 41
You have a Microsoft Foundry project that processes procurement documents submitted by suppliers. You need to implement two pipelines by using Azure Content Understanding in Foundry Tools.

The solution must meet the following requirements:
- Include a pipeline named `Pipeline1` that supports cost-effective, high-volume processing of standalone PDF invoices.
- Include a pipeline named `Pipeline2` that supports cross-document validation by using multi-step reasoning and reference data.

How should you configure each pipeline?

| Pipeline | Available Configurations |
| :--- | :--- |
| **`Pipeline1`** | `Multi-file task in pro mode`, `Multi-file task in standard mode`, `Single-file task in pro mode`, `Single-file task in standard mode` |
| **`Pipeline2`** | `Multi-file task in pro mode`, `Multi-file task in standard mode`, `Single-file task in pro mode`, `Single-file task in standard mode` |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** **`Pipeline1`:** Single-file task in standard mode | **`Pipeline2`:** Multi-file task in pro mode

> **Why:**
> - **`Pipeline1` (Single-file task in standard mode):** **Standard mode** is optimized for fast, cost-effective, high-volume extraction from individual documents like standalone PDF invoices. *Pro mode* is wrong for `Pipeline1` because it adds unnecessary multi-step reasoning cost, and *Multi-file task* is wrong because each invoice is processed as a standalone file.
> - **`Pipeline2` (Multi-file task in pro mode):** **Pro mode** with a **multi-file task** uses advanced multi-step reasoning across multiple files and reference documents for cross-document validation. *Standard mode* and *Single-file tasks* are wrong for `Pipeline2` because they cannot perform multi-document reasoning across reference files.

</details>

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **A** is correct because **Azure Content Understanding in Foundry Tools** combines OCR, layout/multipage table structure analysis, and generative schema-driven field extraction across varied invoice templates without requiring custom model training. **B** (`Azure Language in Foundry Tools`) is wrong because it operates on plain text and does not perform OCR or visual document layout parsing. **C** (`an Azure Machine Learning model`) is wrong because training and managing a custom ML model violates the requirements to avoid custom model training and minimize administrative effort. **D** (`Azure Vision in Foundry Tools`) is wrong because basic image OCR extracts raw text lines without understanding multipage invoice tables or extracting schema fields.

</details>

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **A** is correct because a **custom analyzer in Azure Content Understanding** lets you define a custom field schema (`invoiceNumber`, `invoiceDate`, `vendorName`, `totalAmount`) and outputs structured JSON with per-field **confidence scores** for human-in-the-loop routing (`< 0.80`). **B** (`prebuilt-layout`) is wrong because it extracts only layout elements (text lines, tables, selection marks) without extracting domain-specific invoice fields or field confidence scores. **C** (`prebuilt-documentSearch` and `search.score`) is wrong because `search.score` measures search query relevance in Azure AI Search, not per-field extraction confidence. **D** is wrong because groundedness guardrails evaluate RAG chat responses rather than extracting structured invoice fields with per-field OCR confidence scores.

</details>

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **C** is correct because setting **`estimateFieldSourceAndConfidence`** to `true` in an Azure Content Understanding analyzer instructs the service to return both a per-field confidence score and bounding-box/page source grounding coordinates in the original PDF. **A** is wrong because enabling generative extraction alone does not return confidence scores and bounding-box source grounding unless `estimateFieldSourceAndConfidence` is enabled. **B** (`Provide labeled samples`) is wrong because few-shot examples improve accuracy but do not enable confidence and source location output fields. **D** (`Set enableSegment to true`) is wrong because segmentation splits multi-document files into logical sections rather than returning per-field confidence scores and coordinates.

</details>

---

### Question 45
You have a Microsoft Foundry project that contains an agent. You need to process mixed-format documents that contain scanned text, tables, and multicolumn layouts. The extracted content must preserve the document structure and be converted into the Markdown format for downstream reasoning.

What should you configure first?

- **A.** an Azure OpenAI Responses API call that uses a multimodal model
- **B.** an Azure Language in Foundry Tools text analysis model deployment
- **C.** an Azure Content Understanding in Foundry Tools analyzer
- **D.** a generative chat completion request

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **C** is correct because **Azure Content Understanding in Foundry Tools** analyzers natively parse complex scanned text, tables, and multicolumn layouts and convert the structured document representation directly into **Markdown** for downstream LLM/RAG reasoning. **A** (Responses API call) and **D** (chat completion request) are wrong because generative model inference calls are used for downstream reasoning over the extracted Markdown rather than serving as the primary document-to-Markdown ingestion analyzer. **B** (`Azure Language in Foundry Tools`) is wrong because it analyzes plain text and cannot perform OCR or convert multicolumn PDF layouts and tables into Markdown.

</details>

---

### Question 46
You are building an Azure AI Search indexing pipeline named `Pipeline1` that ingests invoices stored in Azure Blob Storage. The invoices are stored as scanned images.

You need to enable users to search invoice data across the invoice fields.

Which built-in skill should you add to the skillset of `Pipeline1`?

- **A.** Text Split
- **B.** Image Analysis
- **C.** Text Translation
- **D.** optical character recognition (OCR)

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D

> **Why:** **D** is correct because the built-in **Optical Character Recognition (`#Microsoft.Skills.Vision.OcrSkill`)** skill extracts printed and handwritten text from scanned image blobs during indexing so the invoice text can be indexed and searched in Azure AI Search. **A** (`Text Split`) is wrong because it splits existing text into chunks and cannot extract text from images. **B** (`Image Analysis`) is wrong because it generates visual captions, tags, and object detections rather than performing OCR on invoice text. **C** (`Text Translation`) is wrong because it translates existing text strings between languages and cannot read scanned images.

</details>

---

### Question 47
You are creating an enrichment pipeline that will use Azure AI Search. The knowledge store contains unstructured JSON data and the text/files from scanned PDF documents.

Which projection type should you use for each data type in the Azure AI Search Knowledge Store?

| Data Type | Available Projection Types |
| :--- | :--- |
| **JSON data** | `Files`, `Objects`, `Tables` |
| **Extracted text / document data** | `Files`, `Objects`, `Tables` |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** **JSON data:** Objects | **Extracted text / document data:** Files

> **Why:** In an Azure AI Search Knowledge Store:
> - **Objects** is correct for **JSON data** because Object projections serialize enriched document trees as structured JSON blobs in Azure Blob Storage.
> - **Files** is correct for **extracted document/file data** because File projections store normalized images and binary documents extracted from scanned PDFs in Azure Blob Storage.
> - **Why `Tables` is wrong here:** *Table projections* flatten enriched data into relational rows and columns in Azure Table Storage rather than storing unstructured JSON trees or extracted files.

</details>

---

### Question 48
You have a Microsoft Foundry project that contains an agent. The agent uses Azure AI Search for Retrieval Augmented Generation (RAG). You plan to ingest and index PDF product manuals.

You need to build a solution that supports semantic similarity matching. The solution must ensure that the agent retrieves relevant data when user questions use different wording than the product manuals.

Which indexing approach should you use?

- **A.** vector search
- **B.** semantic ranking
- **C.** suggesters
- **D.** analyzers

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **A** is correct because **vector search** indexes vector embeddings of document chunks and queries them by mathematical similarity in semantic space, enabling retrieval of conceptually relevant passages even when user questions share no exact keywords with the product manuals. **B** (`semantic ranking`) is wrong because the semantic ranker is a second-stage reranker that only reorders top candidates already returned by an initial query—it is not an indexing approach that retrieves documents when keyword matching fails completely. **C** (`suggesters`) is wrong because suggesters provide search-box autocomplete/type-ahead suggestions. **D** (`analyzers`) is wrong because lexical analyzers only tokenize and stem individual words for keyword matching, not cross-phrasing semantic similarity.

</details>

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **C** is correct because **Spatial Analysis** in Azure Vision processes real-time video streams (via containers) to detect person movement, count occupancy, and trigger real-time alerts when employees cross lines or enter restricted high-risk zones (`personCrossingPolygon`). **A** (`Azure AI Video Indexer`) is wrong because it performs asynchronous batch analysis of recorded media files rather than real-time spatial zone monitoring. **B** (`Image Analysis`) is wrong because it analyzes static images rather than tracking continuous person movement across live video feeds. **D** (`Object detection in Azure Custom Vision`) is wrong because it requires custom training and detects bounding boxes on individual frames without built-in real-time zone entry alerting.

</details>

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **C** is correct because **Azure AI Custom Vision** allows you to train custom image classification or object detection models using your own labeled image library (approved vs. defective products) with minimal code and development effort. **A** (`Azure Vision in Foundry Tools`) is wrong because its prebuilt models cannot be trained on your custom library of approved/rejected products. **B** (`Azure AI Video Indexer`) is wrong because it extracts general audio/video metadata (transcripts, faces, keywords) from recorded videos rather than training custom defect detectors. **D** (`Azure Machine Learning`) is wrong because building, training, and deploying a custom computer vision pipeline from scratch in Azure ML requires high development effort.

</details>

---

### Question 51
You are building a Custom Vision model. You have images of cats and dogs. Each image contains either a cat or a dog.

You need to use the Azure Custom Vision service to detect whether the image is of a cat or a dog. How should you configure the project in the Azure Custom Vision portal?

| Setting | Available Options |
| :--- | :--- |
| **Project Types** | `Classification`, `Object Detection` |
| **Classification Types** | `Multiclass (Single tag per image)`, `Multilabel (Multiple tags per image)` |
| **Domains** | `Adult`, `Food`, `General`, `General (compact)`, `Landmarks`, `Retail` |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** **Project Types:** `Classification` | **Classification Types:** `Multiclass (Single tag per image)` | **Domains:** `General`

> **Why:**
> - **Project Types (`Classification`):** Categorizing a whole image as a cat or a dog requires **Classification**, whereas *Object Detection* is wrong because you are not locating bounding boxes around multiple objects within an image.
> - **Classification Types (`Multiclass (Single tag per image)`):** Each image contains *either* a cat *or* a dog (mutually exclusive classes), whereas *Multilabel (Multiple tags per image)* is wrong because it applies when an image can have multiple tags at once.
> - **Domains (`General`):** **General** is the standard domain for cloud-based classification of everyday subjects like animals. *Adult*, *Food*, *Landmarks*, and *Retail* are wrong because they target specialized verticals, and *General (compact)* is only needed when exporting models to run offline on edge devices.

</details>

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:**
1. **Change Domains to `General (compact)`.**
2. **Retrain the model.**
3. **Export the model.**

> **Why:** Only **compact domains** (such as `General (compact)`) can be exported to edge/offline formats (ONNX, TensorFlow, CoreML, Dockerfile). When converting an existing project from `General` to `General (compact)`, you must first **change the domain to `General (compact)`** (**Step 1**), then **retrain the model** (**Step 2**) so a new iteration is built using the compact architecture, and finally **export the model** (**Step 3**). *Change the classification type* and *Create a new classification model* are wrong because the existing project is already configured and converting an existing project only requires switching to a compact domain and retraining.

</details>

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B, E

> **Why:** **B** and **E** are correct because prebuilt **Azure Vision in Foundry Tools** Image Analysis provides **image descriptions/captions** (**B**) to generate natural-language captions and **image type detection** (`ImageType`, **E**) to determine whether an image is clip art / a line drawing vs. a photograph with minimal development effort. **A** (`image classification in Azure Custom Vision`) is wrong because training a custom classifier requires collecting images and training a model when prebuilt `ImageType` detection already exists. **C** (`content tags`) is wrong because it returns individual keyword tags rather than a natural-language caption or photo-vs-drawing classification. **D** (`object detection`) is wrong because it identifies bounding boxes around objects rather than generating captions or detecting image types.

</details>

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

| Statement | Options |
| :--- | :---: |
| 1. The code will detect the language of documents. | Yes / No |
| 2. The `url` attribute returned for each linked entity will be a Bing search link. | Yes / No |
| 3. The `matches` attribute returned for each linked entity will provide the location in a document where the entity is referenced. | Yes / No |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** Statement 1: **No**, Statement 2: **No**, Statement 3: **Yes**

> **Why:**
> - **Statement 1 (No):** `recognize_linked_entities()` performs entity linking to disambiguate named entities, not language detection (language detection requires calling `detect_language()`).
> - **Statement 2 (No):** Entity linking disambiguates entities by returning a **Wikipedia URL** (e.g., `https://en.wikipedia.org/wiki/Space_Needle`) from its knowledge base, not a Bing search link.
> - **Statement 3 (Yes):** Each linked entity's `matches` collection includes `offset` and `length` properties specifying the exact character position in the document where the entity is referenced.

</details>

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **A** is correct because despite the custom function name `get_key_words`, the code calls `recognize_entities()`, which performs **Named Entity Recognition (NER)** and extracts only the named geographic/location entities **`London`** and **`Buckingham Palace`**. **B** (`Tour` and `visit` only) and **D** (`London` and `Tour` only) are wrong because general nouns like `tour` and `visit` are not named entities (they would only be part of key phrases extracted by `extract_key_phrases()`). **C** is wrong because `recognize_entities()` returns individual entity spans rather than echoing the full input sentence.

</details>

---

### Question 56
You have a Microsoft Foundry project that contains an agent. The agent uses Azure Speech in Foundry Tools. You fine-tune a baseline speech-to-text model for the `en-US` locale and publish the model.

The agent calls the Speech-to-text REST API and returns an error message indicating that the project ID is invalid. You need to set the project property to the correct ID.

To what should you set the project property?

- **A.** the custom speech endpoint URL
- **B.** the Microsoft Foundry project URL
- **C.** the custom speech project ID
- **D.** the Microsoft Foundry project ID

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **C** is correct because when referencing a Custom Speech project in Speech-to-text REST API requests, the `project` property must be set to the **Custom Speech project ID**. **A** (`the custom speech endpoint URL`) and **B** (`the Microsoft Foundry project URL`) are wrong because the `project` parameter expects a project ID string/GUID rather than an HTTPS endpoint URL. **D** (`the Microsoft Foundry project ID`) is wrong because Custom Speech uses its own dedicated project identifier rather than the parent Microsoft Foundry project ID.

</details>

---

### Question 57
You have an application named `App1` that uses Azure Speech in Foundry Tools to transcribe live calls. Transcript segments often contain both English and Spanish. `App1` sends each segment to Azure Translator in Foundry Tools to translate to another language.

Sometimes, mixed-language segments result in incomplete or incorrect translations. You need to reduce translation errors. The solution must ensure that the entire transcript is translated successfully and minimize development effort.

What should you do before sending the segments to Translator?

- **A.** Enable automatic language detection for the translation request.
- **B.** Specify English as the source language in the translation request for all the segments.
- **C.** Split the mixed-language segments into single-language segments and translate each segment separately.
- **D.** Use document translation to translate the entire transcript as a single document.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** A

> **Why:** **A** is correct because omitting the fixed `from` source language parameter enables **automatic language detection** in Azure Translator, dynamically identifying the language of each segment with minimal development effort. **B** is wrong because forcing English (`from=en`) on all segments causes Spanish segments to fail or produce garbled translations. **C** is wrong because writing custom logic to split mixed-language segments into single-language substrings requires significant development effort. **D** is wrong because Document Translation is an asynchronous batch service for whole document files in Blob Storage, not for real-time live call transcript segments.

</details>

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

| Dropdown | Available Options |
| :--- | :--- |
| **Dropdown 1 (`client.videos.<Dropdown 1>`)** | `create`, `generate`, `start` |
| **Dropdown 2 (`client.videos.<Dropdown 2>`)** | `get`, `list`, `retrieve` |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** **Dropdown 1:** `create` | **Dropdown 2:** `retrieve`

> **Why:**
> - **Dropdown 1 (`create`):** **`client.videos.create(...)`** is the standard OpenAI SDK method to submit an asynchronous video generation job. `generate` and `start` are wrong because they are not valid methods on the `client.videos` resource.
> - **Dropdown 2 (`retrieve`):** **`client.videos.retrieve(video.id)`** polls the status of the specific video job by its ID until it reaches `"completed"`. `list` is wrong because it returns a paginated collection of all video jobs rather than fetching a single job by ID, and `get` is not the OpenAI SDK method name for resource retrieval.

</details>

---

### Question 59 (Case Study 2/7)
You need to recommend a solution to assess the responses generated by `Agent1` when the agent uses the product information stored in `storage1`. The solution must meet the technical requirements (verifying that responses are grounded, complete, and accurate).

What should you include in the recommendation?

- **A.** a custom guardrail
- **B.** a Retrieval Augmented Generation (RAG) evaluator
- **C.** model fine-tuning
- **D.** a coherence evaluator

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **B** is correct because a **Retrieval Augmented Generation (RAG) evaluator** in Microsoft Foundry measures retrieval quality, groundedness, completeness, and relevance of `Agent1`'s responses against the retrieved product documents from `storage1`. **A** (`a custom guardrail`) is wrong because guardrails enforce runtime content filtering/blocking rather than assessing RAG groundedness and completeness metrics. **C** (`model fine-tuning`) is wrong because fine-tuning trains model weights rather than evaluating response quality. **D** (`a coherence evaluator`) is wrong because coherence only evaluates whether sentences flow logically together, without checking whether the answer is grounded in `storage1` product sheets.

</details>

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

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** D, E

> **Why:** **D** and **E** are correct because building a vector search index over PDF documents in Azure AI Search requires the **`Text Split` skill** (**D**) to chunk long documents into smaller passages and the **`Azure OpenAI Embedding` skill** (**E**) to generate vector embeddings for each chunk. **A** (`Entity Recognition`), **B** (`Language Detection`), and **C** (`Key Phrase Extraction`) are wrong because they extract NLP metadata tags rather than chunking text or generating embeddings for vector search. **F** (`Merge`) is wrong because it combines text fields rather than splitting documents into chunks or generating vector embeddings.

</details>

---

### Question 61 (Case Study 4/7)
You need to configure `Agent1` to answer customer questions about only the Contoso products. The solution must meet the business requirements.

What should you do?

- **A.** Apply top-p sampling.
- **B.** Add few-shot examples.
- **C.** Modify the system message instructions.
- **D.** Increase the value of the temperature parameter.

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** C

> **Why:** **C** is correct because modifying the **system message instructions** defines the agent's scope, persona, and topic boundaries—instructing `Agent1` to answer questions strictly about Contoso products and politely refuse off-topic queries. **A** (`Apply top-p sampling`) and **D** (`Increase the value of the temperature parameter`) are wrong because they control token sampling randomness rather than restricting the allowed conversation domain. **B** (`Add few-shot examples`) is wrong because few-shot examples guide response formatting and tone, whereas strict behavioral boundaries must be enforced in the system instructions.

</details>

---

### Question 62 (Case Study 5/7)
You need to configure the model deployment for `Agent1` to meet the technical requirements:
- Support generative AI workloads and burst traffic without requiring reserved capacity.
- Ensure the model version used by `Agent1` produces consistent responses over time.

What should you configure?

| Setting | Available Options |
| :--- | :--- |
| **Deployment type** | `Standard`, `Global Standard`, `Global Provisioned` |
| **Version update policy** | `Once the current version expires`, `Opt out of automatic model version upgrades`, `Upgrade once a new default version becomes available` |

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** **Deployment type:** `Global Standard` | **Version update policy:** `Opt out of automatic model version upgrades`

> **Why:**
> - **Deployment type (`Global Standard`):** **Global Standard** provides high-throughput pay-per-token routing across global capacity for variable/burst traffic without purchasing reserved capacity. *Global Provisioned* is wrong because it requires reserved Provisioned Throughput Units (PTUs), and regional *Standard* has lower burst rate limits than Global Standard.
> - **Version update policy (`Opt out of automatic model version upgrades`):** Pinning the model version by opting out of automatic upgrades prevents silent model version changes from altering `Agent1`'s response behavior over time, whereas *Upgrade once a new default version becomes available* automatically updates the model and can change output consistency.

</details>

---

### Question 63 (Case Study 6/7)
You need to recommend a solution to support the planned changes and technical requirements for `Agent1` to use the product information stored in `storage1` (supporting both semantic and vector search).

What should you include in the recommendation?

- **A.** Grounding with Bing Search
- **B.** Azure AI Search
- **C.** Azure Document Intelligence in Foundry Tools
- **D.** Azure Translator in Foundry Tools

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **B** is correct because **Azure AI Search** is the knowledge retrieval engine that indexes content from `storage1` and provides hybrid **semantic and vector search** integration with Microsoft Foundry agents. **A** (`Grounding with Bing Search`) is wrong because it grounds responses in public web search results rather than private PDF product sheets in `storage1`. **C** (`Azure Document Intelligence in Foundry Tools`) is wrong because it parses documents via OCR but does not provide a semantic or vector search index. **D** (`Azure Translator in Foundry Tools`) is wrong because it translates text between languages rather than indexing and searching product sheets.

</details>

---

### Question 64 (Case Study 7/7)
You need to recommend an invoice review solution that resolves the issue reported by the finance department. The solution must support multimodal understanding of textual and visual document content.

What should you include in the recommendation?

- **A.** Azure Document Intelligence in Foundry Tools
- **B.** Azure Content Understanding in Foundry Tools
- **C.** chat completions
- **D.** Image Analysis

<details>
<summary>💡 <b>View Answer & Explanation</b></summary>

**Correct answer:** B

> **Why:** **B** is correct because **Azure Content Understanding in Foundry Tools** provides multimodal document analysis combining OCR, visual layout/figure comprehension, and generative reasoning for complex invoices and contracts. **A** (`Azure Document Intelligence in Foundry Tools`) is wrong because it focuses on traditional OCR and structural form extraction rather than unified generative multimodal reasoning over both visual and textual content. **C** (`chat completions`) is wrong because raw chat completions lack built-in multi-page document ingestion, OCR layout parsing, and structured schema extraction pipelines. **D** (`Image Analysis`) is wrong because it generates general captions and tags for standalone images rather than parsing complex multi-page financial invoices and contracts.

</details>
