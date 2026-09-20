# 016 - Inference Autoscaling

## Script

Ever asked ChatGPT a question and had to wait for the answer?

That's AI inference.

Every prompt you send is processed by a large language model running on expensive GPUs.

When lots of users arrive at the same time, requests start queueing up. Response times increase and users get frustrated.

With a normal web application, Kubernetes can scale based on CPU usage.

But AI inference is different as we need to scale based on inference 

So instead of just scaling on CPU, we scale on inference-specific metrics like request queue depth, latency, GPU utilisation, time-to-first-token, or tokens per second.

You can do this with the Kubernetes Horizontal Pod Autoscaler using custom metrics that the DCGM can export to Promethus.

For example, if GPU utilisation stays above 80%, or the queue of waiting requests grows too large, Kubernetes can automatically spin up another inference pod.

As more users arrive, more pods are added. As traffic drops, pods are removed, helping reduce the cost of idle GPU capacity.

That's inference autoscaling in Kubernetes.



## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "Ever asked ChatGPT a question and had to wait" | ChatGPT-style prompt box, cursor blinking, loading spinner going round |
| "That's AI inference" | Text overlay: "AI Inference" — GPU chip icon, arrow flowing from prompt to response |
| "large language model running on expensive GPUs" | GPU server rack with temperature and power indicators climbing |
| "lots of users arrive at the same time" | Animated user icons flooding in towards a single inference pod |
| "requests start queueing up" | Queue bar filling up, response time counter ticking upward, user icons showing frustration |
| "Response times increase and users get frustrated" | Angry emoji / rage face appearing next to the loading spinner |
| "Kubernetes often scales based on CPU usage" | HPA diagram watching a CPU gauge, adding pod copies smoothly |
| "The GPU is usually the bottleneck" | Split screen: CPU at 8%, GPU at 98% — GPU meter red-lining |
| "inference-specific metrics" | Bullet list animating in one by one: request queue depth, latency, GPU utilisation, time-to-first-token, tokens per second |
| "Horizontal Pod Autoscaler using custom or external metrics" | HPA icon with a custom metrics feed (Prometheus logo) plugged into it |
| "GPU utilisation stays above 80%" | GPU gauge hitting 80%, threshold line appearing, HPA triggering |
| "queue of waiting requests grows too large" | Queue bar overflowing, HPA reacting and spinning up a new pod |
| "more pods are added" | New inference pods appearing side by side, queue draining, response times dropping |
| "As traffic drops, pods are removed" | Traffic graph falling, pods disappearing one by one |
| "reduce the cost of idle GPU capacity" | Dollar sign counter dropping, idle GPU nodes powering down |
| "That's inference autoscaling in Kubernetes" | Clean architecture diagram: users → HPA → inference pods → GPU nodes |

## Meme Opportunity
- "It's not CPU, never was" — astronaut meme, GPU highlighted
- Waiting skeleton meme — user waiting for inference response with no autoscaling
- "Why is my GPU bill so high?" — before autoscaling; "Why is it gone?" — after scale-to-zero

## GPU Metrics for Scaling (via DCGM Exporter)

### Compute
| Metric | Description |
|--------|-------------|
| `DCGM_FI_DEV_GPU_UTIL` | GPU utilisation (%) — primary compute pressure signal |
| `DCGM_FI_DEV_SM_CLOCK` | Streaming Multiprocessor clock speed |

### Memory
| Metric | Description |
|--------|-------------|
| `DCGM_FI_DEV_FB_USED` | Framebuffer memory used (MB) — scale before OOM |
| `DCGM_FI_DEV_FB_FREE` | Framebuffer memory free (MB) |
| `DCGM_FI_DEV_MEM_COPY_UTIL` | Memory copy engine utilisation (%) |

### Power & Thermal
| Metric | Description |
|--------|-------------|
| `DCGM_FI_DEV_POWER_USAGE` | Power draw (W) — proxy for sustained load |
| `DCGM_FI_DEV_GPU_TEMP` | GPU temperature (°C) |

### Interconnect
| Metric | Description |
|--------|-------------|
| `DCGM_FI_DEV_NVLINK_BANDWIDTH_TOTAL` | NVLink bandwidth — relevant for multi-GPU inference |
| `DCGM_FI_DEV_PCIE_TX_THROUGHPUT` | PCIe TX throughput |
| `DCGM_FI_DEV_PCIE_RX_THROUGHPUT` | PCIe RX throughput |

### App-level (vLLM)
| Metric | Description |
|--------|-------------|
| `vllm_num_requests_waiting` | Requests queued — best leading indicator for scale-out |
| `vllm_num_requests_running` | Requests actively being processed |
| `vllm_gpu_cache_usage_perc` | KV cache usage (%) — high value = memory pressure |
| `vllm_avg_generation_throughput` | Tokens generated per second |
