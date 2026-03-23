Here’s a clean, structured Markdown summary of everything you learned today, starting exactly from your real-world scenario.


---

# Debug & Learning Summary – Git, Databricks, Local Setup

---

# 1. When 2 Developers Work on the Same Feature

## ❌ What NOT to do

feature/ticket_matching        (colleague) feature/ticket_match_v1        (you)

Problems:
- duplicate logic
- merge conflicts later
- confusion on which branch is source of truth
- wasted time syncing branches

---

## ✅ Correct Team Workflow

### Option A — Single Shared Feature Branch (simple teams)

feature/ticket_matching

Workflow:
```bash
git checkout feature/ticket_matching
git pull

# do work

git add .
git commit -m "your changes"
git push


---

Option B — Sub-branches (best practice in teams)

feature/ticket_matching
   ├── anupam-work
   ├── colleague-work

Workflow:

git checkout -b anupam-work

# work

git push origin anupam-work

Then:

Create PR → feature/ticket_matching

Merge via PR



---

🔥 Key Rule

One feature → One main branch
Multiple developers → sub-branches or coordinated commits


---

2. Core Git Concepts You Learned

Pull vs Merge vs Checkout

Command	Meaning

checkout	switch branch
pull	update from remote
merge	combine branches



---

Important Insight

git pull DOES NOT compare branches

It only does:

local branch vs its remote tracking branch


---

Why you saw:

Already up to date

Because:

feature/ticket_matching == origin/feature/ticket_matching

NOT because of your other branch.


---

3. Correct Way to Combine Work

git checkout feature/ticket_matching
git pull
git merge feature/ticket_match_v1
git push


---

4. Branch Management

Create branch from remote

git checkout -b feature/ticket_matching origin/feature/ticket_matching


---

Delete remote branch

git push origin --delete feature/ticket_match_v1


---

Restore deleted branch

git checkout -b branch-name origin/branch-name


---

5. Reset / Undo Commits

Remove last 2 commits

git reset --hard HEAD~2
git push --force


---

Safe alternative

git revert HEAD
git revert HEAD~1


---

Key Difference

Method	Effect

reset + force push	deletes history
revert	keeps history



---

6. GitHub Limitations

❌ Cannot do from UI:

delete specific commits

rewrite history


✅ Can do:

revert commits

delete branches



---

7. Local Repo Issues (.git)

Error:

not a git repository

Means:

.git folder missing OR wrong directory


---

Fix:

git clone <repo-url>
cd repo


---

Key Insight

.git exists ONLY locally
NOT on GitHub UI


---

8. .gitignore Understanding

Important Truth

.gitignore DOES NOT delete files

It only prevents tracking.


---

Common mistake found

requirements.txt in .gitignore ❌

Should usually NOT be ignored.


---

9. Restoring Deleted Files

Restore from remote

git fetch origin
git reset --hard origin/<branch>


---

10. Branch Visibility

Why only main showed

git branch

Shows only local branches.


---

Show remote branches

git branch -r


---

Show all

git branch -a


---

11. uv + FastAPI Issue

Error

Failed to spawn: uvicorn

Fix

uv add "uvicorn[standard]"


---

12. Databricks Key Learning

databricks auth login

Works for:

CLI

VS Code extension


Does NOT work for:

Python connector

backend apps



---

Important Rule

CLI auth ≠ Python auth


---

For Python you need:

PAT token OR

Azure identity (DefaultAzureCredential)



---

13. Databricks Connection Model

Local → API/Connector → Databricks

NOT:

Local → direct DB


---

14. Final Key Takeaways

Git

Pull ≠ merge

Branches are independent

Always merge intentionally

Avoid multiple branches for same feature



---

Team Workflow

Communicate + share branch strategy early


---

Debugging Mindset

Most issues were NOT code issues:

They were:
- environment
- authentication
- Git misunderstanding


---

🔥 Final One-Line Summary

You didn’t have a coding problem.
You had a workflow + Git mental model problem.


---

---
