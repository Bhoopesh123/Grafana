# SMTP Configuration using Gmail
Below Steps will help to configure Gmail SMTP Server to send emails to mailboxes. 


# 1. Install Kube-Prometheus-Stack  
Reference Documentation is as below:  

https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack

This will installs the kube-prometheus stack, a collection of Kubernetes manifests, Grafana dashboards, and Prometheus rules combined with documentation and scripts to provide easy to operate end-to-end Kubernetes cluster monitoring with Prometheus using the Prometheus Operator.

Below Steps needs to be followed: 

    helm upgrade --install prod prometheus-community/kube-prometheus-stack -n metrics 

# 2. Configure Kube-Prometheus-Stack  with GMAIL SMTP Server

Below Steps needs to be followed: 

    helm upgrade --install prod prometheus-community/kube-prometheus-stack -n metrics --values smtp-values.yaml



