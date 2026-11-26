# 040 · Your Vendor Left. Their SSH Key Didn't.

_Campaign: Data centers. Blog: https://goteleport.com/blog/third-party-access/. Format: talking head with graphics. End card: Teleport logo + goteleport.com/use-cases/data-centers._

## Script

A switch in your data centre fails, and the vendor needs to fix it tonight.

So you send them an SSH key, or a VPN login for access. The switch gets fixed.

But SSH keys don't expire. Six months later, that key still works.

The VPN opens up a whole section of your network, not just that one switch. And your logs show a tunnel opened. Not who was on the other end, or what they touched.


[Speak to camera]
Teleport gives your data centre the identity-based access you expect in the cloud.

The vendor signs in with their own company login, so there's no account to create. They request access, and you approve it.

They get a short-lived certificate for that one switch, for a set time. Nothing else even shows up.

Every session and command is recorded against a named person.

When the job's done, access expires on its own. Check out the blog to see how Teleport can implement this for your data centre.


## Visuals & Animations

| Timestamp | Visual |
|-----------|--------|
| "A switch in your data centre fails" | Rack room, one switch blinking red |
| "the vendor needs to fix it tonight" | Phone call to the vendor, clock reading 22:00 |
| "you send them an SSH key, or a VPN login" | A key and a VPN password slide across into an email to the vendor |
| "The switch gets fixed" | Switch light turns green. Ticket stamped CLOSED |
| "SSH keys don't expire" | `authorized_keys` file, one line highlighted, "Expires: never" |
| "Six months later, that key still works" | Calendar pages flip past. The key is still glowing in the server door lock |
| "a whole section of your network, not just that one switch" | Map of the rack room. Vendor needs one switch, but the whole floor lights up |
| "your logs show a tunnel opened" | VPN log: `tunnel up 22:04`, `tunnel down 23:51` |
| "Not who was on the other end, or what they touched" | Question marks over everything between the two log lines |
| "identity-based access you'd expect in the cloud" | Split screen. Cloud side: every action has a name badge. Data centre side: blank badges, which then fill in with names |
| "their own company login" | Vendor's own sign-in page, with their company logo |
| "no account to create" | An empty "new user" form fades away |
| "They request access, and you approve it" | Access request in Slack: "switch-14, 2 hours", with an Approve button being clicked |
| "short-lived certificate for that one switch, for a set time" | Certificate card with the vendor's name, `switch-14` and a countdown timer |
| "Nothing else even shows up" | Vendor's view of the inventory: one switch listed, everything else gone |
| "recorded against a named person" | Session timeline with the vendor's name badge, commands scrolling past |
| "access expires on its own" | Timer hits zero, certificate fades out, the door locks itself |
| "Nothing to clean up" | The empty lock, no key in it |
| End card | Teleport logo + goteleport.com/use-cases/data-centers |

## Meme Opportunity
- "It's been 84 years..." with the vendor's SSH key still active
- Ghost in the server room labelled "contractor from 2023"
- Vendor at the leaving do: "I'll never leave you", with a `.pem` file
