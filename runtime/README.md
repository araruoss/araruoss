# Araru Development Runtime

The runtime is a versioned directory in `araruoss/araruoss`. It provides local discovery, repository pre-flight checks, validation commands, and operational guidance for the Araru development workflow. It is not a server, daemon, CI system, or independent Git repository.

## Requirements

- Git
- Ruby with YAML support
- Bash or a POSIX-compatible shell
- GitHub CLI (`gh`) for Issue and pull request operations
- Docker Compose only when running the optional local stack

## Workspace setup

The recommended layout keeps the central repository and components as siblings:

```text
workspace/
├── araruoss/
├── araru-server/
├── araru-web/
├── araru-design/
└── ...
```

The workspace may live anywhere. Set an explicit root when using another layout:

```bash
export ARARU_WORKSPACE_ROOT=/path/to/workspace
```

The runtime resolves its own location first, then uses `ARARU_WORKSPACE_ROOT`, and finally the parent workspace inferred from the central checkout. `ARARU_CONFIG` can override the repository configuration file when testing an alternate configuration.

Repositories that are not cloned are reported as `not cloned` by status and do not make global discovery fail.

## Commands

Run these commands from any directory:

```bash
path/to/araruoss/runtime/scripts/araru-status
path/to/araruoss/runtime/scripts/araru-start araru-web --dry-run
path/to/araruoss/runtime/scripts/araru-validate araru-web
path/to/araruoss/runtime/scripts/araru-finish araru-web --dry-run
```

`--dry-run` performs read-only discovery and pre-flight. It never creates Issues, branches, commits, pull requests, releases, or other GitHub state.

## Development workflow

```text
Pre-flight → Issue → Branch → Development → Validation → Commit → Push
→ Pull Request → GitHub Actions → Merge → Release/Deploy → Final validation → Issue close
```

The workflow is Issue-first. Branches use `<type>/<issue>-<slug>` and commits use Conventional Commits, for example `feat(security): add password policy`. Pull requests reference the Issue with `Refs #<issue>` and must include context, scope, acceptance criteria, validation, and release impact. Issues remain open until required CI, release, deploy, and final validation gates pass.

Read [AGENTS.md](AGENTS.md) and [the workflow skill](skills/araru-development-workflow/SKILL.md) before making changes with an agent.

## Configuration and local data

Repository definitions live in [config/repositories.yaml](config/repositories.yaml). State in `.state/`, local storage, `.env`, credentials, caches, and personal libraries are never part of the versioned runtime. Use `.env.example` as a neutral template when the optional Docker stack is needed.

`ARARU_LIBRARY_PATH` is an external path for a local library and must always be configured by the operator; it has no personal default.

## Optional Docker stack

Docker support is for local development only and is independent of the GitHub workflow. Copy `.env.example` to `.env`, set a local password and any required paths, then run the Compose commands from the runtime directory. Do not commit `.env`, storage, database volumes, books, or caches.

The Compose build context follows `ARARU_WORKSPACE_ROOT`. The default `../..` targets the recommended sibling layout. For a workspace with component repositories inside the central checkout, set `ARARU_WORKSPACE_ROOT=..` and `ARARU_RUNTIME_DOCKERFILE=runtime/Dockerfile` in `.env`.

For production, pin exact Server and Web image versions. Each distributable component has an independent Semantic Versioning cycle; a Web release does not require an artificial Server release.
