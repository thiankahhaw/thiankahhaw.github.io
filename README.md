Prometheus, a `Cloud Native Computing Foundation` project, is a systems and service monitoring system. It collects metrics from configured targets at given intervals, evaluates rule expressions, displays the results, and can trigger alerts when specified conditions are observed.
​
The features that distinguish Prometheus from other metrics and monitoring systems are:
​
* A multi-dimensional data model (time series defined by metric name and set of key/value dimensions)
* PromQL, a powerful and flexible query language to leverage this dimensionality
* No dependency on distributed storage; single server nodes are autonomous
* An HTTP pull model for time series collection
* Pushing time series is supported via an intermediary gateway for batch jobs
* Targets are discovered via service discovery or static configuration
* Multiple modes of graphing and dashboarding support
* Support for hierarchical and horizontal federation
​
## Architecture overview
​
![Architecture overview](https://cdn.jsdelivr.net/gh/prometheus/prometheus@c34257d069c630685da35bcef084632ffd5d6209/documentation/images/architecture.svg)
​
## Prerequisites
​
- Kubernetes 1.21+
- Helm 3.7+
​
we are installing `prometheus` using helm chart which bootstraps a [Prometheus](https://prometheus.io/) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager and with `2` replicas to make sure it is `highly available (HA)`
​
## Get Repository Info
​
```console
git clone https://prometheus-community.github.io/helm-charts
```
## Dependencies
​
Along with this chart installs additional, we are deploying below dependent charts:
​
- [alertmanager](https://github.com/prometheus-community/helm-charts/tree/main/charts/alertmanager)
- [prometheus-node-exporter](https://github.com/prometheus-community/helm-charts/tree/main/charts/prometheus-node-exporter)
- [prometheus-pushgateway](https://github.com/walker-tom/helm-charts/tree/main/charts/prometheus-pushgateway)
​
## Purpose - Why we are deploying Prometheus
​
We are deploying Prometheus on `prometheus-infra` namespace to integrate with other services like `istio`, `kong` and collect metrics from it and forward them to `datadog` as there is no direct integration between these services with `datadog` and there is a need of `prometheus` plugin 
​
### How to deploy Prometheus deployment on a new EKS cluster
​
If we provision a new cluster and want to deploy prometheus on it then we need to checkout the kubernetes repository
- [kubernetes_repo](https://github.com/propertyguru/kubernetes/argocd/infrastructure/prometheus)
need to create an `overlays` using `kustomize`(https://kustomize.io/) similar to the [Karpenter](https://github.com/propertyguru/kubernetes/argocd/infrastructure/karpenter/overlays) by creating a folder with cluster name.
​
