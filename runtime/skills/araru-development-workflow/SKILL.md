# Araru Development Workflow Skill

Use this skill for changes in any Araru repository. The runtime is versioned inside `araruoss/araruoss`; resolve paths through its configuration and never assume a user, home directory, hostname, or checkout location.

## Required sequence

Discover the repository → run read-only pre-flight → verify the working tree is clean → fast-forward the base branch → create or associate an Issue → obtain its number → suggest and confirm the branch → implement → validate → inspect the diff → commit → push → open a pull request → wait for CI → merge → wait for release/deploy → validate the result → close the Issue.

All workflow-generated commits, Issues, pull requests, and release notes must be written in English and contain enough context for review. If requirements or scope are ambiguous, ask before creating remote resources or changing files.

Branches use `<type>/<issue>-<slug>` with one of `feat`, `fix`, `refactor`, `docs`, `perf`, `test`, `chore`, `ci`, or `build`. Commits follow Conventional Commits, such as `feat(runtime): add portable workspace discovery`.

## Pre-flight and safety

Read `config/repositories.yaml`, run `git status --short --branch`, `git branch --show-current`, and `git remote -v`, and verify the configured remote points to the expected GitHub repository. Preserve dirty trees and never use `git reset --hard`, `git clean`, force push, or branch deletion automatically.

`araru-status` may report missing repositories without failing globally. A target selected for work must exist, contain `.git`, expose the configured remote, and match the expected GitHub owner/repository.

## Validation and release gates

Run only commands configured for the target repository. A failed lint, typecheck, test, build, CI, release, or deploy gate blocks the next step. Review release workflows to ensure Semantic Versioning is derived from Conventional Commits, package/publish runs only after a release is created, and deploy consumes the intended immutable artifact. Do not modify versions manually unless the repository's release policy requires it.

Pull requests must use `Refs #<issue>` while release or deployment remains a gate. Do not use `Closes`, `Fixes`, or `Resolves` when that would close the Issue before final validation.

Use `araru-start <repository> --dry-run` to simulate discovery and pre-flight. Dry-run must not create or modify Git or GitHub state.
