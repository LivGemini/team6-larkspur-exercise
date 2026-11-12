# PITCH.md

Six lines and a lever. Your words. The last two are scored.

Built: A chat agent that looks up a disrupted passenger's booking, checks the flight, reads Larkspur's own policy, and proposes a rebooking, a voucher or a hand-off to a person.
Does: A customer with a cancelled flight, a delay or a missed connection gets a policy-correct answer in one conversation. It can also tell them the next day with an open seat when no same-day option exists.
Number: 5 of 5 test disruptions resolved, no failures, about 12,000 input tokens per conversation (59,171 across 19 turns and 14 tool calls).
Safety check: The agent cannot invent an entitlement. Fare family, loyalty tier and overnight status are re-read from the booking on every policy check, and a rebooking only goes through after the customer's own confirm click.
Next: Test the cases a customer would actually complain about, starting with parties of more than one, and make the agent answer for the whole party.
Still broken: An abusive customer gets the same calm, routine reply as everyone else, with no change of tone and no escalation. Seat availability is also checked for one traveller only.
Lever: intelligence

## Priya asked

Costs: About 12,000 input tokens per conversation today. Each extra tool adds roughly 2,200 tokens of description to every turn, so we add a tool only when it answers a question customers really ask.
Wrong: Two known gaps. It does not adjust for abusive customers, and a family or group could be told a day is open when only one seat is. Both are visible in our tests, and neither is hidden.
Runs it: Larkspur's disruption-care team owns it. The agent handles routine disruptions, and anything out of scope, such as large groups, goes to a human agent through a built-in hand-off.
Left out: Group bookings, abusive-customer handling and party-size availability. We left them out on purpose until they can be tested, and they are the next things to build.
