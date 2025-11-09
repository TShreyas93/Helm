# Helm - Deploy Prometheus to Local kind Cluster (Windows Self-hosted, PowerShell)

This repository automates the deployment of the Prometheus monitoring stack onto a local Kubernetes cluster managed by [kind](https://kind.sigs.k8s.io/) on Windows, using GitHub Actions and PowerShell.

## GitHub Actions Workflow

The included workflow (see `.github/workflows/`) is triggered on:
- Manual dispatch (`workflow_dispatch`)
- Pushes to the `main` branch

**Key Features:**
- Runs on a Windows self-hosted runner
- Uses PowerShell as the default shell for all steps
- Deploys Prometheus using Helm in a local kind cluster, with support for custom values (via `charts/prom-values.yaml` if present)

## Deployment Steps (summarized from GitHub Actions workflow)

1. **Checkout Code**
2. **Environment Check**  
   Verifies Docker, kind, kubectl, and helm installation, checking for kubeconfig file.
3. **Cluster Access Verification**  
   Confirms access to your local kind cluster and displays node info.
4. **Add Prometheus Helm Repo**  
   Adds and updates the Prometheus charts repository.
5. **Deploy Prometheus**  
   Installs/updates the Prometheus stack to the `monitoring` namespace. Uses a custom values file if present, or falls back to default overrides.
6. **Show Monitoring Resources**  
   Lists monitoring-related pods and services.
7. **Show Events**  
   Displays all events in the monitoring namespace, sorted by time.

## Pre-requisites

Before using this workflow, ensure your self-hosted Windows runner has:
- [Docker](https://docs.docker.com/get-docker/)
- [kind](https://kind.sigs.k8s.io/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [Helm](https://helm.sh/)
- Access to your `.kube/config` file in your user profile directory (or set `KUBECONFIG`).

## Customization

- To provide custom Prometheus Helm values, create a file:  
  `charts/prom-values.yaml`
- The workflow will automatically detect and use this file during deployment.

## License

This project currently has no license.  
You may wish to add a license file to ensure the code can be shared or modified according to your terms.

## Author

- [TShreyas93](https://github.com/TShreyas93)

---

For help or questions, open an issue in this repository.
