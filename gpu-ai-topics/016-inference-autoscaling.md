# 016 - Inference Autoscaling

## Hook
Scaling web apps is easy. Scaling GPU inference servers? That's a different game.

## Script

Scaling web apps is easy. Scaling GPU inference servers? That's a different game.

With web apps, the Horizontal Pod Autoscaler watches CPU usage and spins up more replicas when needed. Simple.

But for inference servers, CPU tells you nothing. You need to scale based on GPU metrics or request queue depth.

KEDA makes this possible.

KEDA is an event-driven autoscaler for Kubernetes. It can scale based on custom metrics like Prometheus queries.

You create a ScaledObject that watches your inference server's queue length. When requests pile up, KEDA adds more replicas. When the queue empties, it scales down.

You can also scale on GPU utilization from DCGM metrics, or even scale to zero when there's no traffic, which saves serious money on GPU nodes.

The tricky part? GPUs take time to initialize. Configure longer stabilization windows so you're not constantly scaling up and down.

For production inference, pair KEDA with Kueue and you've got a cost-effective, responsive serving platform.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "Scaling web apps is easy" | Simple diagram: HPA watching CPU meter, adding pod copies smoothly |
| "different game" | GPU inference server with complex dials and metrics |
| "CPU tells you nothing" | CPU meter showing 5%, but GPU fully loaded, queue backed up |
| "request queue depth" | Queue visualization filling up with inference requests |
| "KEDA" | KEDA logo appearing with event streams flowing into it |
| "event-driven autoscaler" | Multiple event sources (queues, metrics, webhooks) feeding into KEDA |
| "ScaledObject" | YAML snippet showing ScaledObject with Prometheus trigger |
| "requests pile up" | Queue growing, KEDA notices, triggers scale-up |
| "adds more replicas" | New inference server pods spinning up, queue draining |
| "scale to zero" | Night time / low traffic, pods scaling down to 0, dollar signs being saved |
| "GPUs take time to initialize" | Pod starting with loading bar, model loading animation (30s, 60s) |
| "stabilization windows" | Graph showing scaling decisions smoothed out over time, not spiky |
| "KEDA with Kueue" | Architecture diagram: Kueue managing jobs, KEDA scaling inference, working together |

## Meme Opportunity
- "You guys scale on CPU?" - Inference server looking at web app
- "Patience" meme for GPU cold start times
