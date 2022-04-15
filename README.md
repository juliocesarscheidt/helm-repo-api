

docker image pull juliocesarmidia/http-simple-api:latest

docker container run --rm -d \
  -p 9000:9000 \
  --env API_PORT=9000 \
  --name http-simple-api \
  juliocesarmidia/http-simple-api:latest

docker container logs -f http-simple-api

curl http://localhost:9000
# hello world

docker container rm -f http-simple-api


--values custom-values.yaml
helm upgrade -i -n default helm-repo-api ./charts/helm-repo-api/ --set image.tag="v2.0.0"

helm upgrade -i -n default helm-repo-api ./charts/helm-repo-api/ --values custom-values.yaml


helm upgrade -i --dry-run --debug -n default helm-repo-api ./charts/helm-repo-api/

helm upgrade -i -n default helm-repo-api ./charts/helm-repo-api/


helm ls -n default
kubectl get deploy,pod,svc -n default

kubectl logs -f deployment.apps/helm-repo-api -n default

SVC_IP="$(kubectl get service/helm-repo-api -n default --no-headers | tr -s ' ' ' ' | cut -d' ' -f3)"
echo "${SVC_IP}"


curl -X GET --silent "http://${SVC_IP}:9000"


helm uninstall -n default helm-repo-api



cd charts
tar -czvf helm-repo-api-0.0.1.tgz ./helm-repo-api
helm repo index .



helm repo add helm-repo-api https://juliocesarscheidt.github.io/helm-repo-api

