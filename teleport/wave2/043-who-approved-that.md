# 043 · Who Approved That?

_Campaign: Digital payments and banking. Blog: https://goteleport.com/blog/pci-dss-infrastructure-evidence/. Format: talking head or screen share. End card: Teleport logo + goteleport.com/use-cases/digital-payments-and-banking._

## Script

An admin just reached your production database. Who approved that?

You've got the log. For PCI DSS 4.0, that's not enough.

Assessors want the chain. Why did they elevate? Who approved it? Did anyone review it afterwards? What changed?

A control only counts if someone acted on it.

And it's not just people. A service account that can log in needs a reason, and a trail back to a named individual.

So try this today. Pick one access anomaly, and trace it from detection to outcome. If you get stuck, so will your assessor.

Teleport gives you one identity and access record across your cardholder data environment. Short-lived credentials and scoped roles mean access doesn't linger. And every session traces back to a person, service account or agent.

So you're not rebuilding the trail by hand.

## Notes
- The scenario is the blog's own: a user elevates to an admin role and reaches a production database, with no record of why, who approved it, or whether anyone reviewed it.
- The blog's line: controls "don't secure an environment unless they are acted on". Assessors look for a traceable chain from access, to review, to corrective action.
- The "try this today" tip is item 1 of the blog's audit readiness checklist. The other two: compare a recent access review with live permissions, and trace one known gap (such as stale admin access) through to a fix.
- Requirements the blog cites, to check against the standard before putting any on screen: 7.2.4 (user access reviews at least every six months), 7.2.5 and 7.2.5.1 (application and system accounts), 8.6 and 8.6.1 (interactive-capable service accounts), 10.4.1.1 (automated audit log review).
- Keep the wording to "evidence" and "trace". The blog presents Teleport as supporting compliance, not guaranteeing it. People still have to do the reviews and own the follow-up, so don't say Teleport "makes you compliant".
- The blog says the most common gap its author finds is over-privileged RBAC, followed by access that outlives a role change and service accounts nobody reviews. Any of these could be a follow-up short.
- Niche follow-up: https://goteleport.com/blog/sama-adgm-dfsa-compliance/ applies the same "show the evidence" idea to Gulf regulators. It would suit a regional cut if Teleport wants one.

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "An admin just reached your production database" | Terminal: `role: db-admin`, connecting to `prod-payments-db`, green tick |
| "Who approved that?" | Text fills the screen. Question mark lingers |
| "You've got the log" | Log line appears: `db-admin connected 02:14` |
| "that's not enough" | The log line shrinks to a small dot in an empty audit folder |
| "Assessors want the chain" | Four empty chain links appear in a row |
| "Why did they elevate?... What changed?" | Each question lights one link in turn, all four showing a red gap |
| "A control only counts if someone acted on it" | Policy document with a shiny seal, and an empty "Reviewed by" box |
| "a service account that can log in" | Robot-style badge `svc-batch` opens a shell, and a line runs from it to a person's name |
| "Pick one access anomaly" | Finger picks one alert from a list |
| "trace it from detection to outcome" | A line runs from the alert through DETECTED, REVIEWED, ACTION, OUTCOME |
| "If you get stuck" | The line stops at REVIEWED, nothing after it |
| "one identity and access record" | Servers, databases and Kubernetes feeding into one timeline |
| "access doesn't linger" | Certificate timer reaches zero, role badge drops off |
| "a person, service account or agent" | Timeline entries with three badges: person, service account, agent |
| "rebuilding the trail by hand" | Spreadsheet of logs slides off screen. Chain links close up, all green |
| End card | Teleport logo + goteleport.com/use-cases/digital-payments-and-banking |

## Meme Opportunity
- Assessor as the "Show me" guy from Jerry Maguire: "Show me the evidence!"
- Spider-Man pointing meme: security, platform and the DBA all pointing at each other over "who reviewed this?"
- "It's in the logs" / assessor: "Which logs?" / "...All of them"
