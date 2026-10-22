# 0002. Flutter and Dart for the app

- **Status:** Accepted
- **Date:** 2026-10-22

## Context

The app must run on Android and iOS from one codebase, be developed from
Windows, and be easy for open-source contributors to build. It needs Bluetooth
LE, mDNS discovery and secure storage.

## Decision

Use Flutter with Dart 3. State management uses Riverpod. The JSON-RPC client is
a separate pure Dart package (`lanrpc`) in the same workspace.

iOS builds run on GitHub Actions macOS runners, so no Mac is required for
day-to-day development.

## Consequences

- One codebase and one UI toolkit for both platforms.
- Dart's sealed classes make error handling and device components exhaustive.
- `lanrpc` can be tested without Flutter and reused by other Dart projects.
- Contributors need the Flutter SDK; plain Dart is enough for `lanrpc`.
