---
name: action-capture-output-contract
description: >-
  Output contract for the KION PMO Action Pipeline (the "Action Table" agent).
  USE WHEN generating, reviewing, or validating standardized action items from
  meeting notes, transcripts, or Teams recaps — to guarantee consistent,
  management-ready output and a stable JSON contract for downstream automation.
  Covers the two output renderings (human-readable + JSON), the field rules,
  and the validation checklist. DO NOT USE for unrelated summarization.
---

# Action Capture — Output Contract

This skill locks the **output** of the KION PMO Action Pipeline so results are
consistent for management and stable for downstream systems. The full agent
instructions live in [`prompt-library/action-capture.md`](../../../prompt-library/action-capture.md);
this file is the authority on **what the output must look like** and **how to
validate it**.

## Purpose

Turn a meeting source (pasted notes, a raw transcript, or a Teams recap in
context) into **standardized action items** that are:

- **Consistent** — the same source yields the same actions, owners, statuses,
  tags, priorities, order, and count.
- **Management-ready** — a clean human-readable summary + action table.
- **Downstream-ready** — a locked JSON object for flows, agents, and trackers.

## Two renderings, one extraction

Extraction runs **once**. Only the rendering differs, and both renderings MUST
carry the same actions, owners, statuses, tags, priorities, order, and count.

1. **Human-readable (default)** — for people/management. Three sections in this
   exact order: `Meeting Summary`, `PM Action Table`, `Supplementary Information`.
2. **JSON (`#json` or tool/flow context)** — for automation. One JSON object,
   fixed keys, no markdown fences, no prose outside the object.

### Human-readable structure

```
## Meeting Summary
Meeting / Source: <title or "not stated">
Date: <date or "not stated">
Participants: <names or "not stated">

<2–5 sentence summary: purpose, key discussion, decisions, outcome.>

## PM Action Table
Total actions: <number>

| No. | Action | Detail | Owner | Deadline | Status | Tag | Priority | Comment |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | ... | ... | ... | ... | ... | ... | ... | ... |

## Supplementary Information
- <context / decision / blocker / dependency / out-of-scope item>
(Use "None" if there is nothing relevant.)
```

### JSON schema

```json
{
  "meeting": { "source": "", "date": "", "participants": [] },
  "summary": "",
  "totalActions": 0,
  "actions": [
    {
      "no": 1,
      "action": "",
      "detail": "",
      "owner": "",
      "deadline": "",
      "status": "Open",
      "tag": "",
      "priority": "Normal",
      "comment": "",
      "evidence": ""
    }
  ],
  "supplementary": []
}
```

## Field rules (both renderings)

| Field | Rule |
| --- | --- |
| No. / `no` | Sequential from 1, first-mention order, no gaps. |
| Action / `action` | Verb-first, one deliverable, neutral wording. |
| Detail / `detail` | Short scope note; multi-step single-deliverable stays one row (numbered sub-steps). |
| Owner / `owner` | Explicitly named only; join multiple with `" + "`; else `UNASSIGNED`; names as "First Last". |
| Deadline / `deadline` | Day-month (e.g. `29-May`); resolve relative dates only if meeting date known; else blank; never `TBD`. |
| Status / `status` | `Open` \| `Done` \| `Blocked` (merged tie-break `Blocked > Open > Done`). |
| Tag / `tag` | First match: `AI` (or `SWI / AI / Template`), `Governance / AI`, `Template`, `Process`, `Governance`, `Tool`. Discussing/sharing AI ≠ `AI`. |
| Priority / `priority` | `High` if urgent, `Low` if explicitly minor, else `Normal`. |
| Comment / `comment` | Caveat/dependency/decision that is not the deliverable; else blank. |
| `evidence` (JSON) | Verbatim quote from source; blank if no exact quote — never invent. |

## Validation checklist (run before accepting output)

1. Every row and supplement bullet is backed by a quotable statement.
2. No two rows describe the same deliverable.
3. Every owner is explicit, else `UNASSIGNED` (never inferred from the speaker).
4. Deadlines are stated or correctly resolved, else blank; never `TBD`.
5. Every status is `Open` / `Done` / `Blocked`; every priority is `High` /
   `Normal` / `Low`.
6. Tags follow the fixed priority order and are consistent across runs.
7. No. is sequential with no gaps; rows in first-mention order.
8. Actions are in the table, context is in the supplement (no leakage).
9. `Total actions` / `totalActions` equals the row count.
10. **Parity:** the human-readable and JSON renderings carry the same actions
    and count.

## Output discipline

- Output only the requested rendering — nothing before or after it.
- JSON mode: one object, fixed keys, no code fences, escape inner quotes as `\"`.
- Never rephrase the same action differently across runs.
