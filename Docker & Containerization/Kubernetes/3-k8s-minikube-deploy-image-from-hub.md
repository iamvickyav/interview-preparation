# Kubernetes Deploying Image from Docker Hub

### Deployment Steps

#### Deploying Tomcat Image in Kubernetes

```sh
> minikube start

> kubectl create deployment tomcat-depl --image=tomcat:8.5.21-jre8-alpine
deployment.apps/tomcat-depl created
```

#### Verify status of deployment, pod & service

```sh
# To show list of deployments done. Ready state 1 means deployment is success
> kubectl get deployments
NAME          READY   UP-TO-DATE   AVAILABLE   AGE
tomcat-depl   1/1     1            1           71s

# To get information about pods running. Ready state 1 means container instance inside pod is running successfully
> kubectl get pods
NAME                          READY   STATUS    RESTARTS   AGE
tomcat-depl-968b6f4f7-rplt5   1/1     Running   0          7s

# To get information about services running. By default kubernetes cluster runs
> kubectl get services
NAME         TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
kubernetes   ClusterIP      10.96.0.1        <none>        443/TCP          34h

# To get IP Address Details of Pod
> kubectl get pods -o wide
NAME                          READY   STATUS    RESTARTS   AGE     IP           NODE       NOMINATED NODE   READINESS GATES
tomcat-depl-968b6f4f7-rplt5   1/1     Running   0          5m51s   172.18.0.5   minikube   <none>           <none>

# To get detailed information about Pod
> kubectl describe pod tomcat-depl
```

#### To increase instance of Tomcat containers

Using the `kubectl edit` command open the YAML in VIM editor. Modify the number of replicas under the spec section with VIM editor & save the file

```sh
> kubectl edit deployment tomcat-depl
deployment.apps/tomcat-depl edited
```

Once save is done, Kubernetes will create new pods to match the replicas changed in YAML file. You can verify instance count using `kubectl get pods` command

```sh
> kubectl get pods
NAME                          READY   STATUS    RESTARTS   AGE
tomcat-depl-968b6f4f7-fg5mt   1/1     Running   0          101s
tomcat-depl-968b6f4f7-rplt5   1/1     Running   0          15m
```

### Exposing Tomcat pods outside of Kubernetes Cluster

Pods can be exposed to outside world using `kubectl expose` command. Expose commands creates Kubenertes components called service.

Service has it own static IP & it can do load balancing also. To use Load Balancer, use the type as LoadBalancer. `--port` specifies from which port you want to access the service from outside of cluster

```sh
> kubectl expose deployment tomcat-depl --type=LoadBalancer --port=8080
service/tomcat-depl exposed
```

Once we create Kubernetes service, we can get the external IP using `kubectl get service`

When we run `kubectl get service` command, we could have noticed that EXTERNAL-IP section is pending state

```sh
> kubectl get services
NAME          TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
kubernetes    ClusterIP      10.96.0.1        <none>        443/TCP          34h
tomcat-depl   LoadBalancer   10.108.215.217   <pending>     8080:31072/TCP   2m10s
```

Reason being, minikube needs to start tunnel to get the EXTERNAL-IP

```sh
> minikube tunnel

> kubectl get services
NAME          TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
kubernetes    ClusterIP      10.96.0.1        <none>        443/TCP          34h
tomcat-depl   LoadBalancer   10.108.215.217   127.0.0.1     8080:31072/TCP   2m10s
```

You can see the EXTERNAL-IP as 127.0.0.1 now in `kubectl get services` command

Time to access Tomcat using http://127.0.0.1:8080
