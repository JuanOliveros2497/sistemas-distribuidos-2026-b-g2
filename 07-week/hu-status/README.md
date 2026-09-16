<!-- HU-STATUS TEMPLATE - do NOT remove the <!-- ... --> markers or the table headers.

     Your weekly grade is read AUTOMATICALLY from this file:
       07-week/hu-status/README.md  (inside YOUR fork). English. -->

# Weekly Status - Week 07

<!-- CONFIG-START - must match your profile repo (username/username) CONFIG -->

- FULL_NAME: Juan Esteban Oliveros Duran
- GITHUB_USER: JuanOliveros2497
- TEAM: pms-properties
- SPRINT_GOAL: Decide and document the communication mode (synchronous vs asynchronous) for every interaction in the system, justify the technology choice for each, and confirm that at least one consumer is idempotent.
<!-- CONFIG-END -->

## 1. User stories worked this week

| HU ID       | Title                                                                                | Status (todo/doing/done) | Evidence (PR or commit URL) |
| ----------- | ------------------------------------------------------------------------------------ | ------------------------ | --------------------------- |
| HU-COMM-001 | Document sync vs async decision with justification for all seven system interactions | done                     | Not added yet               |
| HU-COMM-002 | Document delivery semantics (at-least-once) and exactly-once processing strategy     | done                     | Not added yet               |
| HU-COMM-003 | Verify and document the idempotent consumer in Payment Service                       | done                     | Not added yet               |
| HU-COMM-004 | Add timeouts and circuit breakers to remaining synchronous calls                     | todo                     | Not added yet               |

## 2. My individual contribution

- Created `communication-matrix.md`, documenting all seven interactions in the system with an explicit synchronous/asynchronous decision and a written justification for each.
- Classified the three synchronous interactions as REST (frontend → Booking, frontend → Catalog, Booking → Catalog for property validation) and documented why gRPC was not adopted: the sync paths are either browser-facing or low-volume, while the critical internal traffic is already asynchronous by design through the Saga.
- Classified the four asynchronous interactions as pub/sub topics, including the pub/sub case where a single fact (`ReservaConfirmada`) fans out to multiple independent consumers (Catalog read model + Notification).
- Documented the delivery semantics table: the broker runs at-least-once, exactly-once delivery is impossible end-to-end, and the system targets exactly-once _processing_ via idempotency keys and deduplication.
- Verified and documented the idempotent consumer requirement: Payment Service handling `ReservaCreada` applies both technical idempotency (`eventId` in `processed_events`) and business idempotency (`reservaId` already charged), backed by the `UNIQUE` constraint on `processed_event_id` in the `payments` table.
- Identified the two remaining synchronous service-to-service calls (Booking → Catalog, Payment → external gateway) as the points that require timeouts, retry with backoff, and circuit breakers to prevent the cascading-failure scenario.

## 3. Blockers and risks

- Timeouts and circuit breakers for the two remaining synchronous calls are documented as requirements but not yet implemented in code — until then, a slow external payment gateway could still exhaust Payment Service's thread pool.
- Broker choice (Kafka vs RabbitMQ) is still not finalized, so topic naming remains in neutral dot-notation and no broker-specific configuration (partitions, exchanges, consumer groups) has been defined.
- The idempotent consumer logic is documented and designed but not yet running against a real broker — it has not been validated under actual duplicate delivery conditions.

## 4. Plan for next week

- Implement timeouts, retry with backoff, and a circuit breaker for the Booking → Catalog call and the Payment → external gateway call.
- Decide the broker (Kafka or RabbitMQ) and update `communication-matrix.md` and `domain-events.md` with broker-specific configuration.
- Write an integration test that delivers the same `ReservaCreada` event twice and asserts only one `Pago` row is created, validating the idempotency design end-to-end.

## 5. Compliance self-check

- [ ] Conventional Commits - `type(scope): summary`
- [ ] Per-environment HU branch + PR to that environment (hu-xxx-dev -> develop, ...) — not yet in place; team still works directly on `main`
- [x] Testable acceptance criteria — defined for HU-COMM-003: delivering the same `ReservaCreada` twice must result in exactly one `Pago` record
- [ ] Tests added/updated (unit / integration) — N/A this week; the idempotency integration test is planned for next week
- [x] DDD / hexagonal boundaries respected (domain has no I/O) — the idempotency check lives in the application/use-case layer and the repository port, not inside the `Pago` domain entity
- [x] No secrets; config via environment variables — no credentials involved in this week's documentation work

## 6. Evidence links

- Not added yet
