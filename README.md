# claude-toolkit

A Claude Code plugin marketplace with commands shared across projects.

## Install

```text
/plugin marketplace add andersr/claude-toolkit
/plugin install toolkit@claude-toolkit
```

To give everyone on a project the plugin automatically, add this to the project's `.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "claude-toolkit": {
      "source": { "source": "github", "repo": "andersr/claude-toolkit" }
    }
  },
  "enabledPlugins": {
    "toolkit@claude-toolkit": true
  }
}
```

## Commands

| Command | What it does |
|---|---|
| `/toolkit:commit` | Groups every changed file into logical commits |
| `/toolkit:pr` | Opens a PR for the current branch, linked to its Linear ticket |
| `/toolkit:start-task <ID>` | Fetches a Linear ticket, creates its branch and starts planning |

## Per-project differences

Everything in this toolkit must be generic: no project names, ticket prefixes, package managers, branch names or other details specific to one codebase. The commands are written generically and take project details from each project's `CLAUDE.md` (commit conventions, for example) or from the repository itself (base branch, PR template). Put project-specific rules in `CLAUDE.md`, not in a copy of the command.

## Releasing a change

Bump `version` in both `.claude-plugin/marketplace.json` and `plugins/toolkit/.claude-plugin/plugin.json`, then push. Users pick it up with `/plugin marketplace update claude-toolkit`.
