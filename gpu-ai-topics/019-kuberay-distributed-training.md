# 019 - KubeRay for Distributed Training

## Hook
Training a model on one GPU takes forever. What if you could use 100 GPUs at once?

## Script

Training a model on one GPU takes forever. What if you could use 100 GPUs at once?

Ray is a framework for distributed computing, and KubeRay brings it to Kubernetes.

With Ray, you write Python code that automatically distributes across multiple machines. No MPI, no manual coordination.

KubeRay deploys this on Kubernetes using custom resources.

A RayCluster defines your head node and worker nodes. The head node coordinates, workers do the heavy lifting.

Each worker can have GPUs, and Ray handles distributing your training across all of them.

Submitting jobs is easy. Create a RayJob resource with your training script. KubeRay spins up a cluster, runs the job, and can tear it down when finished.

RayServe handles inference, so you can train AND serve from the same platform.

For large-scale ML training and inference on Kubernetes, KubeRay is becoming the standard. PyTorch, TensorFlow, JAX, it works with all of them.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "one GPU takes forever" | Single GPU with progress bar crawling slowly, clock ticking |
| "100 GPUs at once" | Grid of 100 GPUs, progress bar filling rapidly |
| "Ray distributed computing" | Ray logo with distributed nodes connected |
| "KubeRay brings it to Kubernetes" | Ray logo merging with Kubernetes logo |
| "automatically distributes" | Python code being split and sent to multiple workers |
| "no MPI, no manual coordination" | MPI commands crossed out, complex scripts crossed out |
| "RayCluster custom resource" | YAML snippet showing RayCluster with head and worker specs |
| "head node and workers" | Diagram: One head node connected to multiple worker nodes |
| "workers do heavy lifting" | Worker nodes with GPU icons processing data chunks |
| "distributing training" | Model being split (data parallel or model parallel), pieces going to different workers |
| "RayJob resource" | YAML snippet for RayJob, showing entrypoint script |
| "spins up, runs, tears down" | Cluster appearing, job running, cluster disappearing (ephemeral) |
| "RayServe" | Transition from training to serving, same cluster handling both |
| "PyTorch, TensorFlow, JAX" | Framework logos appearing as compatible options |

## Meme Opportunity
- "Distributed training is hard" crossed out, "Ray makes it easy"
- "I am speed" with Ray across 100 GPUs
