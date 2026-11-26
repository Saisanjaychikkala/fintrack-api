# FinTrack API — GitHub Copilot PL2 Assessment

## Technology stack
- Java 21, Spring Boot 3.4.5, Spring Web
- Spring Data JPA / Hibernate ORM
- H2 in-memory database for local assessment execution
- Spring Security HTTP Basic authentication (demo users)
- Jakarta Bean Validation, JUnit 5, Mockito, Maven

## Run
```bash
mvn clean test
mvn spring-boot:run
```
Base URL: `http://localhost:8080`

Demo credentials (local assessment only): `alice / change-me-alice`, `bob / change-me-bob`, `carol / change-me-carol`.

## API
- `POST /api/transactions` — create a transaction
- `GET /api/transactions` — list current user's transactions
- `GET /api/transactions/{id}` — get an owned transaction
- `DELETE /api/transactions` — delete current user's transactions only
- `POST /api/expenses` — create a shared expense
- `GET /api/expenses/balances` — get the authenticated user's net balances

Example create expense:
```json
{
  "description": "Dinner",
  "totalAmount": 120.00,
  "splitType": "EQUAL",
  "participants": [
    {"userId":"alice"},
    {"userId":"bob"},
    {"userId":"carol"}
  ]
}
```
For `CUSTOM`, provide `shareAmount` for every participant and ensure the values sum exactly to `totalAmount`.

## Important assessment notes
The initial intentionally weak Transaction module must be generated separately in GitHub Copilot using the exact prompt in `PROMPTS.md`, saved untouched, reviewed, and then replaced by the production implementation in this project. See `BASELINE_NOT_GENERATED.md` for the reserved location and provenance note. This ZIP does not claim to contain an authentic Copilot transcript or screenshots.

## Tests and cloud CI
See [UNIT_TESTS.md](UNIT_TESTS.md) for the 20-test coverage map. Maven could not be executed in the preparation environment because Maven is not installed and package downloads are unavailable. The included GitHub Actions workflow (`.github/workflows/maven.yml`) runs `mvn clean test` on GitHub-hosted runners after you upload/push the repository; it also uploads Surefire reports. Do not describe the tests as passing until the workflow finishes successfully.

## Commit history
The repository includes a Conventional Commit history. See `git log --oneline` or `GIT_HISTORY.md`. Commit metadata identifies this as AI-assisted assessment preparation; review the changes and add your own commits before submission.

## Architecture
See [ARCHITECTURE.md](ARCHITECTURE.md) and [ARCHITECTURE_DIAGRAM.md](ARCHITECTURE_DIAGRAM.md). The rendered diagram is `architecture.png`; editable Graphviz source is `architecture.dot`.

## Local/demo limitations
H2 is in-memory and resets on restart. Demo credentials are hard-coded for local assessment only. Before production, use managed identity, external secret storage, a durable database, migrations, audit events, idempotency keys, currency-aware ledger rules, and integration/security testing.
