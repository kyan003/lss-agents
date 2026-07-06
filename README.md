# LSS Agents

Production repository for **Microsoft Copilot Studio** agents in the LSS workspace.

Each agent is authored in Copilot Studio and synced to this repo through the
Copilot Studio Visual Studio Code extension. This repository provides the
structure, conventions, and guardrails for building and promoting agents across
environments.

> The current `test-agent` and the `action-capture` prompt are seed examples.
> They demonstrate the layout and are meant to be replaced by real agents.

## Structure

| Path | Purpose |
| --- | --- |
| `agents/` | One folder per Copilot Studio agent. Each folder is **owned by Copilot Studio** — its internal files are managed by the sync tooling and must not be manually rearranged. |
| `prompt-library/` | Reusable prompt sources (system prompts, instruction blocks) that are pasted into agent instructions in Copilot Studio. |
| `docs/` | Repository conventions: how to add an agent, how to contribute, and how environments map to Power Platform. |
| `.github/` | Ownership (`CODEOWNERS`) and CI validation workflows. |

## Golden rule

**Wrap, don't reshape.** Everything inside an `agents/<name>/` folder is managed
by Copilot Studio. Add structure *around* agents (docs, prompt library, CI), but
never move or rename the files *inside* an agent folder by hand — doing so breaks
Copilot Studio's sync and change tracking.

## Adding a new agent

See [docs/AGENT_TEMPLATE.md](docs/AGENT_TEMPLATE.md).

## Environments and promotion

See [docs/ENVIRONMENTS.md](docs/ENVIRONMENTS.md) and
[docs/CONTRIBUTING.md](docs/CONTRIBUTING.md).

## Security

- Local Copilot Studio sync state lives in each agent's `.mcs/` folder. It
  contains tenant IDs, Dataverse endpoints, account details, and secrets. It is
  **git-ignored** and must never be committed.
- Never commit secret values. Use Power Platform environment variables and set
  their values per environment. See [docs/ENVIRONMENTS.md](docs/ENVIRONMENTS.md).
