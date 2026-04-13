---
name: squash
description: Squash multiple commits into one
disable-model-invocation: false
argument-hint: optional number of commits to squash
allowed-tools: Bash(git log:*), Bash(git reset:*), Bash(git add:*), Bash(git commit:*), Bash(git diff:*), Bash(git status:*), Bash(git merge-base:*), Bash(git branch:*)
---

## Context

- Current branch: !`git branch --show-current`
- Recent commits: !`git log --oneline -20`

## Your task

Squash multiple commits on the current branch into a single commit.

### Steps

1. Find the merge base with the main branch:
   ```
   git merge-base HEAD main
   ```
   (also try `master` if `main` doesn't exist)

2. Count how many commits will be squashed and show them to confirm the scope

3. Soft reset to the merge base:
   ```
   git reset --soft <merge-base>
   ```

4. Create a single new commit using **Conventional Commits** format, summarizing all the squashed changes:
   ```
   <type>(<scope>): <short description>

   <body summarizing the squashed commits>
   ```

### Rules

- If the user provides a number (e.g. `/git-command:squash 3`), squash only the last N commits instead of all commits since the merge base
- Always show the user which commits will be squashed before proceeding
- Use HEREDOC for the commit message

Do not use any other tools or do anything else besides the squash operation.

$ARGUMENTS
