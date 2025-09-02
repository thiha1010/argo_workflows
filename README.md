# Argo Workflows with quay.io

## create the quay.io secret
```sh
kubectl create secret docker-registry quay-creds \
  --docker-server=quay.io \
  --docker-username=<USERNAME> \
  --docker-password=<TOKEN>
```
### verify the quay.io secret
```sh
kubectl  get secrets  quay-creds -ojsonpath='{.data.\.dockerconfigjson}' | base64 -d | jq
```

## build the image
```sh
argo submit --watch argo-workflows.yaml \
-p repo-url= https://github.com/xxx/xxx.git \
-p image= quay.io/xxx/xxx
```