# Liquibase playground

POC for k8s and liquibase.

## Cluster with k3d

`k3d cluster create -p "9999:80@loadbalancer" playground`

## Liquibase on K8s

Requirements:
* postgres DB
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

1. Deploy postgres : `k apply -k base/postgres`
2. deploy app: `k -n app apply -k base/app`
3. Try: `http POST localhost:9999/echo msg="hello ddd"` ==> 200
4. Try: `http POST localhost:9999/counter` ==> `"msg": "pq: relation \"counters\" does not exist"`
5. Apply overlay with init containers: `k -n app apply -k overlays/app`
6. try 4

## Scenario three: Liquibase job

Setup liquibase job.

1. Deploy postgres: `k apply -k base/postgres`
2. Deploy app: `k -n app apply -k base/app`
3. Try: `http POST localhost:9999/echo msg="hello ddd"` ==> 200
4. Try: `http POST localhost:9999/counter` ==> `"msg": "pq: relation \"counters\" does not exist"`
5. Apply overlay with job: `k -n app apply -k overlays/liquibase`
6. Try 4.

Shield: [![CC BY 4.0][cc-by-shield]][cc-by]

This work is licensed under a
[Creative Commons Attribution 4.0 International License][cc-by].

[![CC BY 4.0][cc-by-image]][cc-by]

[cc-by]: http://creativecommons.org/licenses/by/4.0/
[cc-by-image]: https://i.creativecommons.org/l/by/4.0/88x31.png
[cc-by-shield]: https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg