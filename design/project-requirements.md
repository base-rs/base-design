# Preserve Project Requirements

## Requirement

Design requirements belong to the project and express the user's intended constraints. Shared guidance must distinguish active requirements from proposals and implementation details, and must not invent acceptance criteria.

Review must consider changes to requirements, including removals, alongside implementation compliance. A requirement may be deliberately revised, but implementation convenience alone does not establish that the user's requirement has changed. Missing validation evidence must remain visible as unverified.

## Rationale

The purpose of `base-design` is to preserve specific user requirements as a project evolves. A review that silently weakens those requirements or substitutes confidence for evidence defeats that purpose.

## Scope

The document convention and authoring and review skills shipped by this crate. The procedure applies across programming languages; Cargo is its distribution mechanism.

## Validation

Inspect guidance changes against concrete scenarios: an implementation violates an unchanged requirement, a user deliberately changes a requirement, a PR deletes a design document, or required measurements are unavailable. Confirm that the guidance distinguishes these outcomes and preserves the user's intended constraints.
