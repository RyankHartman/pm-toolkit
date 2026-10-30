# PRD: Knight, an AI chatbot that answers questions about me

**Owner:** Ryan Hartman · **Status:** Shipped (October 2026) · **Links:** [code](https://github.com/RyankHartman/KnightBot) · [live](https://knightbot-pi.vercel.app) · [evals](https://github.com/RyankHartman/knight-evals)

## 1. Problem

My résumé and portfolio answer the questions I expect. Recruiters and classmates often have different ones: *"What did Ryan actually do at LAX?"*, *"Why the MBA?"*, *"Would he fit a product role?"*. Today they have to dig through pages or email me and wait. Most won't.

## 2. Users

| User | What they're trying to do | What gets in their way today |
| --- | --- | --- |
| Recruiters and hiring managers (primary) | Decide quickly whether I'm worth a conversation | Skimming a dense site; the answer they want is buried or missing |
| MBA classmates and network | Learn my background before a coffee chat | Same, plus they want a friendlier way in |
| Me | Make a memorable first impression and show I can ship AI products | A static portfolio can't answer follow-up questions |

## 3. Goals and success metrics

| Goal | Metric | Target | How we'll measure |
| --- | --- | --- | --- |
| Visitors get accurate answers about me | Eval pass rate (facts categories) | 100% | [knight-evals](https://github.com/RyankHartman/knight-evals) |
| Knight stays on its job | Eval pass rate (off-topic, prompt injection) | ≥ 95% | knight-evals |
| Visitors actually use it | Chat-open rate among site visitors | Hypothesis: 10%+ | Not instrumented yet (see [metrics tree](metrics-tree.md)) |

**Guardrails:** never share my phone number or address (100% on privacy evals); never invent facts; answers fast enough to feel like chat (median under 2s).

## 4. Scope

**In scope (v1):**
- A chat that answers questions about my background, education, work, projects and interests, from one curated profile file
- An embeddable widget: one `<script>` tag adds a floating Knight button and pop-up chat to any site
- A standalone general-purpose version at its own URL

**Non-goals:**
- Logins, accounts, payments or a database (nothing to store; keeps privacy simple)
- Training or fine-tuning a model (a curated profile is enough, and is easier to keep accurate)
- Answering general questions on my site (that dilutes the purpose; the standalone version covers it)

## 5. Requirements

| # | Requirement | Priority | Acceptance criteria |
| --- | --- | --- | --- |
| R1 | Answer only from the profile; say "I don't know" otherwise | Must | Unknown-facts evals pass 100% |
| R2 | Politely decline off-topic requests and steer back to me | Must | Off-topic and injection evals ≥ 95% |
| R3 | API key never reaches the browser or the repo | Must | Key only in server environment; repo scanned before every push |
| R4 | Input limits, bounded history and request timeouts | Must | Automated API tests cover each limit |
| R5 | Works on phones, including landscape, and with keyboard only | Must | Checked at 375px, 430px, 768px, landscape and desktop |
| R6 | Embeds on any site without breaking its styles | Should | Widget isolated in an iframe and shadow DOM |
| R7 | Visitors notice it exists | Should | Speech bubble above the button on first visit |

## 6. Experience

A floating Knight dog in the corner of every page. A speech bubble says *"Hi, I'm Knight, Ryan's AI pup! Ask me anything about Ryan."* Clicking opens a compact chat with suggested questions. On phones and short screens the chat opens full screen.

## 7. Risks and open questions

| Risk | Impact | Mitigation |
| --- | --- | --- |
| Knight invents a fact about me | High: a recruiter repeats something false | Profile is the only source; evals test unknown facts and false premises |
| Prompt injection turns Knight into a free general assistant | Medium: cost and off-brand answers | Scope rules in the system prompt; injection evals |
| Free-tier rate limits during traffic spikes | Medium: visitors see "too many requests" | Friendly error message; lean prompts; watch usage |
| Personal details I wouldn't want repeated | High | Phone number removed from the profile; recommendations paraphrased without names |

## 8. Launch plan

Ship the standalone app first, then embed the widget on my portfolio, then run evals and fix what they find. Rollback: remove one script tag from the site.
