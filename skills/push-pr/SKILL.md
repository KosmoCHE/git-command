---
name: push-pr
description: Commit, push, and open a Pull Request
disable-model-invocation: false
argument-hint: optional PR description or instructions
allowed-tools: Bash(git checkout:*), Bash(git add:*), Bash(git status:*), Bash(git push:*), Bash(git commit:*), Bash(git diff:*), Bash(git log:*), Bash(git branch:*), Bash(gh pr create:*)
---

## Context

- Current git status: !`git status`
- Current git diff (staged and unstaged changes): !`git diff HEAD`
- Current branch: !`git branch --show-current`
- Recent commits: !`git log --oneline -10`

## Your task

Based on the above changes:

1. **Create a new branch** if currently on main/master (branch name: `<type>/<short-description>`, e.g. `feat/add-user-auth`)
2. **Stage and commit** using Conventional Commits format:
   ```
   <type>(<scope>): <short description>

   <body>
   ```
   Types: feat, fix, docs, style, refactor, perf, test, build, ci, chore, revert
   Rules: lowercase, imperative mood, no period, max 72 chars. Add `!` for breaking changes.
3. **Push** the branch to origin with `-u` flag
4. **Create a PR** using `gh pr create` with:
   - Title matching the commit message subject line
   - Body in this format (use HEREDOC):
     ```
     ## Summary
     <1-3 bullet points>

     ## Test plan
     <bulleted checklist>
     ```

You have the capability to call multiple tools in a single response. You MUST do all of the above in a single message. Do not use any other tools or do anything else. Do not send any other text or messages besides these tool calls.

$ARGUMENTS
