Here’s a clean **Markdown (MD) summary** of everything you’ve gone through so far:

---

# Git Workflow Notes – Branching & Sync

## Current Branch Status

```bash
git branch
```

Output:

* `feature/ticket_match_v1` (current)
* `main`

---

## Issue Faced

Tried switching to a branch:

```bash
git checkout feature/ticket_matching
```

Error:

```
pathspec did not match any file(s) known to git
```

### Root Cause

* Local repo did not have latest remote branches
* Branch existed remotely but not fetched locally

---

## Fix – Fetch Remote Branches

```bash
git fetch origin
```

---

## Verify Remote Branches

```bash
git branch -r
```

Found:

```
origin/feature/ticket_matching
```

---

## Checkout Remote Branch Locally

```bash
git checkout feature/ticket_matching
```

### OR (explicit way)

```bash
git checkout -b feature/ticket_matching origin/feature/ticket_matching
```

---

## Pull Latest Changes

```bash
git pull origin feature/ticket_matching
```

---

## If Working on Another Branch (e.g., feature/ticket_match_v1)

### To bring changes from another branch:

```bash
git fetch origin
git merge origin/feature/ticket_matching
```

---

## Push Changes to Your Branch

```bash
git add .
git commit -m "your message"
git push origin feature/ticket_match_v1
```

---

## Safe Workflow Before Pulling

### Option 1: Commit changes

```bash
git add .
git commit -m "WIP"
git pull origin <branch>
```

### Option 2: Stash changes

```bash
git stash
git pull
git stash pop
```

---

## Key Learnings

* Always run:

```bash
git fetch origin
```

before working with new branches

* Branch names must match exactly

* Git does NOT override your code automatically:

  * Conflicts → manual resolution
  * Silent merge → review logic carefully

* Avoid merging branches unless intended

---

## Simple Rule

> Fetch → Check → Checkout → Pull → Work → Commit → Push

---

If you want, I can also give you:

* **PR (Pull Request) flow**
* **Rebase vs Merge (what to use in your project)**
* **Real-world workflow for your team setup**

Just tell me 👍
