# CHEC QS Skill — Team Marketplace

> [ภาษาไทย](./README_TH.md)

A public Claude Code marketplace for the CHEC team — construction QS tools, document processing, and project workflows. Add once, install individual plugins as needed.

## Add as Marketplace

In Claude Code → Manage Plugins → Marketplaces → Add:

```bash
https://github.com/singkhonji/chec-qs-skill
```

Then go to the **Plugins** tab to browse and install available plugins.

---

## Contributing a Plugin

Anyone on the team can add a new plugin. Follow this structure:

### 1. Create the plugin folder

```text
plugins/
└── your-plugin-name/
    ├── .claude-plugin/
    │   └── plugin.json       ← required metadata
    └── skills/
        └── your-plugin-name/
            └── SKILL.md      ← skill definition
```

### 2. plugin.json format

```json
{
  "name": "your-plugin-name",
  "description": "One sentence — what this plugin does.",
  "author": {
    "name": "Your Name",
    "email": "your@email.com"
  }
}
```

### 3. SKILL.md format

```markdown
---
name: your-plugin-name
description: >
  When should Claude use this skill?
  List trigger phrases, commands, or conditions here.
  The more specific the triggers, the better.
---

# Your Plugin Title

[Skill instructions here — what Claude should do when this skill is invoked]
```

**Model-invoked skill** (Claude picks it up automatically from context):
- Write natural trigger phrases in the `description` field

**User-invoked slash command** (user types `/your-plugin-name`):
- Add `argument-hint: <arg>` to the frontmatter

### 4. Register in marketplace.json

Add an entry to `.claude-plugin/marketplace.json` under `"plugins"`:

```json
{
  "name": "your-plugin-name",
  "description": "Same one-liner as plugin.json",
  "author": {
    "name": "Your Name",
    "email": "your@email.com"
  },
  "category": "productivity",
  "source": {
    "source": "git-subdir",
    "url": "https://github.com/singkhonji/chec-qs-skill.git",
    "path": "plugins/your-plugin-name",
    "ref": "main"
  }
}
```

### 5. Commit and push

```bash
git add plugins/your-plugin-name .claude-plugin/marketplace.json README.md
git commit -m "Add plugin: your-plugin-name"
git push
```

---

## Plugin Directory

| Plugin | Description |
| --- | --- |
| *(no plugins yet — be the first to contribute!)* | |

---

## Structure

```text
chec-qs-skill/
├── .claude-plugin/
│   └── marketplace.json      ← marketplace index
├── plugins/
│   └── <plugin-name>/        ← one folder per plugin
│       ├── .claude-plugin/
│       │   └── plugin.json
│       └── skills/
│           └── <skill-name>/
│               └── SKILL.md
└── README.md
```
