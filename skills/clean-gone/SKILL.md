---
name: clean-gone
description: Clean up local branches deleted from remote
disable-model-invocation: false
allowed-tools: Bash(git branch:*), Bash(git worktree:*), Bash(git fetch:*)
---

## Your task

Clean up local branches that have been deleted from the remote (marked as `[gone]`), including associated worktrees.

## Steps

1. **Fetch and prune remote tracking info**
   ```bash
   git fetch --prune
   ```

2. **List branches to identify [gone] status**
   ```bash
   git branch -v
   ```

   Note: Branches with a '+' prefix have associated worktrees.

3. **List worktrees**
   ```bash
   git worktree list
   ```

4. **Remove worktrees and delete [gone] branches**
   ```bash
   git branch -v | grep '\[gone\]' | sed 's/^[+* ]//' | awk '{print $1}' | while read branch; do
     echo "Processing branch: $branch"
     worktree=$(git worktree list | grep "\\[$branch\\]" | awk '{print $1}')
     if [ ! -z "$worktree" ] && [ "$worktree" != "$(git rev-parse --show-toplevel)" ]; then
       echo "  Removing worktree: $worktree"
       git worktree remove --force "$worktree"
     fi
     echo "  Deleting branch: $branch"
     git branch -D "$branch"
   done
   ```

If no branches are marked as [gone], report that no cleanup was needed.

$ARGUMENTS
