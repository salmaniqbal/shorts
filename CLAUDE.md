# Kubernetes Shorts - Claude Guidelines

## About This Project
This repository contains scripts for YouTube Shorts explaining Kubernetes concepts in 30-45 seconds. The goal is to make complex Kubernetes topics accessible and engaging for listeners.

## Content Style

### Structure
- **Hook first**: Start with an attention-grabbing question or surprising fact ("Did you know...", "Imagine...", "You deploy X and it doesn't work...")
- **Simple explanation**: Break down the concept without jargon, using relatable analogies (Tetris for scheduling, pizza for operators, group chat for networking)
- **Visual cues**: Scripts assume Figma slides, animations, zoom effects, YAML snippets, and memes
- **Memorable closer**: End with a takeaway or call-to-action

### Tone
- Conversational and direct
- Uses analogies and metaphors to make concepts stick
- Light humor where appropriate (memes, unexpected examples)
- Practical focus - what does this mean for the listener?

### Timing
- Target: 30-45 seconds
- Maximum: 60 seconds
- Every sentence must earn its place

## Focus Areas

### Core Kubernetes Concepts (Covered)
- API server pipeline
- Operators and custom resources
- Scheduler
- Namespaces and security
- Autoscaling (HPA, VPA, Cluster Autoscaler)
- PriorityClasses
- Node capacity and resource allocation

### GPU/AI + Kubernetes Topics (Priority)
Ideas for upcoming shorts combining Kubernetes with GPU/AI workloads:

1. **GPU Scheduling in Kubernetes** - How the device plugin exposes GPUs, nvidia.com/gpu resource requests, and why you can't share a GPU like CPU
2. **NVIDIA GPU Operator** - Automates driver installation, container toolkit, and device plugin setup
3. **Time-slicing GPUs** - Share a single GPU across multiple pods (with tradeoffs)
4. **MIG (Multi-Instance GPU)** - Physically partition A100/H100 GPUs for isolation
5. **Kueue for AI Workloads** - Job queueing and quota management for batch ML training
6. **Inference Autoscaling** - Scaling model servers based on queue depth or GPU utilization
7. **KServe / Seldon** - Serving ML models on Kubernetes with canary deployments
8. **vLLM on Kubernetes** - Running LLM inference servers efficiently
9. **Ray on Kubernetes (KubeRay)** - Distributed training and inference
10. **DRA (Dynamic Resource Allocation)** - The future of GPU scheduling in Kubernetes
11. **Spot/Preemptible Nodes for Training** - Cost optimization with checkpointing
12. **Node Feature Discovery** - Auto-labeling nodes with GPU capabilities
13. **Topology-aware Scheduling** - NVLink, PCIe locality for multi-GPU workloads
14. **Kagent / K8sGPT** - AI agents that debug your cluster (already covered in 010)
15. **Running Local LLMs in Kubernetes** - Ollama, LocalAI deployments
16. **GPU Memory Management** - OOM kills, memory fragmentation, right-sizing requests

## Script Template

```
## [NUMBER] - [TOPIC]

[Hook - attention-grabbing question or scenario]

[Core explanation - 2-4 short paragraphs]

[Optional: YAML snippet or visual callout]

[Memorable takeaway or question for engagement]
```

## Guidelines for Claude

When generating new short ideas or scripts:

1. **Hook matters most** - If the first line doesn't grab attention, nothing else matters
2. **One concept per short** - Don't try to cover too much
3. **Listener benefit** - Always answer "why should I care?"
4. **Practical examples** - Show real scenarios, not abstract theory
5. **YAML when helpful** - A 3-line YAML snippet can explain more than 3 sentences
6. **Test the timing** - Read aloud, should be under 45 seconds
7. **GPU/AI angle** - Look for ways to connect traditional K8s concepts to AI workloads
8. **Avoid marketing speak** - Be direct, not promotional

## Quality Checklist
- [ ] Does it start with a hook?
- [ ] Can a beginner follow it?
- [ ] Is there a clear takeaway?
- [ ] Under 45 seconds when read aloud?
- [ ] Would this make someone want to learn more?
