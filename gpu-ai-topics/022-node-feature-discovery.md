# 022 - Node Feature Discovery

## Script

How does Kubernetes know which nodes have GPUs, AVX-512, or NVMe drives? It doesn't, unless you install NFD.

Node Feature Discovery, or NFD, is a Kubernetes add-on that detects hardware features and labels nodes automatically.

It scans each node for CPU capabilities, GPU presence, memory configuration, storage types, and network features.

Then it adds labels like `feature.node.kubernetes.io/cpu-cpuid.AVX512F` or `nvidia.com/gpu.present`.

Why does this matter?

You can use node selectors to schedule pods on nodes with specific hardware. Need AVX-512 for vectorized ML inference? NFD labels tell the scheduler exactly which nodes support it.

For GPU workloads, NFD detects GPU model, driver version, and compute capability. You can target specific GPU generations.

NFD pairs perfectly with the GPU Operator. While the GPU Operator sets up drivers and plugins, NFD labels nodes with detailed GPU attributes.

If you're running heterogeneous hardware, NFD brings order to the chaos.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "How does Kubernetes know" | Question marks over cluster nodes, Kubernetes logo shrugging |
| "It doesn't" | Nodes as blank boxes, no labels, scheduler confused |
| "Node Feature Discovery" | NFD logo appearing, scanning beam across cluster |
| "detects hardware features" | Scanner revealing hidden attributes on nodes |
| "labels nodes automatically" | Labels being attached to nodes like tags |
| "CPU capabilities" | CPU chip with feature badges: AVX512, SSE4, etc. |
| "GPU presence" | GPU card icon being detected and labeled |
| "memory, storage, network" | Icons for RAM, NVMe drive, network card being detected |
| "adds labels" | Actual label text appearing on node: `feature.node.kubernetes.io/...` |
| "node selectors" | Pod spec with nodeSelector, arrow pointing to matching labeled node |
| "AVX-512 for ML inference" | Vector operations visualization, pod landing on AVX-512 node |
| "GPU model, driver version" | GPU labels showing: model=A100, driver=535, compute=8.0 |
| "target specific GPU generations" | Filter visualization: only A100 nodes highlighted |
| "pairs with GPU Operator" | NFD and GPU Operator logos working together |
| "heterogeneous hardware" | Cluster with mixed node types, all properly labeled and organized |

## Meme Opportunity
- "You guys know what hardware you have?" - NFD to manual labeling
- Detective meme: NFD discovering node features
