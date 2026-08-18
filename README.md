# posthog-digitalocean

Desired state for one single-node PostHog product analytics suite on DigitalOcean.

## Architecture

- **Host**: `posthog.bigconfig.online`
- **Droplet**: `s-8vcpu-16gb` in `ams3` (Ubuntu 24.04)
- **Services**: ten containers — the PostHog web process and Celery worker, a
  standalone Rust `capture` service, the Node plugin server, Redpanda, Temporal,
  PostgreSQL, ClickHouse with embedded Keeper, Redis, and Caddy. None is
  optional; `../posthog` explains why each is required.
- **Disaster recovery**: nightly Postgres `pg_dump` and native ClickHouse
  `BACKUP`, uploaded to Cloudflare R2 (`posthog-backup`) under the profile prefix

Exact image pins are in `colors.yml`, which is the only file to edit here. Two
of them are constrained: `posthog-image` and `posthog-plugin-server-image` must
be the same commit, and `posthog-clickhouse-image` must be the version upstream
develops against.

## Operations

```sh
# Local dry run — no credentials, no provider calls
./green build
./green create --dry-run

# Converge live deployment
./green create
```
