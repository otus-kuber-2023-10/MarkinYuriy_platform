# MarkinYuriy_platform
MarkinYuriy Platform repository
    
 - uploaded to dockerhub nodejs app 
 - nodejs runiing from user node (uid 1001)
 - kubernetes-intro/web/web-pod.yaml contains last web-pod.yaml contain initContainers and volume from HomeWork Task
 - all checked on my minikube

# Выполнено ДЗ №

- [v] Основное ДЗ
- [v] Задание со *

## В процессе сделано:
### Основное ДЗ первая часть 
- создан простой nodejs проект - все что есть в папке /app доступно из браузера на порту 8000
- создан Dockerfile [файл лежит в kubernetes-intro/web/Dockerfile](kubernetes-intro/web/Dockerfile)
- docker build  && push:
  - sudo docker build -t markinyuriy/web:test_2 . ;sudo  docker push markinyuriy/web:test_2
- REMARK в процессе выполнения задания yaml файл несколько раз менялся в соответствии с дз. Опубликован соответственно последний вариант
- создан web-pod.yaml [файл лежит в kubernetes-intro/web/web-pod.yaml](kubernetes-intro/web/web-pod.yaml)
- поправлен key:value    
### Основное ДЗ вторая  часть
- clone Hipster-Shop, build and push docker to dockerhub:
  - git clone https://github.com/GoogleCloudPlatform/microservices-demo
  - cd microservices-demo/src/frontend/
  - sudo docker build -t markinyuriy/hipster-frontend:0.1 . ; docker push markinyuriy/hipster-frontend:0.1
- генерация манифестa:
  - kubectl run frontend --image  markinyuriy/hipster-frontend:0.1 --restart=Never --dry-run=client -o yaml > frontend-pod.yaml
    [файл](/kubernetes-intro/frontend/frontend-pod.yaml) 
- проверяем ччто статус Error
  - kubectl logs frontend
- проверяем лог 
  -  kubectl   logs  frontend 
- panic: environment variable "PRODUCT_CATALOG_SERVICE_ADDR" not set (исправляем в сл пункте со*)

### со *:
- добавляем в соответствии с [ссылкой](https://github.com/GoogleCloudPlatform/microservices-demo/blob/master/kubernetes-manifests/frontend.yaml) недостающте секции в 
 [файл](/kubernetes-intro/frontend/frontend-pod-healthy.yaml)
- удаляем pod:
  - kubectl delete pod frontend
- применяем новый yaml:
  - kubectl apply -f frontend-pod-healthy.yaml
- проверяем что ошибка ушла 
  - kubectl  get  pod frontend
- видим статус Running
### Как запустить проект (первая часть):
- перейти в тетерминале в [папку kubernetes-intro/web/](kubernetes-intro/web)
-  terminal1:
  - kubectl apply -f web-pod.yaml
    - kubectl get pods -w #проверяем статус
  - terminal2:
    - kubectl port-forward --address 0.0.0.0 pod/web 8000:8000


## Как проверить работоспособность основного ДЗ:
- перейти по ссылке http://localhost:8000/index.html - увидим лого курса.
## Как проверить работоспособность ДЗ со *:
- log
  -  kubectl   logs  frontend

  - ....
  {"http.req.id":"3d6d2d82-e57c-4ba4-a45a-0131970ab8da","http.req.method":"GET","http.req.path":"/_healthz","message":"request started","session":"x-liveness-probe","severity":"debug","timestamp":"2023-11-18T17:23:43.70898208Z"}
  {"http.req.id":"3d6d2d82-e57c-4ba4-a45a-0131970ab8da","http.req.method":"GET","http.req.path":"/_healthz","http.resp.bytes":2,"http.resp.status":200,"http.resp.took_ms":0,"message":"request complete","session":"x-liveness-probe","severity":"debug","timestamp":"2023-11-18T17:23:43.709136384Z"}
.........