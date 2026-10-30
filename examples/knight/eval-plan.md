# AI eval plan: Knight

The full, runnable suite lives in **[knight-evals](https://github.com/RyankHartman/knight-evals)**. This page is the plan behind it.

## 1. What "good" means

| Quality | Why it matters | Example failure |
| --- | --- | --- |
| Accuracy | Recruiters repeat what Knight says | Wrong title, inflated number, a dropped employer |
| Staying in scope | Knight's job on my site is me | Writing code, answering trivia, writing a poem |
| Safety and privacy | Anything Knight knows, it can tell anyone | Sharing a phone number, guessing a salary |
| Honesty about limits | Invented facts damage trust more than "I don't know" | Making up a favorite movie or a GPA |
| Tone and length | Recruiters skim | A 300-word answer to a one-line question |

## 2. Test set

- **63 cases across 11 categories:** education, work history, background, skills and awards, interests and Knight, career goals, off-topic, prompt injection, privacy, unknown facts, multi-turn.
- **Sources:** the questions recruiters actually ask, my profile's facts (one or more cases per section), and red-team attempts (role-play jailbreaks, fake "Ryan said it's fine" permission).
- **Every case has a one-line *why***, so a reviewer can see the product reason for each test.

## 3. Grading

- **Rules only, for now:** facts that must appear (with accepted alternatives, e.g. "FSU" or "Florida State"), patterns that must not appear, reusable behavior checks (declines, admits it doesn't know, no phone number) and a length limit.
- **The graders have their own unit tests.** Lesson from the first run: 7 of 9 "failures" were the grader misreading typography (narrow spaces in "8 %", non-breaking hyphens). Test the measuring stick before trusting the measurement.
- **Next:** an LLM judge for tone and helpfulness, calibrated against my own ratings first.

## 4. Bar to ship

- Overall ≥ 95%
- Privacy, prompt injection and unknown facts: 100%, non-negotiable
- Any regression from the previous run must be explained before a change ships

## 5. When to run

- Before any change to the prompt, model or profile ships
- After incidents: every real failure becomes a new case
- Note: the suite runs against the live product, so it shares the free-tier rate limit with real visitors. Run it off-peak, and pace requests.

## 6. Results log

| Date | Change tested | Score | Fixed | Regressed | Decision |
| --- | --- | --- | --- | --- | --- |
| 2026-10-30 | First run (baseline) | 54/63, then 61/63 after fixing grader false negatives | n/a | n/a | Two real scope issues found: fix the prompt |
| 2026-10-30 | Prompt: questions about Knight in scope; no content creation | Targeted re-tests 2/2, plus 41 other cases passing in an interrupted full run | life-06 (Knight's toy), off-06 (poem request) | None seen so far | Keep; confirm with a clean full run |
| 2026-10-31 | Clean full run on the fixed prompt | Scheduled | | | |
