# 025 - GPU Memory Management

## Hook
Your GPU training job crashed with OOM. But you requested 80GB of GPU memory. What happened?

## Script

Your GPU training job crashed with OOM. But you requested 80GB of GPU memory. What happened?

Here's the thing: Kubernetes doesn't manage GPU memory like CPU or RAM. When you request a GPU, you get the whole card. Memory management is up to your application.

GPU memory fills up fast. Your model weights, optimizer states, activations, and gradients all compete for space.

PyTorch, by default, caches allocated memory even after tensors are deleted. This prevents reuse by other processes and can look like a memory leak.

To debug, use nvidia-smi to see actual usage, or tools like `torch.cuda.memory_summary()` for detailed breakdowns.

Common fixes? Enable gradient checkpointing to trade compute for memory. Use mixed precision training to halve memory for weights and activations. Reduce batch size if needed.

For inference, memory fragmentation is the killer. Long-running servers accumulate fragments that can't be reclaimed. Consider periodic restarts or use vLLM's PagedAttention.

Right-size your GPU requests. Don't request an 80GB A100 if 24GB will do. Your cluster and your budget will thank you.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "crashed with OOM" | Pod with skull icon, OOM error message |
| "requested 80GB" | YAML showing GPU request, but still crashed |
| "Kubernetes doesn't manage GPU memory" | Kubernetes logo with hands up, GPU memory bar unmanaged |
| "whole card" | GPU assigned to pod, entire memory bar now pod's responsibility |
| "memory fills up fast" | GPU memory bar filling: model (blue), optimizer (green), activations (yellow), gradients (red) |
| "compete for space" | Components pushing against each other in memory bar |
| "PyTorch caches memory" | Memory allocated, tensor deleted, memory still cached (yellow striped) |
| "can look like a memory leak" | Memory graph showing usage staying high even after work done |
| "nvidia-smi" | Terminal showing nvidia-smi output with memory stats |
| "torch.cuda.memory_summary()" | Detailed memory breakdown output |
| "gradient checkpointing" | Memory reduced, compute graph recalculated during backward pass |
| "mixed precision" | FP32 blocks shrinking to FP16, half the size |
| "reduce batch size" | Batch size slider going down, memory usage dropping |
| "fragmentation" | Memory bar with gaps/fragments that can't be filled |
| "vLLM PagedAttention" | PagedAttention organizing memory efficiently into pages |
| "Right-size requests" | A100 80GB crossed out, A10 24GB checkmarked for smaller workload |

## Meme Opportunity
- "Where did my GPU memory go?" pie chart meme
- "I have 80GB" / "Best I can do is OOM" Pawn Stars meme
