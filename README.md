# Multi-Application Containerized Deployment and Traffic Management Using Docker and Kubernetes

Two apps deployed on a local kind cluster, routed by the NGINX Ingress Controller.

| URL | App |
|---|---|
| `/` | E-commerce shop (React + Vite, served by Nginx) |
| `/nginx` | Custom Nginx page |
| `/health` | Shop health check |

## Structure
- `application/shop` - shop source + Dockerfile
- `application/nginx-page` - custom Nginx page + Dockerfile
- `kubernetes/` - namespace, deployments, services, ingress, configmap, secret

## Features
3 replicas, liveness/readiness probes, resource limits, ConfigMap and Secret,
rolling updates and rollback, self-healing, image versioning.

## Run
    docker build -t <user>/ecommerce-shop:v1 application/shop
    docker build -t <user>/my-nginx-app:v1 application/nginx-page
    kubectl apply -f kubernetes/namespace.yml
    kubectl apply -f kubernetes/configmap.yml -f kubernetes/secret.yml
    kubectl apply -f kubernetes/deployment.yml -f kubernetes/service.yml
    kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.11.2/deploy/static/provider/kind/deploy.yaml
    kubectl apply -f kubernetes/ingress.yml
