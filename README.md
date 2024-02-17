
# 1. Install Kube-Prometheus-Stack  
Reference Documentation is as below:  

https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack

This will installs the kube-prometheus stack, a collection of Kubernetes manifests, Grafana dashboards, and Prometheus rules combined with documentation and scripts to provide easy to operate end-to-end Kubernetes cluster monitoring with Prometheus using the Prometheus Operator.

Below Steps needs to be followed: 

    helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
    helm repo update
    helm upgrade --install grafana  prometheus-community/kube-prometheus-stack -n metrics

# 2. Install Process Exporter via Helm Chart  
Below Steps will help to install Process Exporter and link it to the Cluster. 

    helm upgrade --install process prometheus-process-exporter/ --debug --create-namespace --namespace metrics --timeout 10m --dry-run

    helm upgrade --install process prometheus-process-exporter/ --debug --create-namespace --namespace metrics --timeout 10m 

# 3.Check the metrics on Grafana 
To Search all of the time series data points grouping by job  
To Findout how many processes have been started under metrics namespace

        count({__name__=~".+"}) by (job)
        process_start_time_seconds{namespace="metrics"}
