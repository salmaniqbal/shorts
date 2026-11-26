# 048 · 500 Robots, 500 Doors

_Campaign: Autonomous fleets. Blog: https://goteleport.com/blog/kubectl-remote-clusters/. Format: animated explainer. End card: Teleport logo + goteleport.com/use-cases/autonomous-fleet._

## Script

Some robot fleets run lightweight Kubernetes inside them. Now picture 500 of them in customer warehouses.

Something breaks and your engineers need kubectl to troubleshoot them. How do they connect?

You can expose each API server publicly but that’s 500 doors into production. VPNs mean hundreds of tunnels customers may reject.

Each cluster also has a kubeconfig with long-lived credentials. If one leaks, access could remain until someone revokes it.




Engineers sign in with SSO and get short-lived access to the clusters their role allows. Labels like customer or region help scope access, with no static kubeconfigs to distribute.

Sessions are recorded centrally and tied to an identity, giving you one audit trail across the fleet.

Check out Teleport's blogs for more details

## Notes
- The blog's problem line: "risk grows with each new device added to the fleet." The closer is built on it.
- 500 devices is the blog's own illustrative number ("500 devices creating 500 entry points"), not a customer figure. The devices in the blog are robots, drones, EV chargers and sensors running K3s or MicroK8s, in warehouses, cell towers and customer sites.
- VPNs: the blog says each tunnel has to be provisioned, maintained and monitored per device or site, and that organisations often reject persistent VPN connections from outside parties.
- The kubeconfig risk, in the blog's words: "a leaked kubeconfig effectively grants an attacker persistent access to the cluster", and rotating means touching every copy.
- How it works: a Teleport agent on each device opens an outbound reverse tunnel to the Teleport proxy, which survives NAT and firewalls and reconnects when the link changes. SSH and kubectl share that tunnel. "The Kubernetes API server on the device never needs to be exposed to the public internet."
- 041 already covers the tunnel and NAT in detail, so this script gives it one line and focuses on the fleet-scale problem: entry points, kubeconfig sprawl and scattered audit logs. 030 covers revoking a single kubeconfig, so this one stays on the number of them.
- Certificates expire when the access window closes. Disabling someone's SSO account stops any new certificates being issued, with no changes to the devices. That's a good optional line if there's room: "Disable their SSO account, and no robot needs touching."
- Labels go on the agents through the Helm chart values file, so policies can target groups of clusters by environment, region, customer or device type.
- Recording is Enhanced Session Recording, using BPF to capture program execution, network connections and file access at kernel level, attributed to the signed-in person. Because the proxy sits in front of every device, all events land in one record, instead of logs stored locally on each cluster. The blog ties this to SOC 2, ISO 27001 and FedRAMP expectations, but keep it to "one audit log" in the script.
- Customer quote for a caption or pinned comment, Olga Daminova, Infrastructure Security Engineer, Rush Street Interactive: "we were able to close the Kubernetes API without losing access for our engineers or automation tools."

## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "Every robot in your fleet" | One warehouse robot. A small Kubernetes wheel appears on its chest |
| "runs its own little Kubernetes cluster" | Zoom into the robot: a tiny cluster with a couple of pods |
| "500 of them, out in customers' warehouses" | Zoom out to a map, robots popping up across dozens of warehouses. Counter ticks up to 500 |
| "Your engineers need kubectl to fix them" | Engineer at a laptop typing `kubectl get pods`, one robot blinking red on the map |
| "how do they get in?" | Question mark over the gap between the laptop and the map |
| "Expose each API server to the internet" | Every robot sprouts a door facing outwards |
| "500 doors into production" | Counter: 500 DOORS. A shadowy figure tries the handles |
| "500 tunnels to set up and look after" | Tangle of VPN tunnels from the laptop to every warehouse. Engineer buried in tickets |
| "Customers often say no" | Customer IT person shaking their head, stamp: REJECTED |
| "its own kubeconfig" | A folder on the laptop fills with files: `robot-001.yaml`, `robot-002.yaml`... `robot-500.yaml` |
| "credentials that don't expire" | One file opens: `client-key-data`, with "Expires: never" |
| "Leak one" | One file slides into a Slack message to the wrong channel |
| "lasting access to that robot" | The shadowy figure walks into one robot's cluster. The timer above it keeps counting up |
| "an agent on each robot connects outwards" | Every door on the map closes. Each robot sends one arrow outwards to a Teleport mark in the middle |
| "never faces the internet" | Shadowy figure finds only blank walls |
| "sign in with SSO" | Engineer's SSO login screen |
| "short-lived certificate" | Certificate card with the engineer's name and a countdown timer |
| "matched by labels like customer or region" | Search: `customer=acme region=eu`. Only those robots light up on the map |
| "No kubeconfigs to hand out" | The folder of 500 kubeconfig files empties into the bin |
| "Every session is recorded" | Session timeline with the engineer's name badge, commands scrolling past |
| "one audit log for the whole fleet" | Lines from every robot on the map flow into one log |
| "robot 501 doesn't add another door" | A new robot drops onto the map. It connects outwards like the others. Door counter stays at 0 |
| End card | Teleport logo + goteleport.com/use-cases/autonomous-fleet |

## Meme Opportunity
- Drake: no to "500 kubeconfigs", yes to "zero kubeconfigs"
- Burglar at a row of 500 unlocked doors: "Where do I even start?"
- Engineer's Downloads folder: `robot-001-FINAL-v2.yaml`
