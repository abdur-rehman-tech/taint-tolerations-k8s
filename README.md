# 🚫 Kubernetes Taints & Tolerations

![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white) ![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)

Shows how **taints and tolerations** control pod placement, using a **Kind** cluster with 1 control-plane and 2 worker nodes.

## 🧪 Lab setup

```yaml
# config.yml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
    image: kindest/node:v1.33.1
  - role: worker
    image: kindest/node:v1.33.1
  - role: worker
    image: kindest/node:v1.33.1
```

## 🚀 Steps

```bash
# 1. create cluster
kind create cluster --name tws-cluster --config config.yml

# 2. taint both workers
kubectl taint nodes node-worker1 prod=true:NoSchedule
kubectl taint nodes node-worker2 prod=true:NoSchedule

# 3. deploy a pod with a matching toleration
kubectl create ns nginx
kubectl apply -f pod.yml
kubectl get pods -n nginx -o wide

# 4. remove taints
kubectl taint nodes node-worker1 prod=true:NoSchedule-
kubectl taint nodes node-worker2 prod=true:NoSchedule-
```

## 💡 Key idea

A taint **repels** pods; a toleration **allows** a pod to be scheduled on a tainted node. It doesn't force placement; combine with node affinity for that.

---

## 👤 Author

**Abdur Rehman** · DevSecOps Engineer · Founder of [ARTechOps](https://artechops.com)

[LinkedIn](https://www.linkedin.com/in/muhamad-abdur-rehman-81777b366/) · [GitHub](https://github.com/abdur-rehman-tech) · [artechops.com](https://artechops.com)
