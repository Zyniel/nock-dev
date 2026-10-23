# Nock Dev Framework

This repository is the operational layer for Nock. It is intentionally separate from the stable application repository.

## Purpose

This repo defines how work enters the system, how design is approved, how features are spec'd, how implementation is reviewed, and how releases remain safe.

## Core principle

No implementation starts from a vague prompt alone.

Every feature must be linked to:
- a backlog item
- an approved design direction or documented design exception
- a behavior spec
- a testable acceptance criteria set
- a review gate
- a release gate

## Lifecycle

1. Idea intake
2. Proposal generation
3. Human design approval
4. Feature spec creation
5. Test writing
6. Implementation
7. Review
8. Release gate

## Governance package

- `Backlog.md`
- `status.md`
- `governance/product-contract.md`
- `governance/review-rules.md`
- `governance/release-checklist.md`
- `governance/quality-gates.md`
- `docs/workflow/design-approval.md`
- `docs/workflow/feature-lifecycle.md`
- `docs/workflow/release-flow.md`
- `docs/workflow/github-operating-model.md`

## Exact human workflow

### 1. New idea arrives
A requirement is captured in a GitHub issue or a human brief.

### 2. Backlog item is created
A backlog item is added to `Backlog.md` or a GitHub Project board.

Each backlog item must indicate:
- status
- priority
- owner
- target release
- problem statement
- scope
- design link
- spec link
- dependencies
- notes

### 3. Design proposal is written
Claude creates 2-4 design options in `docs/design/proposals/` or in a GitHub issue template for design proposals.

### 4. Human picks one design
The chosen direction becomes the approved design contract and moves to `docs/design/approved/`.

### 5. Design contract is linked into the feature
The product and UX contract is linked from the backlog item and the feature spec.

### 6. Feature spec is written
A feature spec is created from the approved design and product goals.

The spec must define:
- goal
- context
- public interface or behavior
- acceptance criteria
- edge cases and errors
- out of scope
- design contract linkage
- open questions

### 7. Tests are written first
Implementation starts only after the spec and acceptance criteria exist.

### 8. Implementation
Claude implements only the approved scope and under the approved design contract.

No hidden scope additions are allowed.

### 9. Review
The review stack checks:
- behavior against the spec
- design conformance against the approved design
- release safety and regression risk

### 10. Release gate
A final human signoff is required before shipping.

## Decision rules

- No vague prompt becomes implementation.
- No workflow starts without a backlog item.
- No design changes become live product without approval.
- No feature is approved without a spec.
- No PR is approved without a linked design + spec + tests.
- No release occurs without passing checks and human signoff.

## Templates included

- `templates/feature-brief.md`
- `templates/design-proposal.md`
- `templates/approved-design.md`
- `templates/spec.md`
- `templates/backlog-item.md`
- `templates/issue-feature.md`
- `templates/issue-design-proposal.md`
- `templates/pr-template.md`

## GitHub integration

The repo also includes the recommended GitHub governance elements:
- `CODEOWNERS`
- `.github/ISSUE_TEMPLATE/*.md`
- `.github/pull_request_template.md`
- `.github/workflows/pr-gate.yml`
- `.claude/settings.json`

## Product-safe AI working model

- Claude may propose ideas and design directions.
- Claude may generate implementation, but only inside approved specs and design contracts.
- Human remains the decision-maker for product changes and release approval.
- Review agents protect product, design, and release safety.

This is the recommended model for Nock and any public app where the app must remain stable even if the owner does not maintain it directly.
