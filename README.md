Launch MySQL on GKE.

https://kubernetes.io/docs/tasks/run-application/run-single-instance-stateful-application/

Modified pvc for GKE.

kubectl create -f mysql-pv.yaml
kubectl create -f mysql-deploy.yaml

```
kubectl run -it --rm --image=mysql:5.6 --restart=Never mysql-client -- mysql -h mysql -ppassword

CREATE USER 'datadog'@'%' IDENTIFIED BY 'dd_pass';
GRANT REPLICATION CLIENT ON *.* TO 'datadog'@'%' WITH MAX_USER_CONNECTIONS 5;
GRANT PROCESS ON *.* TO 'datadog'@'%';
GRANT SELECT ON performance_schema.* TO 'datadog'@'%';
```

```
helm upgrade -f datadog-values.yaml datadog-agent \
--set datadog.env.MYSQLPASS.name=MYSQLPASS \
--set datadog.env.MYSQLPASS.value=dd_pass \
--set datadog.apiKey=<DATADOG_API_KEY> \
stable/datadog
```
