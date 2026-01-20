# 023 - Topology-Aware Scheduling

## Hook
Not all GPUs are created equal. Two GPUs on the same NVLink are 10x faster than two across PCIe.

## Script

Not all GPUs are created equal. Two GPUs on the same NVLink are 10x faster than two across PCIe.

When you request 2 GPUs in Kubernetes, the scheduler just finds a node with 2 available. It doesn't care if they can talk to each other efficiently.

For multi-GPU training, this kills performance.

GPUs on the same NVLink bridge communicate at 600 GB/s. Across PCIe? Maybe 32 GB/s. That's a massive difference for gradient synchronization.

Topology-aware scheduling fixes this.

The Topology Manager in kubelet tracks how devices connect: which GPUs share NVLink, which share a PCIe switch, which NUMA node they're attached to.

When you set the topology policy to `best-effort` or `restricted`, Kubernetes tries to place your pod on GPUs with the best interconnect.

For serious multi-GPU work, you can also use NodeResourceTopology from NFD and custom schedulers that understand GPU topology deeply.

Remember: for distributed training, where your GPUs sit matters as much as how many you have.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "Not all GPUs created equal" | Two identical-looking GPUs, but speed indicators showing different values |
| "NVLink vs PCIe" | Diagram showing two GPUs with fat pipe (NVLink 600GB/s) vs thin pipe (PCIe 32GB/s) |
| "10x faster" | Speed comparison bar chart |
| "scheduler just finds" | Naive scheduler picking any 2 available GPUs, ignoring topology |
| "kills performance" | Training job with terrible throughput graph |
| "gradient synchronization" | Gradients flowing between GPUs, bottlenecked on slow interconnect |
| "Topology-aware scheduling" | Smart scheduler visualizing GPU connections before placing pod |
| "Topology Manager in kubelet" | Kubelet component with topology map of devices |
| "how devices connect" | Node internal diagram: GPUs, NVLinks, PCIe switches, NUMA nodes |
| "best-effort or restricted" | Policy selector showing different topology policy options |
| "best interconnect" | Pod being placed on two NVLink-connected GPUs, green checkmark |
| "NodeResourceTopology" | CRD showing detailed node topology information |
| "custom schedulers" | Advanced scheduler plugin looking at topology graph |
| "where GPUs sit matters" | Final diagram: good placement (fast) vs bad placement (slow) |

## Meme Opportunity
- "They're the same GPU" / "Corporate needs you to find the difference" - but one is NVLink connected
- "Friendship ended with PCIe, now NVLink is my best friend"
