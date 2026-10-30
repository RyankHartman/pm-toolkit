# Decision log: Knight

Real decisions from building and shipping Knight in October 2026, including the ones I reversed.

---

## D1: Plain HTML and one serverless function, no framework

**Date:** 2026-10-19 · **Status:** Active

**Context:** A small chat product that has to be easy to deploy, cheap to run and quick to change.

**Options considered:**
1. A full web framework: richer tooling, but more setup and dependencies than the product needs
2. Plain HTML/CSS/JavaScript plus one Vercel serverless function: nothing to install, deploys anywhere

**Decision:** Option 2.

**Why:** The product is one page and one API call. Fewer moving parts means faster iteration and fewer things to break.

**Revisit if:** Knight needs accounts, history or multiple pages.

---

## D2: The API key lives only on the server

**Date:** 2026-10-19 · **Status:** Active

**Context:** The model provider (Groq) needs a secret key. Anything in browser code is public.

**Decision:** The browser talks only to my own `/api/chat` endpoint; the endpoint holds the key in an environment variable and calls Groq.

**Why:** It's the only safe option. It also lets me add limits (message size, history, timeouts) in one place.

**Revisit if:** Never, for secrets.

---

## D3: Give it a personality: my dog, Knight

**Date:** 2026-10-19 · **Status:** Active

**Context:** "Ask my portfolio a question" is useful but forgettable.

**Options considered:**
1. A neutral assistant
2. A character based on my real Shih Tzu, Knight, with strict limits on the persona

**Decision:** Option 2, with guardrails: at most one light dog touch per reply, none on serious topics, and answers always lead with the point.

**Why:** Memorability is the point of a portfolio. The guardrails stop the persona from getting in the way of good answers.

**Revisit if:** Visitors find it gimmicky, or the persona hurts answer quality in evals.

---

## D4: Ship as an embeddable widget, not just a page

**Date:** 2026-10-19 · **Status:** Active

**Context:** My portfolio is built in a different tool (Lovable). I didn't want to rebuild the chat there.

**Decision:** One `<script>` tag adds a floating Knight button and pop-up chat to any site. The chat runs in an iframe from Knight's own deployment.

**Why:** One codebase, any number of sites. The iframe means the host site's styles can't break Knight, and the key never touches the host page.

**Revisit if:** A host site blocks iframes, or I need deep integration with page content.

---

## D5: Narrow the scope to questions about me (reversed my own v1)

**Date:** 2026-10-20 · **Status:** Active (reversed the original general-purpose design)

**Context:** v1 was a general-purpose assistant. On my portfolio, that meant a recruiter could ask it to write code or explain black holes, which says nothing about me.

**Options considered:**
1. Keep it general: more impressive in a demo, but off-purpose on the site
2. "About Ryan" mode on the site, general mode on its own URL

**Decision:** Option 2. On my site, Knight answers only from my profile and politely declines everything else.

**Why:** Focus beats breadth. The site's job is to help someone learn about me.

**Revisit if:** Evals or feedback show it declining reasonable questions (see D9).

---

## D6: One curated profile file is the single source of truth

**Date:** 2026-10-20 · **Status:** Active

**Context:** Knight needs to know about me, and must not make things up.

**Options considered:**
1. Fine-tune or train a model on my background: slow, expensive, hard to correct
2. Retrieval over many documents: more infrastructure than the content needs
3. One profile file included in every request

**Decision:** Option 3, built from my résumé, portfolio site and public LinkedIn, and reviewed by me before going live.

**Why:** It's small enough to include whole, easy to edit, and easy to audit. What's in the file is what Knight knows.

**Revisit if:** The profile outgrows the model's context or starts costing too much per request.

---

## D7: Leave out what a public chatbot shouldn't repeat

**Date:** 2026-10-20 · **Status:** Active

**Decision:** No phone number or home address in the profile. Email is the only contact route. LinkedIn recommendations are paraphrased, without the recommenders' names.

**Why:** Knight repeats whatever it's given, to anyone. Privacy is decided by what goes into the file, and verified by evals.

---

## D8: Make career goals industry-neutral

**Date:** 2026-10-20 · **Status:** Active

**Context:** My profile listed target industries. A visitor from any other industry would read that as "not you."

**Decision:** Remove industry names; Knight says I'm open across industries and points to relevant experience.

**Why:** A portfolio should widen the funnel, not narrow it.

---

## D9: Help visitors find Knight

**Date:** 2026-10-20 · **Status:** Active

**Context:** A small floating button is easy to miss, and the first hint faded after 7 seconds.

**Decision:** A speech bubble above the dog (*"Hi, I'm Knight, Ryan's AI pup! Ask me anything about Ryan."*) that stays until the visitor opens the chat or dismisses it, once per visit. On phones and short screens, the chat opens full screen.

**Why:** If visitors don't notice it, nothing else matters. Once per visit keeps it from nagging.

**Revisit if:** Data shows the bubble annoys more than it helps (see the [experiment brief](experiment-speech-bubble.md)).

---

## D10: Measure quality with evals, then fix what they find

**Date:** 2026-10-30 · **Status:** Active

**Context:** I'd been spot-checking Knight by hand.

**Decision:** Build [knight-evals](https://github.com/RyankHartman/knight-evals): 63 recruiter-style questions with explicit pass rules, run against the live product.

**What it found:** Knight's scope was both too strict (it declined *"What's Knight's favorite toy?"*) and too loose (it wrote a full poem when asked). I clarified the prompt: questions about Knight are in scope, and Knight answers questions rather than creating content. Both cases now pass.

**Why:** "Seems good" isn't a quality bar. A written test set is, and it catches regressions when anything changes.
