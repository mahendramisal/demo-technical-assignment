# Kubernetes Deployment Files

This folder contains Kubernetes manifests to deploy the bookstore API and a PostgreSQL database.

Files:
- `deployment.yaml`: app Deployment for `bookstore-api`
- `service.yaml`: ClusterIP Service for app traffic
- `secret.yaml`: DB credentials secret
- `postgres-pvc.yaml`: PVC for PostgreSQL storage
- `postgres-deployment.yaml`: PostgreSQL Deployment

## How to deploy

1. Create the DB secret:
   kubectl apply -f actions/k8s/secret.yaml

2. Create storage and PostgreSQL deployment:
   kubectl apply -f actions/k8s/postgres-pvc.yaml
   kubectl apply -f actions/k8s/postgres-deployment.yaml

3. Deploy the API and service:
   kubectl apply -f actions/k8s/deployment.yaml
   kubectl apply -f actions/k8s/service.yaml

## Notes

- The app image is referenced as `bookstore-api:latest`.
- In a real cluster, build and push the image to a registry before deploying.
- The PostgreSQL init script is not automatically loaded in this manifest.
  Use a custom init container or preloaded volume if initial data is required.
