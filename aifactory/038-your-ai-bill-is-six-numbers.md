# 038 · Your AI Bill Is Six Numbers

_Location: Giza Pyramids. Duration: ~45 seconds._

## Script

Imagine you're the Pharaoh building this pyramid.

Thousands of workers, millions of stone blocks, and one massive bill.

Now imagine having no idea where the money's going.

Welcome to AI spending.

Your AI bill doubles. Can you explain why?

If not, you need an AI proxy.

Route every model request through one place, so you can track who's using what and how much it costs.

Your bill comes down to six numbers:

Users, sessions, turns, requests, tokens, and price per token.

Grow the first two. Optimise the rest.

Cheaper models, caching, and smaller context windows.

Uber cut cost per session by 52%, while growing users seven times.

Jon Shanks explains how. Link below.

## On-screen Snippet

```
cost = users
     × sessions per user
     × turns per session
     × requests per turn
     × tokens per request
     × price per token
```

## Notes
- The script shortens the six terms to keep the pace. The snippet shows them in full, so put it on screen on the "six numbers" line.
- The six terms and their levers, from the blog's diagram:
  1. **Users** (adoption): you want more.
  2. **Sessions per user** (engagement): you want more.
  3. **Turns per session** (the loop): skills, context and verifiers that shorten it.
  4. **Requests per turn** (routing): sub-agents on cheaper models, deterministic steps that call no model.
  5. **Tokens per request** (context): context discipline, caching, loading tool schemas on demand, compaction.
  6. **Price per token** (the vendor): pick the model per workload on a cost-against-quality plot.
- The proxy, from the blog: every model request and every tool call goes through it. It stamps each call with a project, a person, a team and a session, applies redaction and policy, and writes a trace.
- Uber's stat: cost per agent session fell 52% from its June peak while weekly active users grew 7x. The blog says the drop came from the work the agent does on its own behalf, terms 3 to 5.
- Uber's gateway handles over 100M model requests a day. Without the proxy, "you can't measure anything that follows".
- Tool schemas are a real example of term 5: at Uber, pre-loading tool schemas added 50K to 70K tokens to every initial prompt. Letting the agent discover tools through a small interface cut token use by more than half.
- Gartner predicts AI coding costs will overtake the average developer salary by 2028. That's a good line for a pinned comment.
- Measure cost per merged change, not total spend. A bigger bill with more merged work can be fine. A bigger bill with the same output is waste.
- The Great Pyramid is usually estimated at around 2.3 million blocks, so "millions of stone blocks" holds up.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "Imagine you're the Pharaoh" | To camera at Giza, animated pharaoh headdress dropping onto your head |
| "Thousands of workers, millions of stone blocks" | Tally counters over the pyramid, both spinning upwards |
| "one massive bill" | A papyrus scroll unrolls down the screen, and keeps unrolling |
| "no idea where the money's going" | The pharaoh squinting at the scroll, gold coins draining out of a chest |
| "Welcome to AI spending" | The papyrus morphs into a modern invoice |
| "Your AI bill doubles" | Invoice amount flips from £20k to £40k, red arrow up |
| "Can you explain why?" | Back to camera, shrug |
| "you need an AI proxy" | Dozens of laptops sending arrows straight to a model logo, a tangled mess |
| "through one place" | The tangle snaps into one funnel labelled PROXY before the model |
| "who's using what and how much it costs" | Each request gets a luggage tag: person, team, project, cost |
| "six numbers" | Six stone blocks slam down in a row with × between them, full formula on screen |
| "Users, sessions, turns, requests, tokens, and price per token" | Each block lights up as it's said |
| "Grow the first two" | Users and Sessions blocks glow green with ↑ arrows |
| "Optimise the rest" | The other four blocks get ↓ arrows and a chisel |
| "Cheaper models, caching, and smaller context windows" | Three quick cuts: big model hands a job to a small one, a CACHE HIT shield, a context window squeezed down |
| "Uber cut cost per session by 52%" | Line chart: cost per session falling 52% from the peak |
| "growing users seven times" | Second line on the same chart: users rising 7x |
| "Link below" | Blog card: "What is an AI software factory?" by Jon Shanks, arrow pointing down |

## Meme Opportunity
- Pharaoh reading the invoice: "Who authorised 2.3 million blocks?"
- "Where does the money go?" pie chart where one slice is labelled "re-reading the same 70K tokens of tool schemas"
- Drake: rejecting "one huge model for everything", approving "cheap sub-agent for the boring bits"
