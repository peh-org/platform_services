# platform_services
Platform Services

## About
- Deploy services needed for Platform
    - base (namespaces, PV, ClusterSecretStore)
    - istio
    - openbao
    - ExternalSecretsOperator
    - Secrets (create k8s resources)
    - Postgres & Keycloak (paired because Keycloak uses Postgres DB)

## Istio (via Helm)
- Istio Base
- Istiod
- Istio Ingress
- Must be enabled for each namespace
    - `kubectl label namespace <namespace> istio-injection=enabled`

## OpenBao and ESO
- Store secrets in OpenBao server
    - `bao kv put -mount=secret postgres/keycloakuser password=<password>`
        - password for keycloakuser in postgres
    - `bao kv put -mount=secret postgres/admin password=<postgres-password>`
        - postgres admin password
    - `bao kv put -mount=secret keycloak/admin password=<postgres-password>`
        - keycloak admin password
- ESO extracts and injects secrets into cluster

## Postgres
- Installed postgres OCIRelease
- to connect to running pod and check DB
    - `kubectl exec --stdin --tty -n keycloak pods/keycloak-postgres-postgresql-0 -- /bin/sh`
    - `psql -U <username> -d <db_name>` then prompted for password
    - `select 1;`
        - Should return: ?column? | 1
- 

## Keycloak (NOT Keycloak Operator)
- Installed via HelmRelease
- uses postgres db
- `kubectl port-forward svc/keycloak-keycloak-keycloakx-http -n keycloak 8081:80`