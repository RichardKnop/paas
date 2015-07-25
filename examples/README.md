# Examples

First, spin up the cluster:

```
cd ../

export KUBERNETES_VERSION=1.0.1
export NODE_MEM=1024
export MASTER_MEM=512
export NODE_CPUS=1
export MASTER_CPUS=1
export NUM_INSTANCES=1
export FLEETCTL_ENDPOINT=http://172.17.8.101:4001
export KUBERNETES_MASTER=http://172.17.8.101:8080

vagrant up
```

## Redis

```
kubectl create -f examples/redis/redis-master-controller.yaml
kubectl create -f examples/redis/redis-master-service.yaml
kubectl create -f examples/redis/redis-slave-controller.yaml
kubectl create -f examples/redis/redis-slave-service.yaml
```

## Ruby With Redis Example App

TODO
