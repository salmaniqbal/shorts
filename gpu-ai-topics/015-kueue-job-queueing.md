# 015 - Kueue for AI Workloads

## Script

What happens when 50 data scientists submit training jobs at the same time? Chaos, unless you have Kueue.

Kubernetes wasn't built for batch AI workloads. Jobs fight for GPUs, there's no fair sharing, and cluster costs spiral out of control.

Kueue fixes this.

It's a job queueing system built specifically for Kubernetes. Instead of jobs immediately grabbing resources, they wait in a queue.

You define ClusterQueues with GPU quotas. Team A gets 10 GPUs, Team B gets 20. Jobs can't exceed their team's quota.

LocalQueues connect namespaces to ClusterQueues. When a data scientist submits a job, it joins their team's queue.

Kueue then admits jobs based on priority, fair sharing, and available resources. Lower priority jobs can even be preempted when urgent work arrives.

It also supports borrowing. If Team A isn't using their GPUs, Team B can temporarily use them.

For any organization running ML training on Kubernetes, Kueue is essential. It brings sanity to GPU resource management.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "50 data scientists submit jobs" | Flood of job requests flying toward a cluster, overwhelming it |
| "Chaos" | Cluster on fire, jobs colliding, error messages everywhere |
| "Kubernetes wasn't built for batch" | Kubernetes logo with a shrug, batch jobs bouncing off |
| "fight for GPUs" | Jobs as characters physically fighting over GPU icons |
| "Kueue fixes this" | Kueue logo appearing, calming the chaos, organizing jobs into neat lines |
| "wait in a queue" | Jobs forming an orderly queue, velvet rope style |
| "ClusterQueues with quotas" | Two queue boxes labeled "Team A: 10 GPUs" and "Team B: 20 GPUs" |
| "LocalQueues connect namespaces" | Namespace boxes with arrows pointing to their respective ClusterQueues |
| "admits jobs based on priority" | Queue with jobs reordering by priority number, high priority moving to front |
| "preempted" | Low priority job being politely escorted out, high priority job taking its place |
| "borrowing" | Team A's unused GPUs flowing temporarily to Team B, dotted line showing it's temporary |
| "sanity to GPU management" | Before/after: Chaos vs organized queues with happy data scientists |

## Meme Opportunity
- "First come first served" crossed out, "Fair queuing" checkmarked
- DMV queue meme but for GPU jobs
