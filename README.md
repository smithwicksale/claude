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
├── commands/
│   └── code-review.md              # /project:code-review <devname>
└── dotfiles/
    ├── CODE_REVIEW.md              # Code review checklist (the source of truth)
    └── code_review_query.md        # Supporting prompt for code reviews
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

Add to `~/.zshrc`:

```bash
gencrnew() {
  claude "Read ~/.claude/CODE_REVIEW.md and perform a code review for developer $1. Get the branch with \`git branch --show-current\`, check for a prior review at ~/tmp/code-reviews/<branch>/$1-review.md, review changed files with \`git diff main...<branch> --name-only\`, and save the report to ~/tmp/code-reviews/<branch>/$1-review.md"
}
```
