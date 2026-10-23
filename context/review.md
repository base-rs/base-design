---
name: core-design-review
description: Assess feature plans, implementation changes, and pull requests against project design/*.md requirements, including changes to the requirements themselves. Use before implementation and when preparing or reviewing changes in projects with design documents.
metadata:
  type: skill
---

# Review Design Requirements

Assess the work against the project's current design requirements in tracked `design/*.md`. Each document describes an independently reviewable concern: concrete properties the project must preserve until deliberately revised. During planning, identify constraints and the evidence implementation will need. Before opening or updating a pull request, assess the actual changes and their validation evidence. This review complements general correctness review and the project's required checks.

## Discover and establish scope

Identify the affected project roots and any repository-wide design requirements. Inventory `design/*.md` and read each document sufficiently to determine applicability, including concerns whose impact crosses file boundaries. Do not select requirements solely by matching changed paths.

In a repository containing several projects, consult repository-wide requirements and those belonging to the affected projects. Use each document's scope to establish applicability; a closer directory does not silently override a broader requirement. Surface conflicts for resolution against the intended design.

For a change review, establish the intended base and the exact proposed revision or working-tree diff. Inspect design documents at both revisions, including additions, edits, and deletions. Use the full proposed change relative to its intended base; if no base is available, state that limitation rather than claiming to have reviewed requirement history.

Record which documents apply and why others do not. If there are no design documents at either revision, report that briefly; do not create requirements as a side effect of review. When the work introduces or changes an enduring user requirement, use `core-design-author` to capture it.

## Delegate focused reviews

When sub-agents are available, assign one reviewer per applicable design document, with bounded concurrency. Use a reviewer that did not implement the change for the final change review. Give each reviewer:

- The user's intent and the plan or exact revision/diff under review.
- The design document, its base version when changed or removed, and relevant project guidance.
- Access to the affected implementation, tests, measurements, and related requirements needed to assess the concern.

Ask each reviewer to inspect and report findings, keeping edits with the coordinating agent. A reviewer should evaluate the whole applicable concern, challenge unsupported assumptions, and cite concrete evidence. For a removed document, review whether its removal is justified by the intended requirement change. If delegation is unavailable, review each applicable document directly and disclose that the review was not independent.

## Assess requirements and evidence

During planning, report applicable constraints, likely conflicts, missing decisions, and the validation needed. A compatible plan is not evidence that the eventual implementation complies.

During change review, assess both whether the requirement changes reflect the user's intended change and whether the implementation satisfies the resulting requirements. Preserve the distinction between a deliberate requirement change and weakening a constraint to accommodate a failing implementation. Include changes to validation procedures or performance baselines in this assessment.

Use evidence appropriate to the requirement: code locations and structural reasoning, relevant test behavior, or benchmark results from comparable conditions. Reuse suitable existing evidence when it covers the reviewed revision and requirement. A passing general test suite does not establish an unrelated structural or performance property. Missing evidence, unavailable environments, and inconclusive measurements must remain visible.

Return an assessment for each applicable requirement:

- **Satisfied:** cite the evidence supporting compliance.
- **Violated:** identify the requirement, affected behavior, and concrete supporting evidence.
- **Not verified:** identify the missing evidence or unresolved interpretation.
- **Not applicable:** explain why the requirement does not apply to this change.

Do not report a whole document as satisfied when a requirement within it is violated or unverified.

## Reconcile and report

The coordinating agent evaluates findings against user intent, resolves interactions between requirements, and fixes substantive issues within the authorized task. Surface unresolved conflicts without silently inventing precedence or changing requirements. When requirements need revision, use `core-design-author` and review that revision too.

After changes, re-review affected requirements and evidence against the final revision. Reuse unaffected assessments only when their evidence still applies. Summarize findings, deliberate requirement changes, and validation gaps concisely for the user or PR reviewer. Never describe an unverified requirement as passed. Follow the project's pull request workflow for its remaining checks and approvals.
