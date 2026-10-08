# 032 - Idea 2c: Your Audit Log Stops at the Shell

_Blog: teleport/audit-logs/how-to-tie-kubernetes-audit-logs-to-individual-engineers.md. Target 40-45 seconds._

## Script

Something got deleted in production. You open the audit log.

There it is: `alice` ran `kubectl exec` into a production pod.

Two problems.

Was it actually Alice? The event records whatever username the API server authenticated. Share a kubeconfig, and Alice and Bob are both `alice`.

Now look at the end of that event. Response code `101`. Switching protocols.

That's the API request finishing and a live stream opening. Everything Alice typed went over that stream. Kubernetes logged that a shell opened, and nothing that happened inside it.

So, one credential per engineer, and check that nothing in the middle swaps their name out.

Then decide what a shell is worth. Alert when one opens, remove `create` on `pods/exec`, or record the session if you need the replay.

Right now your audit log tells you who knocked. Not what they did inside.

## Notes
- The exec event does keep the initial `command=sh` in `requestURI`. It's the typed input afterwards that is invisible.
- Groups are fine for granting permissions. RBAC checks username and groups, so a group binding never replaces the username in the log.
- Watch the audit level: `RequestResponse` on Secrets copies the Secret value straight into the log. Use `Metadata` there.
- Ship audit events somewhere the cluster admins named in them can't edit them.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "Something got deleted" | Production namespace, a deployment vanishing, alert firing |
| "there it is: alice" | Audit JSON line, highlight `"username": "alice"`, `"subresource": "exec"` |
| "was it actually Alice?" | Alice's avatar, then a second avatar sliding in behind it, both feeding the same badge |
| "share a kubeconfig" | One file, two people, one username arriving at the API server |
| "nothing in the middle" | Alice -> proxy / cloud IAM role -> API server, her name dropped on the floor, the middlebox's name arriving instead. Then the fixed version: `user: proxy`, `impersonatedUser: alice` |
| "response code 101" | Zoom hard on `"code": 101` in the JSON |
| "switching protocols" | HTTP request bar ending, a live pipe opening between laptop and pod |
| "everything typed after that" | Terminal typing `echo exec-marker-12345`, characters flowing through the pipe, audit log stays empty |
| "logged that a shell opened" | Split screen: audit log = one line. Shell session = 40 commands |
| "alert on the connection" | Alert card: `alice opened an exec connection to audit/exec-target; response=101` |
| "remove create on pods/exec" | RBAC rule struck through, then `Error from server (Forbidden)` in the terminal |
| "session recorder" | Recorder icon between engineer and cluster, play button, session replaying with the marker visible |
| "who knocked, not what they did" | A door with a visitor log outside it and a blacked-out room behind it |

## Meme Opportunity
- Audit log: "alice opened a shell" / everyone: "and then what?" / audit log: "..."
- CCTV camera pointed at the door, not the room
- "Who did this?" investigation board with every string leading to one sticky note labelled `system:admin`
