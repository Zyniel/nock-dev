# GitHub-based governance for Nock

This file is the operational recap for Claude and humans implementing the proposal to use GitHub as the control layer for product work.

## Goal

Use GitHub to keep the app stable while still enabling Claude-assisted development.

The stable app repo (`Zyniel/nock`) remains the product runtime. The governance repo (`Zyniel/nock-dev`) defines the process, approvals, and quality gates.

## Core rule

Claude must never implement from a vague prompt alone.

Every feature must be linked to:
- a backlog item
- an approved design direction
- a feature spec
- tests
- a review gate
- a release gate

## Required GitHub features and tools

### 1. GitHub Project v2 board
Create a board with these lanes:
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
- Priority: P0 / P1 / P2 / P3
- Area: backend / frontend / design / infra / tests
- Status: proposed / approved / blocked / review / done
- Design link
- Spec link
- Release target
- Risk (low / medium / high)
- Human approval: yes / no

This gives a visible status board and a backlog view that Claude can track.

### 2. Issues for intake and decisions
Use issue templates for:
- feature request
- design proposal
- bug report
- spec request

Required fields:
- goal
- user problem
- in scope
- out of scope
- constraints
- existing product contract
- design link or proposal link
- priority
- release target

These issues are the intake layer for Claude.

### 3. Design proposal flow
Create design proposals as issues or discussion posts.

Rules:
- proposals live outside the live product repo
- design proposals do not become implementation until human approval
- one proposal can generate 2-4 design directions
- the approved design becomes the design contract

### 4. Backlog management
Use GitHub Issues and Projects as the main backlog system.

Each backlog item must include:
- title
- status
- priority
- linked design
- linked spec
- dependencies
- release target
- owner
- notes

The backlog item is the only valid entry point for work.

### 5. Spec-driven work
Every feature requires a spec.

The spec must include:
- goal
- context
- public interface or user-facing behavior
- acceptance criteria
- edge cases and errors
- out of scope
- design contract linkage
- open questions

The spec is the behavior contract. Implementation must follow it.

### 6. Pull requests
Every implementation must be done through a PR.

PRs must include:
- linked issue
- linked approved design
- linked spec
- summary
- in scope / out of scope
- tests added or changed
- quality checks performed
- risks / assumptions
- reviewer notes

The PR template must force review before merge.

### 7. Branch protection
Configure branch protection on main.

Required settings:
- require PR before merge
- require status checks to pass
- require branch to be up to date
- require conversation resolution before merge
- disallow force pushes
- optionally restrict direct pushes to maintainers only

This prevents uncontrolled edits and keeps the product stable.

### 8. Required status checks
Every PR should run at least:
- lint / formatting
- unit tests
- type checks
- web build checks
- browser smoke tests for affected flows
- accessibility checks for affected flows
- design conformance checks for UI changes
- release checklist signoff

These checks should match the project gate used by Claude and by GitHub Actions.

### 9. CODEOWNERS
Create CODEOWNERS to protect ownership boundaries.

Recommended ownership areas:
- `src/**` → backend owner
- `web/**` → frontend owner
- `specs/**` → product / feature owner
- `docs/design/**` → design owner
- `.claude/**` → tooling owner
- `scripts/**` → infra owner
- `.github/**` → governance owner

This prevents the wrong area from being edited by the wrong role.

### 10. GitHub Actions
Use workflow(s) to enforce the quality gate in CI.

Recommended workflow jobs:
- lint
- type checks
- tests
- frontend build
- browser smoke tests
- release-gate check

The local Claude workflow and GitHub CI should be equivalent.

### 11. Releases and versioning
Use GitHub Releases and semver tags for stable baselines.

A release should include:
- version number
- release notes
- design contract references
- spec references
- tested browser matrix
- final human signoff

This allows a clean stable baseline after the app reaches a mature state.

### 12. Discussions (optional but recommended)
If the app is public-facing, add GitHub Discussions for:
- feature ideas
- UX feedback
- public design input
- roadmap conversations

Discussions are not the implementation system; they are the public feedback layer.

## Claude operating model with GitHub

Claude should follow this pattern:

1. Read backlog item
2. Read linked design contract
3. Read spec
4. Write failing tests
5. Implement only approved scope
6. Run the relevant gate
7. Open or update PR
8. Let human and review workflow decide acceptance

Claude must not:
- start work from a vague prompt alone
- mutate the live app without approved design
- change scope without updating spec and backlog
- perform broad redesigns without review

## Guardrails to enforce

- no implementation from a vague prompt
- no design change without approval
- no product drift without a linked specification
- no release without release review and a green quality gate
- no broad refactors during feature work
- no direct pushes to protected branches

## Recommended GitHub setup checklist

- [ ] Create GitHub Project v2 board
- [ ] Add issue templates for feature and design requests
- [ ] Add PR template
- [ ] Define labels for priority, status, area, and release
- [ ] Add CODEOWNERS
- [ ] Enable branch protection on main
- [ ] Require PRs before merge
- [ ] Require checks to pass before merge
- [ ] Add CI workflow for lint, tests, build, and smoke checks
- [ ] Use GitHub Releases for stable baselines
- [ ] Optionally enable Discussions for public feedback

## Implementation objective for Claude

Claude should operate as a bounded feature system inside GitHub:
- it can propose ideas
- it can implement approved work
- it must stay inside the approved design and spec
- it must produce evidence in PRs and checks
- it must not act as an uncontrolled product owner

## Final recommendation

Use GitHub as the source of truth for:
- work intake
- status tracking
- design approval
- spec linkage
- review gating
- release control

Use Claude as the execution and proposal engine inside that system.

This produces a much safer, more maintainable, and more scalable public-app workflow than letting Claude operate freely inside the product repo.
