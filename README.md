# Liquibase playground

Place where test and validate usage of the Liquibase.

## Cluster with k3d

`k3d cluster create playground --agents 2`

## Liquibase on K8s

Requirements:
* postgres DB

Nice to have:
* running application

## Scenario one: Manual run

Access DB directly.

1. Create cluster
2. Create postgres: `k apply -k base/postgres`
3. Port forward: `k -n postgres port-forward svc/postgres 5432`
4. Run liquibase: `liquibase update`

## Scenario two: Init containers

Setup init container.
This requires app to be setup as well. Ingress for too.


## Scenario three: Liquibase job

Setup liquibase job.
