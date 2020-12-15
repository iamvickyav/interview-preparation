# Kuberenetes with Azure

## Commands

```sh
az aks get-credentials --resource-group kube-rg --name kubecluster
az aks browse --resource-group kube-rg --name kubecluster
```

```sh
kubectl get services
kubectl get nodes
```

```sh
docker tag e12149882373 iamvickyav/spring-h2-app:v1
docker push iamvickyav/spring-h2-app:v1
```

## Reference

- [Youtube Video for reference](https://www.youtube.com/watch?v=VafY-qfpM8M)

- [Kubernetes Dashboard](https://docs.microsoft.com/en-us/azure/aks/kubernetes-dashboard)

- [Kubernetes Dashboard Reference](https://github.com/kubernetes/dashboard/blob/master/docs/user/accessing-dashboard/README.md)

- [Dashboard URL](http://127.0.0.1:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/#/login)

- [Deployment Steps Reference](youtube.com/watch?v=K4uNl6JA7g8)

- [Kubernetes Deployment YAML](https://docs.cloud.oracle.com/en-us/iaas/developer-tutorials/tutorials/spring-on-k8s/01oci-spring-k8s-summary.htm)
