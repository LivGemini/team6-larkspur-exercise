# PITCH.md

Six lines and a lever. Your words. The last two are scored.

**Built**: A disruption-care chat agent for Larkspur that handles all five ticket types in our test set, and also answers airport-wide questions such as ground stops and the next available day to rebook.
Does: A stranded customer gives their booking reference and last name, and the agent reads their booking and flight status, checks Larkspur policy, then rebooks them, issues a voucher or hands them to a colleague, and confirms by message.

**Number**: About 21,000 input tokens and 5 tool calls for one traced conversation, of which about 2,600 are tool definitions (one run, not yet priced per chat).
Safety check: Not in place yet. An abusive message currently gets the same calm, standard handling as any other, and we will write and test explicit tone guidance before any live use.

**Next**: Add tone guidance for abusive customers, build evaluation cases from realistic disruption scenarios, and agree with Larkspur who owns the agent.

**Still broken**: Abusive customers are not handled differently, we have no evaluation cases of our own yet, and ground-stop end times are estimates, so the agent says "expected", not "guaranteed".
Lever: cost

## Priya asked

**Costs**: About 21,000 input tokens per conversation on our measured run, and the cost lever targets exactly this: every tool definition is sent on every turn, so trimming what we send is where savings come from. A price per conversation is still to be calculated.

**Wrong**: The agent hands the customer to a colleague when it is unsure, and a wrong rebooking or voucher is caught by the confirmation message the customer receives. We propose a human review of a sample of conversations; Larkspur to confirm the process.

**Runs it**: Proposed: a Larkspur customer-care operations owner monitors conversations and the escalation queue, with our team supporting the agent. Larkspur to confirm who.

**Left out**: Abusive-customer handling for now, plus anything outside the five ticket types, payments and refunds, and live customer use until evaluation cases pass.
