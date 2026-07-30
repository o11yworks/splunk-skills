# 💻 `splunk-dev` — Development, SPL Engine & UI Technical Guide

The **`splunk-dev`** skill provides AI agents with technical patterns for authoring Technology Add-ons (TAs), writing high-performance SPL queries, creating Protocol v2 Custom Search Commands, implementing Persistent REST API Handlers, and building Dashboard Studio / React web UIs.

---

## 1. Domain Scope & Boundaries

### Included in Scope:
- **Technology Add-on (TA) Architecture**: `Splunk_TA_*` directory structure, modular inputs (`bin/*.py`, `inputs.conf.spec`), persistent REST handlers (`restmap.conf`).
- **SPL Query Optimization**: Scope-first filtering, `tstats` high-speed acceleration, streaming vs transforming pipelines, search macros (`macros.conf`), KVStore (`collections.conf`).
- **Enterprise Content**: Enterprise Security (ES) Risk Analysis framework searches & ITSI Service/KPI modeling.
- **Custom Extensions**: Custom Search Commands via `splunklib.searchcommands` (Protocol v2 Chunked Engine).
- **Web UI & Visualization**: Dashboard Studio JSON schemas, classic Simple XML, and `@splunk/react-ui` React apps.

### Out of Scope:
- OS kernel limits (`/etc/security/limits.conf`) (handled by `splunk-build`).
- Queue fill ratio diagnosis (handled by `splunk-ops`).

---

## 2. SPL Query Engine & Performance Optimization

### ⚡ Optimization Rules of Thumb:
1. **Scope Early**: Filter by `index=` and `sourcetype=` in the first pipe.
2. **Prefer `tstats`**: Use `| tstats count WHERE index=... BY sourcetype` to read tsidx metadata directly without raw event loading.
3. **Avoid Leading Wildcards**: Avoid `*error` searches; use exact token matches (`status=500`).

```spl
│ Fast Index Search (Target: < 50ms)
└─► | tstats count WHERE index=netops sourcetype=cisco:asa BY src_ip, action

│ Scope-First Event Pipeline
└─► index=netops sourcetype=cisco:asa action=failure
    | stats count BY src_ip, user
    | sort - count
```

---

## 3. Production Code Boilerplates

### 1. Python Persistent REST API Handler (`bin/custom_api.py`)
```python
import json
import sys
from splunk.persistconn.application import PersistentServerConnectionApplication

class CustomApiHandler(PersistentServerConnectionApplication):
    def __init__(self, command_line, command_arg):
        super(CustomApiHandler, self).__init__()

    def handle(self, in_string):
        try:
            request = json.loads(in_string)
            method = request.get('method', 'GET')
            
            payload = {"status": "success", "message": "Endpoint reached cleanly"}
            return {'status': 200, 'payload': json.dumps(payload)}
        except Exception as e:
            return {'status': 500, 'payload': json.dumps({"error": str(e)})}
```

### 2. Endpoint Registration (`default/restmap.conf`)
```ini
[script:custom_api_endpoint]
match = /custom_api/v1
handler = custom_api.CustomApiHandler
python.version = python3
```

---

## 4. Best Practices & UI Integration

### React Web Apps (`@splunk/react-ui`):
- Connect React frontends to custom REST API endpoints using the Splunk Web proxy path:
  `/en-US/splunkd/__raw/servicesNS/nobody/<app_name>/custom_api/v1`

---

## 5. Usage Workflows & Prompts

### Example Agent Prompts:
- *"Write an optimized SPL query using tstats and scope-first filtering using splunk-dev"*
- *"Write a Python persistent REST handler inheriting from PersistentServerConnectionApplication using splunk-dev"*
- *"Scaffold a Splunk TA with a Python modular input and inputs.conf.spec using splunk-dev"*
