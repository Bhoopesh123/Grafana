# Tempo
Below Steps will help to install Tempo for Tracing  a sample application 


# 1. Install Loki-Stack  

Install Loki and promtail combined in helm chart which will capture the logs from Nodes and send it to Loki Datasource which will be added as a datasource in Grafana.  

    cd loki-stack
    helm install loki . --namespace observability


# 2. Install Tempo  

Grafana Tempo is an open source, easy-to-use and high-scale distributed tracing backend. Tempo is cost-efficient, requiring only object storage to operate, and is deeply integrated with Grafana, Prometheus, and Loki  

    cd tempo
    helm install tempo . --namespace observability

# 3. Install Kube-Prometheus-Stack  
Reference Documentation is as below:  

https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack

This will installs the kube-prometheus stack, a collection of Kubernetes manifests, Grafana dashboards, and Prometheus rules combined with documentation and scripts to provide easy to operate end-to-end Kubernetes cluster monitoring with Prometheus using the Prometheus Operator.

Below Steps needs to be followed: 

    helm upgrade --install prod prometheus-community/kube-prometheus-stack -n observability --values tempo-config.yaml

# 4. Install Sample Application for ingesting Traces to Grafana  

Below Steps needs to be followed: 

    kubectl apply -f tempo-test-dep.yaml
    kubectl apply -f tempo-test-svc.yamlS



