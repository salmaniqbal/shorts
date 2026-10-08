# 030 - Idea 2a: You Can't Revoke a Kubeconfig

_Blog: teleport/kubeconfigs/how-to-eliminate-shared-production-kubeconfigs.md. Target 40-45 seconds._

## Script

Someone leaves the team. You need to kill their production access.

They have a copy of the kubeconfig. And Kubernetes has no revoke button.

Open the file. `client-certificate-data`. That isn't a pointer to a credential, that is the credential. The API server reads the name straight out of it.

So delete the CertificateSigningRequest.

Nothing happens. The certificate keeps working until it expires. Kubernetes never kept a revocation list.

And if it says `system:masters`, RBAC doesn't even apply. Wait for expiry, or rotate the cluster CA and restart everything.

So stop putting the secret in the file. Point kubectl at your company SSO and let it fetch a fresh, short-lived credential each time it runs.

Then offboarding is switching off one account. Not a CA rotation at two in the morning.

If a kubeconfig holds a certificate or a token, the whole file is a production credential.

## Notes
- `system:masters` bypasses RBAC and webhook authorization entirely, which is why the "just fix it with RBAC" answer fails.
- ServiceAccount tokens are no better: deleting and recreating the ServiceAccount changes its UID and kills every copy at once, after roughly a ten-second cache delay.
- The real fix is the `exec` field plus SSO, which is covered in 031.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "Someone leaves the team" | Leaving-do card, laptop being handed back, kubeconfig file quietly still on a USB stick |
| "no revoke button" | Big red REVOKE button, hover, it fades out and disappears |
| "open the file" | `cat ~/.kube/config`, zoom on `client-certificate-data: LS0tLS1CRUdJTi...` |
| "that is the credential" | The base64 blob morphing into a key |
| "common name as username" | `openssl x509` output: `subject=O=system:masters, CN=system:admin` -> arrows to Username and Groups boxes |
| "copy the file, copy the identity" | File duplicated 3x, all three authenticate as the same badge |
| "delete the CSR" | `kubectl delete csr alice-rbac` -> "deleted" -> cut to cert still glowing green |
| "keeps authenticating" | `kubectl auth whoami` -> `alice`. Big X over a "revoked" stamp |
| "no revocation list" | Empty list / filing cabinet with nothing in it |
| "system:masters" | RBAC shield in front of API server, cert walks straight through it |
| "rotate the cluster CA" | `k3s certificate rotate-ca`, then every node, kubelet and kube-proxy flashing "restart required" |
| "treat it like one" | kubeconfig file wrapped in a vault door with a password label |

## Meme Opportunity
- "Delete the CSR" / certificate: "and I took that personally"
- This is fine dog, sitting in a room labelled `system:masters`
- "It's not a config file" / "It IS the config file" / zoom: "It's a password"
