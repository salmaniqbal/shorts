# 013 - GPU Time-Slicing

## Script

When a kubernetes pod gets scheduled on a GPU, it gets exclusive access to it even if it uses it partially.

Any other pod requesting a GPU must wait until the first one finishes

This is great for isolation but terrible for utilisation. 

Enter GPU time slicing

With time-slicing, NVIDIA allows multiple pods to share a single physical GPU. The GPU rapidly switches between workloads, giving each pod a slice of execution time.

It is configured with a ConfigMap that tells the device plugin to advertise multiple GPUs even though only one physical GPU exists

Now 3 pods can each request a GPU each `nvidia.com/gpu: 1` and share that single card.

The trade-off: there is no memory isolation. If one pod consumes all GPU memory, it can cause failures for the others.




## Notes: 
Once a kernel begins, it runs to completion.
The Linux kernel cannot interrupt it, cannot time-slice it, and cannot enforce
fairness across tenants.
This means that when two tenants share a GPU, one can invisibly consume
memory, launch long-running kernels, and starve the other.

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
