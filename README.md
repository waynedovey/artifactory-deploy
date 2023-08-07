# Artifactory Deployment Guide OpenShift

```bash
export MASTER_KEY=$(openssl rand -hex 32)
```

```bash
export JOIN_KEY=$(openssl rand -hex 32)
```

```bash
oc new-project artifactory
```

```bash
kubectl create secret generic my-masterkey-secret -n artifactory --from-literal=master-key=${MASTER_KEY}
```

```bash
kubectl create secret generic my-joinkey-secret -n artifactory --from-literal=join-key=${JOIN_KEY}
```

```bash
oc adm policy add-scc-to-user -z default privileged
```

```bash
helm repo add jfrog https://charts.jfrog.io
```

```bash
helm repo update
```

```bash
#helm upgrade --install artifactory --set artifactory.masterKey=${MASTER_KEY} --set artifactory.joinKey=${JOIN_KEY} --namespace artifactory jfrog/artifactory
```

```bash
helm upgrade --install artifactory --set artifactory.masterKey=${MASTER_KEY} --set artifactory.joinKey=${JOIN_KEY} --namespace artifactory jfrog/artifactory -f values.yaml
```
