# 037 · Skills: Write the Standard Once

_Location: Grand Egyptian Museum. Duration: ~45 seconds._

## Script

Look at these hieroglyphs.

The ancient Egyptians used a shared writing system for thousands of years.

Imagine if every scribe invented their own symbols.

Chaos!

And that's exactly what's happening with AI coding agents.

Every developer uses different prompts, different standards, and a different idea of done.

The result? Reviews taking five times longer and 28% more bugs per pull request.

The solution? AI agent skills.

Think of a skill as a reusable recipe for one job.

A logging standard. A security review. A database migration.

Write it once, and every agent follows it.

But treat skills like code: review them, test them, and retest when models change.

More in Jon Shanks' blog. Link below.

## On-screen Snippet

```markdown
---
name: logging-format
description: Use when adding or changing log statements.
---
Log as JSON. Always include trace_id, service and level.
Never log tokens, passwords or card numbers.
```

## Notes
- The stats are from Faros, as quoted in the blog: AI adoption on its own came with 5x longer median review time and 28% more bugs per pull request. The script says "five times longer", which means the median.
- The blog's diagnosis: without shared skills, "every developer's local agent and skills, or the developer themselves, produce something slightly different", so quality varies with every pull request. A review agent applying the same standards to everything makes the output consistent and easy to review.
- Assuring a skill, from the blog: lint it, review it, then evaluate the agent and skill together to check reliability and how deterministic the result is. Measure cost, how close the run was to optimal, and whether the outcome was the same each run. Build eval sets from real failures, not synthetic ones.
- Re-evaluate when the model changes. Spotify removed its judge as too rigid once the models caught up.
- Central vs project: company-wide standards (security review, logging format, architecture patterns) go central. Domain knowledge and repo conventions stay with the team. Team skills layer on top of central ones, the way a repo's lint config extends the organisation's.
- The snippet is in the Agent Skills `SKILL.md` format (name + description frontmatter, instructions below). The same idea works as an `AGENTS.md` or any shared prompt file checked into a repo.
- Good for a pinned comment: Uber's engineers have built over 3,600 skills. A good first skill is the review comment your seniors leave on every pull request.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "Look at these hieroglyphs" | To camera in the museum, then a slow push in on a carved wall |
| "a shared writing system for thousands of years" | The same symbols highlighted on several different objects around the gallery |
| "every scribe invented their own symbols" | Animated scribes side by side, each carving different made-up symbols, including a smiley face and a Wi-Fi icon |
| "Chaos!" | The hieroglyphs scramble and fall off the wall |
| "exactly what's happening with AI coding agents" | The scribes become developers, each with a small robot on their shoulder |
| "different prompts, different standards, and a different idea of done" | Five pull requests side by side, then five robots holding five different "DONE ✓" signs |
| "five times longer" | Review clock spinning, "Median review time ×5" |
| "28% more bugs" | Bug counter ticking up on a pull request: +28%, reviewer with head in hands |
| "AI agent skills" | A stone tablet slides in, carved with the word SKILL |
| "a reusable recipe for one job" | The tablet turns into a recipe card |
| "A logging standard. A security review. A database migration." | Three cards fanning out, one per example |
| "Write it once, and every agent follows it" | One card copies to every robot, and their five pull requests become identical. Show the `SKILL.md` snippet |
| "treat skills like code" | The card goes through a pull request: diff, review, merge |
| "retest when models change" | Model version badge flips (v1 → v2), tests re-run, green ticks |
| "Link below" | Blog card: "What is an AI software factory?" by Jon Shanks, arrow pointing down |

## Meme Opportunity
- Hieroglyphs on a wall with a translation underneath: "please use structured logging (again)"
- Five Spider-Men pointing at each other, each a scribe with a different alphabet
- "Is this a standard?" butterfly meme: developer pointing at their own agent's output
