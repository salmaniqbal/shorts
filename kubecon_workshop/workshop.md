Break It, Watch It, Fix It (with a little AI help)
A hands-on workshop on Kubernetes observability and AI SRE agents
The Pitch
Attendees deploy a deliberately broken microservices application, instrument it, diagnose failures, and use an AI SRE agent running inside the cluster to investigate and respond.
This is a practical, hype-free workshop exploring what AI agents can do, where they fail, and why permissions and guardrails matter.
Format (2 Hours)
Introduction and setup
Deploy a local Kubernetes cluster or use a provided environment
Complete progressive hands-on exercises
Discuss agent permissions, safety, and governance
Attendees provide their own laptop and AI subscription.
Exercises
Deploy microservices with configurable errors and latency (with pre-provided YAML)
Instrument the application with metrics, dashboards, and traces.(with pre-provided YAML)
Ask an LLM to diagnose issues using telemetry.
Deploy an in-cluster AI SRE agent and observe its response.
Design safe RBAC permissions and operational guardrails.
Each stage provides standalone value, so attendees benefit even if they do not finish every exercise.
Why KubeCon?
Fully hands-on and reusable after the workshop.
Teaches practical observability and debugging skills.
Explores AI agents through real cluster interaction.


Linked in Post 

I asked an AI agent to investigate a problem in my Kubernetes cluster. It deleted a deployment. I hadn’t asked it to. 😬

The agent had permission to delete it. That doesn’t mean it should have.

At our KubeCon workshop, **Break It, Watch It, Fix It (with a little AI help)**, we’ll deploy an AI SRE agent, use telemetry to debug a broken app, and show you how to limit what it can do with Kubernetes RBAC and guardrails around destructive actions.

Bring your laptop. Let’s make those mistakes in a workshop before they happen in production.