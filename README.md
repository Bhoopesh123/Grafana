# Grafana
GBelow Steps will help to create a Grafana using Kube-Prometheus-Stack Operator

# 1. Install Kube-Prometheus-Stack on ubuntu:
Reference Documentation is as below:  

https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack

This will installs the kube-prometheus stack, a collection of Kubernetes manifests, Grafana dashboards, and Prometheus rules combined with documentation and scripts to provide easy to operate end-to-end Kubernetes cluster monitoring with Prometheus using the Prometheus Operator.

Below Steps needs to be followed:

    helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
    helm repo update
    helm install grafana prometheus-community/kube-prometheus-stack

    or you can install with the below command

    helm pull prometheus-community/kube-prometheus-stack --untar=true

    helm install prod kube-prometheus-stack/ --debug --create-namespace --namespace metrics --timeout 10m --dry-run
    kubectl config set-context --current --namespace=metrics

# 2. Change the Default Login Password of Grafana  

Change the adminPassword under kube-prometheus-stack folder section inside values.yaml  

      grafana.adminPassword: xxxx

      helm upgrade prod kube-prometheus-stack/ --debug --create-namespace --namespace metrics --timeout 10m

# 3. Import Node Exporter Full Dashboard  

Reference Documentation:
https://grafana.com/grafana/dashboards/1860-node-exporter-full/  






