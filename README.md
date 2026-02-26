# OpenClaw Docker

Docker image for [OpenClaw](https://openclaw.ai) with additional tools.

## Features

- **OpenClaw** (from npm, version-pinned)
- **AI coding CLIs**: Claude Code, Codex, Gemini CLI
- **Google Cloud CLI** (`gcloud`)
- **Matrix** bot SDK + E2EE crypto
- **GitHub CLI** (gh)
- **Helm** v3.20.0
- **Go** 1.26.0
- **Security tools**: Trivy, govulncheck, gosec, osv-scanner
- **Developer utilities**: git, jq, ripgrep, fzf, bat, ffmpeg, networking tools

## Quick Start

```bash
docker run -it --rm \
  -p 18901:18789 \
  -v ~/.openclaw/localclaw:/home/openclaw \
  docker.io/bborbe/openclaw:2026.2.15
```

Access: http://localhost:18901

## What makes this useful for others

This image is intentionally opinionated but reusable:

- Multi-arch builds (`linux/amd64`, `linux/arm64`)
- Non-root runtime user (`openclaw`)
- Good default toolchain for AI-assisted coding + DevOps work
- Simple Make targets for local run, logs, exec, and release
- Easy to fork and tailor by changing only `Dockerfile` + `Makefile`

## Available Commands

```bash
# Build image (local arch)
make build

# Build multi-arch (amd64 + arm64) and push
make build-multiarch

# Run (foreground)
make run

# Start (background)
make start

# Stop background container
make stop

# View logs
make logs

# Run onboarding
make onboard

# Push to DockerHub
make upload

# Clean local images
make clean
```

## Version

Current OpenClaw version: **2026.2.15**

To update, edit `VERSION` in Makefile and rebuild.

## Architecture

- Base: `node:22-slim` (required by OpenClaw >=22.12.0)
- Platforms: `linux/amd64`, `linux/arm64` (multi-arch)
- User: `openclaw` (non-root)
- Port: 18789 (exposed as 18901)
- State: `/home/openclaw/.openclaw`

## Suggested improvements for broader adoption

1. Add environment variable docs (`OPENCLAW_*`, model/provider config examples)
2. Add a compose example (`docker-compose.yml`) with persistent volumes
3. Add a minimal/extended image split:
   - `openclaw-core` (small base)
   - `openclaw-dev` (extra CLIs/security tooling)
4. Add CI smoke tests (container boots, `openclaw --help`, `gcloud --version`)
5. Add release notes section per image version (what changed + breaking changes)

## License

MIT
