# 018 - vLLM on Kubernetes

## Script

Running LLMs is expensive. vLLM makes them 24x faster. Here's how to run it on Kubernetes.

vLLM is an inference engine for large language models. It uses PagedAttention to manage GPU memory more efficiently than standard serving.

Instead of reserving memory for the maximum sequence length upfront, vLLM allocates memory dynamically as tokens are generated.

This means you can serve more concurrent requests on the same GPU.

Deploying vLLM on Kubernetes is straightforward.

Create a deployment with the vLLM container image, mount your model from a persistent volume or download it at startup, and expose it with a service.

Set GPU resource limits, configure memory, and you're serving.

vLLM exposes an OpenAI-compatible API, so you can swap it into existing applications without code changes.

For production, pair it with KServe for canary deployments and autoscaling, or use KEDA to scale based on queue depth.

If you're running LLMs on Kubernetes, vLLM should be your default serving engine.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "LLMs are expensive" | Dollar signs flying out of a GPU running an LLM, meter spinning |
| "24x faster" | Speed comparison bar: Standard serving vs vLLM |
| "PagedAttention" | Memory visualization: traditional = large fixed blocks; vLLM = small dynamic pages |
| "maximum sequence length upfront" | Traditional: huge memory block reserved mostly empty |
| "allocates dynamically" | vLLM: memory pages being added as tokens generate, efficient packing |
| "more concurrent requests" | Traditional: 2 requests on GPU; vLLM: 10 requests on same GPU |
| "deployment" | YAML snippet showing vLLM deployment with GPU resources |
| "mount your model" | PersistentVolume icon connected to pod, model weights flowing in |
| "expose with service" | Service and Ingress appearing, connecting to vLLM pods |
| "OpenAI-compatible API" | API endpoint showing `/v1/completions`, OpenAI SDK code working unchanged |
| "swap into existing applications" | Old OpenAI endpoint replaced with vLLM endpoint, app keeps working |
| "KServe for canary" | KServe managing vLLM backends with traffic splitting |
| "KEDA scale on queue" | Queue depth metric triggering more vLLM pods |

## Meme Opportunity
- "We have OpenAI at home" pointing to vLLM
- Memory efficiency comparison: "Look how much room I have for activities!"
