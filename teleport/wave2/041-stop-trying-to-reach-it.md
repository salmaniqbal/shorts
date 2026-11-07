# 041 · Stop Trying to Reach It

_Campaign: Autonomous fleets. Blog: https://goteleport.com/blog/remote-access-nat-cgnat-firewalls/. Format: animated explainer. End card: Teleport logo + goteleport.com/use-cases/autonomous-fleet._

## Script

Your robot's down in a customer's warehouse. And you can't reach it.

It's on cellular, behind carrier-grade NAT. One public IP, shared with thousands of subscribers. There's no port to forward.

The customer's firewall blocks inbound anyway. And your VPN died when the robot switched networks. So now you're raising a ticket with their IT team, and waiting.

So stop trying to reach it.

With Teleport, the device opens an outbound connection on port 443, which most networks allow. Your SSH and kubectl sessions ride back down that tunnel. No inbound ports. No public IP.

You stop chasing IP addresses too. Each device gets a cryptographic identity, so you find it by customer or firmware version, not by an address that changes overnight.

If the network drops, it reconnects on whatever's available.

And onboarding a new site is one request: allow outbound HTTPS.

## Notes
- The blog's key line: "The most reliable way to reach a device on a network you do not control is to stop trying to reach it at all."
- Try this on a device: compare `ip addr show wwan0` with `curl -s ifconfig.me`. If the addresses differ, it's behind NAT. Works for a pinned comment.
- "Most networks" matters. The blog says outbound 443 is allowed on most commercial and industrial networks, not all. TLS-inspecting proxies need an exemption, and air-gapped networks need a proxy inside the boundary.
- SSH, Kubernetes, database and application traffic can share one tunnel. That means one policy and one audit trail, and less load on constrained hardware and metered links.
- Device identity replaces IP addresses. Each device gets a cryptographic identity at enrolment, and engineers find it by labels such as customer or firmware version.
- For stolen or decommissioned units, short-lived credentials mean the device doesn't hold standing access for someone to reuse.
- Blog 2 for the same campaign, https://goteleport.com/blog/kubectl-remote-clusters/, is good follow-on reading: 500 devices would mean 500 public API servers (the blog's hypothetical example). Rush Street Interactive is the named customer quote: "With Teleport, we were able to close the Kubernetes API without losing access for our engineers or automation tools."

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "down in a customer's warehouse" | Warehouse floor, one robot stopped mid-aisle with a red warning light |
| "you can't reach it" | Terminal: `ssh robot-042` → `Connection timed out` |
| "carrier-grade NAT" | Robot's signal goes up to a mast, then into a funnel labelled CGNAT |
| "shared with thousands of subscribers" | Thousands of tiny devices all funnelling into one public IP |
| "no port to forward" | A port-forwarding form with every field greyed out |
| "firewall blocks inbound" | Your arrow heads towards the warehouse and hits a brick wall |
| "your VPN died when the robot switched networks" | Wi-Fi icon swaps to cellular, VPN tunnel snaps in two |
| "raising a ticket with their IT team" | Ticket number, status: WAITING. Clock spins, robot still stopped in the aisle |
| "stop trying to reach it" | All the failed arrows vanish. Empty screen, a beat of silence |
| "opens an outbound connection on port 443" | The robot sends a single arrow outwards through the firewall, labelled 443 |
| "ride back down that tunnel" | The arrow becomes a tunnel. `ssh` and `kubectl` travel back along it |
| "No inbound ports. No public IP." | Two ticks over the warehouse wall, which is now untouched |
| "a cryptographic identity" | The robot gets a badge. Search box: `customer=acme firmware=2.1`, and it appears in the results while its IP keeps changing |
| "reconnects on whatever's available" | Link switches cellular → satellite → Wi-Fi, tunnel reforms each time |
| "allow outbound HTTPS" | Customer IT ticket with a single line on it, stamped APPROVED |
| End card | Teleport logo + goteleport.com/use-cases/autonomous-fleet |

## Meme Opportunity
- Field engineer flying to Ohio to plug in a laptop: "This could have been an outbound connection"
- Robot on the phone: "Don't call me. I'll call you."
- "Have you tried turning off the customer's firewall?" / customer's IT team: "No."
