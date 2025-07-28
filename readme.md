# Homelab Kubernetes GitOps

<p align="center">
  <img src="https://raw.githubusercontent.com/cncf/artwork/master/projects/kubernetes/horizontal/color/kubernetes-horizontal-color.png" alt="Kubernetes" height="80"/>
  <img src="https://raw.githubusercontent.com/argoproj/argo-cd/master/docs/assets/argo.png" alt="ArgoCD" height="80"/>
</p>

This repository manages a homelab Kubernetes cluster using GitOps principles. It leverages [ArgoCD](https://argo-cd.readthedocs.io/), [Kustomize](https://kubectl.docs.kubernetes.io/references/kustomize/), and [Helm](https://helm.sh/) to automate infrastructure, networking, monitoring, and application deployments. The goal is to provide a reproducible, secure, and observable platform for running self-hosted services.

---

## Architecture Overview

```mermaid
graph TD
    A[Kubernetes Cluster] --> B[ArgoCD]
    B --> C[Infrastructure]
    B --> D[Monitoring]
    B --> E[Applications]
    C --> F[Networking]
    C --> G[Storage]
    C --> H[RBAC]
    D --> I[Prometheus]
    D --> J[Loki]
    D --> K[Grafana]
    E --> L[Vault]
    E --> M[n8n]
    E --> N[WordPress]
    E --> O[Portfolio]
```

## Repository Structure

- **infrastructure/**  
  Core cluster components, controllers, networking, namespaces, and ArgoCD bootstrapping.
- **monitoring/**  
  Monitoring stack, including Prometheus, Loki, Grafana, and related dashboards.
- **my-apps/**  
  User applications, dashboards, and custom workloads managed via GitOps.

---

## :computer: Hardware

### Nodes
I use a combination of Dell OptiPlex pc's and old desktops to run a few virtual machines. The mini PC's are great because they are small and cheap to buy when you get them refurbished from a reseller.

Dell OptiPlex 7050 PC i5-6500T/16GB/500GB SSD

Dell OptiPlex 5050 PC i5-6500T/16GB/500GB SSD

Dell OptiPlex 5050 PC i5-6500T/16GB/500GB SSD


## Key Applications

| Logo | Name | Description |
|------|------|-------------|
| <img src="https://avatars.githubusercontent.com/u/30269780?s=48&v=4" alt="ArgoCD" height="32"/> | [ArgoCD](https://github.com/argoproj/argo-cd) | Declarative GitOps continuous delivery for Kubernetes. |
| <img src="https://avatars.githubusercontent.com/u/36015203?s=48&v=4" alt="Kustomize" height="32"/> | [Kustomize](https://github.com/kubernetes-sigs/kustomize) | Native Kubernetes configuration customization. |
| <img src="https://avatars.githubusercontent.com/u/15859888?s=48&v=4" alt="Helm" height="32"/> | [Helm](https://github.com/helm/helm) | Package manager for Kubernetes applications. |
| <img src="https://avatars.githubusercontent.com/u/39950598?s=48&v=4" alt="Cert-Manager" height="32"/> | [Cert-Manager](https://github.com/cert-manager/cert-manager) | Automated TLS certificate management (integrated with Cloudflare DNS01). |
| <img src="https://avatars.githubusercontent.com/u/314135?v=4" alt="Cloudflare Zero Trust" height="32"/> | [Cloudflare Zero Trust](https://developers.cloudflare.com/cloudflare-one/) | Used for private tunnels to expose public services (without requiring a public IP). |
| <img src="https://avatars.githubusercontent.com/u/14280338?s=48&v=4" alt="Traefik" height="32"/> | [Traefik](https://github.com/traefik/traefik) | Kubernetes-native ingress controller. |
| <img src="https://avatars.githubusercontent.com/u/3380462?s=48&v=4" alt="Prometheus" height="32"/> | [Prometheus](https://github.com/prometheus/prometheus) | Metrics collection and alerting toolkit. |
| <img src="https://avatars.githubusercontent.com/u/7195757?s=48&v=4" alt="Grafana" height="32"/> | [Grafana](https://github.com/grafana/grafana) | Visualization and dashboarding for metrics/logs. |
| <img src="https://avatars.githubusercontent.com/u/761456?s=48&v=4" alt="Vault" height="32"/> | [Vault](https://www.vaultproject.io/) | Secrets management with Kubernetes auth integration. |
| <img src="https://avatars.githubusercontent.com/u/45487711?s=48&v=4" alt="n8n" height="32"/> | [n8n](https://n8n.io/) | Workflow automation platform with 300+ integrations. |
| <img src="https://avatars.githubusercontent.com/u/276006?s=48&v=4" alt="WordPress" height="32"/> | [WordPress](https://wordpress.org/) | Content management system with persistent storage. |
| <img src="https://avatars.githubusercontent.com/u/23529429?v=4" alt="Portfolio" height="32"/> | [Portfolio](https://portfolio.isandeshsol.com/) | Personal portfolio website developed with Hugo. |
| <img src="https://avatars.githubusercontent.com/u/23529429?v=4" alt="CloudNativePG" height="32"/> | [CloudNativePG](https://cloudnative-pg.io/) | Database operator for running PostgreSQL clusters in Kubernetes. |
## Security Notes

- All components are managed declaratively and versioned in git.
- TLS is automated via Cert-Manager and Cloudflare DNS01.
- Sensitive values (secrets, tokens) should be managed outside of git, using sealed-secrets or external secret managers if possible.
- RBAC and network policies are recommended for production-like setups.

---

## Observability

- **Prometheus** collects cluster and application metrics.
- **Loki** aggregates logs from all workloads.
- **Grafana** provides dashboards for metrics and logs, with pre-configured data sources and derived fields for trace correlation.
- Default dashboards and alerting rules are included for cluster health and workload monitoring.

---

## Contributing

Contributions are welcome! Please open issues or pull requests for improvements, bug fixes, or new features. For major changes, discuss them in an issue first.

---

## References

- [ArgoCD](https://argo-cd.readthedocs.io/)
- [Kustomize](https://kubectl.docs.kubernetes.io/references/kustomize/)
- [Helm](https://helm.sh/)
- [Cert-Manager](https://cert-manager.io/)
- [Cloudflared](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/)
- [Prometheus](https://prometheus.io/)
- [Loki](https://grafana.com/oss/loki/)
- [Grafana](https://grafana.com/)
- [Vault](https://www.vaultproject.io/)
- [n8n](https://n8n.io/)
- [WordPress](https://wordpress.org/)
- [Hugo](https://gohugo.io/)
---

## License

This project is licensed under the MIT License.