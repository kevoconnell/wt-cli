# wt

A simple CLI for managing git worktrees. Worktrees are stored in `../<repo-name>-worktrees/<name>` relative to your repository.

## Installation

```bash
# Copy to your PATH
cp wt ~/.local/bin/wt
chmod +x ~/.local/bin/wt

# Run setup to install dependencies and shell integration
~/.local/bin/wt setup
source ~/.zshrc
```

## Setup

The `wt setup` command will:

1. Install `fzf` via Homebrew (for interactive worktree selection)
2. Add a `wt` shell function to your `~/.zshrc` that enables navigation

## Usage

```bash
wt new <name>    # Create worktree and navigate to it
wt ls            # List worktrees interactively, navigate to selection
wt cd <name>     # Navigate to a worktree by name
wt rm <name>     # Remove worktree and local branch
wt prune         # Remove all worktrees (keeps only main repo)
wt setup         # Install dependencies and shell integration
wt help          # Show help message
```

## Example Workflow

```bash
# First time setup (only once)
wt setup
source ~/.zshrc

# Start a new feature - creates and navigates to the worktree
wt new feature-auth

# Switch between worktrees interactively
wt ls

# Navigate directly by name
wt cd feature-auth

# Work on your feature...

# When done, clean up
wt rm feature-auth
```

## What `wt new` Does

1. Fetches `origin/main`
2. Creates branch `<name>` from `origin/main`
3. Creates worktree at `../<repo-name>-worktrees/<name>`
4. Copies `.env` if it exists
5. Opens in VS Code if available
6. Navigates to the new worktree

## Requirements

- zsh
- git
- Homebrew (for installing fzf)
- fzf (installed automatically via `wt setup`)

## License

MIT
