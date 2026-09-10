<!-- HU-STATUS TEMPLATE - do NOT remove the <!-- ... --> markers or the table headers.

     Your weekly grade is read AUTOMATICALLY from this file:
       06-week/hu-status/README.md  (inside YOUR fork). English. -->

# Weekly Status - Week 06

<!-- CONFIG-START - must match your profile repo (username/username) CONFIG -->

- FULL_NAME: Juan Esteban Oliveros Duran
- GITHUB_USER: JuanOliveros2497
- TEAM: pms-properties
- SPRINT_GOAL: Harden the local orchestration of the three microservices with Docker Compose: real healthchecks, deterministic startup order via condition: service_healthy, and per-environment configuration overrides (dev/prod).
<!-- CONFIG-END -->

## 1. User stories worked this week

| HU ID        | Title                                                                                              | Status (todo/doing/done) | Evidence (PR or commit URL) |
| ------------ | -------------------------------------------------------------------------------------------------- | ------------------------ | --------------------------- |
| HU-INFRA-004 | Add healthchecks to all databases (booking-db, payment-db, catalog-db)                             | done                     | Not added yet               |
| HU-INFRA-005 | Add healthchecks to all microservices and gate startup with depends_on: condition: service_healthy | done                     | Not added yet               |
| HU-INFRA-006 | Split configuration into docker-compose.override.yml (dev) and compose.prod.yml (prod)             | done                     | Not added yet               |
| HU-INFRA-007 | Add curl to each service's runtime image to support HTTP healthchecks                              | done                     | Not added yet               |

## 2. My individual contribution

- Updated `docker-compose.yml` to add a real `healthcheck` for each database: `pg_isready` for `booking-db` and `payment-db` (PostgreSQL), and `mongosh --eval "db.adminCommand('ping')"` for `catalog-db` (MongoDB).
- Replaced the simple `depends_on` list with `depends_on: { <db>: { condition: service_healthy } }` for all three microservices, so each service waits for its database to be truly ready, not just started.
- Added HTTP healthchecks (`curl -f http://localhost:<port>/health`) to `booking-service`, `payment-service`, and `catalog-service`, reusing the `/health` endpoint built in the Week 04 walking skeleton.
- Created `docker-compose.override.yml` for local development (sets `SPRING_PROFILES_ACTIVE=dev` per service, applied automatically with `docker-compose up`).
- Created `compose.prod.yml` for production (sets `SPRING_PROFILES_ACTIVE=prod` and resource limits, applied explicitly with `-f`), keeping all credentials external via environment variables — nothing hardcoded.
- Updated each service's `Dockerfile` to install `curl` in the runtime stage (`eclipse-temurin:21-jre` does not include it by default), required for the service-level healthcheck to work.
- Verified locally that `docker-compose up --build` starts databases first, waits for them to report `healthy`, and only then starts the dependent microservices — eliminating the previous race condition where a service could fail to connect to a database that was "started" but not yet accepting connections.

## 3. Blockers and risks

- Healthchecks are configured but not yet validated against a fully implemented `/health` endpoint in `payment-service` and `catalog-service` (only `booking-service` has it built so far from the Week 04 skeleton) — risk that their healthchecks fail until those endpoints exist.
- `compose.prod.yml` resource limits (`memory: 512M`) are placeholder values, not yet based on real load testing.
- Still pending: deciding whether production deployment will remain single-host Compose for the MVP1 release, or require moving to an orchestrator (Kubernetes) — out of scope for now per the session's guidance ("Compose is fine for a single host; move to an orchestrator only when you need multiple hosts, self-healing, rolling updates or autoscaling").

## 4. Plan for next week

- Build the `/health` endpoints for `payment-service` and `catalog-service` so all three service-level healthchecks actually pass.
- Run a full `docker-compose up --build` in CI (not just locally) to confirm the deterministic startup order holds outside a developer machine.
- Begin wiring the MVP1 vertical slice (`POST /reservas`) end-to-end on top of this now-hardened orchestration setup.

## 5. Compliance self-check

- [ ] Conventional Commits - `type(scope): summary`
- [ ] Per-environment HU branch + PR to that environment (hu-xxx-dev -> develop, ...) — N/A, work done directly on `main` this week
- [x] Testable acceptance criteria — verifiable via `docker-compose up --build`: databases must reach `healthy` before dependent services start
- [ ] Tests added/updated (unit / integration) — N/A, infrastructure/orchestration work, no application code changed
- [ ] DDD / hexagonal boundaries respected (domain has no I/O) — N/A, purely Docker Compose / infrastructure work
- [x] No secrets; config via environment variables — all credentials remain in `.env` / `.env.example`; `compose.prod.yml` only sets non-sensitive profile and resource values

## 6. Evidence links

- Not added yet
