# 📥 `splunk-data` — Ingestion Pipelines & CIM Normalization Technical Guide

The **`splunk-data`** skill provides AI agents with technical standards for data onboarding, line breaking, timestamp extraction, data masking, OpenTelemetry integration, and Common Information Model (CIM) field normalization.

---

## 1. Domain Scope & Boundaries

### Included in Scope:
- **Ingestion Pipelines**: HEC REST API endpoints, SC4S syslog parsing, Deployment Server (`serverclass.conf`), Edge Processor / Ingest Processor SPL2 rules, and OTel Collector exporters.
- **Parsing Rules**: Line breaking (`LINE_BREAKER`), timestamp parsing (`TIME_PREFIX`, `TIME_FORMAT`), and payload truncation (`TRUNCATE`).
- **Data Anonymization**: PII/PCI masking using `SEDCMD` or `transforms.conf` regex replacements.
- **CIM Normalization**: Field Aliases (`FIELDALIAS`), Calculated Fields (`EVAL`), Event Types (`eventtypes.conf`), and Tags (`tags.conf`).

### Out of Scope:
- Dashboard Studio visual design (handled by `splunk-dev`).
- Indexer cluster bucket replication troubleshooting (handled by `splunk-ops`).

---

## 2. Ingestion Pipeline Architecture

```
                          SPLUNK INGESTION PIPELINE
┌──────────────┐    ┌─────────────────────┐    ┌─────────────────────┐    ┌──────────────┐
│ Data Source  │───►│ Parsing & Linebreak │───►│ Anonymization/Mask  │───►│ Index & CIM  │
│ (HEC/Syslog) │    │   (props.conf)      │    │  (transforms.conf)  │    │  Alignment   │
└──────────────┘    └─────────────────────┘    └─────────────────────┘    └──────────────┘
```

---

## 3. Production Configuration Patterns

### 1. Robust Line Breaking & Timestamping (`props.conf`)
```ini
[my_app:syslog]
SHOULD_LINEMATCH = false
LINE_BREAKER = ([\r\n]+)
TIME_PREFIX = ^
TIME_FORMAT = %Y-%m-%dT%H:%M:%S.%fZ
MAX_TIMESTAMP_LOOKAHEAD = 30
TRUNCATE = 10000
KV_MODE = json
```

### 2. PII / SSN Data Masking (`props.conf` & `transforms.conf`)
```ini
# props.conf
[my_app:syslog]
TRANSFORMS-mask_ssn = mask_ssn_regex

# transforms.conf
[mask_ssn_regex]
REGEX = (?<ssn>\d{3}-\d{2}-\d{4})
FORMAT = ssn:::XXX-XX-XXXX
DEST_KEY = _raw
```

### 3. CIM Authentication Data Model Mapping
```ini
# props.conf
[my_app:syslog]
FIELDALIAS-src_ip = src_addr AS src_ip
FIELDALIAS-dest_ip = dst_addr AS dest_ip
FIELDALIAS-user = account_name AS user
EVAL-action = if(status=="200" OR status=="OK", "success", "failure")

# eventtypes.conf
[my_app_auth_events]
search = sourcetype=my_app:syslog (action="success" OR action="failure")

# tags.conf
[eventtype=my_app_auth_events]
authentication = enabled
```

---

## 4. Best Practices & Validation

### ✅ Best Practices:
1. **Never use `KV_MODE = auto` for large high-throughput sourcetypes**: Explicitly use `KV_MODE = json` or regex extractions to reduce search head CPU strain.
2. **Explicit Line Breaking**: Always specify `LINE_BREAKER` to avoid fallback regex scanning that causes pipeline queue backup.

---

## 5. Usage Workflows & Prompts

### Example Agent Prompts:
- *"Write props.conf line breaking and CIM Authentication mapping for firewall logs using splunk-data"*
- *"Configure PII data masking for SSNs and credit cards in transforms.conf using splunk-data"*
