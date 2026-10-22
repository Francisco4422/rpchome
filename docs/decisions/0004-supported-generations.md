# 0004. Support Shelly Gen2, Gen3 and Gen4

- **Status:** Accepted
- **Date:** 2026-10-22

## Context

Gen1 devices use a different, REST-style API. Gen2 and later share the same
JSON-RPC 2.0 API built from components (`Switch`, `Cover`, `Light`, `Input`,
meters), the same digest authentication and the same Bluetooth provisioning.
HTTPS on the device requires Gen3 or later with recent firmware.

## Decision

Support Gen2, Gen3 and Gen4 devices. Gen1 is out of scope. Support is built
around components, not models: any device that reports known components works,
even if its model was released after the app.

Battery-powered sensors that sleep most of the time, Pro models with special
components and non-Wi-Fi devices (BLU, Wave, Zigbee) are deferred to later
milestones.

## Consequences

- One protocol to implement and test.
- New models usually work without an app update.
- HTTPS-related features are only offered on devices that support them; Gen2
  devices are adopted with a password over HTTP.
