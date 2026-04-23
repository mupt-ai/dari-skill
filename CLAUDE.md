# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

`dari-skill` is the public skill shipped for AI coding tools (Claude Code and Codex) so they can guide users through deploying agents on [Dari](https://dari.dev). End-user docs live at https://docs.dari.dev.

**This directory is public.** On every push to `main` of the monorepo, it is force-pushed to `mupt-ai/dari-skill` via a subtree split (`.github/workflows/mirror-public.yml`). Do not reference internal paths, backend internals, or secrets here.

## Layout

```
dari-skill/
├── .claude-plugin/plugin.json   # Claude Code plugin manifest
├── .codex-plugin/plugin.json    # Codex plugin manifest
├── skills/dari/SKILL.md         # canonical skill — consumed by both plugin routes
└── README.md                    # public-facing install + overview
```

The same `skills/dari/SKILL.md` serves Claude Code's plugin marketplace, Codex's plugin marketplace, and both tools' direct-drop paths. Do not fork a second copy — edit this one and both installs stay in sync.

## Keeping the skill accurate

The skill body mirrors two files in this monorepo:

- `docs/quickstart.mdx` — end-to-end flow (install → auth → credentials → `dari.yml` → deploy → first message).
- `docs/manifest.mdx` — the "Common mistakes" list the skill inlines.

When either of those changes, update `skills/dari/SKILL.md` in the same PR. CLI command surface is in `dari-cli/README.md` and `docs/cli.mdx`.

## Testing a change locally

Drop the updated skill into your own Claude Code install and round-trip it:

```bash
rm -rf ~/.claude/skills/dari
cp -r dari-skill/skills/dari ~/.claude/skills/
```

Restart Claude Code. In a fresh conversation, ask "help me deploy an agent to dari" — the skill should fire via description match and walk through the numbered steps.

## Releasing

Version lives in `.claude-plugin/plugin.json` and `.codex-plugin/plugin.json`. Bump both together when the skill body changes meaningfully. The mirror workflow picks up the change on the next push to `main`; no separate release step.
