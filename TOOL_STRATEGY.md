# Copilot Tool Strategy

## Feature Usage Log
Complete the “Observed result” column after using Copilot; entries below are a suggested workflow, not claims of completed tool execution.

| # | Case-study stage | Copilot feature | Why this feature | Expected / observed result |
|---|---|---|---|---|
| 1 | Standards setup | `.github/copilot-instructions.md` | Persistent repository guidance is more reusable than repeating conventions in every prompt. | Use the file as context; record whether output follows it. |
| 2 | Baseline generation | Chat Ask Mode | Required exact low-effort prompt; preserves the intentionally unreviewed starting point. | Save both generated files untouched. |
| 3 | Review | Ask Mode + `@workspace` | Read-only cross-file review is safer before changing inherited code. | Review candidates; manually verify. |
| 4 | Understanding code | `/explain` | Explains a selected block without requiring a broad rewrite. | Compare explanation with actual behavior. |
| 5 | Remediation | Agent Mode | Multi-file architecture changes involve model, repository, service and controller. | Inspect every proposed diff. |
| 6 | Targeted correction | Edit Mode + `/fix` | Narrow changes reduce unintended edits after a defect is isolated. | Run focused tests after accepting. |
| 7 | Tests and docs | `/tests` and `/doc` | Generates a starting point for tests and API documentation. | Correct fixtures and assertions manually. |
| 8 | Commit preparation | Copilot-generated commit message | Helps draft a Conventional Commit from a reviewed diff. | Verify scope and body before committing. |

## Scenario Responses
1. **Understand a complex 500-line function:** Use Ask Mode with the selected function and `/explain`. Ask for a control-flow summary, side effects, dependencies and edge cases before requesting any modification.
2. **Consistent error handling across 8 route handlers:** Use Agent Mode with `@workspace` and a concrete existing handler as the pattern. Ask it to make a consistent multi-file change and review the diff and tests.
3. **Verify an international phone regex:** Use Ask Mode to reason through boundary cases, then run executable parameterized tests in the project's test framework. A regex explanation alone is not proof that it works.
4. **Automated code quality checks on every PR:** Use GitHub Actions (CI workflow), not Copilot Chat. Configure build, tests, static analysis and branch protection so checks run automatically for every pull request.
5. **Review AI-generated authentication for security:** Use Ask Mode with `@workspace` for a threat-oriented review, then manually inspect password storage, token validation, authorization boundaries, session handling and dependency versions. Add negative security tests; do not rely on AI review as a security sign-off.
6. **Consistent project conventions across developers:** Commit `.github/copilot-instructions.md` to the repository and keep it specific, version-controlled and reviewed. It guides Copilot but does not enforce rules, so back it with formatters, static analysis and CI.

## Limitations Encountered / Required Validation
The assessment requires three real examples. Do not submit invented observations. During your session, fill this table with the actual prompt, output, detection and correction.

| # | What you prompted/did | What Copilot produced | How detected | Fix | Next time |
|---|---|---|---|---|---|
| 1 | Ask for equal split logic | Record actual output; check remainder handling | Test 10.00 across 3 participants | Record actual correction | Include rounding examples in prompt |
| 2 | Ask for net balance calculation | Record actual output; test opposing debts | Worked example and integration test | Record actual correction | State payer/participant semantics explicitly |
| 3 | Ask for transaction delete-all | Record actual output; inspect owner scope | Manual security review and cross-user test | Record actual correction | Include tenant isolation as a hard constraint |

**Important:** Replace these planned checks with three genuine Copilot limitations observed during your own assessment. Claiming they occurred without evidence would misrepresent your work.
