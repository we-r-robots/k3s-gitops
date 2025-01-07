# Home K3s Cluster

This repository contains the GitOps configuration for my home Kubernetes (k3s) cluster.

## Cluster Specifications

### Control Plane
- Hostname: ehl-da-kctrl
- IP: 10.0.1.40
- Resources: 4 cores, 8GB RAM, 250GB NVMe
- OS: Ubuntu 24.04 LTS
- Full disk encryption enabled

### Worker Nodes
- 2x Worker nodes (ehl-da-kwrk1, ehl-da-kwrk2)
- Each node:
  - 4 vCPU
  - 4GB RAM
  - 63.5GB OS disk
  - 200GB storage disk mounted at `/var/lib/rancher/k3s/storage`
  - Ubuntu 24.04 LTS cloud image

### Network Configuration
- IP Range: 10.0.1.40-49
- Pod CIDR: 10.42.0.0/16
- Service CIDR: 10.43.0.0/16

## Repository Structure

```
├── clusters/
│   └── home/                 # K3s cluster
│       ├── flux-system/      # Flux components
│       ├── infrastructure/   # Core infrastructure
│       │   ├── external-secrets/  
│       │   ├── monitoring/        
│       │   └── ingress/          
│       └── apps/            # Application deployments
├── infrastructure/
│   ├── sources/            # Helm repositories
│   └── configs/            # Shared configurations
```

## Components

### Core
- k3s v1.31.4+k3s1
- Flannel CNI
- Local-path storage class (default)
- CoreDNS
- Metrics Server
- Traefik Ingress

### Infrastructure
- External Secrets Operator (AWS Secrets Manager integration) (Planned)
- Monitoring stack (planned)
- Ingress configuration (planned)

## Maintenance Notes

- Node Labels:
  ```bash
  storage-type=nfs
  workload-type=general-purpose
  topology.kubernetes.io/zone=home
  ```
- Namespaces:
  - external-secrets
  - monitoring
  - ingress

## TODO
- [ ] Configure monitoring stack
- [ ] Set up External Secrets Operator
- [ ] Configure ingress for applications
- [ ] Add application deployments

---
This document is a work in progress and will be updated as the cluster evolves.