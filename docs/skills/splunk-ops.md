# 🛠️ `splunk-ops` — Platform Operations & Troubleshooting Technical Guide

The **`splunk-ops`** skill provides AI agents with an operational playbook for resolving configuration precedence conflicts (`btool`), triaging `splunkd.log` errors, fixing pipeline queue bottlenecks, checking cluster health, and collecting diagnostic snapshots (`splunk diag`).

---

## 1. Domain Scope & Boundaries

### Included in Scope:
- **Configuration Precedence Debugging**: `splunk btool <conf> list --debug` and `splunk btool check`.
- **`splunkd.log` Log Triage**: Component-level log filtering (`TcpOutputProc`, `HttpInputDataHandler`, `BucketReplicator`, `DiskSpaceChecker`, `LicenseManager`).
- **Ingestion Queue Bottlenecks**: Fill ratio diagnostics on `parsingQ`, `aggregatorQ`, `typingQ`, `indexQ`, regex backtracking fixes, and `metrics.log` parsing.
- **Cluster Operations**: Indexer cluster peer state troubleshooting, fixup queues, searchability/replication factor compliance, SHC captain election, and KVStore (`mongod.log`) synchronization.
- **Diagnostics**: Sanitized `splunk diag` and `RapidDiag` collection.

### Out of Scope:
- Multi-year cloud migration strategy (handled by `splunk-lead`).
- Sizing vCPUs and RAM for new clusters (handled by `splunk-build`).

---

## 2. Configuration Precedence & Debugging (`btool`)

### 🔍 Precedence Order (Lowest to Highest Priority)
```
1. system/default
2. apps/<app_name>/default
3. apps/<app_name>/local
4. system/local
```

### Essential `btool` Commands:
```bash
# Trace origin file of every active configuration setting
splunk btool props list --debug

# Trace inputs setting for a specific sourcetype
splunk btool inputs list --debug | grep -A 10 "[monitor:///var/log]"

# Check for syntax errors across all configuration files
splunk btool check
```

---

## 3. Queue & Pipeline Bottleneck Triage

### Ingestion Pipeline Queues:
```
  [Input] ──► parsingQ ──► aggregatorQ ──► typingQ ──► indexQ ──► [Disk]
```

### Triage Matrix for 100% Full Queues:
| Blocked Queue | Root Cause | Remediation Action |
| :--- | :--- | :--- |
| **`typingQ`** | Catastrophic regex backtracking in `props.conf` or `transforms.conf` | Simplify regex, optimize `LINE_BREAKER` or `KV_MODE`. |
| **`indexQ`** | Slow disk IOPS or indexer network saturation | Upgrade storage IOPS (NVMe), check `metrics.log` throughput. |
| **`parsingQ`** | Unusually large un-truncated event lines | Lower `TRUNCATE` limit in `props.conf` (e.g. `TRUNCATE = 10000`). |

---

## 4. Diagnostics & Health Check Queries

### Query `metrics.log` for Pipeline Throughput:
```spl
index=_internal sourcetype=splunkd group=queue name=indexqueue
| timechart avg(fill_ratio) BY name
```

### Check License Quota Consumption:
```spl
index=_internal sourcetype=splunkd_license type=Usage
| stats sum(b) AS bytes BY h, s
| eval size_gb = round(bytes/1024/1024/1024, 2)
| sort - size_gb
```

---

## 5. Usage Workflows & Prompts

### Example Agent Prompts:
- *"Trace the configuration file origin for props.conf using btool list --debug using splunk-ops"*
- *"Diagnose a 100% full typing queue and check metrics.log for backpressure using splunk-ops"*
- *"Triage indexer cluster peer state and bucket fixup queue errors using splunk-ops"*
