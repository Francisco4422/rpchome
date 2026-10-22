# Contributing to RPCHome

Thanks for taking the time to contribute. This guide explains how the project
is organized and what a pull request needs before it can be merged.

By participating you agree to follow the [Code of Conduct](CODE_OF_CONDUCT.md).

## Before you start

- **Small fixes** (typos, small bugs): open a pull request directly.
- **Anything larger** (new features, new device support, refactors): open an
  issue first so we can agree on the approach before you invest time in it.
- **Security issues**: do not open a public issue. Follow [SECURITY.md](SECURITY.md).
- **Questions** ("does it work with my device?"): use
  [Discussions](https://github.com/Francisco4422/rpchome/discussions), not issues.

## Branches

| Branch | Purpose |
| --- | --- |
| `develop` | Default branch. All work is merged here. |
| `main` | Stable releases only. Updated from `develop` (or `hotfix/*`) when a version is ready. |
| `feat/*`, `fix/*`, `test/*`, `docs/*`, `refactor/*`, `ci/*` | Short-lived branches for a single change, created from `develop`. |
| `hotfix/*` | Urgent fix for a published release, created from `main`. |

Contributors work from a fork and open pull requests against `develop`.
Pull requests to `main` are only accepted from `develop` or `hotfix/*`.

## Development setup

The app and the `lanrpc` package live in one Dart workspace.

1. Install the Flutter SDK (stable channel).
2. Clone your fork and run `flutter pub get` from the repository root.
3. Run the app against the simulated device in `tool/fake_shelly/` if you do not
   have real devices.

Detailed commands are added here as the code lands.

## Architecture

Read [docs/architecture.md](docs/architecture.md) before writing code. The short
version:

- Code is organized by feature (`devices`, `discovery`, `setup`, `rooms`,
  `automations`). Each feature has the same folders: `models`, `repositories`,
  `services`, `controllers` and `ui`.
- Dependencies only point downwards: `ui` → `controllers` → `services` →
  `repositories` / `lanrpc`. The `ui` layer never calls a repository or
  `lanrpc` directly.
- A feature may use another feature's `services` and `models`, never its `ui`
  or `controllers`.
- `core/` never imports from `features/`.
- `packages/lanrpc` is pure Dart. It must not depend on Flutter or on the app.

Significant design decisions are recorded in [docs/decisions/](docs/decisions/).
If your change alters one of them, add a new decision record.

## Tests

Every change ships with tests. A pull request that lowers coverage or adds code
without tests will not be merged.

- `test/` mirrors `lib/`: `lib/features/devices/services/device_service.dart`
  is tested in `test/features/devices/services/device_service_test.dart`.
- Every error type in `lanrpc` has its own fixture in `test/fixtures/errors/`
  and its own test. Adding a new error type without both is not accepted.
- Tests are tagged so they can be filtered:

  | Tag | Covers |
  | --- | --- |
  | `unit`, `widget`, `integration` | Test level |
  | `auth` | Passwords and digest authentication |
  | `network` | Unreachable hosts and connection failures |
  | `timeout` | Requests that take too long |
  | `tls` | Certificates and HTTPS |
  | `protocol` | Malformed or unexpected responses |
  | `device-error` | Errors returned by the device (`-103`, `-109`, …) |

  ```sh
  flutter test                              # everything
  dart test --tags auth                     # only authentication errors
  dart test --name "\-109"                  # only error -109
  flutter test --exclude-tags integration   # skip slow tests
  ```

- Minimum coverage: 95 % for `lanrpc`, 80 % for the app. CI enforces it.

## Commit messages and pull request titles

The project follows [Conventional Commits](https://www.conventionalcommits.org/).
Pull requests are squash-merged, so **the pull request title becomes the commit
message** on `develop`. CI rejects titles that do not follow the format.

```
type(scope): short description in imperative mood
```

**Types**

| Type | Use it for |
| --- | --- |
| `feat` | A new feature |
| `fix` | A bug fix |
| `test` | Adding or fixing tests only |
| `refactor` | Code changes that do not change behavior |
| `perf` | Performance improvements |
| `docs` | Documentation only |
| `style` | Formatting only |
| `build` | Dependencies and build configuration |
| `ci` | GitHub Actions and automation |
| `chore` | Maintenance that fits nowhere else |
| `revert` | Reverting a previous commit |

**Scopes**

| Scope | Area |
| --- | --- |
| `lanrpc` | `packages/lanrpc` |
| `devices`, `discovery`, `setup`, `rooms`, `automations` | The matching folder in `app/lib/features/` |
| `core` | `app/lib/core` |
| `app` | App startup, routing and theme |
| `ui` | Shared widgets |
| `l10n` | Translations |
| `fake-shelly` | `tool/fake_shelly` |
| `deps` | Dependency updates |
| `release` | Release automation |

The scope is optional when a change spans several areas.

**Rules**

- Write in English, in the imperative mood: "add", not "added" or "adds".
- Start with a lowercase letter and do not end with a period.
- Keep the first line under 72 characters.
- One logical change per pull request.
- Mark breaking changes with `!` and explain them in the body:

  ```
  feat(lanrpc)!: rename ShellyRpcError to LanRpcException

  BREAKING CHANGE: catch LanRpcException instead of ShellyRpcError.
  ```

Examples:

```
feat(devices): add cover position slider
fix(discovery): ignore duplicate mDNS answers
test(lanrpc): cover -109 failed precondition
build(deps): bump riverpod to 3.1.0
```

Versions and the changelog are generated from these messages. Do not edit
`CHANGELOG.md` by hand.

## Pull request checklist

- [ ] The branch is up to date with `develop`.
- [ ] The title follows the convention above.
- [ ] Tests are added or updated, and all checks pass.
- [ ] Code is formatted (`dart format .`) and has no analyzer warnings.
- [ ] Screenshots are attached if the change affects the UI.
- [ ] Documentation is updated if behavior changed.

## Requesting support for a new device

Open an issue with the **Device support request** template. It asks for the
output of `Shelly.GetDeviceInfo` and `Shelly.GetComponents`, which you can get
from `http://<device-ip>/rpc/Shelly.GetDeviceInfo` and
`http://<device-ip>/rpc/Shelly.GetComponents`. Remove passwords and Wi-Fi names
before posting.

## Licensing of contributions

- Contributions to the app and tools are licensed under GPL-3.0.
- Contributions to `packages/lanrpc` are licensed under MIT.

Before your first pull request is merged you will be asked to sign the
Contributor License Agreement (CLA). It confirms that you have the right to
submit your contribution and allows the maintainer to distribute the app
through app stores, whose terms are not compatible with GPL-3.0 alone. You keep
the copyright of your work. A bot will guide you through signing in the pull
request.
