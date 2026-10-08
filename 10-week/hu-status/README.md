<!-- HU-STATUS TEMPLATE - do NOT remove the <!-- ... --> markers or the table headers.

     Your weekly grade is read AUTOMATICALLY from this file:
       10-week/hu-status/README.md  (inside YOUR fork). English. -->

# Weekly Status - Week 10

<!-- CONFIG-START - must match your profile repo (username/username) CONFIG -->

- FULL_NAME: Juan Esteban Oliveros Duran
- GITHUB_USER: JuanOliveros2497
- TEAM: pms-properties
- SPRINT_GOAL: Ship MVP 2 as an integrated distributed system: contracts respected between services, cross-service consistency via saga + outbox, and per-environment config.
<!-- CONFIG-END -->

## 1. User stories worked this week

| HU ID                                    | Title                                                          | Status (todo/doing/done) | Evidence (PR or commit URL)                                             |
| ---------------------------------------- | -------------------------------------------------------------- | ------------------------ | ----------------------------------------------------------------------- |
| HU-PLAT-002                              | One web application — layout and design tokens                 | done                     | `feat(front): add the layout and the design tokens`                     |
| EP-007 / HU-PLAT-001,002,003 / HU-QA-001 | Platform epic — gateway, web app, environments, contract tests | done                     | `docs(requirements): add the platform stories and close the story file` |
| HU-PLAT-002 (backlog order)              | Start cut 2 with the web application                           | done                     | `docs(product): start cut 2 with the web application`                   |
| N/A (UML docs)                           | State, Saga and event-path diagrams + diagram index            | done                     | `docs(uml): add state and event diagrams and update the index`          |

## 2. My individual contribution

- Implemented the application frame per the mockup (`feat/hu-plat-002-layout-tokens`): design tokens from `design-system.md` published as CSS custom properties on `:root`, top bar (brand, avatar with initials, sign-out), bottom navigation with the three in-scope entries (Explorar, Reservas, Perfil), the landing page with its `landingGuard` redirect, and the container's 404 page. Covered by 46 passing tests; verified against the mockup PDF and AA contrast/keyboard-focus requirements.
- Closed `user-stories.md` by adding the new EP-007 Platform epic (gateway, web application, environments, and the contract-test story moved from Payment), bringing the file to its complete 28 stories across 7 epics, with ids matching what `functional.md`, `traceability-matrix.md` and `product-backlog.md` already cite.
- Reordered the first eight stories of cut 2 in `product-backlog.md` so the web application starts first (it has its own dev sign-in, so it doesn't block on Identity), followed by the environment, the gateway, Catalog search/detail, and then Identity — with a paragraph documenting why.
- Fixed `08-uml/diagram-index.md`, which cited a state diagram file that didn't exist under that name; renamed the misfiled source, added a new Saga state diagram (`RUNNING → COMPLETED/COMPENSATED/FAILED`) and a sequence diagram for how a domain event reaches its consumers through the outbox, and brought the index up to date with all 14 diagrams.
- Reviewed this week's persistence session (database-per-service, saga orchestration/choreography, the outbox pattern against the dual-write problem, CQRS and eventual consistency) and the MVP 2 release session (promotion through environments, the release DoD, demoing a failure path, and the Corte 2 → Corte 3 retrospective).

## 3. Blockers and risks

- PR URLs are not yet filled in above — need to add them once each PR is open on GitHub.
- `feat/hu-plat-002-layout-tokens` depended on PR F2 being merged into `develop` first; confirm that merge landed before this branch's PR is requested for review.
- The platform-stories PR (`docs/stories-platform`) required PR-17b/17c/17d already merged into `main`; the backlog-reorder PR (`docs/backlog-front-first`) required PR-17 merged; the UML PR (`docs/uml-states-events-index`) assumed PR-18/18b/18c merged. Any of those still pending blocks this work from being mergeable.
- Per the course norm, branches must be re-synced with `main`/`develop` right before requesting merge, or the automatic approval fails.

## 4. Plan for next week

- Confirm all four PRs above are merged and add their final URLs to this file.
- Pick up the next HU in the cut-2 order now that the web application, environment, gateway and Catalog search/detail precede Identity.
- Start applying the saga + outbox pattern concretely in the Booking↔Payment flow, per this week's session, ahead of the MVP 2 failure-path demo.

## 5. Compliance self-check

- [x] Conventional Commits - `type(scope): summary`
- [x] Per-environment HU branch + PR to that environment (hu-xxx-dev -> develop, ...)
- [x] Testable acceptance criteria
- [x] Tests added/updated (unit / integration)
- [ ] DDD / hexagonal boundaries respected (domain has no I/O)
- [x] No secrets; config via environment variables

## 6. Evidence links

- `feat/hu-plat-002-layout-tokens` — layout and design tokens
- `docs/stories-platform` — EP-007 Platform epic, closes `user-stories.md`
- `docs/backlog-front-first` — cut 2 reordered to start with the web app
- `docs/uml-states-events-index` — Saga/event diagrams + index fix
