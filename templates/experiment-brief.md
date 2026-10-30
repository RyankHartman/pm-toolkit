# Experiment brief: [Short name]

**Owner:** [name] · **Status:** Proposed / Running / Concluded · **Dates:** [start to end]

## Hypothesis

We believe **[change]** will cause **[effect on metric]** for **[users]**, because **[reason or evidence]**.

## Design

| | Control | Variant |
| --- | --- | --- |
| Experience | | |
| Traffic split | | |

**Unit of randomization:** [user, session, page view]

## Metrics

| Type | Metric | Expected direction |
| --- | --- | --- |
| Primary | | |
| Secondary | | |
| Guardrail | | must not get worse |

## Sample size and duration

Baseline rate, minimum detectable effect, and the resulting sample size and run time. If traffic is too low for a reliable test, say so and pick a different method (before/after, user interviews, a fake-door test).

## Decision rule

Written **before** the results come in:

- If primary improves by ≥ [x] and no guardrail drops: **ship**.
- If flat: **[keep the simpler option / iterate]**.
- If a guardrail drops: **don't ship**, investigate.

## Results and decision

Filled in when the experiment ends.
