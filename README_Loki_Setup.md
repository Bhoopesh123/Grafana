# Loki
Below Steps will help to install Loki for collecting logs from cluster and sending it to Grafana for Analysis

# 1. Install Kube-Prometheus-Stack on ubuntu:
Configure the already installed or do a fresh installation with below command.  

    helm upgrade --install prod prometheus-community/kube-prometheus-stack -n monitoring --values grafana-config.yaml

# 2. Install Promtail  
Install Promtail which collects the logs from all nodes by below commands:  

    helm repo add grafana https://grafana.github.io/helm-charts
    helm repo update
    helm upgrade --install promtail grafana/promtail --values promtail-config.yaml -n monitoring

# 3. Install Loki  
Loki's job is to collect the logs from Promtail and forward them to Grafana.  

    helm upgrade --install loki grafana/loki-distributed -n monitoring

# 4. Validate the logs on Grafana:
Login to Grafana by below port-forwarding: 

    kubectl port-forward service/prod-grafana -n monitoring 3000:80
