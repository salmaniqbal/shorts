# 014 - MIG (Multi-Instance GPU)

## Hook
Time-slicing shares GPUs, but MIG actually splits them. Here's the difference.

## Script

Time-slicing shares GPUs, but MIG actually splits them. Here's the difference.

MIG stands for Multi-Instance GPU, and it's only available on NVIDIA A100 and H100 cards.

Instead of software sharing like time-slicing, MIG physically partitions the GPU into smaller, isolated instances.

An A100 with 80GB of memory can be split into up to 7 separate GPU instances. Each instance gets its own dedicated memory, compute cores, and cache.

The key difference? Complete isolation. If one workload crashes or goes rogue, the others keep running. No memory conflicts, no noisy neighbors.

In Kubernetes, each MIG instance appears as a separate GPU resource. You can request a specific slice size like `nvidia.com/mig-3g.20gb` for a 3-slice instance with 20GB memory.

MIG is perfect for inference workloads where you need isolation but don't need a full GPU.

The tradeoff? Less flexibility than time-slicing, and you need expensive A100 or H100 hardware.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "Time-slicing shares, MIG splits" | Side-by-side: Time-slicing shows overlapping translucent pods on GPU; MIG shows GPU physically divided into sections |
| "Multi-Instance GPU" | A100/H100 card with "MIG" label, zoom into the chip |
| "physically partitions" | Animation: GPU chip being divided by solid walls into separate chambers |
| "7 separate instances" | A100 diagram splitting into 7 colored sections, each labeled (1g.10gb, etc.) |
| "dedicated memory, compute, cache" | Each partition showing its own memory bar, compute units, and cache block |
| "Complete isolation" | Brick walls between instances, one instance on fire but others unaffected |
| "crashes or goes rogue" | One partition showing explosion/error, neighboring partitions showing green checkmarks |
| "separate GPU resource" | Kubernetes node view: One physical GPU, multiple nvidia.com/mig-* resources listed |
| "specific slice size" | YAML snippet with `nvidia.com/mig-3g.20gb: 1` highlighted |
| "perfect for inference" | Multiple inference server pods, each in their own MIG partition |
| "expensive hardware" | Price tag icon on A100/H100, vs cheaper GPUs without MIG support |

## Meme Opportunity
- "We have isolation at home" - Time-slicing vs actual MIG isolation
- Real estate meme: "I'll take the 3g.20gb apartment please"
