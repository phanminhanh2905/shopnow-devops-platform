## ShopNow DevOps Platform

A production-like DevOps platform built to simulate a real-world software delivery workflow using Kubernetes, GitLab CI/CD, Harbor, Prometheus, Grafana, ELK Stack, SonarQube and Telegram ChatOps.

This project was designed as a personal hands-on lab to practice deploying, operating and troubleshooting a cloud-native microservices platform from source code to production.

---

## 📌 Overview

The platform demonstrates the complete DevOps lifecycle, including:

- Kubernetes-based microservices deployment
- GitLab CI/CD automation
- Private container registry with Harbor
- Code quality analysis using SonarQube
- Centralized monitoring with Prometheus & Grafana
- Centralized logging using ELK Stack
- Telegram ChatOps for remote operations
- NGINX Ingress and Kong API Gateway

## Architecture Overview

```text
                                      Internet
                                          │
                                   Cloudflare DNS
                                  (*.pma-server.site)
                                          │
                                          ▼
                         Ingress NGINX (Static Public IP)
                                          │
                                          ▼
┌────────────────────────────────────────────────────────────────────────────┐
│                 Kubernetes Cluster (3 Control Plane + Worker Nodes)        │
│                                                                            │
│  ┌──────────────────────────────────────────────────────────────────────┐  │
│  │                     ShopNow Microservices Platform                   │  │
│  │                                                                      │  │
│  │  Frontend                                                            │  │
│  │      │                                                               │  │
│  │      ▼                                                               │  │
│  │  API Gateway                                                         │  │
│  │      │                                                               │  │
│  │  ┌───┴───────────────┐                                               │  │
│  │  │                   │                                               │  │
│  │ Discovery        Product Service                                     │  │
│  │ User Service     Cart Service                                        │  │
│  │                   │                                                  │  │
│  │              PostgreSQL                                              │  │
│  └──────────────────────────────────────────────────────────────────────┘  │
│                                                                            │
│  Monitoring Stack             Logging Stack             CI/CD              │
│  ────────────────             ─────────────             ─────              │
│  Prometheus                  Filebeat                 GitLab Runner        │
│  Grafana                     Logstash                                      │
│  Alertmanager                Elasticsearch                                 │
│                               Kibana                                       │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘


                    Git Push
                       │
                       ▼
                 GitLab VM
                       │
                 Trigger Pipeline
                       │
                       ▼
                GitLab Runner
                       │
                 SonarQube Scan
                       │
                 Build Docker Image
                       │
                       ▼
                 Harbor Registry
                       │
                 Pull Image
                       │
                       ▼
              Kubernetes Deployment


                  Telegram
                      │
                      ▼
            Telegram ChatOps Bot
              (Dev Server)
                      │
                 SSH Tunnel
                      │
                 kubectl
                      │
                      ▼
             Kubernetes Cluster
```
## Project Screenshots

# GitLab

| Dashboard | Pipeline |
|-----------|----------|
| ![](docs/screenshots/gitlab-dashboard.png) | ![](docs/screenshots/gitlab-pipeline.png) |

| Projects | Repository |
|----------|------------|
| ![](docs/screenshots/gitlab-projects.png) | ![](docs/screenshots/gitlab-repo-userservice.png) |

---

# Harbor

![](docs/screenshots/harbor-shopnow-project.png)

---

# Monitoring

| Grafana | Prometheus |
|---------|------------|
| ![](docs/screenshots/grafana-dashboard.png) | ![](docs/screenshots/prometheus-targets.png) |

Prometheus Alerts

![](docs/screenshots/prometheus-alerts.png)

---

# Logging

> Kibana dashboard screenshot

---

# Rancher

| Cluster | Workloads |
|---------|-----------|
| ![](docs/screenshots/rancher-cluster-overview.png) | ![](docs/screenshots/rancher-workloads.png) |

## Future Improvements

- Terraform provisioning
- ArgoCD GitOps deployment
- Horizontal Pod Autoscaler optimization
- Disaster Recovery documentation
- Multi-environment deployment
- Automated backup and restore
