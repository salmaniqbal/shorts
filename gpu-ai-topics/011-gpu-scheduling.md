# 011 - GPU Scheduling in Kubernetes

## Script

Did you know that GPUs in Kubernetes don't work like CPUs at all?

When it comes to CPU a pod can request portions of CPU and Kubernetes can slice it up. Half a core here, quarter of a core there. Easy.

But for GPUs, you either get the whole GPU or nothing. This is because the archietcture of the GPU is different than that of a CPU. CPUs can juggle tasks, GPUs do one massive job

To use a GPU in Kubernetes, you need the NVIDIA device plugin running on your nodes. It discovers GPUs and tells Kubernetes "hey, these nodes have 2 GPUs available."

In order to use a GPU in your pod, you request it like this:

```yaml
resources:
  limits:
    nvidia.com/gpu: 1
```

Then the scheduler finds a node with a free GPU and assigns your pod there. No one else can use that GPU even if your workload only uses 10% of it.

So remember: CPUs share nicely, GPUs don't.

## Visuals & Animations
 
| Timestamp | Visual |
|-----------|--------|
| "GPUs don't work like CPUs" | Split screen: CPU shown as a pie being sliced into pieces vs GPU as a solid block that can't be cut |
| "slice it up" | Animation of CPU core being divided into fractions, pods taking small slices |
| "all or nothing" | GPU block with a "NO SLICING" sign, or a pizza that must be taken whole |
| "NVIDIA device plugin" | Diagram: Node with GPU cards, device plugin container scanning and counting them |
| "tells Kubernetes" | Arrow from device plugin to API server, showing "4x nvidia.com/gpu" resource advertisement |
| "pod spec" | Zoom into YAML snippet with the nvidia.com/gpu resource request highlighted |
| "scheduler finds a node" | Animation: Scheduler looking at 3 nodes, one has GPU available (green), places pod there |
| "can't request half" | Show "nvidia.com/gpu: 0.5" with a red X through it |
| "only uses 10%" | GPU utilization meter showing 10% used, 90% wasted, but still "claimed" |
| "CPUs share, GPUs don't" | Final comparison graphic: CPU = communal pizza, GPU = reserved parking spot |

## Meme Opportunity
- GPU being a diva: "I don't share" with sunglasses
- "You guys are getting fractions?" meme with GPU looking at CPU
