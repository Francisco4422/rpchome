# 0003. GPL-3.0 for the app, MIT for lanrpc, CLA for contributors

- **Status:** Accepted
- **Date:** 2026-10-22

## Context

The app should stay free software: nobody should be able to take it, close the
source and redistribute it. At the same time, the JSON-RPC client is useful for
any project, including proprietary ones. The maintainer plans to publish the app
on app stores for a small price to fund development, while the source stays
free. App store terms add restrictions that conflict with GPL-3.0 when the
publisher does not hold the rights to all the code.

## Decision

- The app (`app/`), tools and documentation are licensed under GPL-3.0.
- `packages/lanrpc` is licensed under MIT.
- Contributors sign a Contributor License Agreement before their first pull
  request is merged. They keep their copyright and grant the maintainer the
  right to distribute their contribution, including through app stores.

## Consequences

- Forks of the app must remain GPL-3.0 and publish their source.
- `lanrpc` can be adopted widely, which brings more users and contributors.
- The CLA adds one step for first-time contributors; a bot automates it.
- Builds from the source and F-Droid builds remain free of charge.
