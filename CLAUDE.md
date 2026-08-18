# CLAUDE.md

## Repository

Desired state for `posthog-digitalocean`: PostHog single-node analytics suite
on one DigitalOcean Droplet in Amsterdam, published at `https://posthog.bigconfig.online`
through Cloudflare and Caddy. Behavior lives in `../posthog`.

Tracked source is `colors.yml`, toolchain and documentation, the installed
Package Skill, and a root launcher copied from its payload.
`.colors/` is generated private state and `.envrc.private` contains credentials;
never read, edit or commit either.

## Commands

```sh
./green build
./green create --dry-run
./green create
./green delete
```

Build and dry-run require no credentials. Never export `COLORS_PAR_PROFILE`.
Keep `compute-prevent-destroy: true`; deletion requires separate authorization
and a one-run `COLORS_PAR_COMPUTE_PREVENT_DESTROY=false` override.

The root `green` is a copy, not a symlink. After a Package Skill update copy
`.agents/skills/package-posthog-green/green` over it. Never hand-edit its SHA.

## Verification

A real create verifies the deployment rather than the gate, because this stack
fails by reporting success. It checks HTTPS health **with a valid certificate**,
posts a synthetic event and polls ClickHouse until the row appears, asks PostHog
whether Celery is alive and whether any async migration is pending, and confirms
the backup by finding a fresh object in R2.

A 200 from `/capture/` means the event reached the capture service and nothing
more; the failure this stack produces most often is an accepted event that is
never stored. Do not treat a health check or a status code as evidence.

## Git

Work on the current branch. Do not commit or push unless explicitly authorized.
