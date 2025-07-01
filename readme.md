# Homelab Kubernetes GitOps

<p align="center">
  <img src="https://raw.githubusercontent.com/cncf/artwork/master/projects/kubernetes/horizontal/color/kubernetes-horizontal-color.png" alt="Kubernetes" height="80"/>
  <img src="https://raw.githubusercontent.com/argoproj/argo-cd/master/docs/assets/argo.png" alt="ArgoCD" height="80"/>
  <img src="https://raw.githubusercontent.com/grafana/grafana/main/public/img/grafana_icon.svg" alt="Grafana" height="80"/>
</p>

This repository manages a homelab Kubernetes cluster using GitOps principles. It leverages [ArgoCD](https://argo-cd.readthedocs.io/), [Kustomize](https://kubectl.docs.kubernetes.io/references/kustomize/), and [Helm](https://helm.sh/) to automate infrastructure, networking, monitoring, and application deployments. The goal is to provide a reproducible, secure, and observable platform for running self-hosted services.

---

## Repository Structure

- **infrastructure/**  
  Core cluster components, controllers, networking, namespaces, and ArgoCD bootstrapping.
- **monitoring/**  
  Monitoring stack, including Prometheus, Loki, Grafana, and related dashboards.
- **my-apps/**  
  User applications, dashboards, and custom workloads managed via GitOps.

---

## Key Applications

| Name | Description |
|------|-------------|
| [ArgoCD](https://github.com/argoproj/argo-cd) | Declarative GitOps continuous delivery for Kubernetes. |
| [Kustomize](https://github.com/kubernetes-sigs/kustomize) | Native Kubernetes configuration customization. |
| [Helm](https://github.com/helm/helm) | Package manager for Kubernetes applications. |
| [Cert-Manager](https://github.com/cert-manager/cert-manager) | Automated TLS certificate management (integrated with Cloudflare DNS01). |
| [Cloudflared](https://github.com/cloudflare/cloudflared) | Secure ingress via Cloudflare Tunnel. |
| [Traefik](https://github.com/traefik/traefik) | Kubernetes-native ingress controller. |
| [Prometheus](https://github.com/prometheus/prometheus) | Metrics collection and alerting toolkit. |
| [Loki](https://github.com/grafana/loki) | Log aggregation system. |
| [Grafana](https://github.com/grafana/grafana) | Visualization and dashboarding for metrics/logs. |
| [ApplicationSet](https://argo-cd.readthedocs.io/en/stable/operator-manual/applicationset/) | Automated multi-app deployments for ArgoCD. |

---

## Getting Started

### Prerequisites

- A running Kubernetes cluster (bare metal, k3s, or kubeadm recommended for homelab).
- `kubectl` configured for your cluster.
- [Helm](https://helm.sh/) installed.
- Cloudflare account and API token for DNS and tunnel integration.

### Bootstrap Process

1. **Install CRDs and ArgoCD**
   ```sh
   kubectl apply -k infrastructure/controllers/argocd/
   ```

2. **Configure Secrets**
   - Add Cloudflare credentials for Cloudflared and Cert-Manager DNS01 challenge.
   - Store secrets as Kubernetes `Secret` resources (do not commit secrets to git).

3. **Apply Infrastructure**
   ```sh
   kubectl apply -k infrastructure/
   ```

4. **Apply Monitoring Stack**
   ```sh
   kubectl apply -k monitoring/
   ```

5. **Deploy Applications**
   ```sh
   kubectl apply -k my-apps/
   ```

---

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

---

## License

This project is licensed under the MIT License.