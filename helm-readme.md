# Helm

## Install helm 
```
wget https://get.helm.sh/helm-v3.5.3-linux-amd64.tar.gz
tar -xzvf helm-v2.11.0-linux-amd64.tar.gz
sudo mv linux-amd64/helm /usr/local/bin/helm
```


## Initialize Helm

```
helm repo add stable https://charts.helm.sh/stable
helm search repo stable
```


## Install an Example Chart

```
helm repo update
helm install stable/mysql --generate-name
```

### Connect to above msql
```
kubectl port-forward svc/mysql-???? 3306
````

In another window 
```
MYSQL_ROOT_PASSWORD=$(kubectl get secret --namespace default <mysql-???> -o jsonpath="{.data.mysql-root-password}" | base64 --decode; echo)
MYSQL_HOST=127.0.0.1
MYSQL_PORT=3306

mysql -h ${MYSQL_HOST} -P${MYSQL_PORT} -u root -p${MYSQL_ROOT_PASSWORD}
```

## Test it with redis

```
helm repo add stable https://charts.helm.sh/stable --force-update
helm install myredis stable/redis

-- get password
export REDIS_PASSWORD=$(kubectl get secret --namespace default myredis -o jsonpath="{.data.redis-password}" | base64 --decode)

-- Use Redis CLI to connect to cluster
redis-cli -h myredis-master -a $REDIS_PASSWORD

>help
>SET mykey myvalue
>GET mykey
>exit

-- check how much memory pods are taking
docker stats

kubectl get pods

-- remove redis
helm delete myredis

kubectl get pods
kubectl get svc
```

