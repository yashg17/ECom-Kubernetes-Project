# High-Availability & Zero-Trust Kubernetes E-Commerce Stack

A production-ready, local Kubernetes e-commerce application deployed on **KinD (Kubernetes in Docker)**. This repository showcases zero-trust network security, automated horizontal autoscaling (HPA), fault tolerance, and dynamic ingress routing.

---

## 🏗️ Architecture Overview

The application runs inside a dedicated `ecommerce-prod` namespace and is architected around three key infrastructure pillars:

1. **Traffic & Routing:** Ingress NGINX routes edge traffic on `localhost` directly to service endpoints.
2. **Zero-Trust Security:** Strict Kubernetes `NetworkPolicy` drops all unauthorized direct internal pod communications, only allowing incoming traffic explicitly originating from the NGINX Ingress controller.
3. **Autoscaling & Resilience:** Automated scaling via Horizontal Pod Autoscaler (HPA) targeting 50% CPU utilization, backed by high availability controls (`PodDisruptionBudget`, `RollingUpdate`, and readiness/liveness probes).

---

## 📁 Repository Structure

```text
ECom-K8/
├── app/
│   ├── Dockerfile             # Container image definition for custom web application
│   └── index.html             # Application frontend code
├── manifests/
│   ├── namespace.yml          # ecommerce-prod Namespace definition
│   ├── cm.yml                 # ConfigMaps for dynamic application configuration
│   ├── secret.yml             # Kubernetes Secrets (base64 encoded)
│   ├── pvc.yml                # PersistentVolumeClaim for storage binding
│   ├── dep.yml                # Main Application Deployment (requests, limits, probes)
│   ├── svc.yml                # ClusterIP Service for application pods
│   ├── ingress.yml            # Ingress rule mapping localhost to service
│   ├── networkpolicy.yml      # Zero-trust NetworkPolicy enforcing Ingress-only access
│   ├── hpa.yml                # Horizontal Pod Autoscaler configuration (CPU-based)
│   ├── pdb.yml                # PodDisruptionBudget ensuring minimum availability during disruptions
│   ├── sa.yml                 # Custom ServiceAccount for RBAC scoping
│   ├── role.yml               # RBAC Role defining resource permissions
│   └── rolebind.yml           # RoleBinding attaching SA to Role
├── config.yml                 # KinD cluster setup configuration (with extraPortMappings)
└── README.md                  # Project documentation# ECom-Kubernetes-Project
