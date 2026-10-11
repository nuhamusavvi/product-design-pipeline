# Phase 1 — Cursor runtime compatibility

This is the implementation plan for Phase 1. The skill files have not been edited yet. The 18-stage workflow, Plane intake, and Lovable prompt generation stay unchanged.

Work only in `D:\Skills\product-design-pipeline`. Do not touch `C:\Users\Nuha\.claude\skills\product-design-pipeline`. Do not delete files. Do not add Plane intake, Lovable prompts, or a new stage order.

`AskQuestion` is a real tool in the Cursor session that produced this plan (structured questions with option ids). `rg` was not confirmed on PATH, so the verification note will use `rg` only when `Get-Command rg` succeeds, and PowerShell `Select-String` otherwise.

## Edits

### `SKILL.md`

- Rewrite the frontmatter `description` (keep it under 1024 characters). Describe the current Arabic-to-handoff package. Trigger on analyzing requirements, documenting workflows, and preparing UI design deliverables. Remove `/product-brief`. Do not claim Plane or Lovable.
- Add a short `## Cursor runtime` section after the opening paragraphs:
  - Canonical repo: `D:\Skills\product-design-pipeline`.
  - Cursor only discovers the skill after it is installed in the user Agent Store at `skills/product-design-pipeline/` or in a project's `.cursor/skills/`. This repo is not that install.
  - Plane MCP is not configured. Do not read Plane issues.
  - Lovable authentication has not been verified. Do not call Lovable tools.
- Gate protocol (around line 163) and the stage-0 MUST DO (around line 335): use `AskQuestion` when that tool is available, with real options including an approve path, at most four questions. If it is not available, ask the same questions in chat and wait. Do not invent a tool name or continue as if the user answered.
- Stage 15 MUST DO: read `frontend-design/SKILL.md` in this repo. Do not invoke `frontend-design` as a registered skill.
- Keep the stage 5/8/12 loads of `feature-forge/references/ears-syntax.md` and `acceptance-criteria.md`, and state those paths are relative to the skill root. Add one line: do not run the Feature Forge workshop or its Task-subagent flow.

### `references/spec-templates.md` and `references/backlog-templates.md`

Replace both broken `../../feature-forge/...` loads and the skill-root-only mentions (`feature-forge/references/...` at the EARS quick reference and the story-writing rules) with paths that resolve from `references/`:

- `../feature-forge/references/ears-syntax.md`
- `../feature-forge/references/acceptance-criteria.md`

### `references/intake-questions.md`

Replace the two `AskUserQuestion` mentions with the same `AskQuestion`-or-chat rule. Keep the question content and the four-question batch limit.

### `references/rtl-html-guide.md` and `references/style-picker-guide.md`

Where they say to use the `frontend-design` skill, say to read `frontend-design/SKILL.md` from this repo. Leave the precedence order as it is.

### `references/html-docs-guide.md`

Replace the `bash` `grep` block in the mechanical checks (near line 589). If `rg` is on PATH, run the five checks with `rg`. Otherwise run the same five checks with PowerShell `Select-String`. Do not assume `bash` or GNU `grep`.

### `feature-forge/SKILL.md`

Add a short banner under the title: this pipeline loads only `references/ears-syntax.md` and `references/acceptance-criteria.md`. The workshop and Task-subagent workflow in this file are not part of a product-design-pipeline run. Do not rewrite the workshop, and do not edit the EARS or acceptance-criteria files.

## Left unchanged on purpose

- Stage order, templates' product content, assets, ID registry, and `AUDIT.md`.
- `feature-forge/references/interview-questions.md` and the workshop body still say `AskUserQuestions` and Task subagents. Those stay because the workshop is not invoked.
- `frontend-design/SKILL.md` body, including the "Claude is capable..." sentence and the missing `LICENSE.txt` pointer. Out of scope for this phase.
- Informal "grep the output" wording in the RTL and flow-board guides. Those are review checks, not the shell script.

## Validation after the edits

- Resolve each edited relative path from its file's directory and confirm the target exists.
- Confirm the Claude install `SKILL.md` hash is unchanged and no repo files were deleted.
- Search the edited files for `AskUserQuestion`, `/product-brief`, and `../../feature-forge`.
- Report changed files, a one-line summary of each change, and remaining Claude-specific references with whether they are intentional.
- Do not claim the skill is installed or operational. Discovery still requires a separate install step, which this phase does not perform.
