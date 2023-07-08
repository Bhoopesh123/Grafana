# Jira Integration with Grafana
Below Steps will help to integrate Jira with Grafana for Alert Routing for Kubernetes Cluster

# 1. Install Jiralert on ubuntu:
Reference Documentation is as below:  

https://github.com/prometheus-community/jiralert

JIRAlert implements Alertmanager's webhook HTTP API and connects to one or more JIRA instances to create highly configurable JIRA issues. One issue is created per distinct group key — as defined by the group_by parameter of Alertmanager's route configuration section — but not closed when the alert is resolved. The expectation is that a human will look at the issue, take any necessary action, then close it. If no human interaction is necessary then it should probably not alert in the first place. This behavior however can be modified by setting auto_resolve section, which will resolve the jira issue with required state..

Below Steps needs to be followed, currently Jira Alert webhook will be deployed in metrics namespace.
We can change the namespace as well if needed and keep it as same where Grafana is installed and configured.

    cd jiralert
    kubectl apply -f .

To quickly test if JIRAlert is working you can run from any  container with in the same namespace,
Run the following commands which will spin up a new pod from where we will inovke this webhook api:

    kubectl run mycurlpod --image=curlimages/curl -i --tty -- sh

    kubectl exec -it --stdin --tty pod/mycurlpod sh

    curl -H "Content-type: application/json" -X POST \
    -d '{"receiver": "jiralert", "status": "firing", "alerts": [{"status": "firing", "labels": {"alertname": "TestAlert", "key": "value"} }], "groupLabels": {"alertname": "TestAlert"}}' \
    http://jiralert:9097/alert

# 3. Upgrade the Grafana Alert Manager Configuration by below command:

    helm upgrade grafana kube-prometheus-stack/ -f alert-grafana-values.yaml --debug --create-namespace --namespace metrics --timeout 10m --dry-run

# 4. Validate the Alerts and it should be fired in Jira






