# <h1 align="center">:rocket: PropertyGuru Prometheus Server (Metrics Server) 🚀</h1>

## About this Product
This product aims to be the metrics server in PropertyGuru. It will collect and store the metrics in a time series database, managed by Infrastructure Engineering Team. The main purpose or usage for it, for now, is mainly to act as an intemidiary to stream metrics to Datadog. Another feature of our metrics server is to do data massaging, to only send useful and clean data to Datadog.

We are deploying Prometheus on `prometheus-infra` namespace to integrate with other services like `istio`, `kong` and collect metrics from it and forward them to `datadog` as there is no direct integration between these services with `datadog` and there is a need of `prometheus` plugin 

## Service Diagram

![Architecture overview](https://cdn.jsdelivr.net/gh/prometheus/prometheus@c34257d069c630685da35bcef084632ffd5d6209/documentation/images/architecture.svg)

## How to install and run the product

### Prerequisites
​
- Kubernetes 1.21+
- Helm 3.7+
​
we are installing `prometheus` using helm chart which bootstraps a [Prometheus](https://prometheus.io/) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager and with `2` replicas to make sure it is `highly available (HA)`
​
### Get Repository Info
​
```console
git clone https://prometheus-community.github.io/helm-charts
```
### Dependencies
​
Along with this chart installs additional, we are deploying below dependent charts:
​
- [alertmanager](https://github.com/prometheus-community/helm-charts/tree/main/charts/alertmanager)
- [prometheus-node-exporter](https://github.com/prometheus-community/helm-charts/tree/main/charts/prometheus-node-exporter)
- [prometheus-pushgateway](https://github.com/walker-tom/helm-charts/tree/main/charts/prometheus-pushgateway)

### How to deploy Prometheus deployment on a new EKS cluster
​
If we provision a new cluster and want to deploy prometheus on it then we need to checkout the kubernetes repository
- [kubernetes_repo](https://github.com/propertyguru/kubernetes/argocd/infrastructure/prometheus)
need to create an `overlays` using `kustomize`(https://kustomize.io/) similar to the [Karpenter](https://github.com/propertyguru/kubernetes/argocd/infrastructure/karpenter/overlays) by creating a folder with cluster name.
​
