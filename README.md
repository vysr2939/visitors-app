# Visitors App Operator

This repository contains a sample Kubernetes operator called **Visitors App**. It was generated using [Kubebuilder](https://github.com/kubernetes-sigs/kubebuilder) and the [Operator SDK](https://github.com/operator-framework/operator-sdk).
The operator manages a small web application composed of a MySQL database, a Go backend service and a React frontend.

A custom resource named `VisitorsApp` controls the number of backend replicas (`size`) and the title displayed in the UI (`title`). When a `VisitorsApp` object is created, the operator ensures all three components are deployed and kept up to date.

## Repository layout

```
.
├── api/              # Custom resource API definitions
├── controllers/      # Reconciler logic and resource helpers
│   └── visitorsapp/  # MySQL, backend and frontend implementations
├── config/           # Kustomize overlays, RBAC rules and manifests
├── main.go           # Entry point for the controller manager
└── Makefile          # Build and deployment commands
```

- `api/v1/visitorsapp_types.go` defines the CRD schema and status fields for the backend and frontend images.
- `controllers/visitorsapp/` contains the reconciler and helper functions that create Deployments, Services and Secrets for each component.
- `config/` holds the Kustomize configuration used to install and run the operator.

## Building and running

Use the provided `Makefile` to interact with the project:

```bash
make install   # Install CRDs into your cluster
make run       # Run the controller locally against the cluster
make deploy    # Build the manager container and deploy it
```

See `make help` for the full list of targets.

## Example custom resource

Below is a minimal `VisitorsApp` manifest that deploys one backend replica and sets the page title:

```yaml
apiVersion: example.com.example.com/v1
kind: VisitorsApp
metadata:
  name: visitors-sample
spec:
  size: 1
  title: "Welcome!"
```

Apply this manifest once the operator is running to create the application components.

## Learn more

- Inspect the code under `controllers/` to see how resources are reconciled.
- Explore `config/` to understand how Kustomize assembles the deployment manifests.
- Run `make help` to see all available make commands.

