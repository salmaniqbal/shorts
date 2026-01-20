# 017 - KServe for Model Serving

## Script

Deploying one ML model is easy. Deploying hundreds with canary releases and autoscaling? You need KServe.

KServe is a Kubernetes-native platform for serving machine learning models.

Instead of writing deployments, services, and ingress configs for each model, you create a single InferenceService resource.

KServe handles the rest: it deploys your model, exposes a prediction endpoint, and sets up autoscaling, even scaling to zero.

It supports all major frameworks. TensorFlow, PyTorch, Scikit-learn, XGBoost, and custom containers.

The killer feature? Traffic splitting.

You can run a new model version alongside the old one and gradually shift traffic. Send 10% to the new model, monitor performance, then increase to 100% if it looks good.

If something goes wrong, roll back instantly.

KServe also supports transformers for pre and post-processing, and explainers for model interpretability.

For teams serving multiple models in production, KServe is the standard.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "one model is easy" | Single model box deployed simply |
| "hundreds with canary" | Grid of many models, some with version badges, traffic flowing between versions |
| "KServe" | KServe logo with Kubernetes integration visual |
| "Kubernetes-native platform" | KServe custom resources fitting into Kubernetes ecosystem |
| "InferenceService resource" | YAML snippet showing minimal InferenceService definition |
| "handles the rest" | InferenceService expanding into Deployment, Service, Ingress, HPA automatically |
| "scaling to zero" | Model pods disappearing when idle, reappearing when requests arrive |
| "all major frameworks" | Framework logos: TensorFlow, PyTorch, Scikit-learn, XGBoost appearing in a row |
| "traffic splitting" | Traffic flow diagram: 90% going to v1, 10% going to v2 |
| "gradually shift traffic" | Slider animation moving from 10% to 50% to 100% new version |
| "roll back instantly" | Red alert, traffic immediately shifting back to old version |
| "transformers" | Pipeline visualization: Input -> Transformer -> Model -> Transformer -> Output |
| "explainers" | Model output with explanation overlay (feature importance, SHAP values) |

## Meme Opportunity
- "Look at me, I'm the ML platform now" - KServe
- Canary bird meme for canary deployments
