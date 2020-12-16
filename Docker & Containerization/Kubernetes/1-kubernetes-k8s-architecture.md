# Kubernetes

Open source container orchestration technology for deploying and managing containers

Allows - Service Discovery, Load balancing, Self healing mechanism

When we deploy Kubernetes, we get a cluster

Contains at least one Master node & one or more worker nodes

## Kubernetes Components

### Master Node

Master node contains following components

- kube-apiserver - The only entry point to interact to Kuberenetes cluster from outside. Kubernetes Dashboard or Kubectl commands interact only with kube-apiserver
- kube-controller-manager - Watches pods & ensure creation of new pods if needed to achieve desired state mentioned in configuration
- kube-scheduler - Watches for newly created Pods with no assigned node, and selects a node for deployment
- etcd - key value store which stores all cluster data

### Worker Node

- The worker node host the Pod
- Each workder node can have any number of pods
- Node can be VM or Physical machine

#### Pod

- Pod contains two things mandatorily - Docker runtime & Kubelet
- Kubelet - Agent which runs on every pod in cluster. It monitors Pod's health, Deploy Container application on instruction from Master node & interact with Master node about status
- Docker Runtime - For running the actual our containered application
- Pod is the abstraction above Container instance as we users don't create Container instance in Kuberentes, we only create Pods
