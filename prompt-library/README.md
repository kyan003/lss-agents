# Prompt library

Reusable prompt sources that are pasted into Copilot Studio agent instructions.

Keep prompts here (not duplicated inside agent folders) so they can be shared and
versioned independently.

## Contents

- `action-capture.md` — canonical prompt for the **Action Table** agent
  (`agents/test-agent`). Converts meeting notes, transcripts, or Teams recaps
  into standardized action items. Produces **dual output** from one extraction:
  a human-readable view (Meeting Summary + PM Action Table + Supplementary
  Information) for management, and a locked JSON object for downstream
  automation (triggered by `#json` or a tool/flow call).

The output contract (schema, structure, field rules, validation) is locked in
[`docs/skills/action-capture/SKILL.md`](../docs/skills/action-capture/SKILL.md).
