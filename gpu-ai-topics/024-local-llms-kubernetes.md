# 024 - Running Local LLMs on Kubernetes

## Hook
You don't need OpenAI to run LLMs. Deploy Ollama on Kubernetes and keep your data private.

## Script

You don't need OpenAI to run LLMs. Deploy Ollama on Kubernetes and keep your data private.

Ollama is a tool for running open-source LLMs locally. Llama, Mistral, Phi, and many more.

Running it on Kubernetes means your AI stays in your infrastructure. No data leaves your cluster.

The deployment is simple. Run Ollama as a deployment with GPU resources, expose it with a service, done.

For model storage, use a PersistentVolume. Models are downloaded once and reused, saving bandwidth and startup time.

Ollama exposes an API compatible with many LLM libraries. Point your apps at your internal service instead of external APIs.

For multiple models, run different Ollama instances or use model multiplexing. Some teams run a model router that forwards requests to the right backend.

Pair it with an ingress for team access, add resource quotas so one team doesn't hog the GPU, and you've got a private LLM platform.

Privacy-first AI on Kubernetes. Your data, your models, your control.

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
