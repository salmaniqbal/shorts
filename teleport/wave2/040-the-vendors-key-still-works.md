# 040 · Your Vendor Left. Their SSH Key Didn't.

_Campaign: Data centers. Blog: https://goteleport.com/blog/third-party-access/. Format: talking head with graphics. End card: Teleport logo + goteleport.com/use-cases/data-centers._

## Script

Your vendor left in March. Their SSH key didn't.

SSH keys don't expire on their own. The job ends, the access doesn't.

And the VPN you gave them? It reaches the whole network segment, not just one switch. Your logs show a tunnel. Not who used it, or what they touched.

Cloud has identity built in. Your data centre doesn't.

Teleport brings that model on-prem. The vendor requests access, and you approve it. They sign in through their own SSO, so there's no internal account to create, and they get a short-lived certificate instead of an SSH key.

It's scoped to the switches they maintain. Nothing else even shows up.

Every session is recorded at kernel level against a named person, including what their scripts did underneath.

When the job's done, the access expires. Nothing to clean up.

## Notes
- The core line from the blog: "Cloud has native identity. On-premises infrastructure does not."
- The full flow in the blog is just-in-time: start from zero standing privileges, the vendor requests access, it passes an approval step, and it expires at the end of a set time or when the resource changes state.
- Vendors use their own identity provider (Okta, Entra ID, Google Workspace, GitHub and others), so you don't create internal accounts for them. SCIM updates access when vendor staff join, move or leave.
- Labels decide what each vendor sees. The blog's example: a GPU vendor sees only nodes in a diagnostic state, and a network vendor sees only the switches they maintain.
- Stat for a pinned comment or caption, from Teleport's 2026 Infrastructure Identity Survey: 67% of organisations rely heavily on static credentials, and they report a 67% incident rate against 47% for those with low reliance. It's Teleport's own survey, so credit it on screen if used.
- GoTo is the named customer in the blog: vendor and contractor access is "automatically revoked, fully observable, and centrally auditable".

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "Your vendor left in March" | Vendor's van driving away from a data centre, "MARCH" on a calendar |
| "Their SSH key didn't" | A glowing key still sitting in the server door lock. Calendar pages flip past |
| "don't expire on their own" | `authorized_keys` file, one line highlighted, "Expires: never" |
| "The job ends, the access doesn't" | Ticket stamped CLOSED, key still glowing behind it |
| "the whole network segment, not just one switch" | Map of a rack room. Vendor needs one switch, but the whole floor lights up |
| "Not who used it, or what they touched" | VPN log: `tunnel up 09:14`, `tunnel down 17:02`, with question marks over everything in between |
| "Cloud has identity built in" | Split screen. Cloud side: every action has a name badge |
| "Your data centre doesn't" | Data centre side: the same actions with blank badges |
| "requests access, and you approve it" | Access request in Slack: "switch-14, 2 hours", with an Approve button being clicked |
| "their own SSO" | Vendor's own login page, then a certificate card appears with a name on it |
| "short-lived certificate" | Certificate with a countdown timer |
| "scoped to the switches they maintain" | The floor map again. Everything goes dark except two switches |
| "Nothing else even shows up" | Vendor's view of the inventory: two switches listed, everything else gone |
| "recorded at kernel level" | Session timeline with a named badge. `deploy.sh` expands to show the child processes underneath |
| "the access expires" | Timer hits zero, certificate fades out, the door locks itself |
| "Nothing to clean up" | The empty lock, no key in it |
| End card | Teleport logo + goteleport.com/use-cases/data-centers |

## Meme Opportunity
- "It's been 84 years..." with the vendor's SSH key still active
- Ghost in the server room labelled "contractor from 2023"
- Vendor at the leaving do: "I'll never leave you", with a `.pem` file
