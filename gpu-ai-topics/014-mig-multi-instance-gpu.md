# 014 - MIG (Multi-Instance GPU)

## Script


Roses are red 
Violets are blue 
If you want real isolation, use Multi-Instance GPU

In Kubernetes multiple pods can share a GPU by time slicing.

Multi-Instance GPU, actually splits the GPU. 

This is available on NVIDIA datacenter cards like A100 and H100.

Take a 40GB A100. Under the hood, it is a single pool of compute & memory. 

With MIG enabled, you can split a single GPU up to seven isolated instances. Each with dedicated compute and its own slice of GPU memory

You can also mix different profiles depending on your workload.

In Kubernetes, each slice appears as its own resource, and can be requested by adding this in the requests nvidia.com/mig-3g.20gb. And can be requested like this

Unlike time-slicing, this is true hardware isolation — no noisy neighbours. If one workload crashes, the others keep running.

MIG is perfect for inference when you want isolation without burning a full GPU.


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
