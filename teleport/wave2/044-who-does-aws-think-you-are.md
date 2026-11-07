# 044 · Who Does AWS Think You Are?

_Campaign: AI builders. Blog: https://goteleport.com/blog/ai-agents-aws-agentcore/. Format: screen share with graphics. End card: Teleport logo + goteleport.com/use-cases/ai-builders._

## Script

An AI agent just changed an order. CloudTrail says it was agentcore-bot.

Which human asked? AWS can't tell you.

Everyone's agent runs under one shared role. So you over-provision it, or you break it for your power users. And when someone leaves, those tools keep working for anyone using the same agent.

The fix is carrying the person's identity all the way through.

With Teleport, you log in once, and every tool call carries a short-lived signed token with your identity and roles.

The gateway checks it first. Expired, forged, or missing the right role? The call never reaches your tool.

And they're the same roles you already use for SSH, databases and Kubernetes. No second RBAC system to maintain.

Alice asks to update order 42. Denied. Bob asks. Allowed, and the audit trail shows Bob.

Same agent, same request. Different person, different answer.

## Notes
- This is built on Amazon Bedrock AgentCore. `agentcore-bot` is the blog's example of what CloudTrail shows ("something like `agentcore-bot`"), so treat it as illustrative, not a literal default name.
- The chain, from the blog: `tsh login` and `tsh mcp connect` → Teleport issues a signed JWT → AgentCore validates it → an interceptor Lambda injects the identity into the tool arguments → Amazon Verified Permissions checks Cedar policies → the tool runs scoped to that person.
- A denied call never reaches the Lambda. In the blog, Alice has `mcp-user` and gets a 403. Bob has `order-admin` and the update goes through.
- **Check with Teleport:** the blog says "CloudTrail records Bob's identity" but doesn't explain how, and it describes the identity reaching the Lambda as function parameters. So the script says "the audit trail shows Bob" instead, which also covers Teleport's session logs and the authorisation logs. If Teleport confirms the CloudTrail detail, "and CloudTrail shows Bob" makes a stronger payoff.
- The Teleport roles that control SSH, database and Kubernetes access also control agent tool access, so there's no second RBAC system to maintain.
- Part 1 of the series, https://goteleport.com/blog/your-ai-agent-needs-to-know-who-you-are/, has a good before and after for the audit log: "`update_order_tool` executed at 2:34 PM" becomes "User alice@goteleport.com updated order #42 to 'shipped'".
- Stat for a pinned comment, from Teleport's 2026 Infrastructure Identity Survey: 70% of organisations give their AI systems more access than a human in the same role.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "An AI agent just changed an order" | Chat: "Update order 42 to shipped." Agent replies "Done ✓" |
| "CloudTrail says it was agentcore-bot" | CloudTrail event, hard zoom on the identity field: `agentcore-bot` |
| "Which human asked?" | Three people on screen, all silhouettes, one question mark |
| "one shared role" | Three people's requests all funnel into a single IAM role badge |
| "over-provision it, or you break it" | A slider: too far right, everything's unlocked. Too far left, a power user gets an error |
| "when someone leaves" | A leaving card. The person's gone, but the tool still shows a green "running" light |
| "carrying the person's identity all the way through" | A name badge travels along the chain: login → agent → gateway → tool |
| "you log in once" | Terminal: `tsh login`, then `tsh mcp connect` |
| "short-lived signed token" | Token card opens: `sub: alice`, `roles: mcp-user`, `exp: 1h` |
| "The gateway checks it first" | Three bad tokens bounce off a gate: EXPIRED, FORGED, WRONG ROLE. The tool behind it stays dark |
| "the same roles you already use" | One role card connected to four icons: SSH, database, Kubernetes, AI tools |
| "Alice asks to update order 42. Denied." | Alice's request hits a gate: `403`, in red. The tool never runs |
| "Bob asks. Allowed" | Bob's token has `order-admin`. Gate opens, order updates |
| "the audit trail shows Bob" | Log line appears with Bob's name in place of `agentcore-bot` |
| "Same agent, same request" | Split screen, Alice and Bob, the identical prompt |
| "Different person, different answer" | Red 403 on one side, green tick on the other |
| End card | Teleport logo + goteleport.com/use-cases/ai-builders |

## Meme Opportunity
- Spider-Man pointing: Alice, Bob and the agent, all wearing the same `agentcore-bot` badge
- "I am Spartacus" but everyone's saying `agentcore-bot`
- CloudTrail as a detective: "The suspect is... a Lambda"
