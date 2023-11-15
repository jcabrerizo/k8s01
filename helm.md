# Helm notes

Helm learning notes and POC

## Resources

https://www.youtube.com/watch?v=DQk8HOVlumI&t=741s

## Setup environment

### Install `microk8s`

sudo snap install microk8s --classic --channel=1.28
Needing to run `newgrp microk8s` for load the rights

### Install `helm`

<https://helm.sh/docs/intro/install/>
<https://github.com/helm/helm/releases/tag/v3.8.1>

### Install `kubectl`

<https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/>

## Helm 101

### Create the charm

```shell
helm create helloworld
```
```shell
└── helloworld
 ├── charts
 ├── Chart.yaml
 ├── templates
 │   ├── deployment.yaml
 │   ├── _helpers.tpl
 │   ├── hpa.yaml
 │   ├── ingress.yaml
 │   ├── NOTES.txt
 │   ├── serviceaccount.yaml
 │   ├── service.yaml
 │   └── tests
 │       └── test-connection.yaml
 └── values.yaml
```

### Create release
```shell
helm install releaseName helloworld
```

```shell
helm list -a
```
```shell
WARNING: Kubernetes configuration file is group-readable. This is insecure. Location: /home/juan/.kube/config
WARNING: Kubernetes configuration file is world-readable. This is insecure. Location: /home/juan/.kube/config
NAME    NAMESPACE    REVISION    UPDATED                              STATUS   CHART        APP VERSION
helloworld    default   1     2023-11-12 18:17:39.662551547 +0000 UTC    deployed    helloworld-0.1.01.16.0
```

```shell
kubectl get service
```
```shell
NAME      TYPE     CLUSTER-IP    EXTERNAL-IP   PORT(S)     AGE
kubernetes   ClusterIP   10.152.183.1  <none>     443/TCP     69m
helloworld   NodePort 10.152.183.123   <none>     80:30325/TCP   11m
```

Validate deployment, notice the port
```shell
curl http://localhost:30325
```

## Helm commands
List all
```shell
helm list -a
```
```shell
helm uninstall helmDir
```

### Validating helm chart
Interaction with the actual k8s cluster
```shell
helm install releaseName –debug –dry-run helmDir
```
Validating only the ymls
```shell
helm template
```
Run linter
```shell
helm lint
```