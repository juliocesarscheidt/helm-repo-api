## Docker

```bash

docker image pull juliocesarmidia/http-simple-api:latest

docker container run --rm -d \
  -p 9000:9000 \
  --env API_PORT=9000 \
  --name http-simple-api \
  juliocesarmidia/http-simple-api:latest

docker container logs -f http-simple-api

curl -X GET --silent "http://localhost:9000"
# hello world

docker container rm -f http-simple-api

```

## Helm Local

```bash

# install with a different tag
helm upgrade -i -n default helm-repo-api-v1 ./charts/helm-repo-api/ --set image.tag="v2.0.0"

# install with custom values
helm upgrade -i -n default helm-repo-api-v1 ./charts/helm-repo-api/ --values custom-values.yaml

# dry run install
helm upgrade -i --dry-run --debug -n default helm-repo-api-v1 ./charts/helm-repo-api/

# default install
helm upgrade -i -n default helm-repo-api-v1 ./charts/helm-repo-api/


helm ls -n default
kubectl get deploy,pod,svc -n default

kubectl logs -f deployment.apps/helm-repo-api-v1 -n default


SVC_IP="$(kubectl get service/helm-repo-api-v1 -n default --no-headers | tr -s ' ' ' ' | cut -d' ' -f3)"
echo "${SVC_IP}"

curl -X GET --silent "http://${SVC_IP}:9000"


helm uninstall -n default helm-repo-api-v1

```

## Helm Repo Github Pages

```bash
#

helm repo add juliocesarscheidt https://juliocesarscheidt.github.io/helm-repo-api

helm repo update
helm search repo juliocesarscheidt

helm install helm-repo-api-v1 juliocesarscheidt/helm-repo-api -n default


SVC_IP="$(kubectl get service/helm-repo-api-v1 -n default --no-headers | tr -s ' ' ' ' | cut -d' ' -f3)"
echo "${SVC_IP}"

curl -X GET --silent "http://${SVC_IP}:9000"


helm uninstall -n default helm-repo-api-v1

```
