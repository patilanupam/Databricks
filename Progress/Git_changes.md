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

Here’s a clean, human-written markdown version of everything you worked through today. No robotic tone, no clutter, just clarity.

---

```md
# Dev Log: What Actually Happened Today

## 🧠 Big Picture

Today was not about coding.  
It was about understanding how systems behave when multiple tools interact.

Git, Azure, Prompt Flow, Databricks.  
All of them worked fine individually.  
The friction came from how they connect.

---

## 🔧 Git: The Real Lessons

### Branching Reality

Creating multiple branches for the same feature feels safe.  
But it introduces complexity later.

You had:
- feature/ticket_matching (colleague)
- feature/ticket_match_v1 (yours)

This created parallel histories.

👉 Key realization  
Git does not compare branches automatically.  
It only syncs a branch with its remote.

That’s why you saw:
"Already up to date"

Nothing was wrong.  
You were just asking Git the wrong question.

---

### 🧩 What Actually Needed to Happen

Not pull  
Not switch  

But merge

```

git checkout feature/ticket_matching
git merge feature/ticket_match_v1

```

That’s where your work actually combines.

---

### ✍️ Staging and Committing

You learned something subtle but important:

Every time you change code  
You must stage again

```

git add .

```

Git does not auto-track new changes after staging once.

---

### 🧹 Squashing Commits

Your colleague asked about squashing.

That wasn’t random.

It’s about keeping main clean.

Instead of:

```

fix
update
try again
final fix

```

You want:

```

Implement ticket matching feature

```

Main branch should read like a story  
Not like a debugging diary

---

## 🧠 Git Mental Model (This Changes Everything)

```

Working Directory → Staging → Commit → Push

```

and

```

pull = sync
merge = combine
checkout = switch

```

Once this clicks, Git stops feeling random.

---

## ☁️ Azure: The Real Blocker

You thought the issue was regions.

India  
Sweden  
US East  

All failed.

---

### 🚨 Reality Check

The problem was not region.  
It was access and quota.

Azure shows regions that exist  
Not regions you are allowed to use

---

### 🔍 Where You Went Wrong

You were here:

Azure → Quotas (general)

But needed:

Azure OpenAI resource → Quotas

---

### 💡 Key Insight

If you don’t see OpenAI quota  
You don’t have access

No region will work  
No model will deploy

---

### ✅ Correct Regions (When Access Exists)

- East US 2
- West US 3
- Sweden Central

Everything else is hit or miss

---

## 🧠 System Thinking

Today’s biggest lesson:

Most errors are not code errors

They are:
- environment issues
- permission issues
- wrong assumptions

---

## 🔄 Recovery Patterns

You learned how to reset chaos cleanly:

```

git reset --hard origin/branch

```

When local is broken  
Don’t patch it  
Re-align it

---

## 🧱 Local vs Remote (Critical Clarity)

```

Local repo → has .git
GitHub → does not show .git

```

If `.git` is missing  
You are not in a repo  
Simple as that

---

## ⚡ Fast Fix Thinking

Instead of debugging endlessly:

When in doubt

Re-clone  
Re-sync  
Re-test  

---

## 🎯 What Actually Improved Today

Not just commands  
But confidence

You now understand:

- why Git behaves the way it does  
- why pull didn’t work  
- how branches actually relate  
- how Azure hides real constraints  

---

## 🧠 Final Thought

Tools are predictable  
But only if you ask the right question

Most frustration today came from:

Expecting one tool to behave like another

Once you aligned expectations  
Everything made sense

---

## 🚀 Next Level

If you continue this way, next step is:

- cleaner branching strategy  
- controlled commits  
- proper environment setup  
- system-level debugging  

That’s how you move from  
"trying things"  

to  

"knowing exactly what will happen"
```

---

If you want next step, I can turn this into:

* a **resume-ready learning summary**
* or a **Notion dashboard for tracking your growth**

That’s where this becomes long-term valuable, not just one-day learning.


* **PR (Pull Request) flow**
* **Rebase vs Merge (what to use in your project)**
* **Real-world workflow for your team setup**

Just tell me 👍
