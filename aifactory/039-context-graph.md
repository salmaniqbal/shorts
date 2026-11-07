# 039 · The Context Graph: 20 Minutes vs 38 Seconds

_Location: Grand Egyptian Museum. Duration: ~45 seconds._

## Script

Ancient Egypt had hundreds of Pharaohs and thousands of relationships.

Imagine reading every historical document just to find out who was related to whom.

Or you could use a family tree.

AI agents face the same problem.

To fix an incident, they need to know which service is affected, who owns it, and where the code lives.

Without that, they're searching endless documentation.

Uber tested two agents with the same prompt and model.

One took 20 minutes and got it wrong.

The other took 38 seconds and got it right.

The difference? A context graph.

A family tree for your software systems.

Instead of reading everything, agents follow relationships to find answers.

More in Jon Shanks' blog. Link below.

## Notes
- The Uber numbers, as given in the blog: identical prompt, same model. Without the graph: 20 min 9 s, two subagents, three errors along the way, wrong conclusion. With the graph: 38 seconds, one agent, seven hops, right answer. Uber published the two totals. The per-hop times in the blog's diagram are illustrative, so don't quote them.
- The seven things for one incident: service, repository, owner, alert history/runbook, environments, cloud account, sandbox. The script names three to keep the pace.
- The family tree is the blog's own analogy: it tells you what relates to what. The blog also makes the point that the agent "can't tap a colleague on the shoulder".
- Why not load everything into context? It's expensive, slow, and too much context makes agents less accurate. Walking the graph keeps the context window small and the agent accurate.
- Practical start: a service catalogue with ownership and relationships is already most of a context graph. Backstage's catalogue relations (`ownedBy`, `partOf`, `dependsOn`) are a good example. Expose it to agents as a tool or MCP server rather than pasting it into prompts.
- It works for people too. A new joiner on call needs exactly the same answers.
- "Hundreds of Pharaohs": counts vary a lot depending on the source and who you include, so this line may draw a comment.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "hundreds of Pharaohs and thousands of relationships" | To camera in the museum, then a slow pan across statues with name cartouches popping up beside them |
| "reading every historical document" | A mountain of papyrus scrolls piling up around a tiny scribe |
| "who was related to whom" | Scribe holding two cartouches, shrugging |
| "you could use a family tree" | Tutankhamun's family tree draws itself: Amenhotep III → Akhenaten → Tutankhamun |
| "AI agents face the same problem" | The cartouches turn into software boxes, a robot looking up at them |
| "which service is affected, who owns it, and where the code lives" | Three cards appear as they're named: SERVICE, OWNER, REPOSITORY. Alert buzzing in the corner |
| "searching endless documentation" | Robot buried in browser tabs: Wiki, Runbook, Dashboard, error pop-ups |
| "two agents with the same prompt and model" | Split screen, two identical robots, the same prompt card in front of each |
| "One took 20 minutes and got it wrong" | Left robot: stopwatch spinning to 20:09, sweating, a red "✗ wrong conclusion" |
| "The other took 38 seconds and got it right" | Right robot: stopwatch stops at 0:38, green "✓ right answer" |
| "A context graph" | Title card, nodes and edges drawing themselves |
| "A family tree for your software systems" | The Tutankhamun tree morphs into: Incident → Service → Repository → Owner, branching to Environments → Cloud account → Sandbox |
| "agents follow relationships" | Robot hops node to node along glowing edges, a counter ticking 1 to 7 hops |
| "Link below" | Blog card: "What is an AI software factory?" by Jon Shanks, arrow pointing down |

## Meme Opportunity
- Charlie Day conspiracy board made of papyrus, labelled "agent without a context graph"
- "Who owns this service?" Spider-Man pointing at three teams pointing at each other
- Galaxy brain: read one scroll → read all scrolls → stuff everything into context → follow seven edges
