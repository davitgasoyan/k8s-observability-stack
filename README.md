# k8s-observability-stack
Self-hosted Kubernetes observability stack with Prometheus, Loki, Grafana, and cAdvisor deployed via raw manifests on kubeadm cluster.

This project demonstrates manual deployment and configuration of a full monitoring and logging pipeline without Helm charts.

## Components

- Prometheus – Metrics collection
- Loki – Log aggregation
- Grafana – Visualization and dashboards
- cAdvisor – Container metrics
- NFS-backed Persistent Volumes – Storage

## Architecture

- cAdvisor runs as a DaemonSet on all nodes
- Prometheus scrapes metrics from cluster components
- Loki stores logs using filesystem storage
- Grafana connects to Prometheus and Loki via provisioned datasources
- Persistent data is stored on NFS

## Repository Structure
``` bash
k8s-observability-stack/
├── cadvisor/
├── grafana/
├── loki/
└── prometheus/
```

Each component contains:
- Deployment / DaemonSet
- Service
- ConfigMap
- PersistentVolume / PersistentVolumeClaim (where required)

## Features

- TLS-enabled Grafana
- Secret-based credential management
- Resource limits and requests configured
- Persistent storage using NFS
- Manual configuration for deeper Kubernetes understanding

## Storage

Persistent volumes are backed by an NFS server:

- Grafana dashboards
- Prometheus TSDB
- Loki index and chunks

Reclaim policy is set to `Retain` to prevent data loss.

## Deployment

Apply manifests:

```bash
kubectl create namespace logging
kubectl apply -f logging/
