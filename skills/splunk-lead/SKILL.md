---
name: splunk-lead
description: Splunk Strategy, Leadership, Center of Excellence (CoE) Governance, License FinOps, Use Case Management (UCM) & Splunk Success Framework (SSF).
---

# Splunk Leadership, Strategy & Governance Skill (`splunk-lead`)

When advising on Splunk strategy, platform roadmaps, Center of Excellence (CoE) operating models, license cost optimization, or governance inside `o11yworks`, follow this framework:

## 1. Splunk Strategy & Architectural Roadmaps
- **Platform Strategy**: Map multi-year roadmaps for On-Premises to Splunk Cloud Platform migrations, Hybrid architectures, SmartStore adoption, and Splunk Observability Cloud integration.
- **Technology Selection**: Evaluate deployment models: Splunk Enterprise vs Splunk Cloud Platform vs Edge Processor vs Federated Search vs Amazon S3 Data Lakes.

## 2. Center of Excellence (CoE) & Operating Model
- **CoE Governance Charter**: Establish CoE organizational structure, team roles (Program Manager, Architect, Data Engineer, Content Developer, SRE), and responsibilities.
- **Tenant Onboarding & Service Catalog**: Define standardized intake workflows, SLA agreements, and request processes for onboarding new business units and log sources.

## 3. License Cost Optimization & Financial Engineering (FinOps)
- **Ingestion Filtering**: Drop low-value "noise" logs (debug logs, null queues, heartbeat events) at the Edge/Forwarder layer before indexing.
- **Storage Tiering**: Balance Hot/Warm NVMe SSD costs against SmartStore object storage (AWS S3 / Azure Blob) and cold archiving.
- **Federated Search**: Query raw un-indexed data in cloud object storage without incurring full ingestion license costs.

## 4. Use Case Management (UCM) & Business ROI
- **Use Case Intake**: Map every data source directly to a business outcome (SOC Threat Hunting use cases or SRE MTTR reduction).
- **Use Case Lifecycle**: Manage use cases through Idea → Security/Ops Review → Proof of Concept → Production → Value Assessment.

## 5. Splunk Success Framework (SSF) & Executive QBRs
- **SSF 4-Pillar Maturity Assessment**: Evaluate organizational maturity across **Program**, **People**, **Platform**, and **Data**.
- **Executive QBR Reporting**: Report metrics on license ROI, search performance, search head concurrency, and MTTR/MTTD improvements.

## 6. Enterprise Data Governance, Security & Compliance
- **Data Segregation & RBAC Policy**: Configure multi-tenant index isolation, role-based access control (RBAC), and data access policies.
- **Compliance & Auditing**: Ensure PII/PCI masking enforcement for GDPR, HIPAA, and SOC2 compliance. Purge orphaned search head bundles and unused dashboard views.
