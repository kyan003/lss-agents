# Environments

Copilot Studio agents run in **Power Platform environments**. This repository
tracks the *source* of each agent; the running agents live in those environments.

## Recommended environment tiers

| Tier | Purpose | Power Platform environment |
| --- | --- | --- |
| Dev | Authoring and experimentation | `LSS-Dev` (or per-developer) |
| Test | Validation / UAT | `LSS-Test` |
| Prod | Live usage | `LSS-Prod` |

## Promotion flow

1. Author and sync agents from **Dev**.
2. Merge changes to `main` via pull request (see `CONTRIBUTING.md`).
3. Promote to **Test**, then **Prod**, using Copilot Studio / Power Platform
   solution export and import (ALM), keeping environment-specific values in
   environment variables.

## Environment variables and secrets

- Agents reference configuration through **Power Platform environment variables**
  (for example SharePoint site URLs, library paths, and secrets).
- Commit only the environment variable **definitions**, never environment-specific
  **values** or secrets.
- Set values per environment in Power Platform, not in this repository.
- Local sync state (`agents/*/​.mcs/`) is git-ignored because it contains
  environment-specific identifiers and secrets.
