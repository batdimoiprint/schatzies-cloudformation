# Git SSH Migration and Sync Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Migrate git remote from HTTPS to SSH and sync local `master` branch with GitHub.

**Architecture:** Configuration update using standard `git remote` and `git push` commands.

**Tech Stack:** Git, SSH.

---

### Task 1: Update Remote URL

**Files:**
- Modify: `.git/config` (via git command)

- [ ] **Step 1: Update origin URL to SSH**

```bash
git remote set-url origin git@github.com:batdimoiprint/schatzies-cloudformation.git
```

- [ ] **Step 2: Verify remote URL updated**

Run: `git remote -v`
Expected: `origin git@github.com:batdimoiprint/schatzies-cloudformation.git (fetch)` and `(push)`

---

### Task 2: Push Changes to Remote

- [ ] **Step 1: Push local master to origin**

```bash
git push origin master
```

- [ ] **Step 2: Verify push success**

Run: `git status`
Expected: `Your branch is up to date with 'origin/master'.`

---

### Task 3: Commit Documentation

**Files:**
- Create: `docs/superpowers/specs/2026-06-11-git-ssh-sync-design.md`
- Create: `docs/superpowers/plans/2026-06-11-git-ssh-sync.md`

- [ ] **Step 1: Add and commit docs**

```bash
git add docs/superpowers/specs/2026-06-11-git-ssh-sync-design.md docs/superpowers/plans/2026-06-11-git-ssh-sync.md
git commit -m "docs: add git sync design and implementation plan"
```

- [ ] **Step 2: Final push to sync docs**

```bash
git push origin master
```
