# Postgres

```bash
k apply -f pg-pv.yml
k apply -f pg-namespace.yml
k apply -n postgres -f pg-pvc.yml
k apply -n postgres -f pg-secret.yml
k apply -n postgres -f pg-service.yml
k apply -n postgres -f pg-deployment.yml

```
