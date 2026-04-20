# 015 - Running Local LLMs on Kubernetes

## Script (Solo version)

What if you could run powerful AI
without sending your data anywhere?

You don’t need OpenAI or Anthropic to run LLMs for you.

Deploy Ollama on Kubernetes and keep everything inside your cluster.

Ollama lets you run open-source models like Llama, Mistral and Phi locally. No external API calls. No data leaving your infrastructure.

In Kubernetes, it’s simple:
Run Ollama as a Deployment with GPU resources, expose it with a Service, and mount a PersistentVolume so models download once and persist.

It exposes a standard API, so your apps just point to an internal service instead of the internet.

Need multiple models?
Run separate Ollama instances or add a lightweight model router.

Add an Ingress for internal access, set resource quotas to protect your GPUs, and you’ve built a private LLM platform.

Privacy-first AI.
Your data. Your models. Your control.

---

## Script (Option 2 - Dialogue/Debate format with Salaboy)

**Salman**: What if you could run AI without sending your data anywhere?

**Salaboy**: That’s exactly what we do — Ollama on Kubernetes. Open-source models like Llama, Mistral, and Phi, running inside your own cluster. No external API calls. No data leaving your infrastructure.

**Salman**: But isn’t it complex to set up?

**Salaboy**: Not really. It’s just a Deployment with GPU resources, a Service to expose it, and a PersistentVolume so models download once and persist. Ollama exposes a standard API — your apps just point to an internal service instead of the internet.

**Salman**: And if you need multiple models?

**Salaboy**: Run separate Ollama instances or add a lightweight model router. Throw in an Ingress for internal access, set resource quotas to protect your GPUs — and you’ve got a private LLM platform.

**Salman**: Your data. Your models. Your control.

---

## Script (Option 3 - Intro + Deep Dive with Salaboy)

**Salman**: I brought in my friend Salaboy — he literally wrote the book on Platform engineering. Salaboy, how do you run private AI without sending data to OpenAI?

**Salaboy**: Deploy Ollama on Kubernetes. It runs open-source models like Llama, Mistral, and Phi — locally, inside your cluster. No external API calls. No data leaving your infrastructure.

In Kubernetes, it’s straightforward: a Deployment with GPU resources, a Service to expose it, and a PersistentVolume so models download once and persist. Ollama exposes a standard API, so your apps just point to an internal service instead of the internet.

Need multiple models? Run separate Ollama instances or add a model router. Add an Ingress for internal access, set resource quotas to protect your GPUs — and you’ve built a private LLM platform.

**Salman**: Privacy-first AI. Follow Salaboy on X @salaboy.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "Don't need OpenAI" | OpenAI logo fading out, replaced with self-hosted option |
| "keep your data private" | Data staying inside cluster boundary, lock icon |
| "Ollama" | Ollama logo, llama character |
| "open-source LLMs" | Model logos: Llama, Mistral, Phi appearing |
| "AI stays in your infrastructure" | Cluster diagram with LLM running inside, no external arrows |
| "deployment with GPU resources" | YAML snippet showing Ollama deployment with nvidia.com/gpu |
| "expose with service" | Service resource connecting to Ollama pods |
| "PersistentVolume for models" | PV icon connected to pod, model files stored |
| "downloaded once, reused" | Download happening once, subsequent pods using cached model |
| "API compatible" | Code snippet showing API call to internal Ollama endpoint |
| "internal service instead of external" | Request path: App -> Internal Service vs App -> Internet -> OpenAI |
| "model multiplexing" | Router receiving requests, forwarding to different model backends |
| "ingress for team access" | Ingress exposing Ollama to internal users |
| "resource quotas" | Namespace quotas preventing GPU hogging |
| "Your data, your models" | Summary graphic: Private cloud with LLM inside |

## Meme Opportunity
- "We have ChatGPT at home" and home actually has a solid setup
- "My data, my choice" privacy meme
