# `core-design`

Project-specific design requirements, captured in `design/*.md` and applied during feature planning and pull request review.

## Motivation

Projects need to preserve concrete requirements as their implementation evolves: performance targets, resource ownership semantics, architectural boundaries, or compatibility guarantees. Each design document describes one independently reviewable concern, why it matters, where it applies, and how to validate it.

Design documents record current requirements. A pull request that introduces, changes, or removes a requirement updates the corresponding document alongside the implementation. Review covers both compliance and the intended changes to the requirements themselves.

## Usage

Add `core-design` to the development tooling dependencies resolved by Agent Context. In a Rust project with a private Bake package:

```sh
cargo add --manifest-path bake/Cargo.toml core-design
cargo bake agent:context:install --package core-design
```

The install command is provided by `bake-agent-context`, which `core-project` includes. `core-design` provides guidance and skills, with no runtime API or Bake tasks of its own. The document convention and skills are language-independent.

The package provides two self-contained skills:

- [Author Design Requirements](context/author.md), installed as `core-design-author`: the `design/*.md` convention, document structure, and procedure for capturing, revising, or removing specific requirements.
- [Review Design Requirements](context/review.md), installed as `core-design-review`: assess plans and changes, using a sub-agent per applicable design document when available.

Keep project requirements in the project's tracked `design/` directory. Installing this package installs the shared procedure; it does not create or replace project requirements.

Add this instruction to the project's agent guidance so requirements are considered before implementation:

> Before planning or changing behavior, discover and read applicable `design/*.md`. Use `core-design-review` to assess plans and changes, and `core-design-author` when user requirements are introduced, changed, or removed. Review design compliance before opening or updating a pull request.

## Releasing

Prepare a release with `cargo bake cargo:version:patch` (or `minor`, `major`, or `bump --version X.Y.Z`), commit with a `Release: vVERSION` trailer, then run `cargo bake cargo:release` and open a pull request. After review and merge, GitHub Actions publishes the release when the configured `crates-io` environment approves it. Follow the shared [Releasing skill](https://github.com/core-rs/core-project/blob/main/context/releasing.md) for the standard process.

## Releases

<!-- bake-readme:releases:start -->

See [releases.md](releases.md) for the full release history.

<!-- bake-readme:releases:end -->

## See Also

- [`core-project`](https://github.com/core-rs/core-project).
- [`bake-agent-context`](https://github.com/core-rs/bake-agent-context).

## Contributing

Please open an issue or pull request on [GitHub](https://github.com/core-rs/core-design).

The private `bake/` package uses `core-project` for development and release tasks. Run `cargo bake --regenerate` after changing task dependencies. Use `cargo bake test` for the workspace tests and `cargo bake test:coverage --all-targets true` for the standard coverage check. The tests package the crate and verify that a consumer can discover and install both skills from the packaged contents.

### Agent Context

Run `cargo bake agent:context:install` to install shared context and skills. Use `cargo bake agent:context:list` and `cargo bake agent:context:show` to discover relevant guides, follow `agents.md` if present, and apply skills under `.agents/skills/`.

Before planning or changing behavior, read applicable `design/*.md`. This crate's own skills are authored in `context/author.md` and `context/review.md`; use those sources when maintaining or reviewing its requirements. The installer discovers dependency guidance and excludes workspace members, so it does not install this crate's own skills into this checkout. Edit the source skill documents, and use their installed names in consuming projects.
