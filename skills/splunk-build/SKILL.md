---
name: splunk-build
description: Splunk Architecture, Topology Design, Hardware/OS Sizing, Capacity Planning, SmartStore, Federated Search, AppInspect Packaging & Cloud Certification.
---

# Splunk Architecture & Build Skill (`splunk-build`)

When designing, sizing, architecting, or packaging Splunk environments and applications inside `o11yworks`, follow these principles:

## 1. Capacity Planning & Sizing Rules
- **Daily Ingestion**: Calculate required Indexer nodes assuming ~300GB/day raw ingestion per Indexer node.
- **CPU & RAM Ratios**: Minimum 12–24 vCPUs per Indexer. Allocate at least 32GB–64GB RAM per node (8GB RAM per active concurrent search process).
- **Storage IOPS**: Require 1000+ IOPS for Hot/Warm data volumes (NVMe/SSD). Cold volumes may use lower-tier storage or object store.

## 2. Architecture Topologies & Component Roles
- **Standalone**: Single instance for Dev/Test.
- **Distributed**: Dedicated Search Head, Indexers, Heavy Forwarders, Deployment Server, License Manager.
- **Indexer Cluster (IDC)**: Multi-site or single-site cluster with Replication Factor (RF=2 or 3) and Search Factor (SF=2).
- **Search Head Cluster (SHC)**: Minimum 3 Search Heads with Captain election, Deployer node, and KVStore synchronization.
- **SmartStore**: Offload warm/cold buckets to remote object storage (AWS S3, Azure Blob, Google Cloud Storage) with local disk cache manager.
- **Federated Search**: Configure Federated Search heads to query remote Splunk deployments or S3 data lakes transparently.

## 3. OS Tuning, Security & Network Specs
- **Linux Kernel Tuning**: `echo never > /sys/kernel/mm/transparent_hugepage/enabled`.
- **Limits**: Set file descriptors in `/etc/security/limits.conf`: `splunk soft nofile 64000`, `splunk hard nofile 64000`.
- **Authentication & RBAC**: SAML 2.0 / LDAP authentication stanzas in `authentication.conf`, custom capabilities in `authorize.conf`.
- **TLS/SSL Encryption**: Configure TLS 1.3 / SSL certificates in `server.conf` and `web.conf`.
- **Required Ports**: `8000` (Web), `8089` (Management REST), `9997` (Forwarding), `8088` (HEC), `8191` (KVStore), `9887` (Clustering).

## 4. AppInspect Packaging & Cloud Certification
- Package metadata in `app.manifest`.
- Validate configurations with `ksconf check` and `splunk-appinspect inspect <app_folder> --mode appinspect`.
- Enforce Python 3.9+ compatibility, no hardcoded `/tmp` paths, and proper SSL validation for Splunk Cloud Platform compliance.
