# Local Installation from Fork

Instructions for installing the Karpathy Guidelines skill directly from [github.com/springzh/andrej-karpathy-skills](https://github.com/springzh/andrej-karpathy-skills), bypassing the upstream plugin marketplace.

## Prerequisites

- [Claude Code](https://claude.ai/code) installed and authenticated

## Option A: Install as Plugin via Marketplace Source (Recommended)

Add your fork as a plugin marketplace source, then install the skill:

```bash
# From within Claude Code:
/plugin marketplace add springzh/andrej-karpathy-skills

# Then install the skill:
/plugin install andrej-karpathy-skills@karpathy-skills
```

Once installed, invoke the skill in any Claude Code session with:

```
/karpathy-guidelines
```

To update the skill after pulling new changes to your fork, re-run the install command — Claude Code fetches from the latest commit on `main`.

## Option B: Per-Project CLAUDE.md

Add the guidelines to a specific project's `CLAUDE.md`:

```bash
# New project
curl -o CLAUDE.md https://raw.githubusercontent.com/springzh/andrej-karpathy-skills/main/CLAUDE.md

# Existing project (append)
echo "" >> CLAUDE.md
curl https://raw.githubusercontent.com/springzh/andrej-karpathy-skills/main/CLAUDE.md >> CLAUDE.md
```

## Option C: Cursor

If you use Cursor, committed project rules are included in this fork. See [CURSOR.md](./CURSOR.md) for setup instructions.

## Keeping Updated

```bash
# Pull latest changes to your fork
git pull upstream main

# Reinstall the plugin to refresh
/plugin install andrej-karpathy-skills@karpathy-skills
```

## Uninstall

```bash
/plugin uninstall andrej-karpathy-skills
```
