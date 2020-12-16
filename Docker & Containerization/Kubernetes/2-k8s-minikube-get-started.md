# Minikube

Minikube is used for developing & testing applications in Kubernetes in local

For installation - https://minikube.sigs.k8s.io/docs/start/

Minikube comes with its own Docker Runtime. We don't have to install Docker runtime explicitly

## Minikube Architecture

Usually Kubernetes contains Master & Worker nodes

    Master node contains components like kube-apiserver, kube-controller-manager, kube-scheduler, etcd

    Worker nodes contain Container runtime & Kubelet agent

Minikube contains only one node - combining components of Master & Worker node in a single node

## Start Minikube

To start Kuberenetes with Minikube

```sh
minikube start
```

Kubernetes Dashboard can be opened with Minikube using

```sh
minikube dashboard
```
