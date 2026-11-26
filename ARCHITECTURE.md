# Architecture

1. The Transaction module stores individual user-owned ledger entries; Expense Splitting records a shared expense and each participant's allocated share.
2. The expense creator is treated as the payer; participant shares define each person's portion of the total.
3. A shared expense is persisted as one parent entity with participant rows, while transaction records remain independently owner-scoped.
4. HTTP requests enter through REST controllers, which obtain the acting user from Spring Security's authenticated principal.
5. Controllers validate DTOs and delegate business operations to services; they do not access repositories directly.
6. Services enforce financial and ownership invariants and define transaction boundaries.
7. Spring Data JPA repositories isolate database access and use owner-scoped query methods where applicable.
8. Entities use UUID identifiers, `Instant` timestamps and `BigDecimal` amounts to avoid floating-point money errors.
9. Equal splits allocate residual cents deterministically so participant shares always equal the total.
10. Custom splits are rejected unless every share is supplied and the sum exactly matches the expense total.
11. Balance calculation nets amounts between each user and counterparty, cancelling opposing debts.
12. This layering supports testability, audit-oriented extension, clear authorization boundaries and future database replacement.
13. The local H2 database and demo users are assessment conveniences, not production deployment choices.
14. Production fintech use additionally requires durable storage, migrations, immutable audit events, idempotency, settlement workflows and currency-aware rules.
