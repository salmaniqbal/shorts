# 031 - Idea 2b: One Token, Three Clusters

_Blog: teleport/sso/sso-backed-kubectl-access-across-many-clusters.md. Target 40-45 seconds._

## Script

You wired dev, staging and production up to company SSO. Nice.

You also made one cached token work on all three.

When Alice runs kubectl, the API server checks the token first. Signed by an issuer I trust, for an audience I accept? That gives it a username. Then RBAC decides what she can do.

So production denies her. But read the error: "User alice@example.com cannot list pods."

Production recognised her. It accepted a development token, then refused on permissions. That token was valid everywhere, because all three clusters accept the same `aud`.

Fix that in the authentication config. Dev and staging accept `kubectl-nonproduction`. Production accepts only `kubectl-production`. Now a leaked non-prod token gets `401` before RBAC ever runs.

Test every token twice. Once where it must work, once where it must fail.

## Notes
- `iss` = who issued the token, `aud` = which client it was made for, `email` = the claim mapped to the Kubernetes username.
- Each extra audience costs one more client ID, one more kubeconfig user entry and one more cached token on the workstation.
- When merging kubeconfigs, give each client ID a unique user name. Two files both calling their user `oidc` will silently collapse into one entry.
- OIDC tokens still can't be revoked individually. Token lifetime is your real offboarding delay.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "dev, staging and production" | Three cluster boxes, all three wiring into one SSO logo |
| "one cached token works on all three" | Single token key unlocking three padlocks in sequence |
| "checks the token first" | Pipeline: request -> [Authentication] -> [RBAC] -> response, first box lighting up |
| "is this signed by an issuer I trust" | JWT expanded, highlight `iss` and `aud`, green tick on signature check |
| "that gives it a username" | `email: alice@example.com` claim -> user badge `alice@example.com` |
| "then RBAC decides" | RBAC table per cluster: dev = read/write, staging = read, prod = none |
| "watch the error" | Terminal: `Error from server (Forbidden): pods is forbidden: User "alice@example.com"...` zoom on the username |
| "production recognised her" | 403 badge, caption "authenticated, then denied" |
| "same aud value" | Three API servers, all showing `audiences: [kubectl-all-clusters]` highlighted in red |
| "fix it in the auth config" | AuthenticationConfiguration YAML, the `audiences` list changing per cluster |
| "dev and staging accept nonproduction" | Two clusters accept the blue token, production greys out |
| "401 before RBAC" | Request hits authentication, bounces off with 401, RBAC box never lights up |
| "test every token twice" | Split screen: same token, green 200 against staging, red 401 against production |

## Meme Opportunity
- "We have SSO" / "SSO at home" with one shared audience
- Master key meme: janitor opening the server room labelled PRODUCTION
- Two buttons sweating: "one kubeconfig for everything" / "actually revoke prod access"
