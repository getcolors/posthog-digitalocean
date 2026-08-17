# posthog-digitalocean

Desired state for one single-node PostHog product analytics suite on DigitalOcean.

## Architecture

- **Host**: `posthog.bigconfig.online`
- **Droplet**: `s-4vcpu-8gb` in `ams3` (Ubuntu 24.04)
- **Services**: PostHog Web, Celery Worker, PostgreSQL 17, ClickHouse 24.8, Redis 7.2, Caddy 2.11.4
- **Disaster Recovery**: Backups stored in Cloudflare R2 (`posthog-backup`)

## Operations

```sh
# Local dry run
./green build
./green create --dry-run

# Converge live deployment
./green create
```
