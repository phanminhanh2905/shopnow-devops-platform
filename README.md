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
│  Alert manager                Elasticsearch                                 │
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
