# 013 - GPU Time-Slicing

## Script

What if I told you multiple pods CAN share a single GPU?

By default, Kubernetes gives each pod exclusive access to a GPU. Great for isolation, terrible for utilization.

Enter GPU time-slicing.

With time-slicing, NVIDIA lets you configure how many pods can share a single GPU. The GPU rapidly switches between workloads, giving each one a slice of time.

You configure it with a ConfigMap that tells the device plugin "advertise 4 GPUs instead of 1" even though there's only one physical GPU.

Now 4 pods can each request `nvidia.com/gpu: 1` and share that single card.

But here's the tradeoff: there's no memory isolation. If one pod goes crazy and eats all the GPU memory, everyone crashes.

Time-slicing works great for inference workloads and development. For production training jobs that need guaranteed resources? Stick with dedicated GPUs or use MIG.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "multiple pods CAN share" | Single GPU with multiple pods connected to it, question marks turning to checkmarks |
| "exclusive access" | One GPU, one pod, "RESERVED" sign, other pods waiting outside |
| "terrible for utilization" | GPU meter showing 20% usage, money flying away |
| "time-slicing" | Clock/timer graphic, GPU switching rapidly between colored workloads (red, blue, green, yellow) |
| "rapidly switches" | Animation showing context switching: Pod A runs -> pause -> Pod B runs -> pause -> repeat |
| "ConfigMap" | YAML snippet showing replicas: 4 configuration |
| "advertise 4 GPUs instead of 1" | Node view: 1 physical GPU icon expanding into 4 virtual GPU icons |
| "4 pods can share" | 4 pods each with nvidia.com/gpu: 1, all pointing to same physical GPU |
| "no memory isolation" | GPU memory bar, 4 pods drawing from same pool, one greedy pod expanding |
| "everyone crashes" | One pod expands to fill memory, other pods show OOM errors, skull icons |
| "inference and development" | Checkmark next to inference server icon, checkmark next to laptop/dev icon |
| "production training" | X mark next to training job icon with "use MIG instead" |

## Meme Opportunity
- "You guys are getting your own GPUs?" with time-sliced pods looking at dedicated pods
- Musical chairs meme with pods and a single GPU chair
