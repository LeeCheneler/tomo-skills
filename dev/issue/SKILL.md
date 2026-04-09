---
name: issue
description: Create a well-structured GitHub issue. Supports user stories, bug reports, and technical chores with appropriate templates and labelling. Invoke with //issue.
---

# Skill: Create a GitHub Issue

Create a GitHub issue with a well-structured description using the appropriate template for the type
of work.

## Tools Required

- `gh` CLI (for creating the issue on GitHub)

## Operating Principle

**You draft, the user reviews.** Your job is to produce a complete first draft by inferring from the
conversation, the repo state, and the user's intent. The user's job is to review your draft in
Step 5 and request changes.

You MUST NOT ask the user to write any part of the issue body for you — not the user story, not
acceptance criteria, not repro steps, not the summary, not the scope. Fill every section with your
best-effort draft. If something is genuinely unknowable (e.g. a specific version number), make a
reasonable assumption and flag it inline with `[assumption: ...]` for the user to confirm during
review.

## Do NOT

- Ask the user to write the user story in "As a / I want / So that" form
- Ask the user to list acceptance criteria
- Ask the user to provide steps to reproduce
- Ask the user to fill in any template section
- Present an empty or partially-filled template and ask the user to complete it
- Interview the user field-by-field through the template

If you catch yourself about to do any of the above, stop and draft it yourself instead. A wrong
first draft the user can correct is infinitely more useful than a blank template they have to fill
in.

## Procedure

Work through each step sequentially. Do not skip steps.

### Step 1 — Issue Type

Use `ask` to ask the user what type of issue they want to create. You MUST present
exactly these three options in exactly this order — do not omit, reorder, or rephrase any option:

- **1. User story** — a new feature or enhancement from the user's perspective
- **2. Bug report** — a defect or unexpected behaviour
- **3. Technical chore** — maintenance, upgrades, refactoring, or other non-user-facing work

### Step 2 — Understand Intent

Get just enough to draft. In most cases the user has already described the issue in the
conversation — use that directly. Only ask a clarifying question if the **core intent** is
genuinely unclear (e.g. you can't tell whether a described behaviour is a bug or a desired
feature, or you don't know which component the issue applies to).

Do not ask the user to write or supply template content. Do not ask them to phrase things in
"As a / I want / So that" form. That is your job in Step 3.

### Step 3 — Draft the Issue

Write the **complete** draft yourself using the template for the chosen type below. Every section
must be filled in — no placeholders, no "TODO", no "please add...". Infer from:

- The conversation so far
- The repo state (recent commits, relevant files, existing issues, code patterns)
- Reasonable assumptions about the domain

For acceptance criteria, repro steps, and scope items specifically: **propose them**. The user
will correct you in Step 5 if you're wrong. If you genuinely cannot infer a detail, make a
reasonable assumption and mark it inline with `[assumption: ...]` — never leave a section blank
and never hand the work back to the user.

---

#### User Story

**Title:** `feat: <short description>`

**Labels:** `enhancement`

**Body:**

```markdown
## User Story

As a [type of user],
I want [action/feature],
so that [benefit/value].

## Acceptance Criteria

- [ ] [Criterion 1]
- [ ] [Criterion 2]
- [ ] [Criterion 3]

## Additional Context

[Optional. Designs, edge cases, constraints, or anything else relevant. Omit this section entirely
if there's nothing to add.]
```

---

#### Bug Report

**Title:** `bug: <short description>`

**Labels:** `bug`

**Body:**

```markdown
## Description

[Clear, concise description of the bug.]

## Steps to Reproduce

1. [Step 1]
2. [Step 2]
3. [Step 3]

## Expected Behaviour

[What should happen.]

## Actual Behaviour

[What happens instead.]

## Environment

[Relevant environment details — browser, OS, version, deployment, etc. Omit this section if not
applicable.]

## Additional Context

[Optional. Screenshots, logs, error messages, or anything else relevant. Omit this section entirely
if there's nothing to add.]
```

---

#### Technical Chore

**Title:** `chore: <short description>`

**Labels:** `chore`

**Body:**

```markdown
## Summary

[What needs to be done and why.]

## Scope

- [Item 1]
- [Item 2]
- [Item 3]

## Acceptance Criteria

- [ ] [Criterion 1]
- [ ] [Criterion 2]
- [ ] [Criterion 3]

## Additional Context

[Optional. Links to docs, related issues, or anything else relevant. Omit this section entirely if
there's nothing to add.]
```

---

### Step 4 — Labelling

Apply the primary label from the template above (`enhancement`, `bug`, or `chore`).

If additional labels are clearly applicable, add them. Common labels to consider:

- `documentation` — docs-only changes
- `security` — security-related issues
- `performance` — performance-related issues
- `breaking-change` — introduces a breaking change
- `good first issue` — simple and well-scoped, suitable for new contributors

Do not invent labels. Only use labels that already exist on the repository. Run
`gh label list --limit 100` to check what labels are available before applying any. If a label from
the template (e.g. `chore`) does not exist on the repo, skip it rather than creating it — flag this
to the user.

### Step 5 — Review and Confirm

Present the full issue (title, labels, body) to the user. Ask if they want to change anything.
Iterate until approved.

### Step 6 — Create

Create the issue using `gh issue create` with the approved title, labels, and body. Use a HEREDOC to
pass the body for correct formatting.

Report the issue URL to the user.
