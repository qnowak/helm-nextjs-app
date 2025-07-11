# Helm template for Next.js application

## Description

This Helm chart allows you to easily deploy a Next.js application on Kubernetes with full support for routing, health probes, and environment configuration. It is designed for flexibility and production-readiness, leveraging best practices from the Kubernetes and Helm ecosystem.

---

## Requirements

- **Kubernetes**: 1.22+
- **Helm**: 3.8+
- **Access to GitHub Container Registry** (`ghcr.io`) with a Personal Access Token (PAT) that has at least `read:packages` scope (for pulling charts)

---

## Key Parameters

| Parameter                | Default value                    | Description                               |
|--------------------------|----------------------------------|-------------------------------------------|
| `image.registry`         | `ghcr.io`                        | Docker registry for the app image         |
| `image.repository`       | `qnowak/helm-nextjs-app`         | Image repository name                     |
| `image.tag`              | `0.0.0`                          | Image tag/version                         |
| `service.port`           | `8080`                           | Service port exposed by Kubernetes        |
| `pod.port`               | `3000`                           | Application container port                |
| `routing.enabled`        | `false`                          | Enable routing (Ingress/Traefik)          |
| `routing.default_url`    | `example.com`                    | Default domain for routing                |
| `routing.type`           | `none`                           | Routing type: `ingress`, `traefik`, `none`|

---

## Installation

1. **Login to GitHub Container Registry (if needed):**

   ```sh
   helm registry login ghcr.io -u <github_username> -p <your_pat_token>
   ```

2. **Install the chart:**

   ```sh
   helm install my-nextjs-app oci://ghcr.io/qnowak/charts/helm-nextjs-app --version 0.0.0
   ```

---

## Usage Example

To use this chart as a dependency in your Next.js app:

```yaml
dependencies:
  - name: helm-nextjs-app
    alias: app
    version: ^0
    repository: oci://ghcr.io/qnowak/charts
```

---

## Configuration

You can customize the deployment by providing your own `values.yaml`. Below are the most important options:

| Parameter                | Default value                    | Description                               |
|--------------------------|----------------------------------|-------------------------------------------|
| `image.registry`         | `ghcr.io`                        | Docker registry for the app image         |
| `image.repository`       | `qnowak/helm-nextjs-app`         | Image repository name                     |
| `image.tag`              | `0.0.0`                          | Image tag/version                         |
| `service.port`           | `8080`                           | Service port exposed by Kubernetes        |
| `pod.port`               | `3000`                           | Application container port                |
| `routing.enabled`        | `false`                          | Enable routing (Ingress/Traefik)          |
| `routing.default_url`    | `example.com`                    | Default domain for routing                |
| `routing.type`           | `none`                           | Routing type: `ingress`, `traefik`, `none`|

### Config Maps
- `inject_maps`: Inject custom config map environment variables.

### Secrets
- `env_secrets`: Map of env key and value which will be put in the secret `<release-name>-<chart-name>-env`.

---

## Example values.yaml

```yaml
image:
  registry: ghcr.io
  repository: qnowak/helm-nextjs-app
  tag: "0.0.0"

service:
  port: 8080

pod:
  port: 3000

routing:
  enabled: true
  default_url: "example.com"
  type: ingress
  path: /
```

## Troubleshooting

- Make sure your Kubernetes cluster and Helm version meet the requirements.
- For Ingress, check that your cluster supports the specified ingress controller (e.g., Traefik, NGINX).
