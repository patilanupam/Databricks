Alright, here’s a clean, structured **Markdown (.md) document** capturing everything we debugged today—no fluff, just what matters.

---

````md
# Debug Log – Databricks + Prompt Flow + Postgres Setup

## Context

Goal:
Build and debug a system integrating:
- Prompt Flow (VS Code)
- Databricks (Genie / SQL Warehouse)
- Postgres (Docker)
- FastAPI backend

---

# 1. Git + Repo Issue (ZIP vs Repo)

## Problem
User had:
- Code downloaded via ZIP
- Local modifications
- Needed to pull latest changes

## Root Cause
ZIP download does NOT contain git history → cannot use `git pull`

## Solution (Best Practice)

```bash
# Backup changes
cp -r project project_backup

# Clone repo properly
git clone git@github.com:org/repo.git
cd repo

# Copy changes back
# Then commit
git add .
git commit -m "Applied local changes"

# Pull latest
git pull origin main
````

---

# 2. Branch Naming Best Practices

## Standard Format

```
<type>/<short-description>
```

## Examples

```
feature/pdf-claim-parser
feature/c4c-ticket-matching
bugfix/null-pointer
```

## Rules

* lowercase only
* use hyphens
* avoid names
* prefer ticket IDs if available

---

# 3. FastAPI + uvicorn Error

## Error

```
Failed to spawn: `uvicorn`
program not found
```

## Root Cause

`uvicorn` not installed in `uv` environment

## Fix

```bash
uv add "uvicorn[standard]"
uv run uvicorn backend.main:app --reload
```

---

# 4. Postgres Setup (Docker)

## docker-compose.yml

```yaml
version: "3.9"

services:
  db:
    image: postgres:17
    container_name: postgres-db
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: mydb
    ports:
      - "5432:5432"
```

## Run

```bash
docker compose up -d db
```

## Connect

```
Host: localhost
Port: 5432
User: postgres
Password: postgres
DB: mydb
```

---

# 5. Databricks Auth (Critical Insight)

## Current Setup

```
az login
databricks auth login
```

## Problem

Python connector:

```
from databricks import sql
```

DOES NOT use CLI login sessions.

---

# 6. Databricks Error

## Error

```
databricks.sql.exc.RequestError: Error during request to server
```

## Meaning

This is NOT SQL failure.

It is:

* auth failure
* connection failure
* config issue

---

# 7. Required Variables

## DATABRICKS_HTTP_PATH

Location:
Databricks → SQL Warehouses → Connection Details

Example:

```
/sql/1.0/warehouses/abcd1234
```

---

## DATABRICKS_SP_TABLE_PATH

Not standard → project-specific

Examples:

```
main.schema.table
```

or

```
dbfs:/mnt/data/table
```

---

## KEY_VAULT_URL

Location:
Azure → Key Vault → Overview

Example:

```
https://your-vault.vault.azure.net/
```

---

# 8. Authentication Fix Options

## Option 1 — PAT Token (Recommended)

### Get Token

Databricks → User Settings → Access Tokens

### Use

```python
conn = sql.connect(
    server_hostname="adb-xxxx.azuredatabricks.net",
    http_path="/sql/1.0/warehouses/xxxx",
    access_token="dapi-xxxx"
)
```

---

## Option 2 — AAD (Proper way)

```python
from azure.identity import DefaultAzureCredential
from databricks import sql

credential = DefaultAzureCredential()

token = credential.get_token("https://databricks.azure.net/.default")

conn = sql.connect(
    server_hostname="adb-xxxx.azuredatabricks.net",
    http_path="/sql/1.0/warehouses/xxxx",
    access_token=token.token
)
```

---

# 9. Prompt Flow Custom Connection

## YAML

```yaml
$schema: https://azuremlschemas.azureedge.net/promptflow/latest/CustomConnection.schema.json
name: databricks_genie_connection
type: custom

configs:
  base_url: "https://adb-xxxx.azuredatabricks.net/serving-endpoints/genie"
  endpoint: "/invocations"

secrets:
  databricks_token: "<user-input>"
```

---

## Usage in Python Node

```python
import requests

url = f"{connection.configs['base_url']}{connection.configs['endpoint']}"

headers = {
    "Authorization": f"Bearer {connection.secrets['databricks_token']}",
    "Content-Type": "application/json"
}

response = requests.post(url, headers=headers, json={"inputs": input_data})

return response.json()
```

---

# 10. Root Cause Summary

## Main Issue

```
CLI auth != Python auth
```

## Why failure happened

* Python connector had no credentials
* `az login` not used automatically
* `databricks auth login` not used automatically

---

# 11. Debug Checklist

✔ SQL Warehouse running
✔ Correct HTTP path
✔ No `https://` in hostname
✔ Token exists
✔ Token passed correctly
✔ Standalone Python test works

---

# 12. Recommended Architecture

```
Prompt Flow
    ↓
FastAPI Wrapper
    ↓
Databricks (Genie / SQL)
    ↓
Postgres (Docker)
```

---

# 13. Key Takeaways

* ZIP ≠ Git repo
* Copilot needs structure, not magic prompts
* CLI auth is not reusable in code
* Databricks errors are usually config/auth issues
* Always isolate system components when debugging

---

# Final Insight

You were not stuck on logic.

You were stuck on:

```
Authentication + Environment + Integration boundaries
```

Once those are correct → everything works.

```

---

If you want, next step I’d recommend:

→ I can convert this into a **proper project README + architecture diagram + interview explanation**, which is way more valuable than just debugging notes.
```
