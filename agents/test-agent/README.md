# test-agent (Action Table)

Copilot Studio agent that turns meeting notes, transcripts, or Teams recaps into
**standardized action items** for downstream activities.

## Output

From a single extraction the agent renders two ways:

- **Human-readable (default)** — Meeting Summary + PM Action Table +
  Supplementary Information, for management.
- **JSON** — one locked JSON object for downstream automation, triggered by
  `#json` or when the agent is called as a tool/flow.

Instructions source: [`prompt-library/action-capture.md`](../../prompt-library/action-capture.md).
Output contract: [`docs/skills/action-capture/SKILL.md`](../../docs/skills/action-capture/SKILL.md).

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
