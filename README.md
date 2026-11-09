# platform_services
Platform Services

## Istio (via Helm)
- Istio Base
- Istiod
- Istio Ingress
- Must be enabled for each namespace
    - `kubectl label namespace <namespace> istio-injection=enabled`