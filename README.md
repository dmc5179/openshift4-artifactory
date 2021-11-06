
- Create namespace

```
oc new-project artifactory
```

- Postgresql DB uses the default SA but need more permissions

```
oc adm policy add-scc-to-user anyuid -z default
```

- Artifactory also needs anyuid

```
oc create -f serviceaccounts.yaml
oc adm policy add-scc-to-user anyuid -z artifactory
```

- Deploy Helm Chart

```
helm install artifactory --namespace artifactory --values values.yaml jfrog/artifactory
```

- Expose Artifactory service to cluster external users

```
oc create -f ./routes.yaml
```
