# Security policy

RPCHome stores device passwords and talks to devices on your home network, so
security reports are taken seriously.

## Supported versions

Until version 1.0, only the latest release receives security fixes.

| Version | Supported |
| --- | --- |
| Latest release | Yes |
| Older releases | No |

## Reporting a vulnerability

**Do not open a public issue, discussion or pull request.**

Report it privately through GitHub:

1. Go to the [Security tab](https://github.com/Francisco4422/rpchome/security)
   of the repository.
2. Click **Report a vulnerability**.
3. Describe the issue, the affected version and the steps to reproduce it.

You can expect:

- An acknowledgement within 7 days.
- An assessment and a plan within 30 days.
- Credit in the release notes once the fix is published, unless you prefer to
  stay anonymous.

## Scope

In scope:

- The RPCHome app and the `lanrpc` package.
- How the app stores credentials, handles certificates and talks to devices.

Out of scope:

- Vulnerabilities in Shelly firmware itself. Report those to Shelly Group.
- Attacks that require physical access to an unlocked phone.
