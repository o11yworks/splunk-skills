# 🚀 o11yworks Splunk Master Skills Hub

A complete, enterprise-grade suite of **AI Agent Skills** for Splunk leadership, architecture, data engineering, application development, and platform operations. Built for AI coding assistants (Antigravity, Cursor, Claude Code, Vercel Skills).

---

## 📦 What's Included

| Skill Name | Role Focus | Description |
| :--- | :--- | :--- |
| **`splunk-lead`** | **Splunk Program Owner / Strategy Lead** | Multi-year roadmaps, Center of Excellence (CoE) charter, License FinOps cost optimization, Use Case Management (UCM), and Splunk Success Framework (SSF) maturity assessments. |
| **`splunk-build`** | **Enterprise Architect** | Topology design (Distributed, Indexer Clusters, SHC, SmartStore, Federated Search), hardware sizing calculations (vCPU/RAM/IOPS), OS kernel tuning, TLS encryption, and `splunk-appinspect` Cloud vetting. |
| **`splunk-data`** | **Data Engineer & Knowledge Manager** | HEC streaming, SC4S, OpenTelemetry Collector integration, Edge Processor SPL2 rules, line breaking (`LINE_BREAKER`), timestamping, data masking (`SEDCMD`), and CIM normalization. |
| **`splunk-dev`** | **Developer & Dashboard Engineer** | TA structuring (`Splunk_TA_*`), Python modular inputs, SPL query engine optimization (`tstats`), Protocol v2 Custom Search Commands, ES Risk Scoring, ITSI KPIs, Dashboard Studio JSON, and `@splunk/react-ui`. |
| **`splunk-ops`** | **Splunk Admin & SRE** | `btool` precedence debugging (`btool list --debug`, `btool check`), `splunkd.log` triage, pipeline queue bottleneck analysis (`parsingQ`, `typingQ`, `indexQ`), Monitoring Console alerts, and `splunk diag`. |

---

## ⚡ Quick Installation & Usage

### Method 1: Install via Skills CLI (Recommended)
Add all 5 skills to any project using the Vercel / Agent Skills CLI:

```bash
npx skills add o11yworks/splunk-skills
```

Or install a specific skill:

```bash
npx skills add o11yworks/splunk-skills/skills/splunk-dev
```

---

### Method 2: Manual Installation into Local Workspace

#### For Antigravity IDE:
Clone or copy the `skills/` directory into your project's `.agents/skills/` directory:

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

---

## 📖 Example Agent Prompts

Try asking your AI agent:

- **Strategic**: *"Create a 3-year Splunk roadmap and License FinOps optimization strategy using splunk-lead"*
- **Architecture**: *"Size an indexer cluster and RAM/vCPU specs for 1.5TB/day ingestion using splunk-build"*
- **Data Engineering**: *"Build props.conf line breaking and CIM Authentication mapping for Cisco firewall logs using splunk-data"*
- **Development**: *"Scaffold a Splunk Technology Add-on for AWS with a Python modular input using splunk-dev"*
- **Troubleshooting**: *"Diagnose a 100% full typing queue and check btool precedence for props.conf using splunk-ops"*

---

## 📄 License
MIT © [o11yworks](https://github.com/o11yworks)
