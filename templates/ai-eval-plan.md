# AI eval plan: [Feature name]

An AI feature isn't done when it demos well. It's done when it passes a written test set, and keeps passing after every model, prompt or data change.

## 1. What "good" means

List the qualities that matter, in priority order. For each, say how a failure would hurt users or the business.

| Quality | Why it matters | Example failure |
| --- | --- | --- |
| Accuracy | | |
| Staying in scope | | |
| Safety and privacy | | |
| Honesty about limits | | |
| Tone and length | | |

## 2. Test set

- **Size and mix:** how many cases, split across categories (aim for real user questions first, then edge cases and attacks).
- **Where cases come from:** real logs, user interviews, the PRD's requirements, red-teaming.
- **Each case has:** an input, explicit pass rules, and a one-line *why* (the product reason the test exists).

## 3. Grading

| Method | Use it for | Watch out for |
| --- | --- | --- |
| Rules (must include / must not include) | Facts, numbers, leaks, refusals | False failures from formatting; test the graders too |
| LLM-as-judge | Tone, helpfulness, reasoning | Calibrate against human ratings before trusting it |
| Human review | New categories, disagreements | Slow; sample, don't review everything |

## 4. Bar to ship

- Overall: [e.g. ≥ 95% pass]
- Non-negotiable categories: [e.g. privacy and safety at 100%]
- Any regression from the last run must be explained before shipping.

## 5. When to run

- Before every prompt, model or knowledge-base change ships
- On a schedule against production, to catch drift
- After incidents: every real failure becomes a new test case

## 6. Results log

| Date | Change tested | Score | Fixed | Regressed | Decision |
| --- | --- | --- | --- | --- | --- |
| | | | | | |
