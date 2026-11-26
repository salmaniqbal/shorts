# 042 · Nobody Wants to Rotate That Key

_Campaign: Digital payments and banking. Blog: https://goteleport.com/blog/certificate-based-authentication-payment-banking/. Format: talking head with graphics. End card: Teleport logo + goteleport.com/use-cases/digital-payments-and-banking._

## Script

Nobody on your team wants to rotate that long-lived credential.

 

You can push a new key to thousands of hosts. But you can't see which pipeline or cron job still needs the old one. Miss one, and you've caused an outage. In payments, there's no room for that.

[Face]
So the key stays, and it keeps working.

The fix isn't better rotation. It's having nothing to rotate.

Teleport replaces static keys with short-lived certificates. Engineers get theirs through SSO. Pipelines get their own machine identity. And they expire on their own.

Every connection gets four checks. Did your certificate authority sign it? Has it expired? Do its roles allow this? Does the client hold the private key? Fail one, and access is denied.

[Face]c
If a build server is compromised, its short-lived certificate soon expires, so the access doesn’t last and nobody has to rotate a thing.

## Notes
- From the blog: keys live in `authorized_keys` files, build-server environment variables and sometimes container images. Config management can push a new key quickly, but it can't reveal what depends on the old one.
- Certificate checks, in order: did the CA sign it, has it expired, do its roles grant access, and does the client hold the matching private key? Any failure rejects the connection.
- Pipelines: `tbot` joins with no pre-shared secret, for example an AWS identity document or a GitHub Actions OIDC token. A CI/CD certificate's validity window can close within minutes of the pipeline stopping renewal.
- Optional extra line, if there's room: "And a stolen certificate fails from a laptop that isn't enrolled." That's Teleport Device Trust, using the TPM or Secure Enclave, and it needs to be turned on, so don't imply it's automatic.
- Engineers never see database passwords: the Database Service presents a Teleport-issued certificate on their behalf.
- PCI DSS is deliberately left out of this script because 043 covers it. The blog cites 8.6.2, 8.6.3 and 10.2, and says its summaries are paraphrases, so check the standard before quoting them on screen.
- The blog has no statistics, so this script doesn't use any. The use-case page says "up to 80%" less time on access troubleshooting and audit prep. That's Teleport's claim, with no source given.
- Customer quote: Bjarne Lamczak, Cloud DevOps Engineer, PPI Financial Services: "We needed secure access that scales with our infrastructure."

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "Nobody on your payments team" | Team round a table, a single key in the middle. Everyone slowly leans back |
| "nobody knows what depends on it" | The key with dozens of faint strings running off screen |
| "push a new key to thousands of hosts" | One key multiplying across a grid of servers, all turning green |
| "which pipeline or cron job" | Zoom out: a pipeline and a `crontab` line still pointing at the old key, in red |
| "Miss one, and you've caused an outage" | Payment terminal: `DECLINED`. Dashboard turning red |
| "no room for that" | Availability counter: 99.999%, shaking |
| "the key stays, and it keeps working" | Old key back on the table, sticky note: "do not touch" |
| "nothing to rotate" | The key dissolves. The table's empty |
| "short-lived certificates" | Certificate card with a countdown timer |
| "Engineers get theirs through SSO" | SSO login, certificate issued with the engineer's name |
| "Pipelines get their own machine identity" | CI job gets its own certificate, badge reads `pipeline: deploy-payments` |
| "they expire on their own" | Timers reach zero, certificates fade, no one touches anything |
| "four checks" | Certificate passes four gates, ticking each: SIGNED, NOT EXPIRED, ROLE OK, KEY MATCHES |
| "Fail one, and it's refused" | A certificate with an old date stopped at gate two, red `connection refused` |
| "a compromised build server" | Attacker opens a build server and finds one certificate, already greyed out and stamped EXPIRED |
| "nobody has to rotate a thing" | Team round the same table, relaxed, the sticky note gone |
| End card | Teleport logo + goteleport.com/use-cases/digital-payments-and-banking |

## Meme Opportunity
- This is fine dog, sitting next to a key labelled `prod_2019.pem`
- Bomb disposal scene: red wire, blue wire, `id_rsa`
- "If it works, don't touch it" tattooed on a platform engineer
