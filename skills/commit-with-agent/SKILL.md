---
name: commit-with-agent
description: Add AI co-author attribution to a new Git commit without changing the user's normal commit workflow. Use when the user wants to commit changes and also wants AI co-authored info, a `Co-authored-by` trailer, AI attribution in the commit message, or wording like "commit with AI co-author", "commit with Codex/Claude co-author", or "add AI collaborator info to this commit". Support one explicit override trigger, `$commit-with-agent ...`, when the user wants to force one or more specific agent trailers such as `claude`, `codex`, or `claude,codex`.
license: MIT
metadata: 
  version: "1.0.1"
---

# Commit With Agent

Preserve the active commit workflow and change only its commit-message output.

Prefer semantic triggering for ordinary requests about committing with AI attribution. Treat `$commit-with-agent ...` as the single explicit trigger for forced agent selection.

## Workflow

1. Check whether the user supplied an explicit agent override after the skill name, for example `$commit-with-agent claude`, `$commit-with-agent claude code`, or `$commit-with-agent claude,codex`.
2. If an explicit override is present, normalize it to one or more supported agent identities and bypass runtime agent detection entirely.
3. If no explicit override is present, detect the current AI agent before preparing the commit message.
4. Read only the matching template or templates:
   - Codex or OpenAI Codex: [references/codex.md](references/codex.md)
   - Claude Code: [references/cc.md](references/cc.md)
5. Follow the existing `/commit` skill, explicit user instructions, or default commit behavior for repository inspection, staging, message generation, commit execution, and any later push behavior.
6. Edit the generated commit message before the commit command runs:
   - Preserve the generated subject and body.
   - Ensure exactly one blank line before the trailer block.
   - Append each matching `Co-authored-by` trailer in the explicit order requested by the user, or the single detected-agent trailer when no override was provided.
   - Do not duplicate an equivalent trailer, matched case-insensitively by email address.
7. Execute the original commit workflow with the edited message.

## Explicit Agent Overrides

When the user provides agent names after `$commit-with-agent`, treat them as an instruction to force those co-author trailers even if the active agent is different.

Supported normalization:

- `codex`, `openai codex` -> Codex
- `claude`, `cluade`, `claude code` -> Claude Code

Parsing rules:

- Split multiple requested agents on commas.
- Trim whitespace around each requested item.
- Normalize case-insensitively.
- Preserve the first occurrence order after normalization.
- If every requested agent is invalid or ambiguous, ask the user to choose from the supported set before committing.

## Agent Detection

Skip this section entirely when an explicit agent override is present.

Use the strongest available evidence in this order:

1. Use the identity declared by the active system or developer instructions.
2. Use explicit runtime or harness metadata that names the agent.
3. Use agent-specific environment or configuration markers only as supporting evidence.
4. If the identity remains ambiguous, ask the user which agent attribution to use before committing.

Do not infer the AI agent from Git author configuration, repository contents, an installed skill, or the co-author trailers of previous commits.

## Codex Behavior

When running as Codex:

1. Read [references/codex.md](references/codex.md).
2. Let the active commit workflow generate or select the normal commit message.
3. Add `Co-authored-by: Codex <codex@openai.com>` to that message before invoking `git commit`, unless an explicit override supplied a different set of trailers.
4. Pass the complete edited message through the same command or mechanism the original workflow would have used.
5. Continue with the original workflow after the commit. Do not add, remove, or trigger a push unless that workflow or the user already requires it.

For a command-line commit, use multiple `-m` arguments or an equivalent message-file mechanism so the trailer is part of the commit created initially. Preserve multiline bodies exactly where practical.

## Boundaries

- Do not install, edit, or depend on Git hooks.
- Do not change local or global Git configuration.
- Do not replace the repository's configured human author.
- Do not amend or rewrite an existing commit unless the user explicitly asks.
- Do not change which files are staged or committed beyond the original workflow.
- Do not change push, pull-request, or publication behavior.
- Do not invoke a second competing commit workflow after one has already been selected.
- Stop before committing if the selected agent template is empty or missing.
- Do not silently map unknown names to a supported agent. Only the documented aliases above may bypass detection.

## Message Shape

Use the selected reference or references as the shape, not as literal placeholder text:

```text
<original subject>

<original body, when present>

Co-authored-by: <agent name> <agent email>
Co-authored-by: <agent name> <agent email>
```
