# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Purpose

Builds and publishes custom Docker images used by `straigent-engine` for language-specific static analysis. Only tools that need custom configuration or pinned behavior live here; upstream images (e.g. `golang:1.24`, `golangci-lint`) are used directly.

## Layout

```
resources/languages/
├── _all/              # language-agnostic tools (ast-grep, ripgrep)
│   ├── ast-grep/
│   └── ripgrep/
├── go/tools/
│   └── go-test-cov/
└── python/tools/
    ├── bandit/
    ├── pyright/
    ├── pytest-cov/
    ├── radon/
    ├── ruff/
    ├── tach/
    └── vulture/
```

Each tool directory is a standalone Docker build context with its own `Dockerfile` and corresponding GitHub Actions workflow in `.github/workflows/build-<resource-path>.yml`.

## Image Naming Convention

`ghcr.io/<owner>/straigent-engine-<resource-path-with-dashes>`

Example: `resources/languages/python/tools/ruff` → `straigent-engine-languages-python-tools-ruff`

## CI/CD

Each workflow triggers on changes to its image directory or its own workflow file. Published tags: `sha`, `branch`, `tag`, and `latest` (default branch only).

## Adding a New Image

1. Create `resources/languages/<lang>/tools/<tool>/Dockerfile`
2. Create `.github/workflows/build-languages-<lang>-tools-<tool>.yml` following the existing pattern
