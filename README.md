# Controller Deploy
```
helm repo add presslabs https://presslabs.github.io/charts
helm install presslabs/mysql-operator --name mysql-operator
```

# Remove Mysql Operator  completely from k8s cluster to do a fresh deploy

```
helm -n <namespace> delete <operator-release>
kubectl delete -f https://raw.githubusercontent.com/presslabs/mysql-operator/master/mysql.presslabs.org_mysqlbackups.yaml
kubectl delete -f https://raw.githubusercontent.com/presslabs/mysql-operator/master/mysql.presslabs.org_mysqlclusters.yaml 
kubectl delete -f https://raw.githubusercontent.com/presslabs/mysql-operator/master/mysql.presslabs.org_mysqldatabases.yaml 
kubectl delete -f https://raw.githubusercontent.com/presslabs/mysql-operator/master/mysql.presslabs.org_mysqlusers.yaml
```
# Deploy mysql-cluster
```
# remote
kubectl apply -f https://raw.githubusercontent.com/presslabs/mysql-operator/master/examples/example-cluster-secret.yaml
kubectl apply -f https://raw.githubusercontent.com/presslabs/mysql-operator/master/examples/example-cluster.yaml
```
```
# local
kubectl apply -f deploy-cluster/example-cluster-secret.yaml 
kubectl apply -f deploy-cluster/example-cluster.yaml
```
## List the deployed clusters use
```
kubectl get mysql
```
## Check cluster state use
```
kubectl describe mysql my-cluster
```
# Backups use rclone
**GCS_SERVICE_ACCOUNT_JSON_KEY and GCS_PROJECT_ID must be base64 encoded.**
## Setup a backup on S3
```
kubectl apply -f ./backup-cluster/example-s3-secret.yaml
```

## Setup a backup on google-cloud
```
kubectl apply -f ./backup-cluster/example-google-cloud-secret.yaml
```
## Requesting a backup
```
kubectl apply -f example-backup.yaml
```


## Listing all backups
```
kubectl get mysqlbackup
```

## Checking the backup state
```
kubectl describe backup my-cluster-backup
```
