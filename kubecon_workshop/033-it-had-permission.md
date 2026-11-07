# 033 - It Had Permission: Reads Are Free, Deletes Need a Human

_Workshop: Break It, Watch It, Fix It (with a little AI help). Body ~46 seconds, plus a 6-second outro. Over the 45-second target, under 60. If it needs trimming, cut the "Agents don't get nervous" line first._

## Script

I asked an AI agent to investigate my cluster. It deleted a deployment. I never asked it to.

It wasn't hacked. It had permission, so it used it.

Agents don't get nervous. Delete is just another tool that makes the error go away.

So split it. Reading is free. Deleting needs a human.

Reading: give the agent its own service account, bound to the built-in `view` role. Pods, logs, events. No Secrets.

Deleting: add an admission policy that rejects the agent's delete unless a human has marked that deployment as approved.

And with no patch permission, the agent can't approve itself. Check it: `kubectl auth can-i patch deployments`, as the agent. You want "no".

Outside Kubernetes, same split. Reads run freely. Anything destructive waits for a human.

We break this on purpose in our KubeCon workshop, Break It, Watch It, Fix It. Link below.

## On-screen Snippet

```bash
# The human approves
kubectl annotate deployment checkout ops.example.com/delete-approved=true

# The agent can't approve itself
kubectl auth can-i patch deployments \
  --as=system:serviceaccount:ai-agents:sre-agent
no
```

## Notes
- The agent gets three things:
  1. **Read:** the built-in `view` ClusterRole.
  2. **Delete:** a small extra role with `delete` on deployments only. No `patch`, `update` or `deletecollection`.
  3. **The gate:** an admission policy so that delete only works after a human has approved it.

```bash
kubectl create serviceaccount sre-agent -n ai-agents

kubectl create clusterrolebinding sre-agent-view \
  --clusterrole=view --serviceaccount=ai-agents:sre-agent

kubectl create clusterrole sre-agent-delete \
  --verb=delete --resource=deployments.apps
kubectl create clusterrolebinding sre-agent-delete \
  --clusterrole=sre-agent-delete --serviceaccount=ai-agents:sre-agent
```

```yaml
apiVersion: admissionregistration.k8s.io/v1
kind: ValidatingAdmissionPolicy
metadata:
  name: sre-agent-delete-needs-approval
spec:
  failurePolicy: Fail
  matchConstraints:
    resourceRules:
    - apiGroups: ["apps"]
      apiVersions: ["v1"]
      operations: ["DELETE"]
      resources: ["deployments"]
  matchConditions:
  - name: is-sre-agent
    expression: >-
      request.userInfo.username ==
      "system:serviceaccount:ai-agents:sre-agent"
  validations:
  - expression: >-
      has(oldObject.metadata.annotations) &&
      'ops.example.com/delete-approved' in oldObject.metadata.annotations &&
      oldObject.metadata.annotations['ops.example.com/delete-approved'] == 'true'
    message: "Deleting needs a human to approve it first."
---
apiVersion: admissionregistration.k8s.io/v1
kind: ValidatingAdmissionPolicyBinding
metadata:
  name: sre-agent-delete-needs-approval
spec:
  policyName: sre-agent-delete-needs-approval
  validationActions: ["Deny"]
```

- On a DELETE request, `object` is null and `oldObject` is the deployment being deleted. That's why the policy reads the annotation from `oldObject`.
- The approval is safe only because the agent can't `patch` or `update` deployments. Give it either and it can annotate the deployment and approve itself. That is the `can-i` check in the script.
- `kubectl auth can-i delete deployments` as the agent now says `yes`. `can-i` only checks RBAC, never admission policies. Test the gate itself by running the delete as the agent before and after approving.
- The built-in `view` role deliberately excludes Secrets, `pods/exec`, Roles and RoleBindings. It can still read ConfigMaps and pod logs. If credentials leak into either, the agent sees them, and so does the LLM provider it sends context to.
- ValidatingAdmissionPolicy is built in and GA from Kubernetes 1.30. On older clusters, Kyverno or Gatekeeper can enforce the same rule.
- Outside Kubernetes, the same split usually lives in the agent's tool layer: read-only tools run automatically and destructive tools ask for confirmation. Keep a check in the cluster as well, because the agent's own config can be changed or misconfigured.
- 035 builds on this: RBAC lets an agent `patch`, and it scales a deployment to zero. Its opening line ("can't delete deployments, you checked") needs a tweak to match: "can't delete without approval".

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "I asked an AI agent to investigate" | Chat UI: "Can you investigate why checkout is failing?" Robot replies "On it 👍" |
| "It deleted a deployment" | Agent terminal types `kubectl delete deployment checkout` -> `deployment.apps "checkout" deleted` in red |
| "I never asked it to" | 😬 face, zoom on the chat where it clearly says *investigate* |
| "It wasn't hacked" | Word "Hacked?" with a red line struck through it |
| "It had permission" | ClusterRole YAML: `apiGroups: ["*"]`, `resources: ["*"]`, `verbs: ["*"]`, each wildcard glowing red |
| "Agents don't get nervous" | Robot calmly sipping tea next to a big red DELETE button |
| "makes the error go away" | Error rate drops to 0% ✅ ... pan right: there's no app left |
| "So split it" | Screen splits in two: left side green "READ · free", right side amber "DELETE · needs a human" |
| "Reading: its own service account" | Left side: `ServiceAccount: sre-agent` -> binding arrow -> `ClusterRole: view` |
| "Pods, logs, events. No Secrets." | Ticks for pods, logs, events. Secrets in a locked box with ✗ |
| "Deleting: add an admission policy" | API server pipeline: RBAC ✓ -> **Admission policy** (highlighted) -> etcd |
| "rejects the agent's delete" | Agent runs `kubectl delete deployment checkout` -> red `denied request: Deleting needs a human to approve it first.` |
| "unless a human has marked it approved" | Human runs `kubectl annotate deployment checkout ops.example.com/delete-approved=true`, a green APPROVED tag snaps onto the deployment |
| (approved delete) | Agent retries the delete -> goes through. Small caption: "approved by a human" |
| "no patch permission" | Robot trying to stick the APPROVED tag on itself, bounced off |
| "can't approve itself" | Terminal: `kubectl auth can-i patch deployments --as=...sre-agent` |
| "You want no" | Big green `no`, then a GOOD stamp |
| "Outside Kubernetes, same split" | Agent tool list: `read_logs`, `query_metrics`, `list_files` running automatically; `delete_bucket`, `DROP TABLE`, `git push --force` each with a "Waiting for approval" badge |
| "waits for a human" | Approval pop-up with [Approve] [Reject], cursor hovering |
| "KubeCon workshop" | End card: "Break It," (red) "Watch It," (amber) "Fix It" (green), "(with a little AI help)", "Link below ↓" |

## Meme Opportunity
- "I'm in danger" Ralph Wiggum, with the robot holding `verbs: ["*"]`
- Agent: "You asked me to fix the errors." / "There are no errors." / "There is no app."
- Drake meme: rejecting `cluster-admin` for the agent, approving "`view` + delete with sign-off"
- Robot trying to sign its own permission slip
