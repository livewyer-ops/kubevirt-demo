# kubevirt-demo

## Kubernetes Cluster Setup

### Kind Cluster

Setup Local Kubernetes Cluster with Kind Cluster

```
kind create cluster --config examples/kind-cluster/kind-multi-node.yaml
```

### Install Kubevirt's Operator and Custom Resource Definitions

This demo was tested with kubevirt version v0.38.1. You may choose to run `export VERSION=v0.38.1` instead of the export command below.

```
export VERSION=$(curl -s https://api.github.com/repos/kubevirt/kubevirt/releases | grep tag_name | grep -v -- '-rc' | head -1 | awk -F': ' '{print $2}' | sed 's/,//' | xargs)
echo $VERSION
kubectl create -f https://github.com/kubevirt/kubevirt/releases/download/${VERSION}/kubevirt-operator.yaml
kubectl create -f https://github.com/kubevirt/kubevirt/releases/download/${VERSION}/kubevirt-cr.yaml
```

### Install Kubevirt's Containerized Data Importer

This demo was tested with CDI version v1.30.0. You may choose to run `export VERSION=v1.30.0` instead of the export command below.

```
export VERSION=$(curl -s https://github.com/kubevirt/containerized-data-importer/releases/latest | grep -o "v[0-9]\.[0-9]*\.[0-9]*")
kubectl create -f https://github.com/kubevirt/containerized-data-importer/releases/download/$VERSION/cdi-operator.yaml
kubectl create -f https://github.com/kubevirt/containerized-data-importer/releases/download/$VERSION/cdi-cr.yaml
```
