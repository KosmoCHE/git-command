---
name: amend
description: Amend the most recent commit
disable-model-invocation: false
argument-hint: optional new commit message
allowed-tools: Bash(git add:*), Bash(git status:*), Bash(git commit:*), Bash(git diff:*), Bash(git log:*)
---

## Context

- Current git status: !`git status`
- Current git diff (staged and unstaged changes): !`git diff HEAD`
- Last commit message: !`git log -1 --format=%B`
- Last commit files: !`git diff --name-only HEAD~1 HEAD`

## Your task

Amend the most recent commit:

1. If there are unstaged/staged changes, add them to the last commit
2. If the user provided a new message in the arguments, use it (in Conventional Commits format)
3. If no new message is provided and there are new changes, keep the existing commit message
4. Use `git commit --amend` (with `--no-edit` if keeping the existing message)
5. Always pass commit messages via a HEREDOC for correct formatting

**Warning**: Do NOT amend if the commit has already been pushed to a shared remote branch. Check with `git status` for ahead/behind info. If already pushed, warn the user and stop.

You have the capability to call multiple tools in a single response. Stage and amend using a single message. Do not use any other tools or do anything else. Do not send any other text or messages besides these tool calls.

$ARGUMENTS
