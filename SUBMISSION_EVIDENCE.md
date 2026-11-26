# Submission Evidence Checklist — Complete in Your Own IDE

The source ZIP is one permitted route, but the assessment evaluates process and judgment. Use your actual VS Code/JetBrains + GitHub Copilot session to capture truthful evidence.

## Required screenshots for the screenshot-based route
- [ ] 1.1 IDE, project tree, Copilot extensions active, account/license details as requested by the guide.
- [ ] 1.2 Full `.github/copilot-instructions.md`.
- [ ] 2.1 Exact low-effort Transaction prompt and Copilot mode/response.
- [ ] 2.2 Untouched generated Transaction model and service.
- [ ] 3.1 Copilot-assisted review prompts and responses (2–3 screenshots).
- [ ] 3.2 At least one issue you personally identified that Copilot missed.
- [ ] 4.1 Remediation prompts and mode indicators (2–3 screenshots).
- [ ] 4.2 Remediated model, repository and service code.
- [ ] 5.1 At least four prompts in the feature prompt chain.
- [ ] 5.2 At least two different Copilot modes in action.
- [ ] 5.3 Shared Expense model, balance service and endpoints.
- [ ] 5.4 At least six tests and actual passing test output, if passing.
- [ ] Embed screenshots directly in one Word document; keep it below 4 MB.

## Source-code ZIP route
Include the application source, documentation, architecture/flow diagram and unit-test documentation. Do not include `target/`, `.git/`, IDE caches or downloaded dependency folders. Keep the ZIP below 300 MB.

## Filename
The guide's screenshot-document naming is `<AssociateID>_SBA_GitHubCopilot_<YourName>.docx`. Its source-code section repeats `.docx` despite asking for a ZIP, which is internally inconsistent. For the ZIP, use the same stem with `.zip`: `<AssociateID>_SBA_GitHubCopilot_<YourName>.zip`.

Current prepared name uses `YOUR_ASSOCIATE_ID` because the associate ID was not present in the supplied material. Replace it with your actual associate ID before uploading.

## Git commit history
From the project root, run these commands after reviewing the files:
```bash
git init
git add .github README.md
git commit -m "chore: add project standards" -m "Define Java stack, architecture, security and testing conventions."
git add src/main/java/com/fintrack/transaction REVIEW.md
git commit -m "fix: remediate transaction module" -m "Introduce owner-scoped persistence, validation and layered transaction services."
git add src/main/java/com/fintrack/expense
git commit -m "feat: add shared expense splitting" -m "Support equal and custom allocations with net balance calculation."
git add src/test PROMPTS.md PR_DESCRIPTION.md TOOL_STRATEGY.md ARCHITECTURE.md
git commit -m "test: document expense splitting delivery" -m "Add assessment tests, prompt record, PR notes and architecture documentation."
```

## Final verification
- [ ] Replace all placeholders and planned observations with truthful evidence.
- [ ] Run `mvn clean test` and record the actual result.
- [ ] Add integration tests for persisted netting and authorization before claiming those paths are fully tested.
- [ ] Ensure your own generated baseline files are preserved separately and unmodified.
