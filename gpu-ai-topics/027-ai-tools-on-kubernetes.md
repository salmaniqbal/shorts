# 027 - Famous AI Tools That Run on Kubernetes

## Script

Want to run AI at scale? These tools were built for Kubernetes.

Let's start with training. Kubeflow is the OG ML platform. Pipelines, notebooks, training operators, it's got everything. But it's complex, so many teams pick just the pieces they need.

MLflow handles experiment tracking and model registry. Run your training anywhere, but track metrics, compare runs, and version models in one place.

For serving, we've got options. Triton Inference Server from NVIDIA handles multiple models and frameworks with serious GPU optimization. KServe wraps it all in Kubernetes-native resources with autoscaling and canary deployments.

vLLM and Text Generation Inference are the LLM specialists. PagedAttention, continuous batching, blazing fast token generation.

Ray and Spark run distributed workloads. Training across hundreds of GPUs or processing petabytes of data.

Weights & Biases and Neptune track your experiments with slick dashboards and team collaboration.

And Airflow or Argo Workflows orchestrate it all, chaining data prep, training, evaluation, and deployment into repeatable pipelines.

The Kubernetes AI ecosystem is massive. Pick the tools that fit your workflow.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "AI at scale" | Large cluster with many GPU nodes, AI workloads flowing through |
| "Kubeflow" | Kubeflow logo, showing components: Pipelines, Notebooks, Training Operators |
| "OG ML platform" | Timeline showing Kubeflow as early Kubernetes ML solution |
| "complex" | Kubeflow architecture diagram with many components, slightly overwhelming |
| "pick pieces they need" | Cherry-picking specific Kubeflow components (just Pipelines, just KFServing) |
| "MLflow" | MLflow logo, experiment tracking dashboard with metrics graphs |
| "track metrics, compare runs" | Side-by-side run comparison, accuracy curves overlaid |
| "version models" | Model registry showing v1, v2, v3 with metadata |
| "Triton Inference Server" | NVIDIA Triton logo, multiple model formats (PyTorch, TensorFlow, ONNX) loading |
| "GPU optimization" | Triton batching requests, maximizing GPU utilization meter |
| "KServe wraps it" | KServe InferenceService YAML creating Triton deployment automatically |
| "vLLM and TGI" | vLLM and HuggingFace TGI logos side by side |
| "PagedAttention, continuous batching" | Memory pages being efficiently managed, requests streaming through |
| "Ray and Spark" | Ray and Spark logos, distributed nodes processing in parallel |
| "hundreds of GPUs" | Large GPU grid with training job distributed across all |
| "petabytes of data" | Data lake icon with massive scale indicator |
| "Weights & Biases, Neptune" | W&B and Neptune dashboards showing experiment comparisons |
| "team collaboration" | Multiple users viewing shared experiment results |
| "Airflow or Argo" | Airflow and Argo logos, DAG visualization showing pipeline stages |
| "repeatable pipelines" | Pipeline: Data Prep -> Train -> Evaluate -> Deploy, looping |
| "ecosystem is massive" | Logo cloud of all mentioned tools orbiting Kubernetes |

## Tools Mentioned

| Tool | Category | Key Feature |
|------|----------|-------------|
| Kubeflow | ML Platform | End-to-end ML on Kubernetes |
| MLflow | Experiment Tracking | Model registry & metrics |
| Triton Inference Server | Model Serving | Multi-framework GPU inference |
| KServe | Model Serving | Kubernetes-native serving |
| vLLM | LLM Inference | PagedAttention for LLMs |
| Text Generation Inference | LLM Inference | HuggingFace's LLM server |
| Ray | Distributed Compute | Distributed training & serving |
| Apache Spark | Data Processing | Large-scale data pipelines |
| Weights & Biases | Experiment Tracking | Collaborative ML tracking |
| Neptune | Experiment Tracking | Metadata & experiment store |
| Apache Airflow | Orchestration | Workflow scheduling |
| Argo Workflows | Orchestration | Kubernetes-native pipelines |

## Meme Opportunity
- "One does not simply choose an ML platform" with all the logos
- "They're all good tools, Brent" with overwhelmed engineer looking at options
- XKCD "standards" meme but with ML platforms
