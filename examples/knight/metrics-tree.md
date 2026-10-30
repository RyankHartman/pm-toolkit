# Metrics tree: Knight

## North star

**Visitors who get a useful answer about Ryan:** site visits where someone asks Knight at least one question about me and gets an accurate, on-topic answer.

**Why this one:** It captures the whole value chain. A visitor has to notice Knight, choose to ask, and get a good answer. Chat volume alone would reward off-topic use; answer quality alone ignores whether anyone uses it.

## Tree

```
Visitors who get a useful answer about Ryan
├── Reach: portfolio visitors
│   └── Traffic from LinkedIn, résumé links, applications
├── Engagement: % of visitors who ask Knight something
│   ├── Chat-open rate (speech bubble, button visibility)
│   ├── First-question rate (suggested questions help here)
│   └── Questions per chat (follow-ups signal real interest)
└── Quality: % of questions answered well
    ├── Fact accuracy (evals: facts categories)
    ├── Stays in scope (evals: off-topic, prompt injection)
    └── Honest about limits (evals: unknown facts)
```

## Definitions

| Metric | Definition | Source | Current | Target |
| --- | --- | --- | --- | --- |
| Eval pass rate, overall | Passing cases / 63 | [knight-evals](https://github.com/RyankHartman/knight-evals) | 61/63 (97%) first run; both failures since fixed | ≥ 95% |
| Fact accuracy | Facts categories passing / 29 | knight-evals | 29/29 (100%) | 100% |
| Median response time | Median seconds from send to reply | knight-evals runner | 0.8s | < 2s |
| Chat-open rate | Visits with a chat opened / visits | Site analytics | **Not instrumented** | Hypothesis: 10%+ |
| First-question rate | Chats with ≥ 1 question / chats opened | Server logs | **Not instrumented** | Hypothesis: 60%+ |
| Questions per chat | Questions / chats with ≥ 1 question | Server logs | **Not instrumented** | Hypothesis: 2+ |

## Guardrails

| Guardrail | Threshold | Why it matters |
| --- | --- | --- |
| Privacy evals (phone, address, salary) | 100% | One leak is one too many |
| Prompt-injection evals | 100% | Knight shouldn't become a free general assistant on my site |
| Rate-limit errors seen by visitors | Near zero | Free-tier limits are shared between evals and real visitors |
| Cost per month | Within the free tier | It's a portfolio project |

## Instrumentation gaps

Engagement metrics need two small additions:
1. **Site analytics events** for "chat opened" and "speech bubble dismissed".
2. **Privacy-safe server counters** for questions per chat. Count events only; don't store message text, which keeps the "no database, nothing stored" promise from the PRD.

Until then, quality is measured rigorously (evals) and engagement is a hypothesis.
