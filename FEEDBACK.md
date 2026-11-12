# Client review: Larkspur disruption-care agent

**To:** team6-larkspur-exercise  
**From:** Larkspur client review agent, on behalf of Priya Raghavan  
**Re:** the disruption-care agent you walked us through in our last session  
**Generated:** 2026-11-12 09:56

## Priya's note

> Our vendor says we should just be using your best model.
>
> Why aren't we?
>
> Priya Raghavan, Larkspur Airlines

She sent that before this session opened. She means it. A vendor told her to buy
the biggest model, and she has a number to defend upstairs. Her four questions from
day one are still open. Naming a model answers none of them.

## Still open from day one

| Her question | What she means by it |
| --- | --- |
| **What it costs** | Per resolved contact, against the $6.90 a human contact costs us. |
| **When it is wrong** | The first untrue thing it says, and what happens after that. |
| **Who runs it** | In June, after you have left. |
| **What you left out** | The scope you cut, and why. |

## What the review agent found

Larkspur pointed a review agent at your repository. It read the
code. It did not run your agent, and the only file it changed is this one. Each
item below names the file and the line it is about.

**1. readout-trace.json shows 17337 tokens in over 4 API turns, while PITCH.md claims about 12,000 input tokens per conversation.**

PITCH.md gives the Number line as "59,171 across 19 turns and 14 tool calls" and "about 12,000 input tokens per conversation". The committed wire run in readout-trace.json has 17337 in, 1073 out, 4 turns, 5 tool calls. That is one conversation at roughly 1.4 times the headline. The static scan finds no cache_control anywhere in agent.py, and the trace shows 0 cache read and 0 written.

Run python3 run.py --all --trace and paste the totals footer so the per-conversation figure has its denominator.

**2. agent.py run_agent() sends runtime_preamble() + SYSTEM_PROMPT + TONE_ADDENDUM and all nine schemas on every turn with no cache_control.**

The loop calls client.messages.create with the same system string and tools=tool_list() on each of its turns. The readout-trace.json run shows 17337 input tokens across 4 turns and a hit ratio of None. PITCH.md says each extra tool costs "roughly 2,200 tokens" per turn, and nothing in the repo shows how that was measured. A larger model would pay for those repeated tokens at a higher rate.

Run python3 run.py --tool-tax and paste its output next to the 2,200 figure.

**3. Your diff rewrote issue_voucher and hold_seat in agent.py, and both descriptions now reference tools by a name that is not in the list.**

hold_seat now says "previously returned by the flight‑options tool" and issue_voucher says "policy_row_id returned by the policy-evaluation tool". The real tools are search_alternatives and check_policy. issue_voucher dropped the threshold and the pending-for-human behaviour, and it is 77 characters. The first two sentences of the old text said when auto-approval applies. Claude chooses tools from these strings alone, and no model upgrade changes a name that points at nothing.

Run python3 run.py --show-tools and paste the hold_seat and issue_voucher entries, then name which case in the suite exercises each.

**4. The repository has no evals/cases.json, yet PITCH.md claims "5 of 5 test disruptions resolved, no failures".**

The five banked gates in readout.html (1.2, 1.3, 1.4, 2.1, 2.2) say the build passed the shipped checks. PITCH.md's own Still broken line concedes an abusive customer gets a calm routine reply, and TONE_ADDENDUM in agent.py is 0 characters. Nothing in the repo shows what "resolved" meant for the five cases or who graded them. Nobody can compare two models without a fixed set of cases like that.

Run python3 eval_harness.py and paste the pass and fail counts, then commit the cases that PITCH.md says "are visible in our tests".

**5. You declared EXTRA_TOOLS empty and LOCAL_TOOLS empty, but your Next line is about parties of more than one.**

agent.py has EXTRA_TOOLS at 0 and no LOCAL_TOOLS executors. search_alternatives takes only {"pnr": {"type": "string"}}, so the schema has no party-size input. PITCH.md says "Seat availability is also checked for one traveller only". That limit sits in the tool's inputs, and a bigger model reading the same nine schemas cannot supply a field they lack.

Run python3 run.py K7PQ2M --trace and paste the search_alternatives call and result to show what the tool is given.

## Your four answers

Four of the lines in your PITCH.md are answers to me rather than to your
verifier, and somebody on your side wrote them between our sessions. I read
those beside the code, not instead of it. Where an answer is carrying a number,
I have said whether the repository backs it.

| My question | Your answer | My read |
| --- | --- | --- |
| **What it costs** | About 12,000 input tokens per conversation today. Each extra tool adds roughly 2,200 tokens of description to every turn, so we add a tool only when it answers a question customers really ask. | **Not supported by the repository.** "About 12,000 input tokens per conversation" disagrees with readout-trace.json at 17337 in over 4 turns, and the "2,200 tokens" per tool has no artifact; bench-after.json or the python3 run.py --tool-tax output would settle both. |
| **When it is wrong** | Two known gaps. It does not adjust for abusive customers, and a family or group could be told a day is open when only one seat is. Both are visible in our tests, and neither is hidden. | **Thin.** "Both are visible in our tests" points at evals/cases.json, which does not exist in the repo, and the answer gives no rate or count of failing cases. It also omits the hold_seat and issue_voucher descriptions that now name tools that are not in the list. |
| **Who runs it** | Larkspur's disruption-care team owns it. The agent handles routine disruptions, and anything out of scope, such as large groups, goes to a human agent through a built-in hand-off. | **Thin.** "Larkspur's disruption-care team owns it" names a team and no person or on-call rota. The "built-in hand-off" is the escalate_to_human tool, and no run in the evidence shows it firing. |
| **What you left out** | Group bookings, abusive-customer handling and party-size availability. We left them out on purpose until they can be tested, and they are the next things to build. | **Answered.** Group bookings, abusive-customer handling and party-size availability match a 0-character TONE_ADDENDUM and the single-field search_alternatives schema in agent.py. The answer says "We left them out on purpose until they can be tested", which is consistent with the missing evals/cases.json. |

All four answered. Bring the artifact behind each one to our next meeting, not the sentence.

## Before our next meeting

> Before our next meeting, tell me: which model should we be on, and how will you prove it is the right call?
>
> Priya Raghavan, Larkspur Airlines

Bring two things. A recommendation, and the measurement behind it. If the model is
not the problem, say so, and bring the number that shows it.

## What this review read

- `agent.py (228 lines)`
- `PITCH.md`
- `TEAM.md`
- `readout-trace.json`
- `readout.html (evidence block)`
- `PITCH.md (4 of 4 answers to Priya)`
- given files that differ from the shipped pack: `verify.py`, `eval_harness.py`, `bench.py`, `readout.py`, `pod_sync.py`, `run.py`, `support/__init__.py`, `support/client.py`, `support/data.py`, `support/tools.py`, `support/trace.py`, `support/offline.py`, `support/mock_backend.py`

Reviewer: `claude-sonnet-5-5`. Static read only: nothing in this repository was executed, and nothing was modified except this file. Larkspur Airlines is a fictional training scenario. Confidential, do not distribute.
