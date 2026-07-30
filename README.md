# 🚀 o11yworks Splunk Master Skills Suite

[![Release Version](https://img.shields.io/badge/release-v1.0.0-blue.svg)](https://github.com/o11yworks/splunk-skills/releases/tag/v1.0.0)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Usage: 100% Free](https://img.shields.io/badge/Usage-100%25%20Free-green.svg)](https://github.com/o11yworks/splunk-skills)
[![Supported Agents](https://img.shields.io/badge/Supported%20Agents-Antigravity%20%7C%20Cursor%20%7C%20Claude%20%7C%20Vercel%20Skills-brightgreen)](https://github.com/o11yworks/splunk-skills)

A complete, enterprise-grade suite of **5 Master AI Agent Skills** providing expert instructions, architectural patterns, and code blueprints for Splunk strategy, platform architecture, data engineering, application development, and operational triage.

---

## ⚡ Core Capabilities Highlight

- 🔍 **SPL Search Engine Optimization**: Teaches AI coding agents to author high-performance SPL queries, enforce scope-first filtering (`index` and `sourcetype`), leverage `tstats` acceleration, structure streaming vs transforming command pipelines, write search macros, and configure CSV/KVStore lookups.
- 🔌 **Splunk REST API & Python SDK Integration**: Provides code patterns for programmatically interacting with `splunkd` REST API endpoints, building persistent Python REST handlers (`PersistentServerConnectionApplication`), HEC event streaming, and writing Protocol v2 Custom Search Commands (`splunklib.searchcommands`).
- ⚙️ **Automatic Manifest Indexing**: Includes a [`skills.json`](https://github.com/o11yworks/splunk-skills/blob/main/skills.json) manifest. When cloned or linked, AI coding agents automatically discover and index all 5 skills without manual configuration.

---

## 📦 What's Included

| Skill Name | Role Focus | Primary Capabilities |
| :--- | :--- | :--- |
| **`splunk-lead`** | **Splunk Program Owner / Strategy Lead** | Multi-year roadmaps, Center of Excellence (CoE) charter, License FinOps cost optimization, Use Case Management (UCM), and Splunk Success Framework (SSF) maturity assessments. |
| **`splunk-build`** | **Enterprise Architect** | Topology design (Distributed, Indexer Clusters, SHC, SmartStore, Federated Search), hardware sizing calculations (vCPU/RAM/IOPS), OS kernel tuning, TLS encryption, and `splunk-appinspect` Cloud vetting. |
| **`splunk-data`** | **Data Engineer & Knowledge Manager** | HEC streaming, SC4S, OpenTelemetry Collector integration, Edge Processor SPL2 rules, line breaking (`LINE_BREAKER`), timestamping, data masking (`SEDCMD`), and CIM normalization. |
| **`splunk-dev`** | **Developer & Dashboard Engineer** | TA structuring (`Splunk_TA_*`), Python modular inputs, SPL query engine optimization (`tstats`), Protocol v2 Custom Search Commands, ES Risk Scoring, ITSI KPIs, Dashboard Studio JSON, and `@splunk/react-ui`. |
| **`splunk-ops`** | **Splunk Admin & SRE** | `btool` precedence debugging (`btool list --debug`, `btool check`), `splunkd.log` triage, pipeline queue bottleneck analysis (`parsingQ`, `typingQ`, `indexQ`), Monitoring Console alerts, and `splunk diag`. |

---

## ⚡ Quick Installation & Usage

### Method 1: Install via Skills CLI (Recommended)
Add all 5 master skills to any project using the Vercel / Agent Skills CLI:

```bash
npx skills add o11yworks/splunk-skills
```

Or install a specific skill (e.g., `splunk-dev`):

```bash
npx skills add o11yworks/splunk-skills/skills/splunk-dev
```

---

### Method 2: Manual Installation into Local Workspace

#### For Antigravity IDE:
Copy or clone the `skills/` directory into your project's `.agents/skills/` directory:

```bash
git clone https://github.com/o11yworks/splunk-skills.git temp-skills
mkdir -p .agents/skills
cp -r temp-skills/skills/* .agents/skills/
rm -rf temp-skills
```

#### For Cursor IDE:
Copy to `.cursor/skills/`:

```bash
mkdir -p .cursor/skills
cp -r temp-skills/skills/* .cursor/skills/
```

#### For Claude Code / Vercel Skills:
Copy to `.claude/skills/`:

```bash
mkdir -p .claude/skills
cp -r temp-skills/skills/* .claude/skills/
```

---

## 📖 Real-World Agent Prompts

Try asking your AI agent after installing these skills:

- 🔍 **SPL Search Engine**: *"Write an optimized SPL query using tstats and scope-first filtering to find top error sourcetypes in the last 24 hours"*
- 🔌 **REST API Integration**: *"Write a Python persistent REST handler using splunk.persistconn.application to expose a custom endpoint"*
- 👑 **Strategic Leadership**: *"Create a 3-year Splunk roadmap and License FinOps optimization strategy using splunk-lead"*
- 🏗️ **Architecture & Sizing**: *"Size an indexer cluster and RAM/vCPU specs for 1.5TB/day ingestion using splunk-build"*
- 📥 **Data Pipelines & CIM**: *"Build props.conf line breaking and CIM Authentication mapping for Cisco firewall logs using splunk-data"*
- 💻 **App & TA Development**: *"Scaffold a Splunk Technology Add-on for AWS with a Python modular input using splunk-dev"*
- 🛠️ **Ops & Triage**: *"Diagnose a 100% full typing queue and check btool precedence for props.conf using splunk-ops"*

---

## 🆓 Free Usage & Disclaimer

> [!NOTE]
> **100% Free & Open Source**: This skill repository is provided completely **free of charge** under the MIT open-source license.
>
> **Discretionary Use**: These skills are provided "as-is" to assist AI coding agents. Individuals, teams, and organizations are free to use, modify, adapt, and integrate these skills into their projects at their own discretion and responsibility.

---

## 📄 License
MIT © [o11yworks](https://github.com/o11yworks)
