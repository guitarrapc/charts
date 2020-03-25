## charts

## local helm w/o serve

```shell
helm upgrade --install verdaccio ./charts/verdaccio --version 0.7.5 --namespace verdaccio -f ./charts/verdaccio/values.yaml --recreate-pods
helm delete verdaccio --purge
```

## local helm serve

create package.

```shell
helm package ./charts/verdaccio
mkdir -p ./charts
mv ./verdaccio-0.7.5.tgz ./charts/.
```

serve local helm

```
helm serve --repo-path ./charts/
```

install local chart repo

```
helm repo add local http://127.0.0.1:8879/charts
helm repo list
```

deploy

```
helm upgrade --install verdaccio local/verdaccio --version 0.7.5 --namespace verdaccio -f ./charts/verdaccio/values.yaml --recreate-pods
helm delete verdaccio --purge
```

update chart

```
helm package ./charts/verdaccio
mv ./verdaccio-0.7.5.tgz ./charts/.
pushd ./charts && helm repo index charts && popd
```

