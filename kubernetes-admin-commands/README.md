In Kubernetes, “admin commands” usually refer to **cluster-level operations** you run with `kubectl` (and sometimes `kubeadm`) to manage nodes, users, workloads, and the cluster itself.

Here’s a practical, categorized list of **common Kubernetes admin commands**:

---

# ⚙️ Cluster Information & Context

```bash
kubectl cluster-info
kubectl version
kubectl config view
kubectl config get-contexts
kubectl config use-context <context-name>
```

---

# 🖥️ Node Management

```bash
kubectl get nodes
kubectl get nodes -o wide
kubectl describe node <node-name>
kubectl cordon <node-name>        # Mark node unschedulable
kubectl uncordon <node-name>      # Allow scheduling again
kubectl drain <node-name>         # Safely evict workloads
```

---

# 📦 Pod Management

```bash
kubectl get pods -A
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl logs -f <pod-name>        # Follow logs
kubectl exec -it <pod-name> -- /bin/bash
kubectl delete pod <pod-name>
```

---

# 🚀 Deployment & Workloads

```bash
kubectl get deployments
kubectl create deployment nginx --image=nginx
kubectl scale deployment nginx --replicas=3
kubectl rollout status deployment/nginx
kubectl rollout undo deployment/nginx
kubectl delete deployment nginx
```

---

# 🌐 Services & Networking

```bash
kubectl get svc
kubectl expose deployment nginx --port=80 --type=NodePort
kubectl describe svc nginx
```

---

# 📁 Namespace Management

```bash
kubectl get namespaces
kubectl create namespace dev
kubectl delete namespace dev
kubectl config set-context --current --namespace=dev
```

---

# 🔐 RBAC (Access Control)

```bash
kubectl get roles -A
kubectl get rolebindings -A
kubectl get clusterroles
kubectl get clusterrolebindings
```

---

# 📊 Resource Monitoring

```bash
kubectl top nodes
kubectl top pods
```

(*Requires Metrics Server installed*)

---

# 📄 Apply / Manage Configurations

```bash
kubectl apply -f app.yaml
kubectl create -f app.yaml
kubectl delete -f app.yaml
kubectl edit deployment nginx
```

---

# 🔍 Debugging & Troubleshooting

```bash
kubectl describe pod <pod-name>
kubectl get events
kubectl logs <pod-name> --previous
kubectl exec -it <pod-name> -- sh
```

---

# 🛠️ ConfigMaps & Secrets

```bash
kubectl get configmaps
kubectl get secrets
kubectl create configmap my-config --from-literal=key=value
kubectl create secret generic my-secret --from-literal=password=1234
```

---

# 🧱 Cluster Bootstrapping (kubeadm - Admin Level)

Using kubeadm:

```bash
kubeadm init
kubeadm join
kubeadm reset
kubeadm token create
```

---

# ⚡ Pro Tips (Admin Usage)

* Use `-A` → all namespaces
* Use `-o wide` → more details
* Use `--watch` → real-time updates
* Use `--dry-run=client -o yaml` → preview configs

---

