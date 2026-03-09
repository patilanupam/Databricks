# <img src="https://www.vectorlogo.zone/logos/databricks/databricks-icon.svg" width="40" align="center"/> &nbsp;Supply Chain × Databricks

**Daily Engineering Experiments — Building Real Systems, Breaking Things, Learning Everything**

![Status](https://img.shields.io/badge/Status-Active%20Experiment-FF3621?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Databricks-FF3621?style=for-the-badge&logo=databricks&logoColor=white)
![Domain](https://img.shields.io/badge/Domain-Supply%20Chain%20AI-1B3A4B?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-3.10+-FFD43B?style=for-the-badge&logo=python&logoColor=black)

---

> *Most Databricks tutorials show clean success paths.*
> *Real projects rarely work that way.*
> **This is the real version.**

---

## 👋 Welcome

This repository is a daily hands-on engineering log.

Every day we pick one piece of Databricks, try to build something real with it, and write down exactly what happened — including the parts that broke, the confusing error messages, and the fixes that actually worked.

The goal is simple: go from a blank Databricks workspace to a fully working **AI-powered Supply Chain Decision Engine**, one experiment at a time.

If you are new to Databricks, or you are trying to build something real and hitting walls — this is for you.

---

## 🧭 What We Are Building

```mermaid
mindmap
  root((Supply Chain\nDecision Engine))
    Data
      Orders & Inventory
      Logistics Feeds
      Delta Tables
    AI
      Foundation Models
      Document Extraction
      Anomaly Detection
    Platform
      Databricks SDK
      Model Serving
      Unity Catalog
      Jobs & Workflows
    Application
      Backend API
      Local Dev Setup
      Workflow Orchestration
```

---

## 🏗️ System Architecture

```mermaid
graph TD
    A[🖥️ Local Frontend] -->|HTTP Request| B[🐍 Python Backend API]
    B -->|Databricks SDK| C[🔐 Auth — databrickscfg]
    C --> D[☁️ Databricks Workspace]
    D --> E[🤖 Foundation Model\nServing Endpoint]
    D --> F[📦 Unity Catalog\nDelta Tables]
    D --> G[⚙️ Databricks Jobs\nOrchestration]
    E -->|LLM Response| B
    F -->|Supply Chain Data| B
    G -->|Workflow Triggers| B

    style A fill:#1B3A4B,color:#fff,stroke:#FF3621
    style B fill:#FF3621,color:#fff,stroke:#FF3621
    style C fill:#2D2D2D,color:#fff,stroke:#FF3621
    style D fill:#FF3621,color:#fff,stroke:#FF3621
    style E fill:#1B1B1B,color:#fff,stroke:#FF3621
    style F fill:#1B3A4B,color:#fff,stroke:#FF3621
    style G fill:#1B3A4B,color:#fff,stroke:#FF3621
```

---

## 🎯 What This Is About

We are not just writing code.

We are learning how real Databricks systems are **designed**, **broken**, and **fixed** — and documenting every step so that anyone can follow along or pick up where we left off.

| What We Do | Why It Matters |
|------------|---------------|
| 🔨 Build working prototypes daily | Learn by doing, not just reading |
| 💥 Record every error we hit | Real issues, not sanitised tutorials |
| 🔍 Document the debugging process | Build a practical troubleshooting guide |
| ✅ Write the working solution | Leave a clear path for others to follow |

---

## 🔬 Experiment Areas

```mermaid
flowchart LR
    subgraph PLATFORM["☁️ Databricks Platform"]
        P1[CLI Auth]
        P2[SDK Setup]
        P3[Model Serving]
        P4[Unity Catalog]
        P5[Jobs]
    end

    subgraph DATA["📊 Data Engineering"]
        D1[Ingestion]
        D2[Delta Tables]
        D3[Transformation]
        D4[Batch Processing]
    end

    subgraph AI["🤖 AI & LLM"]
        A1[Foundation Models]
        A2[Document Extraction]
        A3[Anomaly Detection]
        A4[Workflow Automation]
    end

    subgraph APP["🐍 Application Layer"]
        AP1[Backend API]
        AP2[Local Dev]
        AP3[Orchestration]
    end

    PLATFORM --> DATA
    DATA --> AI
    AI --> APP

    style PLATFORM fill:#FF3621,color:#fff,stroke:none
    style DATA fill:#1B3A4B,color:#fff,stroke:none
    style AI fill:#2D2D2D,color:#fff,stroke:none
    style APP fill:#1B1B1B,color:#fff,stroke:none
```

---

## 📅 Daily Experiment Format

Every day follows the same simple structure:

```mermaid
flowchart LR
    A([🎯 Pick a\nCapability]) --> B([🔨 Build a\nPrototype])
    B --> C([💥 Hit\nErrors])
    C --> D([🔍 Debug\n& Investigate])
    D --> E([✅ Document\nthe Fix])
    E --> F([📝 Log\nthe Day])
    F --> A

    style A fill:#FF3621,color:#fff,stroke:none
    style B fill:#1B3A4B,color:#fff,stroke:none
    style C fill:#2D2D2D,color:#fff,stroke:none
    style D fill:#1B3A4B,color:#fff,stroke:none
    style E fill:#FF3621,color:#fff,stroke:none
    style F fill:#1B1B1B,color:#fff,stroke:none
```

---

## 🗓️ Experiment Log

<details>
<summary><b>📅 Day 1 — Local Setup & First Databricks Connection</b></summary>

<br>

**Goal:** Get the project running locally and make a successful call to a Databricks Foundation Model endpoint.

---

**What we built:**
- Project scaffold with `uv` as the environment manager
- Databricks CLI authentication
- First successful LLM call via the OpenAI-compatible serving endpoint

---

**Errors we hit:**

| Error | What Caused It | How We Fixed It |
|-------|---------------|-----------------|
| `uv not recognized` | Binary not added to PATH after install | Added `~/.local/bin` to system PATH |
| `databricks not recognized` | Python Scripts folder not in PATH | Found Scripts path via `sysconfig` and added to PATH |
| `cannot configure credentials` | Entered full workspace URL with `/browse` path | Used base URL only — no paths, no query strings |
| `ENDPOINT_NOT_FOUND` | Used model identifier instead of endpoint name | Ran `serving-endpoints list` to get correct name |
| `404 Not Found` on API call | Wrong endpoint name flowing into request path | Fixed `.env` value to use serving endpoint name |

---

**Key lesson from Day 1:**

> The serving endpoint name and the model identifier are not the same thing.
> `databricks-claude-sonnet-4-5` ✅
> `system.ai.databricks-claude-sonnet-4-5` ❌
>
> Always verify with `databricks serving-endpoints list` before configuring anything.

</details>

<br>

> 📌 New days are added here as experiments continue.

---

## 🚀 Getting Started From Scratch

If you want to follow along or reproduce any experiment, here is the full setup path.

```mermaid
flowchart TD
    S1["1️⃣ Python 3.10+\npython --version"] --> S2
    S2["2️⃣ Install uv\nPython env manager"] --> S3
    S3["3️⃣ Install Databricks CLI\npip install databricks-cli"] --> S4
    S4["4️⃣ Authenticate\ndatabricks auth login"] --> S5
    S5["5️⃣ Find Serving Endpoint\ndatabricks serving-endpoints list"] --> S6
    S6["6️⃣ Configure .env\nEndpoint name + data paths"] --> S7
    S7["7️⃣ Install Dependencies\nuv sync --all-extras"] --> S8
    S8["8️⃣ Run the App ✅\nuv run python -m core.main"]

    style S1 fill:#1B3A4B,color:#fff,stroke:none
    style S2 fill:#1B3A4B,color:#fff,stroke:none
    style S3 fill:#1B3A4B,color:#fff,stroke:none
    style S4 fill:#FF3621,color:#fff,stroke:none
    style S5 fill:#FF3621,color:#fff,stroke:none
    style S6 fill:#1B3A4B,color:#fff,stroke:none
    style S7 fill:#1B3A4B,color:#fff,stroke:none
    style S8 fill:#2D6A2D,color:#fff,stroke:none
```

### Quick Commands

```bash
# 1. Authenticate with Databricks
databricks auth login
# Enter ONLY: https://your-workspace.azuredatabricks.net

# 2. Verify auth worked
databricks current-user me

# 3. Find your serving endpoint name
databricks serving-endpoints list

# 4. Install and run
uv sync --all-extras
uv run python -m core.main --file
```

---

## 🗂️ Repository Structure

```
supply-chain-databricks/
│
├── 📁 core/                  → Application logic & LLM client
├── 📁 workflow/              → LLM workflows & orchestration
├── 📁 data/
│   ├── input/                → Raw supply chain data
│   ├── output/               → Processed results
│   └── orders/               → Order datasets
├── 📁 docs/                  → Daily experiment logs
├── .env                      → Environment config
└── README.md
```

---

## 🐛 When Things Break

```mermaid
flowchart TD
    START(["❌ Something broke"]) --> Q1{"Does\ndatabricks current-user me\nwork?"}

    Q1 -->|No| F1["Run databricks auth login\nUse base URL only"]
    Q1 -->|Yes| Q2{"Is your endpoint\nvisible in\nserving-endpoints list?"}

    Q2 -->|No| F2["Contact your\nworkspace admin"]
    Q2 -->|Yes| Q3{"Does .env have\nthe endpoint name\nnot the model ID?"}

    Q3 -->|No| F3["Fix .env\nRemove system.ai prefix"]
    Q3 -->|Yes| F4["Check backend logs\nLook at the POST path\nbeing called"]

    F1 --> OK(["✅ Try again"])
    F2 --> OK
    F3 --> OK
    F4 --> OK

    style START fill:#FF3621,color:#fff,stroke:none
    style OK fill:#2D6A2D,color:#fff,stroke:none
    style F1 fill:#1B3A4B,color:#fff,stroke:none
    style F2 fill:#1B3A4B,color:#fff,stroke:none
    style F3 fill:#1B3A4B,color:#fff,stroke:none
    style F4 fill:#1B3A4B,color:#fff,stroke:none
    style Q1 fill:#2D2D2D,color:#fff,stroke:none
    style Q2 fill:#2D2D2D,color:#fff,stroke:none
    style Q3 fill:#2D2D2D,color:#fff,stroke:none
```

---

## 📚 Useful References

| Resource | Link |
|----------|------|
| 📖 Databricks Auth Docs | [docs.databricks.com/en/dev-tools/auth](https://docs.databricks.com/en/dev-tools/auth.html) |
| 🤖 Foundation Model Serving | [Azure Databricks ML Docs](https://learn.microsoft.com/en-us/azure/databricks/machine-learning/foundation-models) |
| 🧠 Supported Models | [Claude Sonnet & Others](https://learn.microsoft.com/en-us/azure/databricks/machine-learning/foundation-models/supported-models) |
| ⚡ uv Package Manager | [docs.astral.sh/uv](https://docs.astral.sh/uv) |
| 🔧 Databricks SDK for Python | [databricks-sdk-py.readthedocs.io](https://databricks-sdk-py.readthedocs.io) |

---

## 🔭 Long-Term Vision

By the end of these experiments we aim to have:

- ✅ A working AI-powered supply chain decision system on Databricks
- ✅ A documented architecture that others can follow and adapt
- ✅ A real-world debugging guide built from actual failures
- ✅ A practical playbook for onboarding engineers to Databricks fast

---

<div align="center">

<img src="https://www.vectorlogo.zone/logos/databricks/databricks-icon.svg" width="24"/>
&nbsp;
**Built daily. Broken often. Fixed always.**
&nbsp;
<img src="https://www.vectorlogo.zone/logos/databricks/databricks-icon.svg" width="24"/>

![Updated](https://img.shields.io/badge/Updated-Daily-FF3621?style=flat-square)
![Experiments](https://img.shields.io/badge/Experiments-In%20Progress-1B3A4B?style=flat-square)
![Contributions](https://img.shields.io/badge/Contributions-Welcome-2D6A2D?style=flat-square)

</div>
