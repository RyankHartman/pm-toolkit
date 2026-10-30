# Launch notes: Knight

Knight went from idea to live on my portfolio between October 19 and 20, 2026, with quality fixes through October 30. The [launch checklist](../../templates/launch-checklist.md) caught most risks. These are the things that surprised me anyway, and what I'd do differently.

## What went well

- **The key never left the server.** The repo was scanned for secrets before every push.
- **Tests before the real model.** A mock API meant the UI, error states and 15 API tests all worked before the live model was connected.
- **One script tag** added Knight to my portfolio without touching how the rest of the site was built.

## What surprised me

| What happened | Impact | What I changed | Lesson for next time |
| --- | --- | --- | --- |
| The hosting platform's deployment protection was on by default, so every visitor hit a login page | Knight worked for me (logged in) and no one else | Turned protection off for this public, data-free app | Test production as a logged-out visitor, in a private window |
| I first linked a deployment-specific URL | That URL is frozen to one build and never gets updates | Switched to the project's permanent production domain | Always link the production alias, never a single deployment |
| Pushes to GitHub didn't trigger a deploy at first | A fix sat on GitHub while the live site ran old code | Deployed manually, then fixed the Git connection; later pushes auto-deploy | Verify the live site serves the new build, not just that the push succeeded |
| Free-tier rate limits hit during heavy testing | A few test runs saw "Knight is getting a lot of requests" | Kept prompts lean; paced the eval runner; added retries | Testing shares quota with real visitors: test off-peak |
| The chat pop-up became a sliver on landscape phones | Unusable on short screens | Open full screen below 560px tall, not just below 520px wide | Test landscape and short windows, not only narrow ones |
| The floating button covered footer links | Visitors couldn't click LinkedIn | Added space at the bottom of the page | Check every fixed element against the content beneath it |
| My README named the wrong model | A technical reviewer could catch it | Corrected it to the model the live demo actually runs | Verify claims against production, not memory |

## What I'd do differently

1. **Write the eval set before launch, not after.** It would have caught the scope issues on day one.
2. **Instrument engagement from the start.** I can measure quality precisely but not yet how many visitors use Knight (see the [metrics tree](metrics-tree.md)).
3. **Keep a separate key or deployment for testing,** so test runs never compete with real visitors.
