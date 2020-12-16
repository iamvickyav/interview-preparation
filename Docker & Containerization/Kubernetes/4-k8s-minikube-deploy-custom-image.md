# Kubernetes Deploying Image from Local Docker images

## Creating Docker image

**Dockerfile**

```sh
FROM openjdk:8-jre-slim
WORKDIR /home
COPY /target/H2Sample.jar H2Sample.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "H2Sample.jar"]
```

Usually we build docker images using following command

```sh
> mvn clean package

> docker build -t sample-img .
```

If you build the docker image like above, it will create Docker image with Docker runtime in your local system. But if you remember, Docker runtime inside minikube is different from docker runtime outside minikube (aka our local system)

### Deploying our Custom Docker Image in Kubernetes

First lets make the terminal or cmd to point to Docker runtime inside minikube instead of the local Docker instance

```sh
> eval $(minikube docker-env)
```

Then lets build the Docker image

```sh
> mvn clean package

> docker build -t sample-img .
```

### Verify Docker image inside minikube

To verify whether our image built successfully, lets first do `minikube ssh` to log inside minikube & then run `docker images` command

```sh

> minikube ssh

docker@minikube:~$ > docker images
REPOSITORY                                TAG                  IMAGE ID            CREATED             SIZE
sample-img                                   latest               c45c0df88ae8        43 hours ago        226MB
openjdk                                   8-jre-slim           cd08b38dfcae        4 days ago          187MB
kubernetesui/dashboard                    v2.0.1               85d666cddd04        6 months ago        223MB
k8s.gcr.io/kube-proxy                     v1.18.3              3439b7546f29        6 months ago        117MB
k8s.gcr.io/kube-controller-manager        v1.18.3              da26705ccb4b        6 months ago        162MB
k8s.gcr.io/kube-scheduler                 v1.18.3              76216c34ed0c        6 months ago        95.3MB
k8s.gcr.io/kube-apiserver                 v1.18.3              7e28efa976bd        6 months ago        173MB
kubernetesui/metrics-scraper              v1.0.4               86262685d9ab        8 months ago        36.9MB
k8s.gcr.io/pause                          3.2                  80d28bedfe5d        10 months ago       683kB
k8s.gcr.io/coredns                        1.6.7                67da37a9a360        10 months ago       43.8MB
k8s.gcr.io/etcd                           3.4.3-0              303ce5db0e90        13 months ago       288MB
gcr.io/k8s-minikube/storage-provisioner   v1.8.1               4689081edb10        3 years ago         80.8MB
```

We can see sample-img along with other Docker images pulled by minikube to run Kubernetes

### Time for deployment

```sh
> kubectl create deployment sample-depl --image=sample-img
deployment.apps/sample-depl created

> kubectl get pods
NAME                           READY   STATUS         RESTARTS   AGE
sample-depl-5df79fdfdc-62tds   0/1     ErrImagePull   0          11s
```

As you can see the STATUS of the sample-depl-5df79fdfdc-62tds pod is `ErrImagePull` which means the Kubernetes is still trying to download the Docker image from internet (docker hub site). But the sample-img is only available only in local

So we should restrict Kubernetes from attempting to download image from internet.

### Restrict Docker Image Download on Pod creation

```sh
> docker edit deployment sample-img
```

As you know, Docker opens YAML in VIM editor. Change `imagePullPolicy` under template -> spec to `Never`

Once the edit is saved, the pods will run successfully. You can check the same with `get pods`

```sh
> kubectl get pods
```

### Exposing Pods to outside world

In order to hit Pods from outside, they have to be exposed to outside world first. Exposing can be done using Service components

```sh
> kubectl expose deployment sample-depl --type=LoadBalancer --port=8080
service/sample-depl exposed

> minikube tunnel

> kubectl get services
NAME          TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
emp-depl      LoadBalancer   10.104.254.244   127.0.0.1     8080:31807/TCP   43h
kubernetes    ClusterIP      10.96.0.1        <none>        443/TCP          44h
sample-depl   LoadBalancer   10.103.78.221    127.0.0.1     8080:32125/TCP   14s
```

To access the application, try hitting http://localhost:8080

Thats all folks !!!
