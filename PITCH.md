# PITCH.md

Six lines and a lever. Your words. The last two are scored.

Built: A disruption-care chat agent for Larkspur that handles all five ticket types in our test set, and also answers airport-wide questions such as ground stops and the next available day to rebook.
Does: A stranded customer gives their booking reference and last name, and the agent reads their booking and flight status, checks Larkspur policy, then rebooks them, issues a voucher or hands them to a colleague, and confirms by message.
Number: About 21,000 input tokens and 5 tool calls for one traced conversation, of which about 2,600 are tool definitions (one run, not yet priced per chat).
Safety check: Not in place yet. An abusive message currently gets the same calm, standard handling as any other, and we will write and test explicit tone guidance before any live use.
Next: Add tone guidance for abusive customers, build evaluation cases from realistic disruption scenarios, and agree with Larkspur who owns the agent.
Still broken: Abusive customers are not handled differently, we have no evaluation cases of our own yet, and ground-stop end times are estimates, so the agent says "expected", not "guaranteed".
Lever: <cost | speed | intelligence>

## Priya asked

Costs: About 21,000 input tokens per conversation on our measured run; a price per conversation is still to be calculated.
Wrong: TEAM TO WRITE. How a wrong rebooking or voucher is caught and corrected.
Runs it: TEAM TO WRITE. Who at Larkspur owns and monitors the agent.
Left out: Abusive-customer handling for now. TEAM TO ADD anything else deliberately out of scope.
