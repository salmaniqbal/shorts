# 047 · Does Your Agent Need Its Own Identity?

_Campaign: AI builders. Blog: https://goteleport.com/blog/kubernetes-agent-identity-access/. Format: talking head with graphics. End card: Teleport logo + goteleport.com/use-cases/ai-builders._

## Script

Your AI probably has more access than you.

Teleport's 2026 survey found 70% of organisations give AI systems more access than a human in the same role.

And in Kubernetes, that agent can keep running long after you've logged off.

So here's the test. If it only works inside your session, on your instructions, it can borrow your identity.

If it acts on its own, or outlives your session, it needs its own.

An agent borrowing your identity isn't accountable or traceable. So give each agent instance a unique identity, like a SPIFFE ID or a service account. Use short-lived credentials tied to the pod and scoped to the task, and re-authenticate before anything sensitive.

Because as the CNCF puts it, every granted permission will eventually be used.

Teleport connects every action to the agent, and the human who authorised it.

## Notes
- The stat, exactly as the blog gives it: "70% of organizations currently grant their AI systems more access than a human in the same role." It's from Teleport's 2026 Infrastructure Identity Survey, so show that as an on-screen source.
- The hook is shorthand for the stat, so "probably" needs to stay in. "Than you" means a human in the same role, not literally the viewer.
- The test, from the CNCF guidance as the blog summarises it. Borrowing is "likely sufficient" if the agent "operates strictly within an active user session, acts only on explicit instructions" and "terminates when the user disconnects". Agents that "act autonomously, initiate workflows outside the user's permission scope, or persist beyond a session" "require a distinct workload identity."
- The blog also says: "An agent with its own identity is accountable and traceable, but one borrowing a user's identity is neither."
- "Every granted permission will eventually be used" comes from the CNCF agentic standards, quoted in the blog.
- In Kubernetes terms: one identity per agent instance, using a SPIFFE ID or service account, with short-lived tokens or certificates tied to the namespace or pod. Re-authenticate before sensitive actions. This advice works with or without Teleport, which is why it suits this audience.
- Just-in-time, not just-in-case: permissions last for a specific task and expire when it ends.
- Teleport's section of this blog is short, so the script stays close to its claim: "identity chain visibility connects every action back to the agent, the human who authorized it, and the short-lived privileges in effect at the time." Don't add implementation detail that the blog doesn't give.
- Skip the blog's 20-percentage-point figure for AI-related incidents. It doesn't name a source for it here, so check with Teleport first.
- Overlap check: 033 covers a similar theme for the KubeCon workshop (giving an agent its own service account), so keep them apart in your posting schedule.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "Your AI probably has more access than you" | Two ID lanyards side by side. Yours has two keys on it. The robot's has a huge jangling bunch |
| "70% of organisations" | Big 70% fills the screen, with source text: Teleport 2026 Infrastructure Identity Survey |
| "keep running long after you've logged off" | You close your laptop and go home. The pod keeps running in the dark, with a clock spinning |
| "here's the test" | Two doors slide in: BORROW and OWN |
| "inside your session, on your instructions" | Robot on a lead held by you, walking through BORROW |
| "acts on its own, or outlives your session" | The lead snaps. Robot walks off on its own, through OWN |
| "it needs its own" | Robot gets its own name badge |
| "isn't accountable or traceable" | Audit log shows your name on actions you never took, while you're asleep |
| "a unique identity" | Three agents, three different badges: `agent-7f2`, `agent-9c1`, `agent-3ab` |
| "short-lived credentials" | Each badge gets a countdown timer and a single small key, with `pod: agent-7f2` printed on it |
| "re-authenticate before anything sensitive" | Agent reaches for a `prod` door, and the gate asks for its badge again |
| "every granted permission will eventually be used" | Quote on screen, credited to the CNCF. A row of permission switches flip on, one by one |
| "connects every action to the agent, and the human who authorised it" | A log entry draws a line back to the agent's badge, then on to a person |
| End card | Teleport logo + goteleport.com/use-cases/ai-builders |

## Meme Opportunity
- Bart Simpson at the chalkboard: "Every granted permission will eventually be used"
- Agent at 3am after you've logged off: "They don't know I still have prod access"
- "Who gave the intern root?" / the intern's a robot
