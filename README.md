# Blue-Green Deployment on Kubernetes

## 📌 Project Overview
This project demonstrates the Blue-Green deployment strategy on Kubernetes to achieve zero-downtime application releases. Two separate deployments (Blue and Green) are created with different versions of the application, and traffic is switched between them using a Kubernetes Service selector.

---

## 🧠 Blue-Green Deployment Concept
- **Blue**: Current live production version
- **Green**: New version ready for release
- Traffic is switched instantly by updating the Service selector

---

## ⚙️ Blue Deployment (v1)
- Deployed application with label `version: blue`
- Runs 3 replicas
- Exposed internally through a Kubernetes Service

**File:** `k8s/blue.yml`

---

## ⚙️ Green Deployment (v2)
- Deployed new application version with label `version: green`
- Runs 3 replicas
- Kept ready without impacting live traffic

**File:** `k8s/green.yml`

---

## 🌐 Service Configuration
- Single Service used for traffic routing
- Traffic is controlled using label selectors
- Switching selector redirects traffic instantly

**File:** `k8s/service.yml`

---

## 🔁 Traffic Switch (Blue → Green)
Traffic is redirected by updating the Service selector:

```yaml
selector:
  app: my-app
  version: green
kubectl apply -f k8s/blue.yml
kubectl apply -f k8s/service.yml

# Deploy green version (v2)
kubectl apply -f k8s/green.yml

# Switch traffic from blue to green
kubectl apply -f k8s/service.yml
🌍 Access Application

Access the application using the LoadBalancer external IP

Refresh browser after switching selector to see new version

🧰 Technologies Used

Kubernetes

Deployments

Services

Labels & Selectors

Blue-Green Deployment Strategy

Docker

---

## 📂 Recommended Repo Structure
kubernetes-blue-green-deployment/
├── README.md
└── k8s/
├── blue.yml
├── green.yml
└── service.yml
