# Adding a Copilot Studio agent

Each agent lives in its own folder under `agents/<agent-name>/` and is managed by
Copilot Studio through the Visual Studio Code extension.

## Steps

1. Create or open the agent in **Copilot Studio** (in the appropriate Power
   Platform environment — normally Dev).
2. Use the **Copilot Studio VS Code extension** to sync the agent into this repo,
   targeting a new folder under `agents/` (e.g. `agents/pmo-action-capture/`).
3. Commit the synced agent folder. Confirm that the agent's `.mcs/` folder is
   git-ignored and not staged.
4. Add a short `README.md` inside the agent folder describing its purpose.
5. Store any reusable prompt text in `prompt-library/` and reference it from the
   agent's instructions.

## Agent folder layout (managed by Copilot Studio)

Do **not** rearrange these files by hand — the sync tooling owns them:

| File / folder | Purpose |
| --- | --- |
| `settings.mcs.yml` | Agent identity and configuration (display name, schema name, model, channels, auth). Source of truth. |
| `agent.sync.yaml` | On-disk layout marker used by the sync tooling. |
| `icon.png` | Agent icon. |
| `workflows/` | Agent workflows / topics. |
| `.mcs/` | Local sync state and secrets. **Git-ignored. Never edit or commit.** |

## Naming

- Folder names are cosmetic and safe to choose freely (use `kebab-case`).
- The agent **identity** (`schemaName` in `settings.mcs.yml`) is assigned by
  Copilot Studio. To rename the agent itself, rename it in Copilot Studio and
  re-sync — do not edit the schema name by hand.
