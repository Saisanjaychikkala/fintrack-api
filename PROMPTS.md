# GitHub Copilot Prompt Record

## Required untouched baseline prompt
Use Copilot Chat and enter this text exactly. Save the generated model and service before changing either file:
> Generate a Transaction model and a Transaction service with create, get-by-user, and delete-all functions. Use a database.

**Evidence reminder:** Capture the Chat panel, exact prompt, response start, and visible Ask/Edit/Agent mode. The following chain is a reproducible prompt plan. Only mark a prompt as executed after you actually run it in Copilot.

## Expense Splitting prompt chain

| # | Exact prompt text to run | Copilot feature / mode | Technique | Rationale |
|---|---|---|---|---|
| 1 | “@workspace Review the current Transaction model, service, repositories and project instructions. Identify security, financial precision, validation and layering risks. Do not edit files. Return findings with file and method references.” | Ask Mode + `@workspace` | Role-based, specificity, constraint | Design/review before edits; no file mutation. |
| 2 | “Act as a senior fintech Java engineer. Propose the SharedExpense and ExpenseParticipant JPA entities. Use BigDecimal, UUID, Instant, explicit ownership, unique participant membership and documented assumptions. Do not generate controllers yet.” | Ask Mode | Role-based, decomposition, constraint | Isolate data model decisions. |
| 3 | “@workspace Implement the expense entities, DTOs, repository and service. Equal splits must preserve every cent deterministically; custom shares must be non-null, non-negative and sum exactly to the total. Require the authenticated creator to be a participant. Keep controllers out of this change.” | Agent Mode | Specificity, decomposition, constraints | Generate a coherent service layer in bounded scope. |
| 4 | “Using #file:BalanceCalculationService.java, review net balance direction when the current user is the payer versus a participant. Give one worked example with opposing expenses and identify any sign error. Do not edit.” | Ask Mode | Few-shot, iterative refinement | Verify business semantics independently. |
| 5 | “Add the REST endpoints for creating a shared expense and retrieving the current user's pending balances. Derive the user ID from Spring Security Authentication, validate request DTOs, and do not accept an acting user ID from the body.” | Agent Mode | Constraint, specificity | Secure API boundary. |
| 6 | “/tests Create JUnit 5 tests for equal split with remainder, valid custom split, invalid custom total, duplicate participant, creator missing from participants, one participant, opposing expenses netting to one balance, and unauthorised access. Use deterministic fixtures.” | Agent Mode + `/tests` | Specificity, decomposition | Translate acceptance criteria into executable tests. |
| 7 | “/fix Review the equal split rounding and net balance aggregation. Make the smallest correction needed, preserve public contracts, and explain the before/after behavior.” | Edit Mode + `/fix` | Iterative refinement, constraint | Targeted correction after reviewing generated output. |
| 8 | “/doc Add concise JavaDoc to public controller and service methods. Do not change behavior.” | Edit Mode + `/doc` | Constraint | Documentation without broad refactoring. |

## Post-Generation Corrections
The following are required review checkpoints for this prepared implementation; confirm them against the actual Copilot output and record the actual changes you make during your session.

1. **Equal-split remainder:** Ensure a total such as 10.00 split three ways allocates 3.33, 3.33 and 3.34, rather than losing a cent.
2. **Creator participation:** Reject expenses where the authenticated creator is not in the participant list, so the payer's own share is explicit.
3. **Duplicate participant IDs:** Reject duplicates before persistence to avoid double-counting.
4. **Custom split completeness:** Reject null shares and totals that do not exactly match the expense amount.
5. **Identity source:** Use `Authentication.getName()` instead of trusting an acting-user field from the request.
6. **Balance direction:** Check payer-versus-participant signs with multiple expenses; cancel opposing debts instead of returning gross amounts.
7. **Demo security caveat:** Replace in-memory demo users and credentials with the approved identity provider before production.
