# dari-skill

A skill that teaches AI coding tools (Claude Code, Codex) how to use [Dari](https://dari.dev) — install the CLI, authenticate, store credentials, write `dari.yml`, and deploy.

Full docs: https://docs.dari.dev.

> This is an **editor-tool skill** (runs inside your coding assistant). It is distinct from Dari's own in-agent `skills:` feature, which bundles playbooks *inside* a deployed agent. See https://docs.dari.dev/skills/overview for the in-agent kind.

## Install

### Claude Code

Add this repo as a plugin marketplace, then install the `dari` plugin:

```
/plugin marketplace add mupt-ai/dari-skill
/plugin install dari@mupt-ai-dari-skill
```

Or drop the skill directly (no marketplace):

```bash
git clone https://github.com/mupt-ai/dari-skill.git
cp -r dari-skill/skills/dari ~/.claude/skills/
```

Restart Claude Code. The skill auto-loads; trigger it by asking about deploying a Dari agent.

### Codex

Add as a Codex plugin marketplace, then enable `dari` from `/plugins`:

```
codex plugin marketplace add mupt-ai/dari-skill
```

Or drop the skill directly:

```bash
mkdir -p ~/.agents/skills/dari
curl -fsSL https://raw.githubusercontent.com/mupt-ai/dari-skill/main/skills/dari/SKILL.md \
  -o ~/.agents/skills/dari/SKILL.md
```

## What's inside

- [`skills/dari/SKILL.md`](skills/dari/SKILL.md) — the skill body. Plain markdown with YAML frontmatter.
- [`.claude-plugin/plugin.json`](.claude-plugin/plugin.json) — Claude Code plugin manifest.
- [`.codex-plugin/plugin.json`](.codex-plugin/plugin.json) — Codex plugin manifest.

## Cursor, Windsurf, Aider, generic

No native `SKILL.md` support in Cursor as of this release; we'll ship a rules variant when it lands. Other tools that consume `AGENTS.md`-style context: copy `skills/dari/SKILL.md` into the file your tool reads.

## Reporting issues

File against the public CLI repo: https://github.com/mupt-ai/dari-cli/issues.
