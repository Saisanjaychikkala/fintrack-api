# Transaction Module — Code Review and Remediation

## Review scope and provenance
The assessment asks the associate to generate the baseline in Copilot with this exact prompt: “Generate a Transaction model and a Transaction service with create, get-by-user, and delete-all functions. Use a database.” Save that output unchanged before review. The baseline below is a review checklist of likely failure modes, not a claim that an unobserved Copilot output contained every item. Replace/confirm findings against the actual generated files and capture the evidence screenshots.

## Review findings (validate against your generated baseline)

| # | Location | Category | Severity | Issue and fintech impact | Detection | Recommended remediation |
|---|---|---|---|---|---|---|
| 1 | Transaction amount field | Standards / financial correctness | Critical | `double`/`float` can introduce rounding drift in balances and ledger totals. | Manual review; inspect numeric type | Use `BigDecimal(19,2)` and explicit rounding. |
| 2 | Delete-all service method | Security | Critical | Unscoped delete can erase every user's financial history. | Ask Mode security review plus manual query inspection | Require authenticated owner and repository `deleteAllByOwnerId`. |
| 3 | Get-by-user query | Security | Critical | Missing owner filter can disclose another user's transactions. | Manual review of repository predicate | Scope every query to authenticated principal. |
| 4 | Database access in service | Architecture | High | Raw JDBC/driver code couples business logic to storage and increases injection/transaction risks. | @workspace architecture review | Use Spring Data JPA repository. |
| 5 | Request amount | Validation | High | Zero, negative, excessive precision or null amounts can corrupt accounting. | /explain plus boundary tests | Bean Validation and service invariants. |
| 6 | Exception handling | Reliability | High | Generic catches or swallowed exceptions hide failed writes and make clients mis-handle outcomes. | Manual review and failure tests | Typed exceptions and centralized HTTP mapping. |
| 7 | Currency representation | Financial correctness | High | Missing currency or inconsistent currency codes make sums ambiguous. | Domain review | Store ISO-like 3-letter code; disallow cross-currency netting without FX. |
| 8 | Logging | Security / operations | Medium | Printing full objects can leak financial data or PII. | Manual review of log statements | Parameterized logs with identifiers only. |
| 9 | Missing ownership test | Testing | High | Cross-user access regressions can ship unnoticed. | Test-gap analysis | Add tests for owner-scoped get/list/delete. |
| 10 | Missing transaction boundary | Reliability | Medium | Partial multi-row writes can leave inconsistent records. | Architecture review | Use service-level `@Transactional`. |

## Review process
1. Preserve the untouched generated files and record the exact prompt and Copilot mode.
2. Ask Copilot in Ask Mode to review the model and service for security, money handling, data integrity, and architecture.
3. Use `/explain` on suspicious persistence and delete code; compare the explanation with the actual code.
4. Manually inspect ownership predicates, decimal types, validation, exception paths, logging, and transaction boundaries.
5. Convert each confirmed finding into a test or a specific remediation. Copilot suggestions are hypotheses, not proof.

## Issues Copilot Introduced That Required Human Judgment
- **Currency precision and rounding policy:** a code model may generate syntactically valid floating-point arithmetic. A developer must recognise that tiny representation errors accumulate and can create incorrect financial balances.
- **Meaning of delete-all:** “delete all” is ambiguous without a tenant/owner boundary. Human review must interpret it as “all records belonging to the authenticated user,” not a global table delete.
- **Balance semantics:** a mathematically valid split can still be financially wrong if the creator/payer and each participant's share are not defined. The domain rule must be confirmed with product requirements.
