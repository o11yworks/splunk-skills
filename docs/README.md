# 📖 o11yworks Splunk Master Skills — Technical Documentation Index

Welcome to the technical documentation hub for the **o11yworks Splunk Master Skills Suite**. This documentation provides detailed technical specifications, scope boundaries, file stanzas, code patterns, and best practices for each skill in the suite.

---

## 🧭 Master Skill Navigation Index

| Skill Guide | Target Role | Primary Focus & Domain Scope |
| :--- | :--- | :--- |
| 👑 **[splunk-lead](file:///Users/vgeriti/Desktop/o11yworks/packages/o11yworks-splunk-skills/docs/skills/splunk-lead.md)** | **Splunk Program Lead** | Multi-year roadmaps, Center of Excellence (CoE) charter, License FinOps cost optimization, Use Case Management (UCM), and Splunk Success Framework (SSF) maturity. |
| 🏗️ **[splunk-build](file:///Users/vgeriti/Desktop/o11yworks/packages/o11yworks-splunk-skills/docs/skills/splunk-build.md)** | **Enterprise Architect** | Topology design (Distributed, Indexer Clusters, SHC, SmartStore, Federated Search), hardware sizing calculations (vCPU/RAM/IOPS), OS kernel tuning, and `splunk-appinspect` Cloud vetting. |
| 📥 **[splunk-data](file:///Users/vgeriti/Desktop/o11yworks/packages/o11yworks-splunk-skills/docs/skills/splunk-data.md)** | **Data Engineer** | HEC streaming, SC4S, OpenTelemetry Collector integration, Edge Processor SPL2 rules, line breaking (`LINE_BREAKER`), timestamping, data masking (`SEDCMD`), and CIM normalization. |
| 💻 **[splunk-dev](file:///Users/vgeriti/Desktop/o11yworks/packages/o11yworks-splunk-skills/docs/skills/splunk-dev.md)** | **Developer / UI Engineer** | TA structuring (`Splunk_TA_*`), Python modular inputs, SPL query engine optimization (`tstats`), Protocol v2 Custom Search Commands, ES Risk Scoring, ITSI KPIs, Dashboard Studio JSON, and `@splunk/react-ui`. |
| 🛠️ **[splunk-ops](file:///Users/vgeriti/Desktop/o11yworks/packages/o11yworks-splunk-skills/docs/skills/splunk-ops.md)** | **Splunk Admin / SRE** | `btool` precedence debugging (`btool list --debug`, `btool check`), `splunkd.log` triage, pipeline queue bottleneck analysis (`parsingQ`, `typingQ`, `indexQ`), Monitoring Console alerts, and `splunk diag`. |

---

## 🏛️ System Taxonomy & Skill Matrix

```
                      o11yworks SPLUNK AGENT SKILLS TAXONOMY
┌────────────────────────────────────────────────────────────────────────────┐
│                    👑 splunk-lead (Strategic Governance)                   │
│         • CoE Operating Model   • License FinOps   • SSF Framework         │
└─────┬──────────────────────┬──────────────────────┬────────────────────────┘
      │                      │                      │
┌─────▼──────────────┐┌──────▼─────────────┐┌───────▼────────────┐┌───────────▼───────────┐
│   splunk-build     ││    splunk-data     ││    splunk-dev      ││    splunk-ops        │
│ Architecture & HW  ││ Ingestion & Pipelines││ TA, SPL & Dashboards││ Ops, btool & Triage  │
└────────────────────┘└────────────────────┘└────────────────────┘└──────────────────────┘
```

---

## 🛡️ Security, Privacy & Compliance Guidelines

All skills in this suite are audited to comply with strict security and privacy standards:
- **Zero Secrets**: No hardcoded API keys, tokens, passwords, or private SSH keys are stored in any skill configuration.
- **Data Anonymization**: All log examples use generic IP addresses (`192.168.1.X`), sanitized hostnames, and anonymized user accounts.
- **Splunk Cloud Vetting**: All development stanzas conform to Splunk AppInspect rules (no raw `/tmp` file writes, mandatory TLS 1.3 / SSL validation, Python 3.9+ runtime compatibility).

---

## 📬 Contact & Maintainer Information

For questions, suggestions, or contributions regarding the `o11yworks-splunk-skills` framework:
- **Maintainer**: Venkatesh
- **Contact Email**: `venkatesh.o11y@gmail.com`
- **GitHub Organization**: [https://github.com/o11yworks](https://github.com/o11yworks)
