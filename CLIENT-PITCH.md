# Disruption care that answers in minutes, with a person behind it

## Executive summary

When a flight is cancelled or delayed, customers want one thing: to know what happens next. We have built a working disruption-care chat agent for Larkspur. A customer gives a booking reference and last name. The agent reads the booking and the flight's status, checks Larkspur's own policy, and then rebooks the customer, issues a voucher, or hands them to a colleague. It confirms the outcome by message.

It handles all five ticket types in our test set. It can also answer airport-wide questions, such as whether an airport is under a ground stop and when it is expected to lift.

It is not finished, and we want to be clear about where it stands. It does not yet handle abusive customers differently from anyone else, and we have not yet built our own evaluation cases. We would close both gaps before it goes anywhere near a live customer.

## What the customer experiences

1. They give their booking reference and last name.
2. The agent looks up their booking and the current status of their flight.
3. It checks what Larkspur policy entitles them to.
4. It acts: it rebooks them, issues a voucher, or escalates to a person.
5. They receive a confirmation.

Two additions go beyond the standard flow:
- **Next available day:** the agent can say when the next rebooking opportunity is.
- **Airport ground stops:** it can say whether an airport is stopped, and when the stop is expected to end. That end time is an estimate taken from operations remarks. The agent tells the customer it is expected, not guaranteed.

## What we measured

On one traced conversation, the agent used about 21,000 input tokens and made 5 tool calls, with 11 tools available. About 2,600 of those tokens are the tool definitions. This is one run, not an average. We have not yet converted it into a price per conversation.

## What we are open about

- **Tone:** an abusive message currently gets the same calm, standard handling as any other. We plan to write explicit guidance for this and test it.
- **Evidence:** our own evaluation cases are still to come. Until they exist, "works" means it passed the workshop's checks, not that it is proven against your real traffic.
- **Estimates:** ground-stop end times are estimates by nature.

## Your questions

- **What does it cost?** About 21k input tokens per conversation on our measured run. A per-conversation price is still to be calculated.
- **What happens when it is wrong?** *[Team to write: how a wrong rebooking or voucher is caught and corrected.]*
- **Who runs it?** *[Team to write: who at Larkspur owns and monitors the agent.]*
- **What is left out?** Abusive-customer handling, for now. *[Team to add anything else deliberately out of scope.]*

## Proposed next step

Write and test the tone guidance, add evaluation cases drawn from realistic disruption scenarios, and agree with Larkspur who owns the agent and how errors are handled.

---
*Draft for internal review. Please check the figures against a fresh run and have the team complete the bracketed items before sharing with the client.*
