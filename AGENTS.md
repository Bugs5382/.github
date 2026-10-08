# AGENTS.md - .github

Guide for AI agents working in this repository. Pair with `CLAUDE.md` (the working agreement and
hook-enforced rules). Keep this file current when the build, layout, or public API changes.

## What this is

GitHub's special `.github` repository for the Bugs5382 account: a config-only repo, no code to
build or test. It holds the canonical `release-drafter.yml` shared across Bugs5382 repos, plus the
community-health and issue/PR templates GitHub falls back to for any Bugs5382 repo that does not
provide its own.

## Using .github

`.github/release-drafter.yml` is the public surface. Another repo consumes it through
[`Bugs5382/release-drafter-action`](https://github.com/Bugs5382/release-drafter-action)'s `extends`
input, pinned at a tag of this repo (`Bugs5382/.github@vX.Y.Z`), never a branch or a moving
major/minor tag. A change here only reaches a consumer at its next release and re-pin; nothing here
is read live off `main`.

## Layout

- `.github/release-drafter.yml` - the canonical config. `job-release-asset.yaml` re-attaches it to
  every published release as a release asset of the same name.
- `.github/workflows/` - this repo's own CI (PR checks, label checker/sync, actionlint) plus
  `job-release-asset.yaml`. No build/test workflow: there is no code to build.
- `.github/ISSUE_TEMPLATE/`, `PULL_REQUEST_TEMPLATE.md`, `CODE_OF_CONDUCT.md`, `CONTRIBUTING.md`,
  `SECURITY.md`, `SUPPORT.md`, `FUNDING.yml` - the account-wide fallbacks GitHub uses for any
  Bugs5382 repo that does not have its own copy.

## Build, test, lint

Nothing to build or test; there is no source code. `yamllint` and `actionlint` cover the YAML.

## Conventions and gotchas

- See `CLAUDE.md` for the branch/commit/PR rules; they are enforced by the git hooks in
  `.claude/hooks` (run `bash .claude/hooks/install.sh` once per clone).
- Open every PR as a draft. CI skips drafts, so run the full checks locally, push once they pass,
  and mark the PR ready when the work is finished; see CLAUDE.md "CI and Actions minutes".
- `CLAUDE.md`'s "Project layout" section is the hub's generic `action/action` layout block
  (action.yml, Dockerfile, cmd/action); none of it applies here. The hub has no layout for a
  config-only `.github` repo yet, and the governance sync overwrites that section on every run, so
  it is left as scaffolded rather than hand-edited out of sync with the hub.
- A new release here does not retroactively change a consumer already running at an older pinned
  tag; a consumer picks up a change only by bumping its own `extends` tag.
