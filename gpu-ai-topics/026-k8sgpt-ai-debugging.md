# 026 - K8sGPT for Cluster Debugging

## Script

Your cluster is broken. Instead of reading logs for an hour, just ask AI what's wrong.

K8sGPT scans your Kubernetes cluster for problems and explains them in plain English.

It connects to your cluster, analyzes resources, and identifies issues like failed pods, misconfigured services, or resource problems.

Then it sends that context to an LLM and returns human-readable explanations with suggested fixes.

Install it as a CLI or run it as an operator in your cluster for continuous analysis.

The CLI is simple. Run `k8sgpt analyze` and it lists problems. Add `--explain` and it uses AI to explain each issue.

You can use OpenAI, Azure OpenAI, or local models like Ollama. Keep your cluster data private by running everything locally.

The operator mode is even better. It runs continuously, stores findings as custom resources, and can integrate with alerting.

K8sGPT won't replace your Kubernetes knowledge, but it will help you find problems faster. Think of it as a senior engineer on call 24/7.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "cluster is broken" | Cluster with red warning icons, fire, chaos |
| "reading logs for an hour" | Developer scrolling through endless log lines, tired |
| "ask AI" | Chat interface with cluster question |
| "K8sGPT" | K8sGPT logo appearing |
| "scans your cluster" | Scanner beam going across cluster resources |
| "identifies issues" | Problems being highlighted: failed pod, bad service, resource limit |
| "sends context to LLM" | Cluster data packaged, sent to AI brain icon |
| "human-readable explanations" | AI response: clear explanation with fix suggestion |
| "CLI or operator" | Two deployment options: terminal CLI vs in-cluster operator |
| "k8sgpt analyze" | Terminal showing analyze command output, list of issues |
| "--explain flag" | Same output but now with AI explanations inline |
| "OpenAI, Azure, or Ollama" | Provider logos as backend options |
| "keep data private" | Ollama running locally, data staying in cluster |
| "operator mode" | Operator watching cluster continuously, storing findings |
| "custom resources" | Result CRDs being created with analysis findings |
| "senior engineer on call" | Robot/AI avatar with SRE badge, always available |

## Meme Opportunity
- "Senior engineer at 3am" vs "K8sGPT at 3am" - one tired, one ready
- "I don't always debug clusters, but when I do, I ask AI first"
