# Governify Helm Charts

[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/governify)](https://artifacthub.io/packages/search?repo=governify)
[![Release Charts](https://github.com/governify/helm-charts/actions/workflows/helm.yaml/badge.svg)](https://github.com/governify/helm-charts/actions/workflows/helm.yaml)

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
        services_prefix: .<infrastructure-prefix>
        dns_suffix: .<your-DNS-zone>
        login_user: <username>
        login_password: <password>
    
    assets_manager:
        assets_repository: <repository_url>
        assets_repository_branch: <branch>
        private_key: test-key
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

2. Configure kubernetes for assigning NodePorts in range (3000-9000) by adding `--service-node-port-range=3000-6000` to the kubernetes kube-apiserver config file. If using docker-desktop [check this page](https://stackoverflow.com/questions/64758012/location-of-kubernetes-config-directory-with-docker-desktop-on-windows).

3. Create a values.yaml file with the following content
```
    global:
        node_env: development
        gov_infrastructure: <assets_call_to_infrastructure-local.yaml>
        login_user: <username>
        login_password: <password>

    assets-manager:
        gov_infrastructure: <local_path_to_infrastructure-local.yaml>
        assets_repository: <repository_url> (defaults to current assets repository inside github governify organization)
        assets_repository_branch: <branch> (default: main)
```

4. Install charts
```
$    helm repo add governify https://governify.github.io/helm-charts
$    helm repo update
$    helm install -f values.yaml <release_name> governify/<chart_name>
```