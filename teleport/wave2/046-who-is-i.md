# 046 · Your Agent Doesn't Know Who "I" Is

_Campaign: AI builders. Blog: https://goteleport.com/blog/your-ai-agent-needs-to-know-who-you-are/. Format: screen share with graphics. End card: Teleport logo + goteleport.com/use-cases/ai-builders._

## Script

Ask your AI agent: what have I been working on?

It has no idea who "I" is.

The tool behind it sees the agent, not you. So it returns nothing, everyone's data, or asks for an email anyone could fake.

And your audit log just says a tool ran at 2:34.

Don't build a new user database. Use the identity you've already got.

With Teleport, you log in through your existing SSO, and every tool call carries a short-lived, signed token. The tool checks it, and knows it's you. The token's locked to one gateway, and it expires, typically within the hour.

Now Alice sees her orders, and an admin sees them all. You change permissions in Teleport, not in tool code.

And your log says Alice updated order 42.

And when Alice leaves, her access to servers, databases and AI tools goes at once.

## Notes
- The blog's lines: "When your AI agent calls an MCP tool, that tool has no idea who actually triggered the request. It sees the agent, not you."
- The three failure modes are the blog's own: the tool "returns nothing, returns everything (leaking data across users), or requires the user to manually pass their own email as an argument, which any user could fake."
- This is the general version of the idea, for any MCP tool. 044 is the AWS-specific version, so don't run them back to back in the same campaign without varying the Alice example.
- The audit log before and after, from the blog: "`update_order_tool` executed at 2:34 PM." becomes "2:34 PM - User alice@goteleport.com updated order #42 to 'shipped'".
- The flow: `tsh login`, then `tsh mcp connect`. The JWT is attached as a Bearer token on every call. The MCP server checks signature, audience, expiry and roles against Teleport's public keys. The blog says "No user database is needed on the MCP side."
- The token: `sub` (who), `roles` (what they can do), `aud` (locks it to one MCP gateway so it can't be replayed elsewhere) and `exp` (typically one hour).
- Once a tool knows who's asking, it can filter by person: an admin sees any order, and everyone else sees only their own. Changing permissions happens in Teleport, not in tool code.
- "Goes at once" is the blog's claim: "When someone leaves the company, their access to servers, databases, and AI tools is revoked simultaneously."
- There's working code in the `gravitational/rev-tech` GitHub repo. It's a good pinned comment for a technical audience.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "what have I been working on?" | Chat window, the question being typed |
| "no idea who "I" is" | Zoom on the word "I", which turns into a question mark |
| "sees the agent, not you" | Person hands a request to a robot. The tool only sees the robot, and the person fades out |
| "returns nothing" | Tool result: `[]` |
| "or everyone's data" | Result floods with other people's rows, in red |
| "an email anyone could fake" | Form field: someone types `ceo@company.com`, and it's accepted |
| "a tool ran at 2:34" | Log line: `update_order_tool executed at 2:34 PM` |
| "a new user database" | A fresh database icon appears, and gets crossed out |
| "the identity you've already got" | Your existing SSO login screen |
| "every tool call carries a short-lived, signed token" | Token attached to each request as it leaves, with a small countdown |
| "The tool checks it" | Tool inspects the signature: ✓ signature, ✓ audience, ✓ expiry, ✓ roles |
| "knows it's you" | Tool's display changes from "agent" to "Alice" |
| "locked to one gateway" | Token tries a second gateway and bounces off. Its countdown keeps running |
| "Alice sees her orders, and an admin sees them all" | Split screen: Alice's list shows three orders, the admin's shows hundreds |
| "in Teleport, not in tool code" | A role card changes. The tool's code stays untouched |
| "Alice updated order 42" | Log line rewrites itself: `User alice updated order #42 to 'shipped'` |
| "when Alice leaves" | Alice's account switched off in SSO. Server, database and AI tool icons all lock at the same moment |
| End card | Teleport logo + goteleport.com/use-cases/ai-builders |

## Meme Opportunity
- "I am you" / "No, I am you" Spider-Man meme, with the agent and the user
- Tool on the phone to the agent: "And who's asking?" / agent: "A friend"
- Blank name badge: "Hello, my name is `agent`"
