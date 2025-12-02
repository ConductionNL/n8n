# n8n (GitOps)

This repo defines an Argo CD Application that deploys n8n via the community Helm chart (`https://community-charts.github.io/helm-charts`).

## Prerequisites
- Argo CD installed and access to this repo
- Namespace  exists
- Secrets in :
  -  with keys: , , , , 
  -  with key: 

Example to create secrets (values resolved from the Postgres operator):



## Deploy via Argo CD
Apply the Application:

```bash
kubectl apply -n argocd -f application.yaml
```

Namespace and sync are handled by Argo CD (`CreateNamespace=true`). Verify in Argo CD UI, or:

```bash
kubectl get pods -n n8n
kubectl get all -n n8n
```

Wait for health:



## Configuration
- Edit `values.yaml` for human-readable config; keep inline values in `application.yaml` in sync.
- Ingress is enabled on `n8n.commonground.nu` with class `nginx`. TLS via cert-manager (`cert-manager.io/cluster-issuer: letsencrypt-prod`) is configured; certificate secret is `n8n-tls`. Protocol is HTTPS.
- Default Service is ClusterIP on port 5678. Use Ingress or port-forward for access.

## Security
- No secrets in Git; reference cluster Secrets only.
- Argo CD uses read-only repo credentials.
- Least-privilege: n8n runs in its own namespace.
