# 021 - Spot Nodes for ML Training

## Hook
GPU nodes are expensive. What if you could get them for 70% off?

## Script

GPU nodes are expensive. What if you could get them for 70% off?

Cloud providers offer spot instances, spare capacity at massive discounts. The catch? They can be reclaimed with just 2 minutes notice.

For ML training, that's actually fine, if you're smart about it.

The key is checkpointing. Save your model state regularly to persistent storage. When a spot node gets reclaimed, your training continues from the last checkpoint on a new node.

In Kubernetes, use the cluster autoscaler with spot node pools. Taint these nodes so only training jobs that tolerate interruption run there.

Set up termination handlers that detect the 2-minute warning and trigger a final checkpoint save.

For fault tolerance, use frameworks like PyTorch Lightning or Ray Train. They handle checkpoint saving and resumption automatically.

Combine spot instances with Kueue for preemption handling, and you've got cost-effective GPU training that survives interruptions.

70% savings on GPU compute adds up fast. Your CFO will thank you.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "expensive" | GPU node with big price tag, dollar signs |
| "70% off" | Price tag slashed, sale sticker |
| "spot instances" | Cloud provider spare capacity visualization, auction-style pricing |
| "reclaimed with 2 minutes" | Timer showing 2:00, warning symbol |
| "smart about it" | Brain icon with checklist |
| "checkpointing" | Training progress bar with checkpoint flags saved along the way |
| "save to persistent storage" | Model state being written to cloud storage bucket |
| "continues from checkpoint" | Node disappears, new node picks up from checkpoint, progress resumes |
| "cluster autoscaler with spot" | Cluster autoscaler config showing spot node pool, cost labels |
| "taint these nodes" | Node with "spot=true:NoSchedule" taint, only tolerating jobs land there |
| "termination handlers" | Warning signal received, handler triggers checkpoint, graceful shutdown |
| "2-minute warning" | Clock countdown, checkpoint save animation completing |
| "PyTorch Lightning, Ray Train" | Framework logos with "auto-checkpoint" badge |
| "Kueue for preemption" | Job being preempted, re-queued, resumed smoothly |
| "70% savings" | Cost comparison chart: on-demand vs spot over time |

## Meme Opportunity
- "The risk I took was calculated, but man am I good at checkpointing"
- Panik (spot termination) / Kalm (checkpoint saved) meme
