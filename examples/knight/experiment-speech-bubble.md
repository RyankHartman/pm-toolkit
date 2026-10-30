# Experiment brief: Does the speech bubble get more visitors to talk to Knight?

**Owner:** Ryan Hartman · **Status:** Proposed (not yet run)

## Hypothesis

We believe **a persistent speech bubble above the Knight button** (*"Hi, I'm Knight, Ryan's AI pup! Ask me anything about Ryan."*) will **increase the chat-open rate** for **first-time portfolio visitors**, because a small floating button alone is easy to miss, and the earlier hint disappeared after 7 seconds.

## Design

| | Control | Variant |
| --- | --- | --- |
| Experience | Knight button only, no bubble | Bubble above the button until opened or dismissed, once per visit |
| Traffic split | 50% | 50% |

**Unit of randomization:** browser session (the bubble already tracks "seen this visit" per session).

## Metrics

| Type | Metric | Expected direction |
| --- | --- | --- |
| Primary | Chat-open rate: sessions with the chat opened / sessions | Up |
| Secondary | First-question rate: chats with ≥ 1 question / chats opened | Flat or up (a bubble shouldn't attract empty opens) |
| Guardrail | Bubble dismiss rate | Watch: high dismissals mean it annoys more than it helps |
| Guardrail | Scroll depth on the portfolio | Must not drop (the bubble covers some content on phones) |

## Sample size and duration

Honest constraint: a personal portfolio gets low traffic. Detecting a lift from, say, 5% to 8% chat opens at standard confidence takes on the order of a thousand sessions per group, which could take months.

**So the practical plan is:**
1. **Instrument first** (chat opened, bubble dismissed): see the [metrics tree](metrics-tree.md).
2. **Run a before/after comparison** around a traffic spike (for example, recruiting season), accepting weaker evidence.
3. **Pair it with 5 to 10 quick user tests:** watch classmates land on the site and note whether they find Knight without prompting.

## Decision rule

Written before any results:

- If chat opens rise meaningfully and dismissals stay under ~50%: **keep the bubble**.
- If opens are flat: **keep the simpler experience** (button only) or test a different message.
- If scroll depth drops on phones: **show the bubble only after the visitor scrolls**.

## Results and decision

Not run yet.
