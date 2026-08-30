# Araru Development Workflow

This runtime is part of the central `araruoss/araruoss` repository. It provides local instructions and orchestration for the ecosystem; it is not an independent Git repository.

Before changing an Araru repository:

1. Resolve it through `config/repositories.yaml` and the runtime workspace resolver.
2. Run the read-only pre-flight: `git status --short --branch`, current branch, remotes, Git, GitHub CLI, and repository identity.
3. Preserve local changes. Stop when the target working tree is dirty.
4. Synchronize the base branch with `git pull --ff-only` only after the tree is clean.
5. Create or associate an Issue with a detailed English context, objective, scope, acceptance criteria, and validation plan.
6. Suggest and confirm `<type>/<issue>-<slug>` before creating the branch.
7. Implement only the approved scope.
8. Run the repository's configured lint, typecheck, tests, and build commands.
9. Review `git diff`, create an English Conventional Commit, push, and open an English pull request using `Refs #<issue>`.
10. Wait for required Actions, merge only through repository policy, then wait for release/deploy and validate the published artifact.
11. Close the Issue only after every required gate passes.

Use `runtime/scripts/araru-start <repository> --dry-run` to inspect the plan without changing Git or GitHub. Never use automatic reset, clean, force push, or premature Issue closing.

The complete operational guidance is in [skills/araru-development-workflow/SKILL.md](skills/araru-development-workflow/SKILL.md).
