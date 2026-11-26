# Unit and Integration Test Documentation

## Cloud execution
The repository includes `.github/workflows/maven.yml`. Once pushed to GitHub, the workflow runs `mvn --batch-mode --no-transfer-progress clean test` on GitHub-hosted Ubuntu with Temurin Java 21 and uploads Surefire reports as an Actions artifact. It runs on pushes to `main`/`master`, pull requests, and manual dispatch.

## Local execution (optional)
```bash
mvn clean test
```

## Test coverage map

| Test | Type | Requirement demonstrated |
|---|---|---|
| `equalSplitAmongThreeAllocatesRemainderWithoutLosingCents` | Unit | Three-way equal split conserves the total and allocates residual cents deterministically. |
| `customSplitMatchingTotalIsAccepted` | Unit | Custom participant shares equal to the total are accepted. |
| `customSplitNotMatchingTotalFails` | Unit | A custom split whose sum differs from the total is rejected. |
| `creatorMustBeOneOfParticipants` | Unit | The authenticated creator must be included in the participant list. |
| `duplicateParticipantsAreRejected` | Unit | Duplicate participant IDs are rejected. |
| `oneParticipantIsRejected` | Unit | A shared expense requires at least two participants. |
| `customSplitRejectsNegativeShareEvenWhenTotalMatches` | Unit | A negative share cannot be hidden by an offsetting positive share. |
| `equalSplitRejectsCustomAmountsToAvoidAmbiguousInput` | Unit | Equal-split requests cannot silently include custom amounts. |
| `customSplitRejectsAmountsWithMoreThanTwoDecimalPlaces` | Unit | Custom monetary shares respect two-decimal precision. |
| `balanceForDebtorShowsAmountTheyOwe` | Unit | A participant sees the amount owed to the payer. |
| `netBalancesCombineOpposingDebtsAndCancel` | Unit | Opposing debts between two people net to one amount. |
| `unauthenticatedTransactionRequestIsRejected` | Integration | Protected transaction endpoints reject anonymous requests. |
| `unauthenticatedExpenseRequestsAreRejected` | Integration | Protected expense creation and balance endpoints reject anonymous requests. |
| `transactionListIsScopedToAuthenticatedUser` | Integration | A user's transaction list does not disclose another user's records. |
| `anotherUserCannotRetrieveTransactionById` | Integration | Direct retrieval is owner-scoped and returns not found for another user's record. |
| `deleteAllOnlyDeletesTheAuthenticatedUsersTransactions` | Integration | Delete-all affects the authenticated user's records only. |
| `expenseCreationRequiresAtLeastTwoParticipants` | Integration | HTTP validation rejects a one-person expense. |
| `invalidCustomSplitAndMalformedJsonReturnBadRequest` | Integration | HTTP API maps mismatched custom splits and malformed JSON payloads to structured 400 responses. |
| `expenseCreationAndBalanceLookupUseAuthenticatedIdentity` | Integration | Persisted expense allocation appears in the other participant's balance. |
| `persistedOpposingExpensesAreNettedBetweenTwoUsers` | Integration | Two saved expenses in opposite directions are netted correctly. |

**Total: 20 test methods (11 unit, 9 integration).** Test sources are included; passing status must come from an actual Maven/CI execution and is not assumed by this document.

## Known test limitations
The suite uses an in-memory H2 database and demo HTTP Basic users. It does not replace PostgreSQL integration testing, concurrency tests, penetration testing, currency-conversion tests, settlement workflows, or a full audit-ledger test suite. The GitHub Actions workflow is included so those Maven tests can run in GitHub's cloud without installing Java or Maven on the associate's computer.
