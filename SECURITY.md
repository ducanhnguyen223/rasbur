# Security Policy

## Reporting a vulnerability

Please don't open a public issue for security problems.

Report it privately instead: open the **Security** tab of this repository and click **Report a vulnerability**. I'll acknowledge it as soon as I can and keep you updated until it's fixed.

Include the affected package or app, the version or commit, and the steps to reproduce it.

## Scope

- `@rasbur/decoders` and `@rasbur/mcp`
- The API and web app in this repository
- The demo at [rasbur.vercel.app](https://rasbur.vercel.app)

Please test against your own local copy, not the demo. Automated scanning and load testing of the demo are out of scope, because it runs on free-tier hosting.

## Supported versions

Rasbur hasn't reached v1.0.0 yet, so fixes land on `main` and go out in the next release of the affected package. Only the latest published version of each package is supported.
