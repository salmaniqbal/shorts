# 029 - Idea 1: The One-Short Version (covers all three blogs)

_Covers: shared kubeconfigs + SSO across clusters + audit log attribution. Beginner-friendly. Body 40-45 seconds, plus a 10-second outro._

## Script

Someone on your team needs access to Kubernetes, so you send them your kubeconfig. Quick fix, right?

But if that file contains your client certificate and private key, you’ve just given them your identity. Their commands now run as you.

Now imagine that file gets passed around the team, and a week later someone deletes a production namespace. You check the audit log, and it points to you, because everyone was using your credentials.

Then someone leaves the team, still holding a copy. You can’t revoke just their copy of that shared certificate.

That’s why access should start with each person signing in through company SSO, rather than someone sending them a file.

Teleport makes that work for Kubernetes. Each engineer signs in, gets their own short-lived certificate, and their roles determine which clusters they can access. So access is individual, and actions are traceable.

Daniele’s written up how it works. Check out the link below.




## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "needs access to Kubernetes" | New starter at a desk, `kubectl get pods` -> `error: You must be logged in to the server` |
| "you send them your kubeconfig" | Slack DM: "here you go 👍" with `config` attached, file sliding from your laptop to theirs |
| "Quick fix, right?" | Green tick stamp that flickers and turns amber |
| "your client certificate and private key" | `cat ~/.kube/config`, camera pushes in on `client-certificate-data` and `client-key-data`, both blobs glowing red |
| "you've just given them your identity" | The blob unfolds into a name badge with YOUR name on it, a hand passes it across the desk |
| "their commands now run as you" | Their terminal: `kubectl auth whoami` -> your username. Request travels to the API server wearing your badge |
| "gets passed around the team" | The DM forwarded, then forwarded again. Five laptops, five identical badges |
| "deletes a production namespace" | `kubectl delete ns production`, dashboard going red, alerts firing |
| "you check the audit log" | Audit JSON scrolling past, `"verb": "delete"`, `"namespace": "production"` |
| "it points to you" | Hard zoom on `"username"` — it's your name. Every line the same. Five avatars behind it collapsing into one |
| "someone leaves the team" | Leaving card and a returned work laptop, while the kubeconfig sits on a personal machine in the corner of frame |
| "can't revoke just their copy" | Five copies of the file. One gets struck through, the other four stay green. REVOKE button greyed out |
| "signing in through company SSO" | SSO login screen, five people signing in one after another, five different badges |
| "rather than someone sending them a file" | The opening Slack DM reappears and is crossed out |
| "Teleport makes that work" | Teleport logo. Engineer -> SSO -> Teleport proxy -> cluster |
| "their own short-lived certificate" | Certificate badge with a countdown timer, expiring, then reissued at next login |
| "roles determine which clusters" | Role card on the left, three cluster doors on the right: dev open, staging open, production locked |
| "access is individual" | Five engineers, five distinct badges, five separate arrows into the cluster |
| "actions are traceable" | The same audit log from earlier, replayed — but now every line carries a different, real name |
| "link below" | Blog card with Daniele's name, arrow pointing down to the description |

## Meme Opportunity
- Office key on a giant wooden fob labelled PRODUCTION
- Spider-Man pointing meme: five engineers pointing at each other, all wearing the same name badge
- CCTV footage of the door, and the room behind it blacked out
