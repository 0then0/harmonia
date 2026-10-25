# Security policy

## Supported versions

Security fixes target the current `main` branch. The package version is 0.1.0; there are no tagged releases yet. Older commits have no separate security backport commitment. Use the committed `uv.lock` and pinned container images when reproducing an issue.

## Report a vulnerability

Do not disclose exploit details, access tokens, browser authentication files, personal library data or private logs in a public issue or pull request.

Private vulnerability reporting is not currently enabled for this repository. Open a [new issue](https://github.com/0then0/Harmonia/issues/new) titled “Private security contact requested” with no vulnerability details. The [maintainer](https://github.com/0then0) will arrange a private channel before you share the report. There is no guaranteed response time or paid bounty program.

A private report should include the affected commit/version, Python and operating system versions, deployment method, expected impact and reproduction steps. Use a minimal fictional canonical library and constraints where possible. Coordinate public disclosure with the maintainer so a fix can be prepared before technical details become public.

## Security boundaries

Harmonia is designed for one trusted operator and one configured account per music service. The API requires a shared operator key; it does not isolate multiple users or tenants. Static assets, OpenAPI and process liveness are public within the deployment's network boundary.

Compose publishes the API on loopback and keeps PostgreSQL and Redis on its private network. Remote access requires an authenticated TLS reverse proxy with request-body, connection and rate limits. Do not expose the plaintext API or database/queue ports directly.

Provider tokens and browser authentication files grant service-account access. Keep them in server configuration, mount files read-only and never include them in snapshots or reports. The web workbench keeps the operator key in tab memory rather than persistent browser storage.

Imports retrieve metadata, not streaming audio. Canonical metadata and supplied features are inputs from trusted users, not an interface for untrusted bulk uploads. Treat unofficial provider SDKs and service account restrictions as part of the deployment's trust boundary.

Exports create new private playlists and can partially succeed before a timeout or crash. An idempotency journal prevents automatic duplicate writes for a key, but does not make remote writes transactional. Follow [export recovery](docs/operations.md#export-recovery) before retrying an uncertain operation.

See [operations](docs/operations.md) for configuration, monitoring and backup requirements, and [testing](docs/testing.md) for the scope of automated verification.
