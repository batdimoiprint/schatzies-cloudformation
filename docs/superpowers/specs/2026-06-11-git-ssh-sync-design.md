# Git Remote SSH Migration and Sync Design

## Purpose
Sync local repository with GitHub using SSH authentication. Migrate from HTTPS to SSH remote URL.

## Context
- Local branch `master` is ahead of `origin/master` by 1 commit (`improve cloudformation swagger access`).
- Current remote `origin` uses HTTPS URL.
- SSH authentication to GitHub for user `batdimoiprint` is verified and working.

## Requirements
- Switch `origin` remote URL to SSH format.
- Push local `master` branch to GitHub.
- Verify remote state matches local state.

## Approach
1. Update remote URL using `git remote set-url`.
2. Push changes using `git push origin master`.
3. Verify with `git remote -v` and `git status`.

## Success Criteria
- Remote URL is `git@github.com:batdimoiprint/schatzies-cloudformation.git`.
- Local `master` matches `origin/master`.
- No pending changes or diverged branches.
