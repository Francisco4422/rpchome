# Decision records

Each file records one significant decision: the context, what was decided and
its consequences. Records are never rewritten; a decision that changes gets a
new record that supersedes the old one.

| # | Decision | Status |
| --- | --- | --- |
| [0001](0001-local-only.md) | Local network only, no cloud | Accepted |
| [0002](0002-flutter-and-dart.md) | Flutter and Dart for the app | Accepted |
| [0003](0003-licensing.md) | GPL-3.0 for the app, MIT for `lanrpc`, CLA for contributors | Accepted |
| [0004](0004-supported-generations.md) | Support Shelly Gen2, Gen3 and Gen4 | Accepted |
| [0005](0005-branching-and-releases.md) | `develop` and `main` branches, squash merges, automated releases | Accepted |

To add a record, copy [template.md](template.md), give it the next number and
add it to this table in the same pull request.
