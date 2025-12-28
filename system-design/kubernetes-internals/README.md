# ☸️ Kubernetes Internals – Deep Dive (Top 1%)

This roadmap explains **how Kubernetes actually works internally** — not just *kubectl commands*, but **what happens inside the cluster**.

If you master this → you can debug production clusters, crack system design interviews, and operate Kubernetes like a Staff Engineer.

---

## 🧠 Kubernetes Architecture (Bird’s Eye View)

Kubernetes = **Control Plane + Worker Nodes**

### 🧩 Control Plane Components
- kube-apiserver
- etcd
- kube-scheduler
- kube-controller-manager
- cloud-controller-manager

### ⚙️ Node Components
- kubelet
- kube-proxy
- Container Runtime (containerd / CRI-O)

---

## 🔐 kube-apiserver (The Brain Gateway)

### What it does
- Entry point for **all operations**
- Exposes REST API
- Handles auth, authz, validation, admission

### Internals
- Authentication chain
- Authorization (RBAC, ABAC)
- Admission Controllers
- Object persistence

📌 **Everything in Kubernetes = API Object**

---

## 🗃️ etcd (Source of Truth)

### Role
- Distributed key-value store
- Stores **entire cluster state**

### Internals
- Raft consensus
- Leader election
- Quorum & consistency
- WAL (Write Ahead Log)
- Snapshots & compaction

📌 If etcd is gone → **cluster is gone**

---

## 📅 kube-scheduler (Placement Engine)

### Responsibilities
- Watches unscheduled Pods
- Selects best Node

### Scheduling Pipeline
1. Filtering
2. Scoring
3. Binding

### Internals
- Node affinity
- Taints & tolerations
- Resource requests & limits
- Custom schedulers

---

## 🔄 Controllers (Desired State Engine)

### Controller Manager
- Runs multiple controllers:
  - Deployment Controller
  - ReplicaSet Controller
  - Node Controller
  - Job / CronJob Controller

### Core Principle
> Kubernetes continuously compares **desired state vs current state**

---

## 🧠 kubelet (Node Brain)

### What kubelet does
- Talks to API server
- Talks to container runtime
- Ensures Pod is running as defined

### Internals
- Pod lifecycle
- Liveness / readiness probes
- cgroups & namespaces
- Image pulling
- Volume mounting

---

## 📦 Container Runtime Interface (CRI)

### Runtime Options
- containerd
- CRI-O

### Flow


---

## 🌐 Networking Internals

### CNI (Container Network Interface)
- Flannel
- Calico
- Cilium

### Concepts
- Pod-to-Pod networking
- Cluster IP
- Service abstraction
- kube-proxy (iptables / IPVS)

📌 **No NAT between pods (flat network)**

---

## 🔀 kube-proxy Internals

### Responsibilities
- Implements Services
- Load balancing

### Modes
- iptables
- IPVS
- userspace (deprecated)

---

## 💾 Storage Internals

### CSI (Container Storage Interface)
- Volume lifecycle
- Attach / Detach
- Mount / Unmount

### Concepts
- PV / PVC binding
- StorageClass
- Dynamic provisioning

---

## 🔐 Security Internals

### Authentication
- Certificates
- Tokens
- OIDC

### Authorization
- RBAC
- Roles & ClusterRoles

### Admission Controllers
- Mutating
- Validating

### Pod Security
- SecurityContext
- Pod Security Standards
- Capabilities

---

## 🔁 Pod Lifecycle (Critical)

1. Pod object created
2. Scheduler assigns node
3. kubelet creates containers
4. Networking setup
5. Volume mounting
6. Containers start
7. Probes evaluated

---

## ⚡ Scaling Internals

### HPA
- Metrics server
- CPU / Memory / Custom metrics

### Cluster Autoscaler
- Node scale up/down
- Pending pods trigger scale

---

## 📊 Observability Internals

- Metrics (cAdvisor, kubelet)
- Logs (stdout/stderr)
- Events
- Tracing (OpenTelemetry)

---

## 🧠 Failure Scenarios (Real World)

- Node crash
- Pod eviction
- etcd quorum loss
- Network partition
- Image pull failures
- Split brain

📌 Kubernetes is designed for **self-healing**

---

## 🧠 Advanced Kubernetes Internals

- Leader election
- Informers & Watch API
- Garbage collection
- Finalizers
- API aggregation layer
- CRDs & Operators
- Control loops

---

## 🧪 Debugging Internals (Must-Know)

- kubectl describe
- kubectl get events
- kubelet logs
- etcdctl
- iptables / ipvsadm
- crictl

---

## 🧠 System Design Perspective

Kubernetes is:
- Distributed system
- Event-driven
- Eventually consistent
- Control-loop based

---

## 🎯 Mastery Level Outcomes

You can:
- Debug prod cluster at 3 AM
- Explain why Pod is Pending
- Design Kubernetes-native systems
- Build operators
- Pass Staff-level interviews

---

🔥 **If you understand Kubernetes Internals → Kubernetes understands you**
