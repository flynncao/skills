# AI Commit Co-Author / ai-commit-co-author

---

## Introduction

This Skill adds the current AI assistant to a Git commit as a co-author while keeping the existing commit workflow unchanged.

**Core Value**

- Keeps your current `/commit` or default commit flow intact and only adjusts the final commit message.
- Adds AI co-author attribution automatically so commit history is easier to track.
- Supports explicit agent selection, such as forcing Codex or Claude Code, without relying on runtime detection.

**Who It's For**

- `💻` Engineers who regularly code with AI assistance — commit history stays clearer and attribution stays consistent.
- `👥` Teams that need traceable commit provenance — AI participation is visible directly in Git history.

---

## Features

### Core Features

- Appends the matching `Co-authored-by` trailer after the commit message is generated.
- Detects the current active AI assistant and adds the matching co-author attribution.
- Supports explicitly requesting one or more agents, such as `claude` and `codex`, and preserves the requested order.
- Prevents duplicates so the same co-author email is not added twice.
- Preserves the original commit subject and body without changing staging, commit scope, or later push behavior.

---

## Usage Guide

Describe your commit request in natural language, or include the AI co-author you want when invoking the Skill.

### Common Phrases

| Intent | Example Prompt | Result |
| --- | --- | --- |
| Use the current AI automatically | `Commit these changes and include the current AI as co-author` | Automatically appends the co-author that matches the active AI |
| Force Claude Code attribution | `$commit-with-agent claude` | Writes the Claude Code co-author trailer directly |
| Force multiple co-authors | `$commit-with-agent claude,codex` | Appends multiple co-author trailers in order |
| Keep the normal commit flow | `Use the normal commit flow, but add the AI co-author` | Keeps the existing workflow and only changes the final commit message |

### Output Example

The final commit message keeps the original subject and body, then appends the co-author trailer block, for example:

```text
feat: refine release script

Improve validation and error handling for release tags.

Co-authored-by: Codex <codex@openai.com>
```

---

## Use Cases

| Scenario | Role | Example Prompt | Benefit |
| --- | --- | --- | --- |
| AI-assisted code commits | Developer | `Commit these changes and include the current AI co-author` | Commit history clearly shows AI participation |
| Forced attribution control | Developer | `$commit-with-agent codex` | Lets you control attribution without relying on auto-detection |
| Multi-agent collaboration | Team member | `$commit-with-agent claude,codex` | Preserves multiple AI co-authors in a single commit |
| Preserve existing workflows | Maintainer | `Keep the usual commit flow and only add the co-author` | No Git hook or config changes are required |

---
