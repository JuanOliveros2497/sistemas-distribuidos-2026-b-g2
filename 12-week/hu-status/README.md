<!-- HU-STATUS TEMPLATE - do NOT remove the <!-- ... --> markers or the table headers.
     Your weekly grade is read AUTOMATICALLY from this file:
       12-week/hu-status/README.md  (inside YOUR fork). English. -->

# Weekly Status - Week 12

<!-- CONFIG-START - must match your profile repo (username/username) CONFIG -->
- FULL_NAME: Juan Esteban Oliveros Duran
- GITHUB_USER: JuanOliveros2497
- TEAM: Group 2 — Property
- SPRINT_GOAL: Start the code of cut 3 for Payment - the payment database (schema, tables and roles) and the base of payment-api
<!-- CONFIG-END -->

## 1. User stories worked this week
| HU ID | Title | Status (todo/doing/done) | Evidence (PR or commit URL) |
|---|---|---|---|
| #162 | HU-PAY-001 — Charge a Reserva | doing | https://github.com/code-corhuila/property-payment-db/pull/2 |

## 2. My individual contribution
- Liquibase repository of property-payment-db: https://github.com/code-corhuila/property-payment-db/pull/1
- Schema `payment` with its tables: https://github.com/code-corhuila/property-payment-db/pull/2
- Roles and grants of `payment_app`: https://github.com/code-corhuila/property-payment-db/pull/3
- Three-module skeleton, Pago and Reembolso domain model and the common HTTP adapters of payment-api: https://github.com/code-corhuila/property-payment-api/pull/1, https://github.com/code-corhuila/property-payment-api/pull/2, https://github.com/code-corhuila/property-payment-api/pull/3

## 3. Blockers and risks
- The CI of the code-corhuila organization does not start (billing lock). With the instructor's authorization, PRs are merged with one peer approval plus the local test output posted in the PR.

## 4. Plan for next week
- Versioned OpenAPI contract of payment-api.
- Threat modeling workshop for the boundary payment-api -> Stripe.

## 5. Compliance self-check
- [x] Conventional Commits - `type(scope): summary`
- [x] Per-environment HU branch + PR to that environment (hu-xxx-dev -> develop, ...)
- [x] Testable acceptance criteria
- [x] Tests added/updated (unit / integration)
- [x] DDD / hexagonal boundaries respected (domain has no I/O)
- [x] No secrets; config via environment variables

## 6. Evidence links
- https://github.com/code-corhuila/property-payment-db/pull/1
- https://github.com/code-corhuila/property-payment-db/pull/2
- https://github.com/code-corhuila/property-payment-db/pull/3
- https://github.com/code-corhuila/property-payment-api/pull/1
- https://github.com/code-corhuila/property-payment-api/pull/2
- https://github.com/code-corhuila/property-payment-api/pull/3
