# Submission Manifest

This ZIP is prepared for the **Source Code (Zipped file)** option described in the associate guide.

| Requirement | Included item | Status / note |
|---|---|---|
| Application code base | `src/main/java` | Included: Java 21 / Spring Boot API. |
| Transaction module | `src/main/java/com/fintrack/transaction` | Included: JPA entity, repository, service and controller. |
| Expense Splitting | `src/main/java/com/fintrack/expense` | Included: entities, DTOs, repository, service and endpoints. |
| Unit tests | `src/test/java`, `.github/workflows/maven.yml` | Included: 20 unit/integration test methods; CI workflow runs them on GitHub-hosted runners after push. |
| Architecture / flow diagram | `architecture.png`, `architecture.dot`, `ARCHITECTURE.md` | Included: rendered and editable diagram, plus text description. |
| Unit test documentation | `UNIT_TESTS.md` | Included. |
| Copilot project standards | `.github/copilot-instructions.md` | Included. |
| Review / prompts / PR / tool strategy | `REVIEW.md`, `PROMPTS.md`, `PR_DESCRIPTION.md`, `TOOL_STRATEGY.md` | Included as assessment documentation. Prompt execution and observed limitations must be truthfully completed from the real Copilot session. |
| Commit history | `.git` and `GIT_HISTORY.md` | Included: nine Conventional Commits after the CI trigger hardening commit. The commit author is disclosed as the assessment preparation workspace, not as a real Copilot session. |
| Untouched Copilot-generated starting point | `BASELINE_NOT_GENERATED.md`, `baseline-transaction/` | Pending: generate the baseline in Copilot and save it unchanged, as the assignment explicitly requires. No substitute code is passed off as Copilot output. |

## Before upload
1. Replace the `YOUR_ASSOCIATE_ID` filename placeholder with your actual associate ID.
2. Push the repository to GitHub and wait for the included Maven Actions workflow to run; retain its genuine test report.
3. Complete the pending baseline-generation step in GitHub Copilot.
4. Update prompt/tool documentation with the prompts you actually executed and genuine limitations you observed.
5. Review the PR disclosure and commit history against your real work.

No `node_modules`, Maven `target/`, or downloaded dependency folders are included. The `.git` directory is intentionally retained to preserve the required commit history.
