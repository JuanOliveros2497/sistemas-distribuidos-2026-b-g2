<!-- HU-STATUS TEMPLATE - do NOT remove the <!-- ... --> markers or the table headers.
     Your weekly grade is read AUTOMATICALLY from this file:
       11-week/hu-status/README.md  (inside YOUR fork). English. -->

# Weekly Status - Week 11

<!-- CONFIG-START - must match your profile repo (username/username) CONFIG -->
- FULL_NAME: Juan Esteban Oliveros Duran
- GITHUB_USER: JuanOliveros2497
- TEAM: Pms_Property
- SPRINT_GOAL: Make the property search observable — the request through the gateway and Catalog, and the availability updates that Catalog consumes from Booking events — and start corte 3 with the real services.
<!-- CONFIG-END -->

## 1. User stories worked this week
| HU ID | Title | Status (todo/doing/done) | Evidence (PR or commit URL) |
|---|---|---|---|
| W11-CP1 | Trace map of the search and of the availability update (gateway, catalog-service, MongoDB, RabbitMQ) | done | https://github.com/JuanOliveros2497/sistemas-distribuidos-2026-b-g2/blob/main/11-week/workshop/01-journey.md |
| W11-CP2 | JSON log contract for Catalog with search and event fields | done | https://github.com/JuanOliveros2497/sistemas-distribuidos-2026-b-g2/blob/main/11-week/workshop/02-log-contract.md |
| W11-CP3 | Python middleware, logger, trace in the Mongo query comment and `/metrics` | done | https://github.com/JuanOliveros2497/sistemas-distribuidos-2026-b-g2/tree/main/11-week/workshop/03-instrumentation |
| W11-CP4 | Golden signals for gateway, Catalog, its consumer and MongoDB | done | https://github.com/JuanOliveros2497/sistemas-distribuidos-2026-b-g2/blob/main/11-week/workshop/04-metrics.md |
| W11-CP6..CP9 | SLOs, alerts, runbook and incident drill | todo | — |

## 2. My individual contribution
- Mapped the search journey and how the trace crosses from Booking to Catalog through the outbox and RabbitMQ.
- Defined the log contract of Catalog, with `event_id` and `delivery_attempt` for the consumer.
- Wrote and tested a Python module of `catalog-service` that carries the `trace_id` into the MongoDB query.
- Wrote the metric catalog, with the labels that must stay out (city, property id).

## 3. Blockers and risks
- Catalog is not built yet; the module runs on in-memory data.
- The outbox of Booking must store `traceparent` so the consumer keeps the same trace.

## 4. Plan for next week
- Delivery 2 of the workshop (CP6 to CP10).
- Corte 3: real `catalog-service` with FastAPI and MongoDB.

## 5. Compliance self-check
- [x] Conventional Commits - `type(scope): summary`
- [ ] Per-environment HU branch + PR to that environment (hu-xxx-dev -> develop, ...) — *(individual workshop in my fork)*
- [x] Testable acceptance criteria
- [x] Tests added/updated (unit / integration) — *(`tests/test_trace_propagation.py`)*
- [ ] DDD / hexagonal boundaries respected (domain has no I/O)
- [x] No secrets; config via environment variables

## 6. Evidence links
- Workshop: https://github.com/JuanOliveros2497/sistemas-distribuidos-2026-b-g2/tree/main/11-week/workshop
- property-docs: https://github.com/code-corhuila/property-docs
