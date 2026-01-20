# 012 - NVIDIA GPU Operator

## Script

Setting up GPUs in Kubernetes used to be a nightmare. Now it's one YAML file.

Before the GPU Operator, you had to manually install NVIDIA drivers on every node, set up the container toolkit, deploy the device plugin, and pray nothing broke on the next kernel update.

The NVIDIA GPU Operator automates all of this.

It's a Kubernetes Operator that watches your nodes and automatically installs everything needed to run GPU workloads.

Drivers? Installed as a container. Container toolkit? Deployed. Device plugin? Running. Even monitoring with DCGM is set up for you.

When you add a new GPU node, the operator detects it and configures it automatically. No SSH, no scripts, no manual work.

Install it with Helm, and your cluster is GPU-ready in minutes.

So if you're running AI workloads on Kubernetes, the GPU Operator is your best friend.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "used to be a nightmare" | Developer at terminal with multiple error messages, sweat drops, chaos |
| "one YAML file" | Single clean YAML file, maybe with sparkles or a magic wand |
| "manually install" | Checklist with 5+ items, person checking them off one by one, exhausted |
| "pray nothing broke" | Kernel update notification popup, followed by explosion/fire on the node |
| "Kubernetes Operator" | Operator pattern diagram: Custom Resource -> Controller -> Managed Resources |
| "watches your nodes" | Eye icon scanning across cluster nodes, detecting GPU hardware |
| "Drivers installed as container" | Container box with NVIDIA driver inside, deployed to node |
| "Container toolkit, Device plugin" | Stack of containers being deployed in sequence, green checkmarks appearing |
| "DCGM monitoring" | Dashboard with GPU metrics: temperature, utilization, memory |
| "add a new GPU node" | New node joining cluster, operator immediately deploying components to it |
| "Install with Helm" | `helm install gpu-operator nvidia/gpu-operator` command, progress bar |
| "GPU-ready in minutes" | Cluster diagram with all nodes showing green GPU status |

## Meme Opportunity
- "It ain't much but it's honest work" - GPU Operator installing drivers
- Before/After meme: Manual setup (crying) vs GPU Operator (relaxed)
