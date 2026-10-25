# Changelog

User-visible changes are recorded here. Changes under **Unreleased** are available on `main` and have not been published as a tagged release.

## Unreleased

### Added

- Canonical music models and metadata adapters for Spotify, YouTube Music and Yandex Music, with MusicBrainz lookup, caching and coordinated rate limiting.
- Explainable cross-catalogue matching with edition checks, alternatives and persistent manual mappings.
- Canonical JSON import/export and a deterministic YAML playlist compiler with bounded beam search and ordering refinement.
- REST API, CLI and web workbench with system, light and dark themes.
- Reviewed exports to new private playlists with an idempotency journal and worker heartbeat health checks.
- PostgreSQL migrations, Redis background jobs, Docker Compose deployment and CI for CPython 3.10–3.15.
- User, provider, API, operations and contributor guides, security and conduct policies, issue/PR templates and shared editor/Git settings.

### Limitations

- The hosted application supports one trusted operator; provider credentials are configured on the server without automatic token refresh.
- Existing-playlist synchronization, local audio analysis and AI interfaces are not available. Audio features must be supplied as metadata.
- Remote exports can partially succeed; unresolved write outcomes require operator recovery before retrying.
