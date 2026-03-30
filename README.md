# Claude Config

Personal Claude Code configuration, commands, and tools — managed as a dotfiles-style repo.

## Setup

Clone and run the setup script to symlink everything into place:

```bash
git clone <repo> ~/src/claude
cd ~/src/claude
bash setup.sh
```

## Structure

```
~/src/claude/
├── setup.sh                        # Symlinks everything into ~/.claude/
├── bin/
│   └── gencr                       # Legacy script (kept for compatibility)
└── dotfiles/
    ├── CODE_REVIEW.md              # Code review checklist (the source of truth)
    ├── code_review_query.md        # Supporting prompt for code reviews
    └── commands/
        └── code-review.md          # /project:code-review <devname>
```

## Commands

### `/project:code-review <devname>`

Performs a structured code review for a developer against the current git branch.

- Reads the checklist from `~/.claude/CODE_REVIEW.md`
- Auto-detects the current branch
- Checks for a prior review and diffs against it if found
- Saves the report to `~/tmp/code-reviews/<branch>/<devname>-review.md`

**Usage inside Claude Code:**
```
/project:code-review swalker
```

**Usage from terminal:**
```bash
gencrnew swalker
```

## Shell Functions

See dotfiles repo, run setup-work.sh

