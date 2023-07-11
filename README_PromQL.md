# Basic PromQL Queries for understanding the Time Series Data for at any Instant Time:

    1. To search all of the time series data points in your dashboard, run the following query  
        count({__name__=~".+"}) by (__name__)

    2. To Search all of the time series data points grouping by job
        count({__name__=~".+"}) by (job)

    4. To Search all of the time series data points grouping by metric for any particular job
        count({__name__=~".+",job="node-exporter"}) by (__name__)

    5. To search for a specific time series point, add the relevant value to the query:
        {__name__=~"node.+"}

    6. Searching a label inside a time series changes the query. You need to add the name of the time series, and the value you’re looking for:
        kube_configmap_labels{namespace="metrics"}
        kube_configmap_labels{namespace=~"met.+"}

# Range Vector Selectors:
Range vector literals work like instant vector literals, except that they select a range of samples back from the current instant.
Syntactically, a time duration is appended in square brackets ([]) at the end of a vector selector to specify how far back in time values should be fetched for each resulting range vector element.

rate(v range-vector) calculates the per-second average rate of increase of the time series in the range vector  

    rate(kubelet_http_requests_total{job="kubelet"}[$__rate_interval])

# Reference Documentation for other Functions:
    https://prometheus.io/docs/prometheus/latest/querying/functions
