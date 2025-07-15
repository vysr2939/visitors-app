# Visitors App Operator

This repository contains a Kubernetes operator built with [Kubebuilder](https://github.com/kubernetes-sigs/kubebuilder) / [Operator SDK](https://github.com/operator-framework/operator-sdk). It manages a custom resource named **VisitorsApp** which deploys a simple web application composed of MySQL, a backend service, and a React based frontend.

## Project structure

```
.
├── api/              # Custom resource API definitions
├── controllers/      # Reconciler logic and resource helpers
│   └── visitorsapp/  # MySQL, backend and frontend implementations
├── config/           # Kustomize overlays, RBAC, manifests
├── main.go           # Entry point for the manager
└── Makefile          # Build and deployment helpers
```

- `api/v1/visitorsapp_types.go` defines the CRD schema including `size` and `title` fields in the spec and status information for the deployed images.
- `controllers/visitorsapp/` contains the reconciler and helper functions that create Deployments, Services and Secrets for each component.
- `config/` holds Kustomize configuration used for installing and running the operator in a cluster.

## Building and running

The operator is managed through the provided **Makefile**. Typical targets include:

```bash
make install   # Install CRDs into the configured cluster
make run       # Run the controller locally
make deploy    # Build and deploy the controller to the cluster
```

See the `Makefile` for the full list of available commands.

## Custom resource example

A VisitorsApp instance declares the number of backend replicas and an optional title for the web UI header:

```yaml
apiVersion: example.com.example.com/v1
kind: VisitorsApp
metadata:
  name: visitors-sample
spec:
  size: 1
  title: "Welcome!"
```

Apply the manifest after the operator is running to deploy the application components.

## Learn more

- Inspect `controllers/` to see how MySQL, backend and frontend resources are built and kept in sync.
- Explore `config/` to understand how Kustomize assembles the deployment manifests.
- Run `make help` to view all make targets and additional details.

