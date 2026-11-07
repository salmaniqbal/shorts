# 035 - RBAC Can't Read the Request: Scale to Zero

_Workshop: Break It, Watch It, Fix It (with a little AI help). Body ~38 seconds, plus a 6-second outro. Follows on from 033._

## Script

Your AI agent can't delete deployments. You checked. So you let it scale them, to help during incidents.

Then checkout starts crash-looping. The fastest way to stop a crash loop? Zero replicas. Alert resolved. Checkout gone.

RBAC only checks the verb and the resource. It never reads the request. Scaling to five and scaling to zero look identical.

To check what's inside, you need an admission policy. A ValidatingAdmissionPolicy sees the actual change, so you can say: the agent can scale, but never to zero.

Outside Kubernetes, same idea. Anything you can't undo, the agent proposes and a human approves.

We build these guardrails in our KubeCon workshop, Break It, Watch It, Fix It. Link below.

## On-screen Snippet

```yaml
matchConditions:
- name: is-sre-agent
  expression: >-
    request.userInfo.username ==
    "system:serviceaccount:ai-agents:sre-agent"
validations:
- expression: "has(object.spec.replicas) && object.spec.replicas > 0"
  message: "Scaling to zero needs a human."
```

## Notes
- Full policy for the description or a pinned comment:

```yaml
apiVersion: admissionregistration.k8s.io/v1
kind: ValidatingAdmissionPolicy
metadata:
  name: sre-agent-no-scale-to-zero
spec:
  failurePolicy: Fail
  matchConstraints:
    resourceRules:
    - apiGroups: ["apps"]
      apiVersions: ["v1"]
      operations: ["UPDATE"]
      resources: ["deployments", "deployments/scale", "statefulsets", "statefulsets/scale"]
  matchConditions:
  - name: is-sre-agent
    expression: >-
      request.userInfo.username ==
      "system:serviceaccount:ai-agents:sre-agent"
  validations:
  - expression: "has(object.spec.replicas) && object.spec.replicas > 0"
    message: "Scaling to zero needs a human."
---
apiVersion: admissionregistration.k8s.io/v1
kind: ValidatingAdmissionPolicyBinding
metadata:
  name: sre-agent-no-scale-to-zero
spec:
  policyName: sre-agent-no-scale-to-zero
  validationActions: ["Deny"]
```

- ValidatingAdmissionPolicy is built in and GA since Kubernetes 1.30, so there's nothing extra to install. Kyverno and Gatekeeper can do the same on older clusters.
- The `has()` check matters. The `Scale` object omits `replicas` when it is 0, so `object.spec.replicas > 0` alone would fail with a CEL error rather than your message.
- `kubectl scale` patches the `deployments/scale` subresource, so the agent needs `patch` on `deployments/scale`. Check with `kubectl auth can-i patch deployments --subresource=scale --as=...`.
- Outside Kubernetes the same pattern shows up as `terraform plan` then a human `apply`, approval gates in CI, or making the agent's tool return a proposal instead of running the command.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "can't delete deployments. You checked." | Terminal: `kubectl auth can-i delete deployments --as=$AGENT` -> green `no` ✓ |
| "So you let it scale them" | `kubectl auth can-i patch deployments --subresource=scale --as=$AGENT` -> amber `yes` |
| "to help during incidents" | Text: "Safe, right?" |
| "checkout starts crash-looping" | Three pods flashing red `CrashLoopBackOff`, alert banner "🔥 FIRING · CheckoutCrashLooping" |
| "The fastest way to stop a crash loop?" | Robot thinking, light bulb |
| "Zero replicas" | Agent terminal: `kubectl scale deployment checkout --replicas=0` -> `deployment.apps/checkout scaled`, pods vanish one by one |
| "Alert resolved" | Banner flips green: "✅ RESOLVED" |
| "Checkout gone" | Empty space where the pods were: "0/0 pods". Shop front with a CLOSED sign |
| "RBAC only checks the verb and the resource" | Request card going through an RBAC gate: user ✓, verb `patch` ✓, resource `deployments/scale` ✓ |
| "It never reads the request" | The request body `replicas: ?` greyed out, labelled "not checked" |
| "Scaling to five and scaling to zero look identical" | Two request cards side by side, `replicas: 5` and `replicas: 0`, both stamped ALLOWED |
| "you need an admission policy" | API server pipeline: Authentication -> RBAC -> **Admission** (highlighted, new) -> etcd |
| "sees the actual change" | Admission box opens the request and reads `replicas: 0` |
| "never to zero" | YAML snippet from above, `replicas > 0` highlighted |
| (blocked) | Agent retries `kubectl scale ... --replicas=0` -> red `denied request: Scaling to zero needs a human.` BLOCKED stamp |
| "Outside Kubernetes, same idea" | Examples sliding in: `terraform plan` -> human `apply`, `DROP TABLE` -> sign-off, `git push --force` -> sign-off |
| "the agent proposes and a human approves" | Approval card: "🤖 sre-agent proposes: scale checkout → 0" with [Approve] [Reject]. A cursor clicks Reject |
| "KubeCon workshop" | End card: "Break It," (red) "Watch It," (amber) "Fix It" (green), "(with a little AI help)", "Link below ↓" |

## Meme Opportunity
- "Task failed successfully": alert resolved, checkout gone
- Gru's plan: "Give the agent scale permissions" / "It can't delete anything" / "It scales to zero" / Gru staring
- Monkey's paw: "I wish the CrashLoopBackOff alert would stop firing"
