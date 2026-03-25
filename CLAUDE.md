# CLAUDE.md

Behavioral rules for Claude Code in the rhi.zone repository.

## Project Overview

Static asset host for rhi.zone — served via Cloudflare Pages.

Part of the [rhi ecosystem](https://rhi.zone).

## Origin

rhi.zone is the public face of the rhi ecosystem. This repo starts as a minimal static host for install scripts (so release pages and docs can link to `rhi.zone/normalize/install.sh` instead of raw.githubusercontent.com URLs). Intended to grow into a landing page; docs.rhi.zone already covers ecosystem-wide documentation.

## Structure

- `normalize/install.sh` — Linux/macOS installer for the normalize CLI
- `normalize/install.ps1` — Windows installer for the normalize CLI
- `_headers` — Cloudflare Pages content-type overrides (ensures scripts are served as `text/plain` so `curl | sh` and `irm | iex` work correctly)

## Keeping scripts in sync

Install scripts here are copies of the canonical versions in `~/git/rhizone/normalize/`. When releasing a new normalize version, copy them here and commit:

```bash
cp ~/git/rhizone/normalize/install.sh normalize/install.sh
cp ~/git/rhizone/normalize/install.ps1 normalize/install.ps1
git add normalize/ && git commit -m "chore(normalize): sync install scripts vX.Y.Z"
```

## Negative Constraints

- Do not add build steps, bundlers, or frameworks — this is a plain static file host
- Do not use `--no-verify`
