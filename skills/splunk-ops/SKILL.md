---
name: splunk-ops
description: Platform Management, btool Precedence Debugging, splunkd.log Log Triage, Ingestion Queue Bottlenecks, Cluster Health & splunk diag.
---

# Splunk Platform Operations & Troubleshooting Skill (`splunk-ops`)

When administering, debugging, or troubleshooting a Splunk instance inside `o11yworks`, follow this operational playbook:

## 1. Configuration Debugging with `btool`
- **Find File Precedence**: Run `splunk btool <conf_name> list --debug` to find which `default/` or `local/` directory defines a setting.
- **Check Syntax Errors**: Run `splunk btool check` to catch typos or invalid stanzas.

## 2. Log Triage (`splunkd.log` & `_internal`)
- **Filter Components**: Look for key component errors:
  - `TcpOutputProc`: Forwarder connection drops.
  - `HttpInputDataHandler`: HEC token authorization / payload errors.
  - `BucketReplicator`: Indexer cluster bucket sync errors.
  - `DiskSpaceChecker`: Low disk space warnings.
  - `LicenseManager`: Pool overage warnings and license violation alerts.
- **Diagnostics SPL**: Query `index=_internal` and `index=_introspection` for memory spikes, open file handle limits, CPU load, and KVStore (`mongod.log`) synchronization.

## 3. Monitoring Console (MC) Health Checks & Alerts
- Monitor health status indicators in Splunk Monitoring Console (MC).
- Set up proactive alerts for license volume thresholds (80%/90% of quota) and indexing pipeline lag.

## 4. Ingestion Queue Bottlenecks
- **Queue Fill Ratio Inspection**: Monitor fill ratios on `parsingQ`, `aggregatorQ`, `typingQ`, and `indexQ`.
- **Regex Backtracking Fix**: A 100% full `typingQ` or `parsingQ` indicates inefficient regular expressions in `props.conf` or `transforms.conf`.
- **Metrics Log**: Query `index=_internal sourcetype=splunkd group=queue` to track queue depth over time.

## 5. Cluster Health & Operations
- **Indexer Cluster**: Inspect peer status (`Up`, `AddingBatch`, `Pending`), bucket fixup queues, and searchability factor compliance.
- **Search Head Cluster (SHC)**: Monitor captain election status, knowledge bundle replication timeouts, and KVStore (`mongod.log`) synchronization.

## 6. Diagnostic Bundles
- Run `splunk diag --disable=auth` to collect anonymized diagnostic packages for troubleshooting.
