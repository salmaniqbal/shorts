# 046 · Your Agent Doesn't Know Who's Asking

_Campaign: AI builders. Blog: https://goteleport.com/blog/your-ai-agent-needs-to-know-who-you-are/. Format: screen share with graphics. End card: Teleport logo + goteleport.com/use-cases/ai-builders._

## Script

Dan and Bart both ask an AI agent the same thing: show me my customers.

They get exactly the same list. Every customer in the company.

That's because the system never sees Dan or Bart. It only sees the agent, so it can't tell who's asking. It returns everything.

And your audit log just says a tool ran at 2:34. Not who asked.

The fix is to pass the person's identity through to the tool.

With Teleport, you sign in once with your company login. Every tool call then carries a short-lived, signed token saying who you are and what your role allows. The tool checks it, and only returns what that person is allowed to see.

Now the same question gets different answers. Dan sees his customers. Bart sees his, even though the agent made the request.

The log now says Dan asked, at 2:34.
 
And when Dan leaves, his access to servers, databases and AI tools goes at once. Check out Teleport's blog for details

## Notes
- The example comes from the blog, where Dan asks the agent to "list all of her customers from the sales database" and should see only her own data, while Bart needs broader team access. 044 also uses Dan and Bart, so if both run in the same campaign, space them apart or change the names in one.
- The blog's core line: "When your AI agent calls an MCP tool, that tool has no idea who actually triggered the request. It sees the agent, not you."
- "It returns everything" is one of the blog's three failure modes: the tool "returns nothing, returns everything (leaking data across users), or requires the user to manually pass their own email as an argument, which any user could fake." The script uses only the leak because it's the easiest to picture.
- The audit log before and after, from the blog: "`update_order_tool` executed at 2:34 PM." becomes "2:34 PM - User Dan@goteleport.com updated order #42 to 'shipped'".
- The filtering happens in the tool: once it knows who's asking from the token, it scopes the query to that person, and anyone with an admin role sees everything. In the blog this is `get_order_tool`, with the `order-admin` role. Permissions are changed in Teleport roles, not in tool code.
- The flow: `tsh login`, then `tsh mcp connect`. The JWT is attached as a Bearer token on every call. The MCP server checks signature, audience, expiry and roles against Teleport's public keys. The blog says "No user database is needed on the MCP side."
- The token: `sub` (who), `roles` (what they can do), `aud` (locks it to one MCP gateway so it can't be replayed elsewhere) and `exp` (typically one hour).
- "Goes at once" is the blog's claim: "When someone leaves the company, their access to servers, databases, and AI tools is revoked simultaneously."
- There's working code in the `gravitational/rev-tech` GitHub repo. It's a good pinned comment for a technical audience.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "Dan and Bart both ask your AI agent" | Split screen, two chat windows with name badges, both typing "Show me my customers" |
| "exactly the same list" | Both windows fill with an identical, very long customer list |
| "Every customer in the company" | The list keeps scrolling. Counter in the corner: 4,812 customers |
| "never sees Dan or Bart. It only sees the agent" | Dan and Bart hand their requests to one robot. The tool only sees the robot, and the two people fade out |
| "can't tell who's asking" | Tool squints at the robot. Speech bubble: "Who is this for?" |
| "a tool ran at 2:34. Not who asked." | Log line: `list_customers executed at 2:34 PM`, with a blank where a name should be |
| "pass the person's identity through" | A name badge travels along the chain: person → agent → tool |
| "sign in once with your company login" | Your existing SSO login screen, Dan signing in |
| "a short-lived, signed token" | Token card opens: `sub: Dan`, `roles: sales`, `exp: 1h` |
| "only returns what that person is allowed to see" | Tool reads the badge. The long list shrinks to Dan's rows |
| "the same question gets different answers" | Back to the split screen, same question in both windows |
| "Dan sees her customers. Bart sees his." | Dan's window shows 12 customers, Bart's shows 9, no overlap |
| "A manager sees the whole team" | Third window appears with both lists combined |
| "The log says Dan asked" | Log line fills in: `User Dan listed customers at 2:34 PM` |
| "when Dan leaves" | Dan's account switched off in SSO. Server, database and AI tool icons all lock at the same moment |
| End card | Teleport logo + goteleport.com/use-cases/ai-builders |

## Meme Opportunity
- Two Spider-Men pointing at each other, both labelled "the agent"
- Tool on the phone to the agent: "And who's asking?" / agent: "A friend"
- Blank name badge: "Hello, my name is `agent`"
