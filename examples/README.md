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
kubectl create -f examples/redis/master-controller.yml
kubectl create -f examples/redis/master-service.yml
kubectl create -f examples/redis/slave-controller.yml
kubectl create -f examples/redis/slave-service.yml
```

## Docker registry

```
kubectl create -f examples/registry/master-controller.yml
kubectl create -f examples/registry/master-service.yml
```

## Guestbook App

```
kubectl create -f examples/guestbook/frontend-controller.yml
kubectl create -f examples/guestbook/frontend-service.yml
```

## Ruby With Redis Example App

You need to have both Redis and Docker registry pods running.

```
vagrant ssh node-01
cd /tmp
git clone https://github.com/RichardKnop/sinatra-redis-blog.git
cd sinatra-redis-blog
docker build -t ruby-redis-app
docker tag ruby-redis-app registry-master/ruby-redis-app
docker push 10.100.129.115:5000/registry-master/ruby-redis-app
```

You can find the registry ip by running `kubectl get services`.

## Cleanup

```
kubectl stop rc -l "name in (registry-master, redis-master, redis-slave, guestbook-frontend, ruby-redis-app)"
kubectl delete service -l "name in (registry-master, redis-master, redis-slave, guestbook-frontend, ruby-redis-app)"
```
