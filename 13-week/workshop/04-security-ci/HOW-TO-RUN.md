# How to run the negative test — property-payment-api

Story: **[security] A Pago is read only by its owner** (STRIDE E).
Acceptance criterion covered: *GET /api/v1/pagos/{id} without a token answers 401
UNAUTHORIZED, checked by an automated HTTP test on every pull request.* The 403 case for
another guest is added when E-07 is implemented (batch 2).

Endpoint: `GET /api/v1/pagos/{id}` (E-07).

1. Clone `code-corhuila/property-payment-api` (branch `develop`).
2. Copy `PagoAuthorizationNegativeTest.java` to
   `payment-app/src/test/java/co/edu/corhuila/property/payment/`.
3. Run:
   ```bash
   mvn -B -pl payment-app -am -Dtest=PagoAuthorizationNegativeTest -Dsurefire.failIfNoSpecifiedTests=false verify
   ```
4. Expected: `Tests run: 2, Failures: 0` — no token and an unsigned token with `alg: none` both
   get 401 with the error envelope.

`security.yml` also runs gitleaks (the Stripe key must never be committed) and OWASP
dependency-check. The real console output is added in CP8.
