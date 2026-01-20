# 020 - DRA (Dynamic Resource Allocation)

## Script

The device plugin API is showing its age. DRA is the future of GPU scheduling in Kubernetes.

Today, GPUs are advertised as simple countable resources. A node says "I have 4 GPUs" and that's it. No details about memory, compute capability, or topology.

Dynamic Resource Allocation changes everything.

With DRA, resources are described as structured objects. A GPU isn't just a count, it's an object with properties: 80GB memory, A100 architecture, MIG partitions available.

Pods can now request specific attributes. "Give me a GPU with at least 40GB memory and MIG support."

DRA also enables dynamic configuration. Resources can be set up just before a pod starts and cleaned up after it stops.

The scheduling gets smarter too. The scheduler understands relationships, like which GPUs share the same NVLink network.

DRA is still maturing in Kubernetes, but vendors like NVIDIA are already building drivers for it.

If you're watching the future of GPU on Kubernetes, DRA is where it's heading.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "device plugin showing its age" | Old device plugin interface with simple counter, looking dated |
| "future of GPU scheduling" | DRA logo/text with modern, futuristic styling |
| "simple countable resources" | Node showing "nvidia.com/gpu: 4", no other info |
| "no details" | Question marks around GPU: Memory? Architecture? Features? |
| "structured objects" | GPU represented as rich object with multiple properties displayed |
| "object with properties" | Expandable card: GPU { memory: 80GB, arch: A100, mig: true, nvlink: [1,2] } |
| "request specific attributes" | Pod spec showing ResourceClaim with attribute requirements |
| "40GB memory and MIG support" | Filter/search visualization narrowing down GPU options |
| "dynamic configuration" | Timeline: Pod scheduled -> GPU configured -> Pod runs -> GPU released |
| "setup and cleanup" | MIG partition being created before pod, destroyed after |
| "scheduler understands relationships" | Graph showing GPU topology: NVLink connections, PCIe hierarchy |
| "NVLink network" | Two GPUs with high-speed NVLink bridge highlighted |
| "NVIDIA building drivers" | NVIDIA logo working on DRA driver, progress indicator |
| "future heading" | Roadmap visualization with DRA as the destination |

## Meme Opportunity
- "Device Plugin: I count GPUs. DRA: I know everything about GPUs"
- "The future is now, old man" with device plugin and DRA
