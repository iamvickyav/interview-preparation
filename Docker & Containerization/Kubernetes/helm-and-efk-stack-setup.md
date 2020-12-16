# Setup Guide for Helm & EFK Stack

## Setup Helm in Mac

Helm 3+ version to be installed

Download the latest release (tar file) of Helm from https://github.com/helm/helm/releases

```sh
> tar -zxvf helm-v3.4.2-darwin-amd64.tar.gz
> cd darwin-amd64/
> mv helm /usr/local/bin/helm
```

## Setup EFK Stack in Kubernetes Minikube

Go to https://artifacthub.io/packages/helm/elastic/elasticsearch & follow the instructions

```sh
> helm repo add elastic https://helm.elastic.co
> helm install elasticsearch --version 7.10.1 elastic/elasticsearch
```




