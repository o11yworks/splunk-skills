# 👑 `splunk-lead` — Leadership, Strategy & Governance Technical Guide

The **`splunk-lead`** skill provides AI agents with the executive, strategic, and governance blueprints needed to lead Splunk programs, manage platform lifecycles, run Center of Excellence (CoE) operations, and optimize licensing costs.

---

## 1. Domain Scope & Boundaries

### Included in Scope:
- **Splunk Platform Roadmaps**: Multi-year evolution from standalone on-prem to distributed Splunk Cloud Platform, SmartStore, and Splunk Observability Cloud.
- **Center of Excellence (CoE)**: Charter definition, team structure, intake process, SLAs, and tenant service catalogs.
- **License FinOps**: Ingestion volume optimization, filtering low-value noise, data tiering economics, and Federated Search cost reduction.
- **Use Case Management (UCM)**: ROI frameworks mapping log ingestion directly to security threat detection or MTTR reduction.
- **Splunk Success Framework (SSF)**: 4-pillar maturity evaluations (**Program**, **People**, **Platform**, **Data**) and executive QBRs.

### Out of Scope:
- Hands-on line breaking regex (handled by `splunk-data`).
- Hands-on SPL query syntax debugging (handled by `splunk-dev`).

---

## 2. Technical Specifications & Frameworks

### 🏛️ Center of Excellence (CoE) Operating Model
```
                       SPLUNK CENTER OF EXCELLENCE (CoE)
┌─────────────────────────────────────────────────────────────────────────────┐
│                       Program Owner / Leadership Lead                        │
│          • Stakeholder Management  • License FinOps  • QBR Reporting        │
└──────────────┬──────────────────────┬──────────────────────┬────────────────┘
               │                      │                      │
┌──────────────▼──────┐┌──────────────▼──────┐┌──────────────▼──────┐
│ Enterprise Architect││    Data Engineer    ││   Content Developer │
│  • Sizing & Topologies││  • Pipelines & CIM   ││   • SPL & Dashboards│
└─────────────────────┘└─────────────────────┘└─────────────────────┘
```

### 💰 License FinOps Optimization Matrix
| Layer | Strategy | Technical Mechanism | Impact |
| :--- | :--- | :--- | :--- |
| **Edge / Source** | Ingestion Filtering | Drop `DEBUG` / null queues at Edge Processor or HF | 15% – 35% Ingestion Reduction |
| **Storage Tiering** | SmartStore S3 | Offload warm/cold buckets to S3 object storage | 50% – 70% Storage Cost Reduction |
| **Federated Search** | Remote Lake Query | Query raw S3 data directly without full ingestion | 100% License Exemption |

---

## 3. Best Practices & Anti-Patterns

### ✅ Best Practices:
1. **Outcome-Driven Onboarding**: Require every new log onboarding request to map to a specific Use Case ID with measurable business ROI.
2. **Standardized Naming**: Enforce `<vendor>:<product>:<format>` sourcetype naming rules across all tenants.
3. **Regular Hygiene Audits**: Schedule monthly reviews to purge orphaned search head bundles, unused dashboards, and stale saved searches.

### ❌ Anti-Patterns to Avoid:
- **Unfiltered Debug Ingestion**: Ingesting high-frequency debug logs directly into primary production indexes.
- **Role Creep**: Granting tenant users `admin` capabilities instead of scoped role-based access control (`authorize.conf`).

---

## 4. Usage Workflows & Prompts

### Example Agent Prompts:
- *"Draft a Splunk Center of Excellence (CoE) charter and tenant onboarding SLA for a new business unit using splunk-lead"*
- *"Provide a License FinOps optimization strategy to reduce daily ingest volume by 25% using splunk-lead"*
