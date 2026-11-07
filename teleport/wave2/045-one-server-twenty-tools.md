# 045 · One MCP Server, 20 Tools

_Campaign: AI builders. Blog: https://goteleport.com/blog/complicating-mcp-enterprise/. Format: animated explainer. End card: Teleport logo + goteleport.com/use-cases/ai-builders._

## Script

Your agent connected to one MCP server. It just got 20 tools.

OAuth scopes authorise access to the server, not to each tool inside it.

And OAuth assumes a human reads a consent screen. With MCP, an LLM decides which scopes it needs at runtime.

So don't let the model decide. Put the policy in front of the server.

Teleport sits in front of your MCP servers as a proxy, so your client never negotiates OAuth with the server at all. Agents get short-lived certificates, with no shared secrets.

New servers start with nothing callable. Allow read tools, and your agent can read. If the model asks for `slack_post_message`, it's denied unless a role says yes. The decision rests on identity, not on what the model asks for.

And every call is logged: who, which tool, and the decision.

## Notes
- The blog's exact lines: "OAuth scopes authorize access to the MCP server, not to individual tools within it." and "In an enterprise with MCP servers exposing 20+ tools, this is way too coarse."
- **Check before this runs as an ad:** the blog is from March 2026 and there has been a newer MCP spec revision since (2026-07-28, as described by secondary sources). Those sources suggest scopes are still the spec's only permission vocabulary, so per-tool decisions still need a separate enforcement point, but I couldn't confirm that against the spec itself. Ask Teleport to check it against the current spec.
- Some servers and gateways do add their own per-tool checks, so the script doesn't say every setup is exposed. Avoid "anyone can call anything" as a blanket claim.
- How Teleport does it, from the blog: MCP servers register as Teleport applications, and two tiers of RBAC control which servers a user can reach and which tools they can invoke (names, globs like `read_*`, or regex).
- The decision rests on cryptographic identity, not on what the LLM asks for: "Even if a model requests `slack_post_message`, the request is denied unless the role policy explicitly permits it."
- Each JSON-RPC request is logged with tool name, input parameters, client identity, authorisation decision, timestamp and session context.
- Stats for a pinned comment. "492 MCP servers were found on the open internet with zero auth" comes from Doyensec research that Teleport sponsored, so credit it that way. Five of the ten risks in the OWASP MCP Top 10 relate to authentication and authorisation.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "Your agent connected to one MCP server" | Robot plugs a single cable into a server box |
| "It just got 20 tools" | The box bursts open. 20 tool icons fan out around the robot |
| "access to the server, not to each tool" | One big key labelled SCOPE unlocking the whole box, every tool lit up |
| "a human reads a consent screen" | Classic OAuth consent dialog, a person thoughtfully clicking Allow |
| "an LLM decides which scopes it needs" | The person's replaced by the robot, ticking every box without reading |
| "don't let the model decide" | A hand stops the robot's hand mid-click |
| "Put the policy in front of the server" | A gate slides in between the robot and the server |
| "sits in front of your MCP servers as a proxy" | Gate gets the Teleport mark, with several servers behind it |
| "never negotiates OAuth" | The consent screen from earlier folds away. Certificate badge with a rotating timer appears on the robot |
| "nothing callable" | All 20 tool icons go dark |
| "Allow read tools" | `read_*` typed into a role. The read tools light up green |
| "slack_post_message" | Robot reaches for the Slack tool. Red DENIED stamp |
| "unless a role says yes" | Role card, with the Slack tool line missing |
| "rests on identity" | Robot shouting its request at the gate. The gate only looks at the badge |
| "who, which tool, and the decision" | Log entries scroll past: `alice`, `read_orders`, `allow`, then `alice`, `slack_post_message`, `deny` |
| End card | Teleport logo + goteleport.com/use-cases/ai-builders |

## Meme Opportunity
- Oprah: "You get a tool! You get a tool! Everybody gets a tool!"
- Robot at a consent screen: "I have read and agree to the terms" in 0.2 seconds
- Kid in a sweet shop labelled "LLM with server-wide scope"
