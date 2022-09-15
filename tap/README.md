# Setup

## Secrets

There are a number of secrets which need to be created which aren't stored in this repo, because who puts passwords in a public GitHub repo?

Anyway, choose your own string adventure here:

```shell
kubectl create secret generic catalog-mongo-pass --from-literal password=NotSecure
kubectl create secret generic cart-redis-pass --from-literal password=NotSecure
kubectl create secret generic order-postgres-pass --from-literal password=NotSecure
kubectl create secret generic users-mongo-pass --from-literal password=NotSecure
kubectl create secret generic users-redis-pass --from-literal password=NotSecure
```

## Databases

There are a number of databases in the `../kubernetes-manifests` directory. These need to be set up before the workloads are applied. Generally, these consist of a data loading configmap and then a deployment + service to run the database. Apply these as:

```shell
for x in kubernetes-manifests/*-db-initdb-configmap.yaml; do kubectl apply -f $x; done
for x in kubernetes-manifests/*-db-total.yaml; do kubectl apply -f $x; done
for x in kubernetes-manifests/*-redis-total.yaml; do kubectl apply -f $x; done
```