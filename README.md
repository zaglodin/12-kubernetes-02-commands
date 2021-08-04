# Домашнее задание к занятию "12.2 Команды для работы с Kubernetes"

Задание 1: Задание 1: Запуск пода из образа в деплойменте
```powershell
PS C:\Users\zaglo\OneDrive\Desktop\Обучение\4 Модуль\12-kubernetes-02-commands> kubectl create deployment hello-node-deployment --image=k8s.gcr.io/echoserver:1.4 --replicas=2
deployment.apps/hello-node-deployment created
PS C:\Users\zaglo\OneDrive\Desktop\Обучение\4 Модуль\12-kubernetes-02-commands> kubectl get deployment
NAME                    READY   UP-TO-DATE   AVAILABLE   AGE
hello-node-deployment   2/2     2            2           2m39s
PS C:\Users\zaglo\OneDrive\Desktop\Обучение\4 Модуль\12-kubernetes-02-commands> kubectl get pods
NAME                                     READY   STATUS    RESTARTS   AGE
hello-node-deployment-6b464d6d69-4gxkf   1/1     Running   0          2m43s
hello-node-deployment-6b464d6d69-h4x5c   1/1     Running   0          2m43s
```

Задание 2: Просмотр логов для разработки

создание пользователя подробно в - [steps.shell](/steps.shell)

```shell
PS C:\Users\zaglo\OneDrive\Desktop\Обучение\4 Модуль\12-kubernetes-02-commands> kubectl config use-context user1-context
Switched to context "user1-context".
PS C:\Users\zaglo\OneDrive\Desktop\Обучение\4 Модуль\12-kubernetes-02-commands> kubectl get pods -n=app-namespace
Error from server (Forbidden): pods is forbidden: User "user1" cannot list resource "pods" in API group "" in the namespace "app-namespace"
PS C:\Users\zaglo\OneDrive\Desktop\Обучение\4 Модуль\12-kubernetes-02-commands> kubectl config use-context minikube     
Switched to context "minikube".
PS C:\Users\zaglo\OneDrive\Desktop\Обучение\4 Модуль\12-kubernetes-02-commands> kubectl get pods -n=app-namespace
NAME                                     READY   STATUS    RESTARTS   AGE
hello-node-deployment-7d9648587d-pqk5t   1/1     Running   0          8m9s
hello-node-deployment-7d9648587d-w8xx9   1/1     Running   0          8m9s
```

Задание 3: Изменение количества реплик

```shell
PS C:\Users\zaglo\OneDrive\Desktop\Обучение\4 Модуль\12-kubernetes-02-commands> kubectl apply -f namespace.yaml          
namespace/app-namespace created
PS C:\Users\zaglo\OneDrive\Desktop\Обучение\4 Модуль\12-kubernetes-02-commands> kubectl apply -f deployment.yaml
deployment.apps/hello-node-deployment created
PS C:\Users\zaglo\OneDrive\Desktop\Обучение\4 Модуль\12-kubernetes-02-commands> kubectl get pods
No resources found in default namespace.
PS C:\Users\zaglo\OneDrive\Desktop\Обучение\4 Модуль\12-kubernetes-02-commands> kubectl get pods -n=app-namespace                 
NAME                                     READY   STATUS    RESTARTS   AGE
hello-node-deployment-7d9648587d-8m2rf   1/1     Running   0          64s
hello-node-deployment-7d9648587d-gl7sh   1/1     Running   0          64s
hello-node-deployment-7d9648587d-pqk5t   1/1     Running   0          64s
hello-node-deployment-7d9648587d-rwf9b   1/1     Running   0          64s
hello-node-deployment-7d9648587d-w8xx9   1/1     Running   0          64s
PS C:\Users\zaglo\OneDrive\Desktop\Обучение\4 Модуль\12-kubernetes-02-commands>
```