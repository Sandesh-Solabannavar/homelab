# Homelab Kubernetes GitOps

This repository manages a homelab Kubernetes cluster using GitOps principles with ArgoCD, Kustomize, and Helm. It provides infrastructure, networking, monitoring, and application deployment automation.

## Structure

- **infrastructure/**: Core cluster components (controllers, networking, namespaces).
- **monitoring/**: Monitoring stack (Prometheus, Loki, etc.).
- **my-apps/**: User applications and dashboards.

## Key Components

- **ArgoCD**: GitOps continuous delivery.
- **Cert-Manager**: Automated TLS certificates.
- **Cloudflared**: Secure ingress via Cloudflare Tunnel.
- **Traefik**: Kubernetes ingress controller.
- **Prometheus & Loki**: Monitoring and logging.

## Usage

1. **Bootstrap ArgoCD**  
   Deploy ArgoCD using the manifests in `infrastructure/controllers/argocd/`.

2. **Configure Secrets**  
   - Cloudflare credentials for Cloudflared.
   - Cloudflare API token for Cert-Manager DNS01.

3. **Apply Infrastructure**
```
kubectl apply -k infrastructure/
```

4. **Apply Monitoring**
```
kubectl apply -k monitoring/
```

5. **Deploy Applications**
```
kubectl apply -k my-apps/
```

## Notes

- All components are managed declaratively.
- ApplicationSets automate multi-app deployments.
- TLS is managed via Cert-Manager and Cloudflare DNS01.

## References

- [ArgoCD](https://argo-cd.readthedocs.io/)
- [Kustomize](https://kubectl.docs.kubernetes.io/references/kustomize/)
- [Helm](https://helm.sh/)
- [Cert-Manager](https://cert-manager.io/)
- [Cloudflared](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/)

---