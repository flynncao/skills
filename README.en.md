<a id="english-guide"></a>

# Flynn's Personal Skills Repository

[中文](README.md#chinese-guide)

---

## Project Overview

This is my personal AI Skills repository. I use it to maintain the Skills I repeatedly rely on in day-to-day development work.

The purpose of these Skills is simple:

- Turn recurring workflows into reusable capabilities
- Let Codex, Claude Code, or compatible clients trigger the right Skill when needed
- Make it easier to reuse the same Skills across different machines and clients

The repository will keep growing over time. You can install the whole repository or just install a single Skill.

## Installation

### Option 1: Install with `npx` in One Command (Recommended)

```bash
npx skills add https://github.com/flynncao/skills --skills commit-with-agent
```

This is the most direct way to install a Skill. It installs the selected Skill into the correct Skills directory automatically.

If more Skills are added later, you can keep using the same pattern and install them by name.

### Option 2: Clone the Entire Repository with Git

```bash
git clone https://github.com/flynncao/skills.git
```

After cloning, copy the specific Skill directory you want into your client's Skills directory.

### Option 3: Install Manually

1. Download the ZIP archive of this repository, or run `git clone`
2. Pick the Skill directory you want, such as `commit-with-agent`
3. Copy that directory into your client's Skills folder

Common locations:

- Codex
  - macOS / Linux: `~/.codex/skills/`
  - Windows: `%USERPROFILE%\\.codex\\skills\\`
- Claude Code
  - macOS / Linux: `~/.claude/skills/`
  - Windows: `%USERPROFILE%\\.claude\\skills\\`

For example, to install `commit-with-agent` into Codex:

```bash
cp -R commit-with-agent ~/.codex/skills/
```

On Windows, you can copy the folder directly to:

```text
%USERPROFILE%\.codex\skills\commit-with-agent\
```

### Directory Structure Example

Keep the installed Skill directory intact, for example:

```text
~/.codex/skills/commit-with-agent/
├── SKILL.md
├── README.md
├── README.en.md
└── references/
```

If `references/` or documentation files are missing, some Skills may not work as expected.

### Verify the Installation

After installation, restart the client or reload Skills, then describe the task directly in chat or mention the Skill by name.

For `commit-with-agent`, you can say:

```text
Commit the current changes and add codex and claude as co-authors
```

If the client detects and triggers the Skill correctly, the installation is working.

## Usage

### Basic Usage

Skills in this repository are mainly designed for natural-language triggering. In most cases, you do not need extra commands as long as your request is clear.

There are three common ways to use them:

#### 1. Describe the task directly

```text
Commit the current changes and include an AI co-author
```

#### 2. Mention a Skill explicitly

```text
Use commit-with-agent to commit these changes
```

#### 3. Read the Skill-specific README

Each Skill directory usually includes its own README, where you can check:

- What problem it solves
- How to ask for it
- What kind of output it produces

## Currently Included Skills

### `commit-with-agent`

Path: [`commit-with-agent`](commit-with-agent/)

Purpose:

- Appends AI co-author trailers while keeping your normal commit workflow unchanged
- Supports `Co-authored-by` identities such as `Codex` and `Claude`
- Useful when you want AI collaboration attribution to appear in Git history

Installation example:

```bash
npx skills add https://github.com/flynncao/skills --skills commit-with-agent
```

## File Reference

- `README.md`: Chinese overview and installation guide
- `README.en.md`: English overview and installation guide
- `README_refernece.md`: reference document used for rewriting this README
- `*/SKILL.md`: definition file for a single Skill
- `*/README.md`: Chinese documentation for a single Skill
- `*/README.en.md`: English documentation for a single Skill
- `*/references/`: supporting references or templates for a Skill

---
