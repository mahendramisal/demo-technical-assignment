# Actions for Bookstore API Deployment

This folder contains the tasks and files needed to prepare the existing FastAPI bookstore application for Kubernetes deployment and optional local container usage.

## Required work

1. Containerize the application
   - Add a `Dockerfile` for building the FastAPI app image
   - Add a `.dockerignore` to keep the image small

2. Support environment-based configuration
   - Confirm current `app/config.py` uses env vars (it does)
   - Ensure Kubernetes can configure database connection settings via env vars

3. Add Kubernetes deployment manifests
   - `deployment.yaml` for app deployment
   - `service.yaml` for app service exposure
   - `configmap.yaml` for non-sensitive configuration if needed
   - `secret.yaml` for DB credentials
   - `postgresql.yaml` for a database deployment or `StatefulSet`
   - `persistentvolumeclaim.yaml` for database storage

4. Add optional local container development support
   - `docker-compose.yaml` for local app + PostgreSQL
   - `Makefile` or scripts for build/run commands

5. Enable database inspection and raw data access
   - The app already exposes `/db_info/`
   - Suggest adding a lightweight admin interface or `pgcli` support in docs

6. Document assumptions and how to run
   - Update top-level `README.md` with deployment instructions
   - Add a separate doc for local compose usage and Kubernetes deployment

## Suggested deliverables

- `actions/Dockerfile`
- `actions/.dockerignore`
- `actions/docker-compose.yml`
- `actions/k8s/deployment.yaml`
- `actions/k8s/service.yaml`
- `actions/k8s/secret.yaml`
- `actions/k8s/postgres-pvc.yaml`
- `actions/k8s/postgres-deployment.yaml`
- `actions/k8s/README.md`
- `actions/README.md` (this file)

## Notes

- The current app uses `psycopg2` and requires a running PostgreSQL database.
- The database schema is created in `initdb/initdb.sql`.
- The app currently queries the `book` table and supports filtering by `name`, `year`, and `author`.
- The highest priority is making the app deployable safely to Kubernetes and configurable through env vars.
