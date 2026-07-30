---
name: splunk-data
description: Data Onboarding, Ingestion Pipelines, Edge/Ingest Processor, Line Breaking, Timestamping, HEC, SC4S, OTel Collector, Data Masking & CIM Normalization.
---

# Splunk Data Pipeline & Normalization Skill (`splunk-data`)

When onboarding, parsing, masking, or normalizing log data inside `o11yworks`, follow these standards:

## 1. Ingestion Pipelines & Processing
- **Edge Processor / Ingest Processor**: Transform, filter, and route telemetry at the edge using SPL2 rules before data leaves your network boundary.
- **Deployment Server**: Manage Universal Forwarder configurations centrally using `serverclass.conf`.
- **HTTP Event Collector (HEC)**: Ingest structured JSON logs to `/services/collector` using `Splunk <HEC_TOKEN>` header. Send metric payloads to dedicated metric indexes.
- **Syslog (SC4S)**: Use Splunk Connect for Syslog containerized parser for RFC 5424/3164 network logs.
- **OpenTelemetry Collector**: Configure `agent_config.yaml` using `splunk_hec` exporter for Splunk Enterprise or `signalfx` exporter for Splunk Observability Cloud.

## 2. Line Breaking & Timestamping (`default/props.conf`)
Always configure explicit line breaking and timestamp parsing:
```ini
[<sourcetype_name>]
SHOULD_LINEMATCH = false
LINE_BREAKER = ([\r\n]+)
TIME_PREFIX = ^
TIME_FORMAT = %Y-%m-%dT%H:%M:%S.%fZ
MAX_TIMESTAMP_LOOKAHEAD = 30
TRUNCATE = 10000
KV_MODE = json
```

## 3. Data Masking & Anonymization (`props.conf` / `transforms.conf`)
Mask sensitive PII/PCI fields (SSN, Credit Cards) before indexing:
```ini
# props.conf
[<sourcetype_name>]
TRANSFORMS-mask_ssn = mask_ssn_transform

# transforms.conf
[mask_ssn_transform]
REGEX = (?<ssn>\d{3}-\d{2}-\d{4})
FORMAT = ssn:::XXX-XX-XXXX
DEST_KEY = _raw
```

## 4. Common Information Model (CIM) Normalization
Normalize raw fields to Splunk CIM standards for Enterprise Security (ES) & ITSI:
- **Field Aliasing (`props.conf`)**: `FIELDALIAS-src_ip = src_addr AS src_ip`
- **Calculated Fields (`props.conf`)**: `EVAL-action = if(status=="200", "success", "failure")`
- **Event Types (`eventtypes.conf`)**: Category search stanzas (e.g. `[auth_events] search = sourcetype=my:auth`)
- **Tags (`tags.conf`)**: Attach CIM tags (`[eventtype=auth_events] authentication = enabled`).
