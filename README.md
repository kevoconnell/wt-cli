# wt

A simple CLI for managing git worktrees. Worktrees are stored in `../<repo-name>-worktrees/<name>` relative to your repository.

## Installation

```bash
# Copy to your PATH
cp wt ~/.local/bin/wt
chmod +x ~/.local/bin/wt

# Add the wtcd helper function to your shell (optional but recommended)
echo '
# Git worktree navigation helper - cd to a worktree by name
wtcd() {
    local path
    path="$(wt cd "$1" 2>/dev/null)" && cd "$path"
}' >> ~/.zshrc

source ~/.zshrc
```

## Usage

```bash
wt new <name>    # Create worktree + branch from origin/main
wt rm <name>     # Remove worktree and local branch
wt ls            # List all worktrees
wt prune         # Clean up stale metadata
wt cd <name>     # Print path (use: cd "$(wt cd name)" or wtcd <name>)
wt help          # Show help message
```

## Example Workflow

```bash
# Start a new feature
wt new feature-auth
# Creates: ../myrepo-worktrees/feature-auth

# Navigate to it
wtcd feature-auth

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

## License

MIT
