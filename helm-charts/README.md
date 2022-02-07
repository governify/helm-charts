# Governify Helm Charts

## Installation
Governify Kubernetes implementation consists in a set of services embedded in Helm charts, which are used by infrastructure charts as dependencies in order to deploy each system with custom configuration.

### Production

1. Create Namespace
```
$    kubectl create namespace <namespace>
```

2. Install Contour
```
$    kubectl apply -f https://projectcontour.io/quickstart/contour.yaml
```

3. Wait a few minutes and get the Load Balancer IP Address
```
$    (kubectl get -n projectcontour service envoy -o json) | jq -r '.status.loadBalancer.ingress[0].ip'
```

4. Install CertManager
```
$    kubectl apply -f https://github.com/jetstack/cert-manager/releases/download/v1.1.0/cert-manager.yaml
```

5. Create a values.yaml file with the following content
```
    global:
        node_env: production
        gov_infrastructure: <assets_call_to_infrastructure.yaml>
    
    assets_manager:
        assets_repository: <repository_url>
        assets_repository_branch: <branch>
        login_user: <username>
        login_password: <password>
    
    render:
        login_user: <username>
        login_password: <password>
```

6. Install charts
```
$    helm repo add governify https://governify.github.io/helm-charts
$    helm repo update
$    helm install -f values.yaml <release_name> governify/<chart_name>
```

### Development - local

1. Create Namespace
```
$    kubectl create namespace <namespace>
```

2. Create a values.yaml file with the following content
```
    global:
        node_env: development
        gov_infrastructure: <assets_call_to_infrastructure-local.yaml>
    
    assets_manager:
        gov_infrastructure: <local_path_to_infrastructure-local.yaml>
        assets_repository: <repository_url>
        assets_repository_branch: <branch>
        login_user: <username>
        login_password: <password>
    
    render:
        login_user: <username>
        login_password: <password>
```

3. Install charts
```
$    helm repo add governify https://governify.github.io/helm-charts
$    helm repo update
$    helm install -f values.yaml <release_name> governify/<chart_name>
```