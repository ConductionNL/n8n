# n8n (GitOps)

This repo defines an Argo CD Application that deploys n8n via the Bitnami Helm chart.

## Prerequisites
- Argo CD installed and access to this repo
- Namespace  exists
- Secrets in :
  -  with keys: , , , , 
  -  with key: 

Example to create secrets (values resolved from the Postgres operator):



## Deploy via Argo CD
Apply the Application:



Wait for health:



## Configuration
- Edit  for human-readable config; keep  inline values in sync.
- Enable Ingress by setting  and Goengoeloe.
- Default Service is ClusterIP on port 5678. Use Ingress or port-forward for access.

## Security
- No secrets in Git; reference cluster Secrets only.
- Argo CD uses read-only repo credentials.
- Least-privilege: n8n runs in its own namespace.
