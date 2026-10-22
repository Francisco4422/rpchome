# 0001. Local network only, no cloud

- **Status:** Accepted
- **Date:** 2026-10-22

## Context

Shelly devices expose a complete JSON-RPC 2.0 API on the local network
(`/rpc` over HTTP, WebSocket and Bluetooth). The official app relies on a cloud
account for many features. Users who care about privacy, or whose internet
connection is unreliable, want full control without an account.

## Decision

RPCHome talks only to devices on the local network. It has no backend, no user
accounts and no telemetry. Automations (schedules, scenes, device-to-device
links) are written to the devices with their own `Schedule.*` and `Webhook.*`
methods, so they run without the phone.

## Consequences

- No server costs and no personal data to protect on our side.
- The app works offline and keeps working if the project is abandoned.
- Remote control from outside the home is out of scope. Users who need it can
  use a VPN to their home network.
- Device credentials are stored only on the phone, in the platform's secure
  storage.
