---
name: base-design-author
description: Capture, revise, or remove project-specific requirements in design/*.md when user requirements change, including performance targets, architectural boundaries, and behavioral contracts.
metadata:
  type: skill
---

# Author Design Requirements

Maintain the project's current requirements in tracked `design/*.md`. Write one document per independently reviewable concern. A requirement describes a concrete property the project must preserve until deliberately revised, whose violation a reviewer could explain.

The project owns `design/` and versions it with its implementation. This package supplies the authoring and review procedure. Installing dependency context does not adopt a dependency's design requirements as requirements for the consuming project.

## Establish the requirement

Read the user's request, existing design documents, and relevant implementation or decision evidence. Identify the enduring property the user needs and the scope in which it applies. Separate agreed requirements from suggestions, open questions, and incidental implementation choices. Ask for missing decisions only when they prevent a faithful requirement or a meaningful validation method; continue independent work when possible.

Requirements can define performance targets, architectural boundaries, or observable semantics such as cancellation and resource ownership. For example, requiring the HTML rendering path to consume events without constructing an AST is specific enough to review. Asking code to be clean or fast needs further definition.

General coding conventions belong in shared guidance. Package explanations and usage belong in context. Development procedures belong in skills or repository instructions. Link those materials when they explain a requirement instead of duplicating them.

## Write or update the document

Use a descriptive lowercase filename and a title. Include:

- **Requirement:** the property that must hold, including relevant limits and permitted alternatives.
- **Rationale:** the user need or design decision it preserves, with a source reference when available.
- **Scope:** the behavior, APIs, components, or workloads it covers.
- **Validation:** the evidence and method a reviewer should use to assess compliance.

Use plain Markdown; no front matter or machine-readable schema is required. For example, `design/runtime-independence.md` could contain:

```markdown
# Runtime Independence

## Requirement
Public protocol types must not require a concrete runtime.

## Rationale
Applications need to select their execution environment.

## Scope
Public protocol APIs and their required dependencies.

## Validation
Inspect public signatures and dependencies.
Exercise the protocol with the supported scheduler implementations.
```

Keep closely related requirements together; split concerns that need independent review. Refer to tests and measurements where useful, while keeping the required behavior clear independently of today's implementation.

For performance requirements, establish named benchmarks and metrics, a baseline, comparable environments and build settings, the measurement procedure, and agreed regression criteria that account for noise. Missing targets remain open questions; do not invent acceptance criteria. For structural or semantic requirements, describe the observable boundary or behavior and how a reviewer can inspect or exercise it. Validation may use tests, measurements, dependency inspection, or reasoned analysis; describe a reproducible method where possible.

## Maintain current requirements

Update the existing authoritative document when its concern changes. Remove a requirement when the user's intended change makes it obsolete, and explain that removal in the change summary. Keep requirement changes with the corresponding implementation change. If the requirement is unchanged, no document edit is necessary.

Keep active documents about current requirements. Link historical decisions separately when useful; Git retains earlier versions. Keep unaccepted proposals distinguishable from active requirements.

## Check the result

Check that a reviewer can identify a concrete violation, establish applicability, and obtain or identify the necessary evidence. Compare with related requirements for contradictions and duplication. Keep unresolved decisions explicit rather than presenting them as active requirements.

Review edits and deletions against the original requirement and user intent. An implementation failing a requirement is a finding to resolve, not by itself a reason to weaken the requirement. Use `base-design-review` to assess the resulting requirements and implementation together.
