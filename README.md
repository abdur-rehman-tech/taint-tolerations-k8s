Kubernetes Taints and Tolerations Demo

This project demonstrates how taints and tolerations work in Kubernetes using a Kind (Kubernetes in Docker) cluster.

In this project:
A Kind cluster with 1 control-plane node and 2 worker nodes is created.
Both worker nodes are tainted to restrict pod scheduling.
A pod with matching tolerations is deployed successfully.
This demonstrates how Kubernetes controls workload placement on nodes.

The cluster was created using the following config.yml:

kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
    image: kindest/node:v1.33.1
  - role: worker
    image: kindest/node:v1.33.1
  - role: worker
    image: kindest/node:v1.33.1



Create Cluster
kind create cluster --name tws-cluster --config config.yml


To taint the nodes:
kubectl taint nodes node-worker1 prod=true:NoSchedule
kubectl taint nodes node-worker2 prod=true:NoSchedule


To create a namespace:
kubectl create ns nginx

To apply toleration use pod.yml:
kubectl apply -f pod.yml 


To remove taint the nodes:
kubectl taint nodes node-worker1 prod=true:NoSchedule-
kubectl taint nodes node-worker2 prod=true:NoSchedule-
