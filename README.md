# kubecon-2025-more-data-plaease-hands-on-green-cloud-experiments

## Commands

```
kubectl create ns kepler

# prometheus setup
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update

helm install prometheus prometheus-community/kube-prometheus-stack \
    --namespace monitoring \
    --create-namespace \
    --wait

# kepler
helm repo add kepler https://sustainable-computing-io.github.io/kepler-helm-chart
helm repo update

helm install kepler kepler/kepler \
    --namespace kepler \
    --create-namespace \
    --set serviceMonitor.enabled=true \
    --set serviceMonitor.labels.release=prometheus \

# google microservice
helm upgrade onlineboutique oci://us-docker.pkg.dev/online-boutique-ci/charts/onlineboutique \
    --install
```