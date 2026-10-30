# PM Toolkit 🧰

The templates I actually use to take a product from idea to launch, each paired with a **real, filled-in example** from a product I shipped: [Knight](https://github.com/RyankHartman/KnightBot), the AI chatbot on my portfolio site.

Templates are easy to find. What's harder to see is how someone uses them. So every template here comes with the version I wrote for Knight, including the decisions I got wrong at first and changed.

## What's inside

| Template | What it's for | Worked example (Knight) |
| --- | --- | --- |
| [PRD](templates/prd.md) | Align on the problem, users, scope and success before building | [Knight PRD](examples/knight/prd.md) |
| [Decision log](templates/decision-log.md) | Record the calls you made, the options you rejected, and why | [Knight decision log](examples/knight/decision-log.md) |
| [Metrics tree](templates/metrics-tree.md) | Connect one north-star metric to the inputs a team can move | [Knight metrics tree](examples/knight/metrics-tree.md) |
| [AI eval plan](templates/ai-eval-plan.md) | Define "good" for an AI feature and measure it before and after changes | [Knight eval plan](examples/knight/eval-plan.md) · [live suite](https://github.com/RyankHartman/knight-evals) |
| [Launch checklist](templates/launch-checklist.md) | Ship without surprises, then write down what surprised you anyway | [Knight launch notes](examples/knight/launch-notes.md) |
| [Experiment brief](templates/experiment-brief.md) | Turn an idea into a testable hypothesis with a decision rule | [Speech bubble experiment](examples/knight/experiment-speech-bubble.md) |

## How I use them

1. **PRD first, short.** One page is the goal. If I can't write the problem and the non-goals in plain sentences, I'm not ready to build.
2. **Decision log as I go.** Every meaningful call gets one entry, the same day. Future me (and future teammates) need the *why*, not just the *what*.
3. **Metrics tree before launch.** Decide what success means before seeing any data, so the numbers can't talk me into a story.
4. **Evals for anything AI.** An AI feature isn't done when it demos well; it's done when it passes a written test set, and keeps passing after every change.
5. **Launch notes after, honestly.** The checklist catches the known risks; the notes capture the unknown ones for next time.

## About the examples

Everything in [`examples/knight`](examples/knight) happened while I built and shipped Knight in October 2026. Where something hasn't been measured yet (for example, real visitor analytics), it's labeled as a **target** or **hypothesis** rather than a result.

Feel free to copy any template. If you use one, I'd love to hear how it went: [LinkedIn](https://www.linkedin.com/in/ryankhartman).

---

<sub>🐾 Built by Ryan · Supervised by Knight</sub>
