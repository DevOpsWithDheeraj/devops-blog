
---

🧩 1. Kubernetes Basics

🔹 What is Kubernetes?

Kubernetes (K8s) is an open-source container orchestration platform used to deploy, scale, and manage containerized applications automatically.
👉 It was developed by Google and now maintained by CNCF (Cloud Native Computing Foundation).

🔹 Why DevOps uses Kubernetes

Automates container deployment and scaling

Enables zero downtime deployment (rolling updates)

Works seamlessly with CI/CD tools (like Jenkins, ArgoCD)

Simplifies infrastructure management (especially with Docker containers)


🔹 Core Concepts

Component	Description

Cluster	A group of nodes (machines) managed by Kubernetes
Node	A worker machine (VM or physical) running containers
Pod	Smallest deployable unit — runs one or more containers
Service	Exposes pods as a network service
Deployment	Manages replicas of pods and rolling updates
ReplicaSet	Ensures a specified number of pod replicas run
Namespace	Logical isolation within a cluster
Ingress	Manages external access (like a reverse proxy)
ConfigMap & Secret	Store configuration and sensitive data separately
PersistentVolume (PV)	Storage resource in the cluster
PersistentVolumeClaim (PVC)	Request for storage by a user



---

⚙️ 2. Kubernetes Architecture

+------------------------------------------------------+
|                    Master Node                       |
|------------------------------------------------------|
|  API Server | Scheduler | Controller Manager | etcd  |
+------------------------------------------------------+
|                    Worker Nodes                      |
|------------------------------------------------------|
|  Kubelet | Kube Proxy | Container Runtime (Docker)   |
+------------------------------------------------------+

Control Plane Components:

API Server: Entry point to the cluster (kubectl interacts here)

etcd: Key-value store for cluster data

Scheduler: Assigns pods to nodes

Controller Manager: Ensures desired state is maintained


Worker Node Components:

Kubelet: Ensures pods are running

Kube-proxy: Handles network communication

Container Runtime: Runs containers (Docker, containerd)



---

🚀 3. Hands-on Commands (kubectl)

Task	Command

View cluster nodes	kubectl get nodes
View all pods	kubectl get pods -A
Deploy an app	kubectl create deployment nginx --image=nginx
Expose app	kubectl expose deployment nginx --port=80 --type=NodePort
Scale replicas	kubectl scale deployment nginx --replicas=3
View logs	kubectl logs <pod-name>
Describe resource	kubectl describe pod <pod-name>
Delete resource	kubectl delete pod <pod-name>



---

🧱 4. YAML Configuration Example

nginx-deployment.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80

Apply it:

kubectl apply -f nginx-deployment.yaml


---

🧰 5. Kubernetes for DevOps Pipelines

🔹 CI/CD Integration

Jenkins → Kubernetes: Use Jenkins agents on K8s (Jenkins Kubernetes plugin)

GitHub Actions / GitLab CI → Kubernetes: Automate build and deploy pipelines

Helm: Package Kubernetes manifests into charts for easy versioning and deployment

ArgoCD: GitOps tool for continuous deployment on K8s


Example CI/CD flow:

1. Developer pushes code → GitHub


2. Jenkins builds Docker image → pushes to ECR/Docker Hub


3. Jenkins deploys updated image to Kubernetes (using kubectl or Helm)




---

☁️ 6. Storage & Networking in Kubernetes

🔹 Storage:

PV/PVC – persistent storage for data

StorageClass – dynamically provision storage

StatefulSet – for stateful apps like MySQL, Redis


🔹 Networking:

ClusterIP – internal communication

NodePort – expose service on each node’s IP

LoadBalancer – integrates with cloud load balancer (AWS, GCP, Azure)

Ingress Controller – manages HTTP/HTTPS routing



---

🧩 7. Advanced Kubernetes Concepts

Concept	Description

Helm Charts	Package manager for Kubernetes (like apt for Linux)
DaemonSet	Runs a pod on all (or selected) nodes
StatefulSet	Manages stateful apps with stable identities
Horizontal Pod Autoscaler (HPA)	Scales pods automatically based on CPU/memory
Vertical Pod Autoscaler (VPA)	Adjusts container resources automatically
Network Policies	Restrict traffic between pods for security
Custom Resource Definition (CRD)	Extend Kubernetes API with custom objects
Service Mesh (Istio/Linkerd)	Adds observability, traffic control, and security between services



---

🧩 8. Monitoring & Logging

Prometheus + Grafana → metrics & dashboards

ELK Stack (Elasticsearch, Logstash, Kibana) → logs aggregation

Loki + Grafana → lightweight logging

Kubernetes Dashboard → GUI for monitoring resources



---

🧠 9. Security in Kubernetes

Use RBAC (Role-Based Access Control)

Use Secrets for credentials

Enable Pod Security Policies or OPA/Gatekeeper

Regularly scan container images (Trivy, Clair)



---

⚡ 10. Kubernetes in Real-World DevOps Workflow

Example 3-Tier Application:

Frontend: React app

Backend: Node.js API

Database: MySQL StatefulSet

Deploy all using Helm chart

Manage traffic using Ingress Controller

Monitor with Prometheus + Grafana

Auto-scale using HPA



---
