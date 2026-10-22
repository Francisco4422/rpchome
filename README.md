# RPCHome

Control your smart home locally. No cloud, no accounts, no servers.

RPCHome is a free and open-source mobile app for Android and iOS that discovers,
secures and controls Shelly devices (Gen2, Gen3 and Gen4) directly over your
local network. Every command goes from your phone to the device; nothing leaves
your home.

> **Status:** early development. There is no release yet.

## Principles

- **Local only.** The app talks to devices on your LAN using their official
  JSON-RPC API. It never contacts a cloud service.
- **The app configures, the device runs.** Schedules, scenes and links are
  stored on the devices themselves, so they keep working when your phone is off.
- **Secure by default.** Adopting a device sets a password and, where the
  firmware supports it, enables HTTPS.
- **Components, not models.** Support is built around what a device contains
  (switches, covers, lights, meters), so new models work without app updates.

## Project layout

| Path | What it is | License |
| --- | --- | --- |
| `app/` | The Flutter app | GPL-3.0 |
| `packages/lanrpc/` | Pure Dart client for JSON-RPC devices on the LAN | MIT |
| `tool/fake_shelly/` | Simulated device used by the test suite | GPL-3.0 |
| `docs/` | Architecture and decision records | GPL-3.0 |

## Contributing

Contributions are welcome. Please read [CONTRIBUTING.md](CONTRIBUTING.md) and the
[architecture overview](docs/architecture.md) before opening a pull request.

To report a security issue, follow [SECURITY.md](SECURITY.md). Do not open a
public issue.

## License

The app is licensed under the [GNU General Public License v3.0](LICENSE).
The `lanrpc` package is licensed under the MIT License, so it can be reused in
any project.

RPCHome is an independent project. It is not affiliated with, endorsed by or
sponsored by Shelly Group. "Shelly" is a trademark of its respective owner.
