## Random collections of useful commands

### GIT
```sh
git submodule add
git submodule update --init --recursive
```

### Kubernetes
```yaml
# Copy /tmp/foo_dir local directory to /tmp/bar_dir in a remote pod in the default namespace
kubectl cp /tmp/foo_dir <some-pod>:/tmp/bar_dir

# Copy /tmp/foo local file to /tmp/bar in a remote pod in a specific container
kubectl cp /tmp/foo <some-pod>:/tmp/bar -c <specific-container>

# Copy /tmp/foo local file to /tmp/bar in a remote pod in namespace <some-namespace>
kubectl cp /tmp/foo <some-namespace>/<some-pod>:/tmp/bar

# Copy /tmp/foo from a remote pod to /tmp/bar locally
kubectl cp <some-namespace>/<some-pod>:/tmp/foo /tmp/bar
```

### PostgresSQL
```postgres
psql -U postgres -d db_name < file_name.sql
pg_dump -U postgres db_name > /tmp/file_name.sql
SELECT * FROM pg_stat_activity WHERE state = 'active';
SELECT pg_cancel_backend(10296)
SELECT pg_terminate_backend(10296)
SELECT pg_size_pretty(pg_total_relation_size('table_name'))
```

### Consul
```sh
NAMESPACE="namespace"  
# Add repo
helm repo add hashicorp https://helm.releases.hashicorp.com  
# Verify
helm search repo hashicorp/consul  
# Install helm
helm install consul hashicorp/consul --set global.name=consul --create-namespace --namespace $NAMESPACE --values values.yaml
# Upgrade Consul helm
helm upgrade consul hashicorp/consul --namespace $NAMESPACE --values values.yaml
# Get Consul token
kubectl get secrets/consul-bootstrap-acl-token -n $NAMESPACE --template='{{.data.token | base64decode }}'
```
