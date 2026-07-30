# 🏗️ `splunk-build` — Architecture, Capacity Sizing & Certification Technical Guide

The **`splunk-build`** skill provides AI agents with precise technical formulas, topology rules, system tuning parameters, and AppInspect validation procedures required to build enterprise Splunk architectures and package compliant applications.

---

## 1. Domain Scope & Boundaries

### Included in Scope:
- **Capacity Sizing Formulas**: Calculating required Indexer nodes, vCPU cores, RAM ratios, and IOPS per daily ingestion volume (GB/TB).
- **Topology Architecture**: Single-Instance, Distributed, Indexer Clusters (IDC), Search Head Clusters (SHC), SmartStore, and Federated Search.
- **System Tuning & Network**: Linux kernel tuning (`transparent_hugepage`), `ulimit` file descriptor limits, TLS 1.3 / SSL certs, SAML/LDAP authentication, and firewall port mappings.
- **App Certification**: Packaging with `app.manifest`, `ksconf` linting, and `splunk-appinspect` static analysis.

### Out of Scope:
- Modular input Python code (handled by `splunk-dev`).
- Day-2 queue fill ratio troubleshooting (handled by `splunk-ops`).

---

## 2. Technical Specifications & Formulas

### 📐 Capacity Sizing Formulas

$$ \text{Indexer Nodes Required} = \left\lceil \frac{\text{Daily Ingestion (GB/day)}}{300 \text{ GB/day/node}} \right\rceil $$

$$ \text{Minimum RAM} = \text{Max Concurrent Searches} \times 8\text{ GB} + 16\text{ GB System} $$

### 🌐 Firewall Port Matrix
| Port | Protocol | Component / Purpose |
| :--- | :--- | :--- |
| `8000` | TCP | Splunk Web UI |
| `8089` | TCP | Management REST API & Inter-node Communication |
| `9997` | TCP | Splunk Forwarding (S2S) |
| `8088` | TCP | HTTP Event Collector (HEC) |
| `8191` | TCP | KVStore Replication |
| `9887` | TCP | Indexer Cluster Bucket Replication |

---

## 3. Production Configuration Boilerplates

### OS Limits (`/etc/security/limits.conf`)
```ini
splunk          soft    nofile          64000
splunk          hard    nofile          64000
splunk          soft    nproc           16384
splunk          hard    nproc           16384
```

### TLS/SSL Server Configuration (`default/server.conf`)
```ini
[sslConfig]
enableSplunkdSSL = true
sslVersions = tls1.2, tls1.3
cipherSuite = ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384
```

---

## 4. Best Practices & AppInspect Vetting

### AppInspect Pre-Flight Checklist:
1. **Manifest Integrity**: Include `app.manifest` specifying app version, target Splunk compatibility, and author details.
2. **Path Sanitization**: Ensure Python scripts use `os.path.join` and avoid hardcoded `/tmp` paths.
3. **No Unauthenticated REST**: Ensure all custom EAI/REST handlers require authenticated Splunk sessions in `restmap.conf`.

---

## 5. Usage Workflows & Prompts

### Example Agent Prompts:
- *"Calculate hardware specs and node topology for a 1.2TB/day distributed indexer cluster using splunk-build"*
- *"Run AppInspect vetting rules and fix compliance issues for Splunk_TA_aws using splunk-build"*
