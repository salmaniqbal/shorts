# 028 - NPUs in Kubernetes

## Script

GPUs aren't the only AI accelerators anymore. Meet the NPU.

A CPU is a generalist. It can do anything but nothing super fast. A GPU has thousands of cores optimized for parallel math, perfect for matrix operations in AI.

An NPU, Neural Processing Unit, is purpose-built for AI inference. It's designed specifically for neural network operations like multiply-accumulate, with dedicated hardware for attention layers and activation functions.

Think of it this way. CPU is a Swiss Army knife. GPU is a power drill. NPU is a surgical laser, built for one job and incredibly efficient at it.

The big players? Google's TPU, Intel's Gaudi, AWS Inferentia and Trainium, AMD's Instinct, and Apple's Neural Engine.

To use NPUs in Kubernetes, you need a device plugin, just like GPUs. Intel has one for Gaudi, AWS has one for Inferentia. The plugin exposes the NPU as a schedulable resource.

```yaml
resources:
  limits:
    habana.ai/gaudi: 1
```

Can you slice NPUs like GPUs? It depends. Some support virtualization or multi-tenancy, but it's less mature than GPU MIG. Most NPUs today are allocated as whole devices.

NPUs are cheaper per inference than GPUs. If you're running models at scale, they're worth exploring.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "GPUs aren't the only accelerators" | GPU icon with other chips appearing around it |
| "Meet the NPU" | NPU chip icon with neural network pattern on it |
| "CPU is a generalist" | CPU with many different task icons (web, database, file, etc.) |
| "GPU has thousands of cores" | GPU with grid of small cores highlighted, matrix multiplication animation |
| "NPU is purpose-built" | NPU with neural network layers flowing through dedicated circuits |
| "multiply-accumulate" | Math operation visualization: weights × inputs + bias |
| "Swiss Army knife" | Actual Swiss Army knife image for CPU |
| "power drill" | Power drill for GPU |
| "surgical laser" | Precision laser for NPU |
| "Google TPU" | TPU v4/v5 chip and pod images |
| "Intel Gaudi" | Gaudi 2/3 chip image |
| "AWS Inferentia/Trainium" | AWS chip images, Inferentia for inference, Trainium for training |
| "AMD Instinct" | MI300 chip image |
| "Apple Neural Engine" | Apple Silicon with Neural Engine highlighted |
| "device plugin" | Plugin connecting NPU hardware to Kubernetes API |
| "exposes as schedulable resource" | NPU appearing in node's allocatable resources |
| "YAML snippet" | Show the resource request YAML |
| "slice NPUs" | NPU being divided (some with ✓, some with ✗) |
| "less mature than MIG" | Comparison: GPU MIG well-supported vs NPU slicing experimental |
| "whole devices" | Single NPU allocated to single pod |
| "cheaper per inference" | Cost comparison graph: GPU vs NPU for inference workloads |

## NPU Comparison Table

| NPU | Vendor | Kubernetes Support | Slicing |
|-----|--------|-------------------|---------|
| TPU | Google | GKE native | TPU slices (yes) |
| Gaudi | Intel | Device plugin | Limited |
| Inferentia/Trainium | AWS | Device plugin | No |
| Instinct MI300 | AMD | Device plugin + ROCm | Partial |
| Neural Engine | Apple | Not for servers | No |

## Meme Opportunity
- "You guys are using GPUs for inference?" - NPU looking at GPU cluster
- "We're not the same" - NPU vs GPU comparison meme
- "Specialized tool for specialized job" with NPU being surgical vs GPU being sledgehammer
