# Nock Development Canvas Methodology

This document is the operating system for reworking the current `nock` repository using a GitHub-backed, design-first, spec-driven development process. It is intended to be fed directly to a Claude AI engine so that the repository is restructured and rebuilt around a safer, more controlled product lifecycle.

## 1. Objective

The goal is to transform `nock` from an ad hoc or loosely governed app repository into a stable, reviewable, product-safe codebase that follows a strict development canvas:

- work is initiated from backlog items
- design is approved before implementation
- behavior is specified before code is written
- tests are written before implementation or alongside the spec
- pull requests are review-gated
- releases are human-approved
- GitHub is the control layer
- Claude is a bounded implementation engine, not an autonomous product owner

This methodology is intentionally more structured than a normal feature workflow. The point is to prevent drift, uncontrolled redesign, hidden scope, and fragile public-facing changes.

## 2. Operating principle

The repository must be reworked around a simple principle:

AI can propose. Humans approve. Code is implemented only in approved scope.

This means:

- Claude may generate design options, rough implementations, and refactors
- Claude may not mutate the live product without a valid design contract and human approval
- Claudia must work from approved backlog items, specs, and design approvals
- every change must be traceable in GitHub

## 3. Separation of responsibilities

### 3.1 Stable app repo
The main app repository (`nock`) is the runtime product repository. It contains:

- product code
- app logic
- UI code
- backend or service code
- tests
- build tooling
- deployment configuration

This repository should be treated as the product implementation layer.

### 3.2 Governance repo
The governance repo (`nock-dev`) is the control layer. It contains:

- product governance
- backlog
- design proposals
- approved design contracts
- feature specs
- review rules
- release gates
- issue and PR templates
- workflow docs
- GitHub automation metadata

The governance repo is not where the live app logic lives. It is where the product process lives.

## 4. Development canvas: the core workflow

The new development canvas is a controlled loop with these stages:

1. Idea intake
2. Requirement capture
3. Backlog item creation
4. Design proposal generation
5. Design approval
6. Feature spec creation
7. Acceptance criteria definition
8. Test writing
9. Implementation
10. Review
11. Release gate
12. Human release signoff

This flow must be applied to every feature, fix, UX improvement, and product change.

## 5. Mandatory rules

These are non-negotiable.

### 5.1 No vague implementation
Claude must never work directly from a vague prompt like:

- “make this app better”
- “redesign the dashboard”
- “fix the UX”
- “improve this flow”

without first converting the request into one of the following:

- backlog item
- approved design proposal
- feature spec
- acceptance criteria
- review gate

### 5.2 No design without approval
No route, page, modal, flow, layout change, or state change may be implemented unless:

- it has been proposed
- a human selected the best option
- it was recorded as an approved design contract

### 5.3 No implementation without spec
Every feature or meaningful change must include a spec that defines:

- context
- expected behavior
- acceptance criteria
- edge cases
- error states
- out of scope items
- linked design contract

### 5.4 No scope creep
Implementation must stay inside approved scope. If additional requirements appear:

- they must be documented
- the spec must be updated
- the backlog item must be updated
- the design must be re-approved if necessary

### 5.5 No release without gate
A feature or change is not releasable unless:

- tests pass
- build passes
- design review passes
- spec compliance passes
- QA or smoke checks pass
- human approval is recorded

### 5.6 Human-owned decision points
The following are explicitly human decisions:

- product goals
- design approval
- release approval
- major UX changes
- behavior changes that affect public-facing flows
- scope expansion
- public release

## 6. GitHub as the product control layer

GitHub must be configured as the central operating layer for the product.

### 6.1 Project board
Create a Project v2 with lanes such as:

- Idea
- Proposal
- Approved
- Spec Ready
- In Progress
- Review
- Blocked
- Done
- Released

Add fields:

- Priority: P0/P1/P2/P3
- Area: backend/frontend/design/infra/tests
- Status: proposed/approved/review/blocked/done
- Design link
- Spec link
- Release target
- Risk: low/medium/high
- Human approval: yes/no

This board represents the product’s real flow.

### 6.2 Issues
Use GitHub Issues as the intake system:

- feature requests
- design proposals
- bug reports
- technical debt
- spec requests
- release notes issues

Each issue must have the required fields:

- summary
- problem statement
- goal
- in scope
- out of scope
- constraints
- design link
- spec link
- priority
- release target

### 6.3 Pull requests
All product changes must go through PRs.

PRs must require:

- linked issue
- linked approved design
- linked spec
- summary of the change
- in scope/out of scope
- tests added or changed
- validation performed
- reviewer notes

PRs should be the only path to merging a feature branch into main.

### 6.4 Branch protection
Protect the main branch.

Required settings:

- require PR before merge
- require status checks to pass
- require approval
- require conversation resolution
- require branch update before merge
- disallow force pushes
- restrict direct pushes to maintainers

## 7. Development canvas phases in detail

### Phase 1: Idea intake
The AI or the human enters a feature concept as a GitHub issue or brief.

The issue must answer:

- what problem needs solving
- who it affects
- what outcome is desired
- what is in scope
- what is out of scope
- any business or technical constraints

This is not yet implementation. This is the entry into the system.

### Phase 2: Backlog creation
Convert the idea into a backlog item.

Backlog item fields:

- title
- status
- priority
- owner
- target release
- problem statement
- scope
- assumptions
- dependencies
- design link
- spec link

The backlog item is the source of truth for the work item. It is not optional.

### Phase 3: Design proposal generation
Claude generates 2–4 design directions.

Each design proposal should include:

- summary
- problem to solve
- design option A/B/C
- pros/cons
- risks
- implementation complexity
- user impact
- alignment with current app shell

Design proposals do not become implementation until someone approves them.

### Phase 4: Design approval
A human picks a design direction.

The selected option becomes the approved design contract.

Approved design contract must specify:

- screens affected
- user flow changes
- interaction rules
- layout conventions
- accessibility requirements
- states and transitions
- boundaries / out-of-scope items

This approved design becomes the binding contract for implementation.

### Phase 5: Feature spec creation
From the approved design, a detailed feature spec is produced.

Spec sections:

- goal
- context
- public behavior or API contract
- user stories
- acceptance criteria
- edge cases
- error handling
- non-goals
- dependency requirements
- design references
- open questions

The feature spec is the implementation contract. It must be written before code.

### Phase 6: Test-first workflow
Before code, write the tests that define expected behavior.

This includes:

- unit tests
- component tests
- integration tests
- browser smoke tests when UI is impacted
- accessibility checks for relevant flows

The rule is simple:

If the behavior is not testable, it is not sufficiently specified.

### Phase 7: Implementation
Implementation occurs only within the approved scope.

Claude must:

- respect the design contract
- respect the feature spec
- avoid hidden scope
- avoid unrelated refactors
- preserve current app conventions unless explicitly approved

If implementation begins drifting away from the contract, it must stop and request a review or approval.

### Phase 8: Review
Review is not optional.

There are three review lenses:

1. Design review
   - Does the implementation match the approved design?

2. Spec review
   - Does the implementation meet the feature spec and ACs?

3. Release / QA review
   - Does it pass the gate and is it safe to release?

A PR should not merge if any of these fail.

### Phase 9: Release gate
Before a feature is released:

- all required tests pass
- build passes
- affected flows smoke-tested
- accessibility checks pass
- design drift is checked
- regression risk is reviewed
- notes are written
- final human approval is granted

The release gate is mandatory.

## 8. Detailed acceptance criteria rules

Every feature must include measurable success criteria.

Examples:

- “When the user presses submit, the server returns success and the UI shows confirmation.”
- “The modal traps focus and returns focus to the trigger after close.”
- “When the request fails, the user sees an inline error state and can retry.”
- “The route remains stable and no existing navigation breaks.”

Acceptance criteria should be written in concrete, testable language.

## 9. Required metadata for each work item

Every feature item should include:

- title
- owner
- priority
- status
- target release
- problem statement
- user impact
- summary
- urgency
- design link
- spec link
- issue link
- dependencies
- rollout risk
- testing plan

This is what Claude must use to understand the current state.

## 10. Claude operating instructions

Claude must operate under this policy:

### 10.1 First action
Read the current backlog item or issue and identify:

- the objective
- the approved design link
- the spec link
- the acceptance criteria
- the relevant tests

### 10.2 Second action
Confirm the work is in scope and matches the approved design contract.

### 10.3 Third action
Write or update the failing tests if applicable.

### 10.4 Fourth action
Implement only the approved scope.

### 10.5 Fifth action
Run the relevant build, test, and validation checks.

### 10.6 Sixth action
Open or update the PR with complete evidence:

- issue link
- design link
- spec link
- summary
- tests
- validation results
- review notes

### 10.7 Seventh action
Do not act beyond the defined feature.

## 11. What Claude is allowed to do

Claude may:

- generate design options
- draft specs
- propose architecture changes within approved scope
- refactor code if required by the approved plan
- create issue drafts
- generate planning docs
- write tests
- implement code for approved features
- produce PR descriptions
- prepare release notes

Claude may not:

- directly ship changes without a PR
- bypass the design approval process
- broaden scope without approval
- redesign the app without a human-approved contract
- merge to main directly
- edit protected repo security settings or governance without approval

## 12. Detailed repository rework methodology

If the goal is to “completely rework the current nock repository with the new development canvas,” then the work must happen in phases.

### Phase A: establish the stable baseline
1. Inventory current repository state
2. Identify current app routes, pages, features, and user flows
3. Identify areas that are high-risk, high-change, or fragile
4. Freeze the current baseline for reference
5. Create a product overview and route map

### Phase B: create the development canvas in the governance repo
1. Add backlog file(s)
2. Add design proposal templates
3. Add approved design templates
4. Add spec templates
5. Add review rules
6. Add release gates
7. Add GitHub labels and board setup
8. Add branch protection configuration docs

### Phase C: map the current app into feature “domains”
Group the existing app into domains such as:

- auth
- dashboard
- settings
- data views
- notifications
- billing / subscriptions
- onboarding
- account management
- user flows

This helps convert ad hoc work into backlog items.

### Phase D: backlog conversion
For each domain or feature, determine:

- what the feature is
- what problem it solves
- what should remain stable
- what is low-risk vs high-risk
- what UI states exist
- what should be redesigned or kept

Then create backlog items and issue templates.

### Phase E: choose design direction
For each feature or group of features:

- generate proposal options
- compare trade-offs
- choose the best approved design
- save the approved design as the product contract

### Phase F: spec creation
Turn each approved design into a feature spec.

The spec is the source for coding requirements and tests.

### Phase G: test-first implementation
For each approved spec:

- write or update failing tests
- run them and confirm failure
- implement the patch
- validate the behavior
- update the PR with evidence

### Phase H: review and release
Once the feature passes:

- design review
- spec review
- quality gate
- smoke tests
- release checklist

Then a human signs off for release.

## 13. Quality gates in detail

### Mandatory gates
- spec check
- tests check
- lint and formatting check
- type check
- build check
- smoke check
- accessibility check if UI affected
- design conformance check if UI affected
- release checklist signoff

### Gate rules
- If a required gate fails, the PR does not merge.
- If a design change was not approved, the PR is blocked.
- If a spec is missing, the PR is blocked.
- If scope expanded unexpectedly, the PR is blocked until re-approved.

## 14. Definitions of done

A feature is done only when all of the following are true:

- backlog item exists
- approved design exists
- feature spec exists
- acceptance criteria are written and tested
- implementation matches the spec
- tests pass
- build passes
- review passes
- release gate passes
- human signoff is recorded

## 15. Release discipline

The release flow should be explicit and stable.

Release checklist:

- version baseline is known
- release notes are written
- QA evidence exists
- design contract remains aligned
- no open blockers remain
- human signoff is recorded

Do not release from a vague “looks good to me” state. Release must be evidence-based and human-approved.

## 16. Risk categories

The system must explicitly track and validate risks.

### Product risk
- Is behavior changing in a way the user will notice?
- Does the design remain coherent?

### Technical risk
- Are new dependencies introduced?
- Are there hidden migrations, schema changes, or route changes?

### UX risk
- Does the change affect accessibility or navigation?
- Does it break a critical user flow?

### Delivery risk
- Is the feature large or vague?
- Is the spec incomplete?

## 17. Detailed repository governance expectations

The repository should be organized around clear boundaries:

- `docs/` for operating docs and product governance
- `templates/` for reusable item templates
- `governance/` for product, design, release, and quality policy
- `specs/` for formal feature specifications
- `issues/` or GitHub issue templates for intake
- `.github/` for GitHub management and PR templates
- app repo for real product code

This separation keeps governance and product implementation distinct and safe.

## 18. What the Claude engine should optimize for

The Claude-powered workflow should optimize for:

- traceability
- design safety
- minimal scope drift
- testability
- release readiness
- maintainability
- operational clarity

It should not optimize for:

- broad large-scale redesigns
- undocumented feature exploration
- unreviewed product changes
- moving fast without evidence

## 19. Final rule set for the new development canvas

Use this as the final guardrail set for the AI engine:

1. All work must begin as a backlog item or issue.
2. Design must be proposed and approved before implementation.
3. Specs must exist before tests and implementation start.
4. Tests must be written before or alongside implementation.
5. No change is accepted without a PR.
6. No broad refactor during a feature unless explicitly approved.
7. No hidden scope additions.
8. No design drift without review and approval.
9. No release without human signoff.
10. GitHub is the source of truth for status, design, review, and release state.

## 20. Practical AI instruction snippet for direct use

If you want a compact instruction block to feed to Claude directly, use this:

"Rework the nock repository using a design-first, spec-driven development canvas. Treat GitHub as the product control layer. Separate the app repo from the governance repo. Create backlog-driven work, design proposals, approved design contracts, feature specs, acceptance criteria, test-first implementation, review gates, and release signoff. Never implement from a vague prompt. All features must be linked to a backlog item, approved design, and spec. No scope creep. No unapproved route or UX change. No release without passing checks and human approval. Use PRs, branch protection, issue templates, project boards, and CODEOWNERS. Keep the governance repo for process and the app repo for runtime code."

## 21. Summary

This methodology transforms an app repo into a disciplined product system where AI becomes useful without being dangerous. It creates a stable, reviewable pipeline for product work, protects design intent, gives the team an audit trail, and keeps the product safe for users while still making rapid innovation possible within controlled boundaries.

This is the recommended development canvas for `nock`.
