# Kubernetes: Pods, Services e ConfigMaps #

## 02. Criando o cluster ##

Obter nós:

``kubectl get nodes``

## 03. Criando e entendendo pods ##

### Criando um pod ###

``kubectl run nginx-pod --image=nginx:latest``

nginx-pod = nome do pod

### Listar pods do cluster ###

``kubectl get pods``

Flags:

- --watch = Acompanha o comando em tempor real
- -o wide = ver o ip na lista

### Ver informações de um Pod específico ###

``kubectl describe pod <nome_do_pod>``

### Editar um pod ###

``kubectl edit pod <nome_do_pod>``

### Criando PODS de maneira declarativa ###

Usando o arquivo .yaml

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: primeiro-pod-declarativo
spec:
  containers:
    - name: nginx-container
      image: nginx:latest
```

Para executar o arquivo:

``kubectl apply -f <arquivo_yaml>``

### Remover um POD ###

``kubectl delete pod <nome_do_pod>``

Flags

- -f arquivo.yaml = apaga o pod pelo arquivo de criação yaml
- --all = remove todas as pods

### Executar comandos no POD ###

``kubectl exec -it  <nome_do_pod> -- bash``

### Criar um serviço ###

Exemplo de arquivo .yaml

```yaml
apiVersion: v1
kind: Service
metadata:
  name: svc-pod-2
spec:
  type: ClusterIP
  selector:
    app: segundo-pod
  ports:
    - port: 9000
      targetPort: 80
```

Comando para executar

``kubectl apply -f <arquivo_yaml>``

### Replica set ###

Serve pra substituir um pod quando ele morre

Verificar replicasets:

``kubectl get replicasets``

### Deployments ###

``kubectl get deployments``
``kubectl delete deploy <nome_deployment>``

Para ver alterações na nossa POD (VCS)

``kubectl rollout history deployment <nome_deployment>``

``kubectl annotate deployment <nome_deployment> kubernetes.io/change-cause="<mensagem>"``

``kubectl rollout undo deployment nginx-deployment --to-revision=<numero_da_revisao>``



``kubectl get pv``
``kubectl get pvc``