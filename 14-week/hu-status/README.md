<!-- HU-STATUS TEMPLATE - do NOT remove the <!-- ... --> markers or the table headers.
     Your weekly grade is read AUTOMATICALLY from this file:
       14-week/hu-status/README.md  (inside YOUR fork). English. -->

# Weekly Status - Week 14

<!-- CONFIG-START - must match your profile repo (username/username) CONFIG -->
- FULL_NAME: Juan Esteban Oliveros Duran
- GITHUB_USER: JuanOliveros2497
- TEAM: Group 2 — Property
- SPRINT_GOAL: Plan batch 2 of Payment and Catalog - charges through Stripe, refunds, the ledger, and the catalog service on MongoDB - and open its stories
<!-- CONFIG-END -->

## 1. User stories worked this week
| HU ID | Title | Status (todo/doing/done) | Evidence (PR or commit URL) |
|---|---|---|---|
| #191 | HU-PAY-002 — Charge only once | doing | https://github.com/code-corhuila/property-docs/issues/191 |
| #192 | HU-PAY-003 — Maintain and read the transaction ledger | doing | https://github.com/code-corhuila/property-docs/issues/192 |
| #193 | HU-PAY-004 — Refund an approved charge | doing | https://github.com/code-corhuila/property-docs/issues/193 |
| #197 | HU-CAT-003 — Filter search by availability | doing | https://github.com/code-corhuila/property-docs/issues/197 |

## 2. My individual contribution
- Opened the issues of my batch 2 stories: #191, #192, #193, #197.
- Started preparing the payment-api and catalog changes of batch 2 so the pull requests can be opened in week 15.

## 3. Blockers and risks
- Batch 2 depends on the batch 1 pull requests of every service being merged first.
- The organization CI is still blocked; evidence is the local test output.

## 4. Plan for next week
- Open and merge the payment and catalog pull requests of batch 2.
- Batch 3: the payment outbox relay, the catalog consumer and the payment portal.

## 5. Compliance self-check
- [x] Conventional Commits - `type(scope): summary`
- [ ] Per-environment HU branch + PR to that environment (hu-xxx-dev -> develop, ...) — *(no pull request this week; they open in week 15)*
- [x] Testable acceptance criteria
- [ ] Tests added/updated (unit / integration) — *(planning week; tests come with the batch 2 pull requests)*
- [ ] DDD / hexagonal boundaries respected (domain has no I/O) — *(no code merged this week)*
- [x] No secrets; config via environment variables

## 6. Evidence links
- https://github.com/code-corhuila/property-docs/issues/191
- https://github.com/code-corhuila/property-docs/issues/192
- https://github.com/code-corhuila/property-docs/issues/193
- https://github.com/code-corhuila/property-docs/issues/197
