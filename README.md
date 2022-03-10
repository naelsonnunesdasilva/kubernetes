# Projeto de estudo de Kubernetes

## Estrutura básica de arquivos .yaml
```
apiVersion: qual é o grupo que eu quero usar
kind: O tipo de objeto
metadata: dados do objeto como por exemplo name
spec: especificações como por exemplo o container e a imagem do container
```

### Comandos e ferramentas

#### Comando para criar o cluster
k3d cluster create meucluster --no-lb
k3d cluster create meucluster --servers 3 --agents 3
servers são os control plane e os agntes os workers node
#### Checar clusters
kubectl get nodes

#### listar
K3d cluster list

#### deletar
k3d cluster delete

#### ver versão de elemento
kubectl api-resources

==========================================
### POD é nele que executamos o container

#### criar cluster a partir de arquivo manifest
kubectl create -f pod.yaml

#### listar pods
kubectl get pods

#### descrição
kubectl describe pod meupod

#### colocar em uma porta
kubectl port-forward pod/meupod 8080:80

#### deletar pod
kubectl delete pod meupod

precisa de um controlador para evitar que morra

#### criar cluster a partir de arquivo manifest
kubectl apply -f pod.yaml

=====================================
### ReplicaSet
Função ter a quantidade replicas de um pod ativa

#### Criar/ atualizar
kubectl apply -f replicaset.yaml

#### Listar
kubectl get replicaset

#### escalar
kubectl scale replicaset meureplicaset --replicas 10

======================================
### Deployment

funciona acima do ReplicaSet gerenciando a atualização gradativa

#### trocar imagem
kubectl set image deployment meudeployment web=kubedevio/web-page:green

#### histórico
kubectl rollout history deployment meuployment

#### voltar versão (rollback)
kubectl rollout undo deployment meuployment

======================================
### Services

Responsável por expor os pods

Tipos de services

-ClusterIP
-NodePort
-LoadBalancer

#### usar

docker container ls (para listar)
docker inspect (para ver detalhes e pegar o ip)
kubectl get service (pegar porta)

===================================
Bind de porta

k3d cluster create --agents 3 --servers 3 -p "8080:30000@loadbalancer"