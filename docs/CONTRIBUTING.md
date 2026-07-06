# Contributing

## Branching

- `main` is always production-ready.
- Create a feature branch per change: `feature/<agent-name>-<summary>`.
- Open a pull request into `main`. At least one review is required (see
  `.github/CODEOWNERS`).

## Working with agents

- Author agents in **Copilot Studio** and sync them via the VS Code extension.
- Keep each agent self-contained under `agents/<agent-name>/`.
- Do not hand-edit files inside an agent folder that are managed by the sync
  tooling (see `docs/AGENT_TEMPLATE.md`).

## Before you commit

- Confirm no `.mcs/` content is staged: `git status` should not list any files
  under an agent's `.mcs/` folder.
- Confirm no secrets or environment-specific values are included.
- Keep reusable prompt text in `prompt-library/`, not duplicated across agents.

## Commits

- Use clear, imperative commit messages (e.g. `Add pmo-action-capture agent`).
- Group related changes; avoid mixing unrelated agents in one commit.
