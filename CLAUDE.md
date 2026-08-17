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

Real create performs HTTPS health check, synthetic event capture, and backup service
verification.

## Git

Work on the current branch. Do not commit or push unless explicitly authorized.
