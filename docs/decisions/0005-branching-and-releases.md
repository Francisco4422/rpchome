# 0005. develop and main branches, squash merges, automated releases

- **Status:** Accepted
- **Date:** 2026-10-22

## Context

The project needs a history that is easy to read, a clear place for stable
code, and releases that do not depend on manual steps.

## Decision

- `develop` is the default branch. Every change reaches it through a pull
  request that is **squash-merged**, so each pull request becomes one commit
  whose message is the pull request title.
- `main` contains stable releases only. It is updated through a pull request
  from `develop` (or from a `hotfix/*` branch) using a **merge commit**, so both
  branches keep a shared history.
- Pull request titles follow Conventional Commits. CI rejects titles that do
  not, and rejects pull requests to `main` from any other branch.
- Releases are automated from the commit messages. release-please keeps a
  release pull request open on `develop` that calculates the next version
  (semantic versioning) and updates `CHANGELOG.md`. Once that pull request is
  merged and `develop` reaches `main`, a workflow on `main` creates the tag and
  the GitHub release. The app and `lanrpc` are versioned independently.
- Both branches are protected: no deletion, no force push, changes only through
  pull requests with passing checks.

## Consequences

- `develop` history reads as a list of features and fixes.
- Releasing is a single pull request from `develop` to `main`.
- Hotfixes must be merged back into `develop` after they reach `main`.
