# Model Access Types — Concept Notes (24 July 2026)

Understanding the difference between **Closed Source**, **Open Weight**, and **Open Source Open Weight** models is critical when deciding how to build, fine-tune, or deploy AI systems.

---

## 1. Closed Source Models

**Closed Source** models are complete black boxes — you have no access to their weights (the learned knowledge encoded in billions of parameters), their training data, or their underlying architecture code.

### How Access Works
- Access is provided exclusively through a **paid API** (e.g., OpenAI API, Anthropic API, Google AI API).
- Users interact via HTTP requests; the model runs on the provider's infrastructure.
- Usage is metered and billed by **tokens consumed** (input + output).

### Key Characteristics

- **Highly polished:** Continuously updated with the latest safety measures, capabilities, and performance improvements.
- **Cutting-edge performance:** Often the best-in-class models on benchmarks (e.g., GPT-4o, Claude 3.5 Sonnet, Gemini 1.5 Pro).
- **No customization:** You cannot retrain, fine-tune, or modify the model weights in any way.
- **Zero infrastructure burden:** The provider handles all hardware, scaling, and maintenance.

### Advantages

- Easiest to integrate — just an API call.
- Best out-of-the-box performance for general tasks.
- No need for GPUs or local hardware.
- Regular updates with no effort from the user.

### Disadvantages & Limitations

- **No access to weights or code** — complete opacity.
- **Data privacy risk:** Your prompts and data are sent to third-party servers.
- **Cost at scale:** Token-based pricing becomes expensive for high-volume applications.
- **Vendor lock-in:** You depend entirely on the provider's availability, pricing, and policy decisions.
- **No fine-tuning control:** Limited or no ability to adapt the model to a niche domain.

### Examples
> GPT-4o, GPT-4 Turbo, Claude 3.5 Sonnet, Gemini 1.5 Pro, Mistral Large (API)

---

## 2. Open Weight Models

**Open Weight** models make their trained weights publicly downloadable, but the underlying training code, data pipeline, and full architecture details may remain proprietary or partially closed.

### How Access Works
- Weights are downloadable from platforms like **Hugging Face** or the model provider's website.
- Models run **locally on your own hardware** or self-hosted cloud infrastructure.
- No per-token cost — you only pay for your own compute.

### Key Characteristics

- **Downloadable weights:** You can load the model directly using frameworks like `transformers`, `llama.cpp`, or `Ollama`.
- **Fine-tunable:** You can adapt the model to your specific domain using techniques like QLoRA, LoRA, or full fine-tuning.
- **Local execution:** Runs entirely on your infrastructure — no data leaves your environment.
- **Less frequently updated:** Provider releases new versions periodically rather than continuously.

### Advantages

- **Data privacy:** 100% local — sensitive data never touches external servers.
- **Fine-tuning freedom:** Adapt the model to specialized domains (medical, legal, code, etc.).
- **No ongoing API costs** after initial compute investment.
- **Offline capable:** Works in air-gapped or internet-restricted environments.

### Disadvantages & Limitations

- **Expensive infrastructure:** Running large models (e.g., 70B) requires high-end GPUs (A100, H100) — not cheap.
- **Weights only — no code:** You can't study or modify the training process itself.
- **Self-managed updates:** You must manually download and manage new versions.
- **Operational overhead:** Requires MLOps knowledge to deploy, monitor, and scale.

### Examples
> Llama 3 (Meta), Qwen3 (Alibaba), Gemma (Google), Mistral 7B, Falcon

---

## 3. Open Source Open Weight Models

**Open Source Open Weight** models are fully transparent — both the **model weights** and the **source code** (training scripts, architecture, data processing pipelines) are publicly available. True open-source AI.

### How Access Works
- Everything is downloadable: weights, training code, architecture definitions, and sometimes training data.
- Hosted on platforms like **Hugging Face**, **GitHub**, or project-specific repositories.
- Community can contribute, audit, and improve the model.

### Key Characteristics

- **Full transparency:** Anyone can inspect, reproduce, or audit the entire system.
- **Maximum customizability:** Modify the architecture, retrain from scratch, or fine-tune with full control.
- **Community-driven:** Improvements and variants are contributed by the global research community.
- **Potentially limited availability:** Some fully open models are released selectively or with usage restrictions due to competitive or safety concerns.

### Advantages

- **Complete control:** Modify weights, architecture, and training pipeline as needed.
- **Reproducibility:** Research can be fully verified and replicated.
- **Community ecosystem:** Rich ecosystem of fine-tuned variants, tools, and integrations.
- **No vendor dependency:** Fully self-sovereign AI infrastructure.

### Disadvantages & Limitations

- **Limited availability:** Some organizations withhold full open-source release for competitive or safety reasons.
- **Infrastructure cost:** Same hardware demands as open weight models.
- **Quality variance:** Community versions vary widely in quality and reliability.
- **Responsibility shifts to you:** Safety, alignment, and reliability are your problem to solve.

### Examples
> Mistral 7B (Apache 2.0), OLMo (AI2), Falcon (TII), some Llama variants with community training code

---

## Direct Comparison

| Feature | Closed Source | Open Weight | Open Source Open Weight |
|---|---|---|---|
| **Weight Access** | ❌ None | ✅ Downloadable | ✅ Downloadable |
| **Code / Architecture Access** | ❌ None | ⚠️ Partial / None | ✅ Fully Public |
| **Training Data Access** | ❌ None | ❌ None | ✅ Often Available |
| **Fine-Tuning** | ❌ Not possible (or very limited) | ✅ Full fine-tuning | ✅ Full fine-tuning + retraining |
| **Data Privacy** | ❌ Data sent to provider | ✅ Fully local | ✅ Fully local |
| **Infrastructure Cost** | Low (API only) | High (own GPUs) | High (own GPUs) |
| **Update Frequency** | Very High (continuous) | Moderate (periodic releases) | Varies (community-driven) |
| **Vendor Lock-in** | ✅ High risk | ❌ None | ❌ None |
| **Ease of Use** | Very Easy (API call) | Moderate | Complex |
| **Best For** | Production apps, fast prototyping | Privacy-first, domain fine-tuning | Research, full customization |
| **Examples** | GPT-4o, Claude, Gemini | Llama 3, Qwen3, Gemma | Mistral, OLMo, Falcon |

---

## When to Use Which?

| Scenario | Choose |
|---|---|
| Quick prototype or general-purpose assistant | **Closed Source** |
| Privacy-sensitive enterprise application | **Open Weight** |
| Fine-tuning on proprietary domain data | **Open Weight** |
| Academic research / full reproducibility | **Open Source Open Weight** |
| Custom architecture modifications | **Open Source Open Weight** |
| No in-house GPU infrastructure | **Closed Source** |
| Offline / air-gapped deployment | **Open Weight** or **Open Source Open Weight** |

> **My Use Case (Fine-tuning Qwen3-8B):** Qwen3-8B is an **Open Weight** model — weights are downloadable and fine-tunable locally. This is the sweet spot: privacy-preserving, cost-efficient fine-tuning with QLoRA on a single GPU, specialized for Software Engineering tasks.
