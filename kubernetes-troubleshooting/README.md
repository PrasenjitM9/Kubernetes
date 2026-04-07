**complete Kubernetes troubleshooting playbook** with 20+ scenarios. Each entry follows the same structure:  

**Definition → Possible Causes → How to Identify → Fix.**  

---

## 🔹 Pod-Level Issues
### 1. Pod in `CrashLoopBackOff`
- **Definition:** Pod keeps restarting.  
- **Causes:** Misconfigurations, missing dependencies, resource limits.  
- **Identify:** `kubectl logs`, `kubectl describe pod`.  
- **Fix:** Correct configs, increase resources, fix dependencies.  

### 2. Pod in `ImagePullBackOff`
- **Definition:** Pod can’t pull image.  
- **Causes:** Wrong image name, private registry auth failure.  
- **Identify:** Pod events in `kubectl describe`.  
- **Fix:** Verify image, add `imagePullSecrets`.  

### 3. Pod Stuck in `Pending`
- **Definition:** Pod scheduled but not running.  
- **Causes:** No resources, PVC not bound, taints.  
- **Identify:** Pod events, PVC status.  
- **Fix:** Add nodes, fix scheduling rules, bind PVC.  

### 4. Pod in `OOMKilled`
- **Definition:** Pod killed due to memory exhaustion.  
- **Causes:** Memory leaks, missing resource limits.  
- **Identify:** Pod events, container logs.  
- **Fix:** Add memory limits, optimize app, scale horizontally.  

---

## 🔹 Node-Level Issues
### 5. Node Not Ready
- **Definition:** Node unavailable.  
- **Causes:** Kubelet down, CNI plugin failure, resource exhaustion.  
- **Identify:** `kubectl get nodes`, `journalctl -u kubelet`.  
- **Fix:** Restart kubelet, fix CNI, free resources.  

### 6. Node Disk Pressure
- **Definition:** Node reports disk pressure.  
- **Causes:** Logs filling disk, unused images.  
- **Identify:** `kubectl describe node`.  
- **Fix:** Clean logs, prune images, expand disk.  

### 7. Node Network Unavailable
- **Definition:** Node cannot join cluster network.  
- **Causes:** CNI misconfig, firewall rules.  
- **Identify:** Node events, CNI logs.  
- **Fix:** Reinstall CNI plugin, open required ports.  

---

## 🔹 Service & Networking Issues
### 8. Service Not Accessible
- **Definition:** Service unreachable.  
- **Causes:** Wrong type, port mismatch, endpoints missing.  
- **Identify:** `kubectl describe svc`, `kubectl get endpoints`.  
- **Fix:** Correct service type, fix ports, ensure pods running.  

### 9. DNS Resolution Failure
- **Definition:** Pods can’t resolve service names.  
- **Causes:** CoreDNS crash, misconfigured ConfigMap.  
- **Identify:** CoreDNS pod logs.  
- **Fix:** Restart CoreDNS, fix ConfigMap.  

### 10. Network Policy Blocking Traffic
- **Definition:** Pods blocked by restrictive policies.  
- **Causes:** Misconfigured NetworkPolicy.  
- **Identify:** `kubectl get networkpolicy`, connectivity tests.  
- **Fix:** Update policies to allow traffic.  

---

## 🔹 Storage Issues
### 11. PVC/PV Binding Issues
- **Definition:** Pod can’t mount volume.  
- **Causes:** StorageClass misconfig, size mismatch.  
- **Identify:** `kubectl describe pvc`.  
- **Fix:** Correct StorageClass, match PV size/mode.  

### 12. Volume Mount Failure
- **Definition:** Pod fails to mount volume.  
- **Causes:** Wrong mount path, permissions.  
- **Identify:** Pod events, container logs.  
- **Fix:** Fix mount path, adjust permissions.  

---

## 🔹 Control Plane Issues
### 13. API Server Unreachable
- **Definition:** `kubectl` fails to connect.  
- **Causes:** Control plane down, firewall blocking port 6443.  
- **Identify:** Ping API server, check kubeconfig.  
- **Fix:** Restart control plane, fix firewall, correct kubeconfig.  

### 14. etcd Unhealthy
- **Definition:** etcd cluster not healthy.  
- **Causes:** Disk latency, network partition.  
- **Identify:** `kubectl get componentstatus`, etcd logs.  
- **Fix:** Restart etcd, fix disk/network issues.  

### 15. Scheduler Not Working
- **Definition:** Pods not scheduled.  
- **Causes:** Scheduler crash, misconfig.  
- **Identify:** Check scheduler pod logs in `kube-system`.  
- **Fix:** Restart scheduler, fix configs.  

---

## 🔹 Security & Certificates
### 16. Expired Certificates
- **Definition:** Cluster components fail due to expired certs.  
- **Causes:** Certificates not renewed.  
- **Identify:** Logs show TLS errors.  
- **Fix:** Renew certs with `kubeadm cert renew`.  

### 17. RBAC Access Denied
- **Definition:** User/service account denied access.  
- **Causes:** Missing RBAC role bindings.  
- **Identify:** Error messages: `Forbidden`.  
- **Fix:** Create Role/ClusterRole and bind to user/service account.  

---

## 🔹 Scaling & Performance
### 18. High CPU/Memory Usage
- **Definition:** Pods consuming excessive resources.  
- **Causes:** Memory leaks, missing limits.  
- **Identify:** `kubectl top pod/node`.  
- **Fix:** Add limits, scale pods, add nodes.  

### 19. HPA Not Scaling
- **Definition:** Horizontal Pod Autoscaler not scaling.  
- **Causes:** Metrics server not working.  
- **Identify:** `kubectl get hpa`, metrics server logs.  
- **Fix:** Deploy metrics server, configure HPA correctly.  

### 20. Cluster Upgrade Failure
- **Definition:** Upgrade process stuck.  
- **Causes:** Version mismatch, incompatible add-ons.  
- **Identify:** Upgrade logs.  
- **Fix:** Upgrade add-ons, follow kubeadm upgrade steps.  

---

## 🔹 Miscellaneous
### 21. ConfigMap/Secret Not Found
- **Definition:** Pod fails due to missing config/secret.  
- **Causes:** Resource not created or wrong name.  
- **Identify:** Pod events.  
- **Fix:** Create config/secret, correct reference.  

### 22. Liveness/Readiness Probe Failures
- **Definition:** Pod restarted or marked unready.  
- **Causes:** Wrong probe path/port.  
- **Identify:** Pod events, logs.  
- **Fix:** Correct probe configuration.  

---

## 📊 Master Quick Reference Table

| Category        | Example Scenario             | Identify with…                  | Fix Summary |
|-----------------|------------------------------|---------------------------------|-------------|
| Pod Issues      | CrashLoopBackOff, Pending    | Logs, describe pod              | Fix configs, resources |
| Node Issues     | NotReady, DiskPressure       | Node describe, kubelet logs     | Restart services, free resources |
| Networking      | Service unreachable, DNS fail| Service endpoints, CoreDNS logs | Fix service type, restart CoreDNS |
| Storage         | PVC binding, mount failure   | PVC describe, pod events        | Fix StorageClass, permissions |
| Control Plane   | API server down, etcd fail   | Componentstatus, logs           | Restart components, renew certs |
| Security        | RBAC denied, expired certs   | Error messages, logs            | Create RBAC roles, renew certs |
| Scaling         | HPA not scaling, high usage  | Metrics server, top commands    | Deploy metrics server, add limits |
| Miscellaneous   | Probe failures, missing secrets | Pod events, logs             | Fix probe configs, create secrets |

---

