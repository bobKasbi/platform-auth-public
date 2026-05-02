# Platform Auth (Keycloak Deployment)

This repository provides a reusable Keycloak deployment module using Helm, designed to act as a centralized Identity and Access Management (IAM) layer for frontend and backend systems.

---

## 🚀 Purpose

- Deploy Keycloak as a standalone service.
- Provide a unified identity and access management (IAM) layer.
- Handle user authentication, token issuance, and role-based access control (RBAC).
- Integrate cleanly with Angular and other frontend apps via OpenID Connect.

---

## 🧩 Repository Structure

platform-auth/  
├── Chart.yaml # Helm chart metadata  
├── values.yaml # Default configuration (Ingress, admin user, DB, etc.)  
├── templates/ # Helm templates for deployment, service, ingress, secrets  
├── ci/ # (optional) CI/CD scripts for GitLab  
└── README.md

---

## ⚙️ Deployment (local Minikube)

1. **Start Minikube**

   minikube start --memory=8192 --cpus=4  
   minikube addons enable ingress

2. **Deploy Keycloak via Helm**

   helm install keycloak ./charts/keycloak

3. **Check services**

   kubectl get pods  
   kubectl get svc  
   kubectl get ingress

4. **Access the Keycloak UI**

   https://keycloak.example.com


---

## 🌍 Integration with Frontend

The `dashboard-app` (Angular) frontend authenticates against this Keycloak instance using OpenID Connect:

| Key          | Example                       |
| ------------ | ----------------------------- |
| Keycloak URL | https://keycloak.example.com  |
| Realm        | dashboard-realm               |
| Client ID    | dashboard-ui                  |

In Angular’s environment config:

keycloak: {  
 url: 'https://keycloak.example.com',  
 realm: 'dashboard-realm',  
 clientId: 'dashboard-ui'  
}

---

## 🧰 Future Improvements

- Add automatic realm import (JSON)
- Add custom Keycloak theme
- CI/CD deployment via GitLab pipelines
- Persistent PostgreSQL storage
- HTTPS (TLS via Ingress or Cert-Manager)

---

## 🏗️ Architecture Overview

This Keycloak deployment acts as the central Identity and Access Management (IAM) service in a typical system architecture:

[Frontend (Angular / SPA)]
        ↓
[BFF / API Layer]
        ↓
[Keycloak (OIDC Provider)]
        ↓
[User / Session / Token Management]

- Frontend authenticates users via OpenID Connect (OIDC)
- BFF handles secured communication and token validation
- Keycloak manages authentication, authorization, and token issuance

---

## 🧑‍💻 Maintainer

**Amin Kasbi** (`bobKasbi`)  
Infrastructure / DevOps / Frontend Engineer
