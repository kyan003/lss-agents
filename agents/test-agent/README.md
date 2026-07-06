# test-agent

Seed example Copilot Studio agent used to establish the repository structure.
Replace with a real agent when development begins.

## Files

This folder is managed by Copilot Studio via the VS Code extension. Do not
rearrange its contents by hand.

- `settings.mcs.yml` — agent identity and configuration (source of truth).
- `agent.sync.yaml` — on-disk layout marker for the sync tooling.
- `icon.png` — agent icon.
- `workflows/` — agent workflows / topics.
- `.mcs/` — local sync state and secrets. Git-ignored; never edit or commit.

## Related

Reusable prompt sources live in [`prompt-library/`](../../prompt-library/), for
example [`action-capture.md`](../../prompt-library/action-capture.md).
