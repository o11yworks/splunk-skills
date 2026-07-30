---
name: splunk-dev
description: Technology Add-on (TA) Development, Modular Inputs, SPL Query Engine, ES Security Content, ITSI KPIs, Custom Search Commands & Dashboards.
---

# Splunk Development Skill (`splunk-dev`)

When building Technology Add-ons (TAs), writing optimized SPL, creating custom commands, or building dashboards inside `o11yworks`, follow these patterns:

## 1. Technology Add-on (TA) Structuring
Create TAs in `projects/Splunk_TA_<addon_name>` with clean separation:
```
projects/Splunk_TA_<addon_name>/
├── default/
│   ├── app.conf
│   ├── inputs.conf
│   ├── props.conf
│   ├── transforms.conf
│   ├── collections.conf
│   ├── macros.conf
│   └── eventtypes.conf
├── README/
│   └── inputs.conf.spec
└── bin/
    └── <modular_input>.py
```

## 2. Enterprise Security (ES) Content & ITSI KPIs
- **ES Correlation Searches**: Write threat detection searches mapping Risk Analysis framework actions (`risk_object`, `risk_score`).
- **ITSI Service & KPI Modeling**: Define IT Service Intelligence KPI search queries and threshold boundaries (Normal, Warning, Critical).

## 3. SPL Query Engine & Performance Rules
- **Scope Early**: Filter by `index=...` and `sourcetype=...` in the first pipe. Avoid leading wildcards (`*error`).
- **Use `tstats`**: Prefer `| tstats count WHERE index=... BY sourcetype` for high-speed indexing stats.
- **Differentiate Command Types**: Streaming (`eval`, `rex`, `where`) vs Transforming (`stats`, `chart`, `timechart`).
- **Lookups & KVStore**: Configure CSV lookups in `transforms.conf` or KVStore collections in `collections.conf`.
- **Search Macros**: Define reusable SPL logic stanzas in `default/macros.conf`.

## 4. Custom Extensions
- **Modular Inputs (`bin/*.py`)**: Implement Python inputs subclassing `splunklib.modularinput`. Define parameter schema in `README/inputs.conf.spec`.
- **Custom Search Commands**: Use `splunklib.searchcommands` (Protocol v2 Chunked Engine) for `GeneratingCommand`, `StreamingCommand`, or `ReportingCommand`.
- **Persistent REST Handlers**: Inherit from `splunk.persistconn.application.PersistentServerConnectionApplication` and register in `default/restmap.conf`.

## 5. Dashboards & Web UI
- **Dashboard Studio**: Build JSON schema dashboards with `$token$` input bindings.
- **React Web Apps**: Use `@splunk/react-ui` and `@splunk/react-page` to connect custom React components to Splunk Web proxy endpoints `/en-US/splunkd/__raw/services/...`.
