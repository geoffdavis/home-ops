# home-ops

This repository contains the configuration and automation for my home Kubernetes cluster, inspired by the [onedr0p/cluster-template](https://github.com/onedr0p/cluster-template). It manages infrastructure, applications, and cluster operations using GitOps principles.

## Features

- **Kubernetes Manifests**: Declarative configuration for all cluster resources.
- **GitOps**: Automated deployment and reconciliation using Flux.
- **Secrets Management**: Secure handling of secrets with SOPS and Age.
- **Infrastructure as Code**: Cluster bootstrapping and management scripts.
- **App Deployments**: Helm, Kustomize, and custom manifests for apps and system components.
- **Cloudflare Integration**: DNS and tunnel configuration for secure remote access.
- **Talos**: Immutable, secure Kubernetes OS for cluster nodes.

## Repository Structure

```none
.
├── bootstrap/           # Initial cluster bootstrapping (Helmfile, etc.)
├── components/          # Common components, namespaces, and secrets
├── kubernetes/          # Main cluster manifests (apps, system, networking, etc.)
├── scripts/             # Helper and automation scripts
├── talos/               # Talos OS configuration and cluster secrets
├── templates/           # Jinja2 templates for config generation
├── overrides/           # Custom overrides and partials
├── cluster.yaml
├── kubeconfig
├── Taskfile.yaml        # Task automation
└── README.md
```

## Getting Started

### Prerequisites

- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [Flux CLI](https://fluxcd.io/docs/installation/)
- [SOPS](https://github.com/mozilla/sops)
- [Age](https://github.com/FiloSottile/age)
- [Talosctl](https://www.talos.dev/docs/latest/introduction/installation/)
- [Helm](https://helm.sh/)
- [yq](https://github.com/mikefarah/yq)
- [jq](https://stedolan.github.io/jq/)

### Bootstrapping the Cluster

1. **Generate Secrets**:
   Encrypt secrets using SOPS and Age.
   Example:

   ```sh
   sops -e --age <your-age-key> secrets.yaml > secrets.sops.yaml
   ```

2. **Provision Talos Nodes**:
   Use the configs in `talos/` to provision your nodes.

3. **Bootstrap Flux**:
   Use the `bootstrap/helmfile.yaml` and Flux CLI to install Flux and sync the repository.

4. **Apply Manifests**:
   Apply manifests in `kubernetes/` and `components/` as needed.

### Managing Applications

- Add or update manifests in `kubernetes/apps/` or `components/`.
- Use Kustomize overlays for environment-specific configuration.
- Use the Taskfile or scripts for automation.

### Secrets Management

- Store secrets in SOPS-encrypted files (`*.sops.yaml`).
- Use Age keys (`age.key`) for encryption/decryption.

### Cloudflare Integration

- Configure DNS and tunnels in `kubernetes/network/cloudflare-dns/` and `cloudflare-tunnel.json`.

## Automation

- Use `Taskfile.yaml` for common tasks:

  ```sh
  task <task-name>
  ```

- Use scripts in `scripts/` for custom automation.

## References

- [onedr0p/cluster-template](https://github.com/onedr0p/cluster-template)
- [Talos Linux](https://www.talos.dev/)
- [FluxCD](https://fluxcd.io/)
- [SOPS](https://github.com/mozilla/sops)
- [Age](https://github.com/FiloSottile/age)
