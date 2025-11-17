HMS Frontend Kubernetes manifests

This folder contains Kubernetes manifests to deploy the Hospital Management System (HMS) frontend.

Files created
- k8s/frontend-deployment.yaml — Deployment for `hms-frontend` (replace the placeholder image).
- k8s/frontend-service.yaml — Service (type LoadBalancer by default).

Quick usage
1. Replace the placeholder image in `k8s/frontend-deployment.yaml` with your built frontend image, e.g. `ghcr.io/<org>/hms-frontend:1.2.3` or `dockerhubuser/hms-frontend:tag`.

2. Choose the appropriate Service type in `k8s/frontend-service.yaml`:
   - LoadBalancer — for cloud providers that support it (AKS/GKE/EKS).
   - ClusterIP — internal-only service.
   - NodePort — expose on node port (for bare-metal or local clusters).

3. Apply manifests:

   kubectl apply -f k8s/frontend-deployment.yaml
   kubectl apply -f k8s/frontend-service.yaml

4. Verify pods and service:

   kubectl get pods -l app=hms-frontend
   kubectl get svc hms-frontend

Pushing to GitHub
- I have committed these files locally. To push them to a GitHub repo, run (replace <REPO_URL>):

   git branch -M main
   git remote add origin <REPO_URL>
   git push -u origin main

If you want me to add the remote and push, provide the repository URL and confirm whether you want me to push to `main` or `master`. If the repository is private, I will need push access (credentials or a PAT configured in your environment).

Notes
- The Deployment uses simple liveness/readiness probes against `/`. If your app serves assets from a different path (e.g. `/index.html`), update the probe paths.
- If you want an Ingress resource (host/path routing and TLS), tell me the domain and ingress controller type and I'll add one.
