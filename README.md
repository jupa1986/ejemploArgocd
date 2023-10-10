# Ejemplo de uso de argocd para deplegar un nginx

En este caso crearemos un deploy con la imagen nginx

## Requerimientos

- kubernetes (minikube)
- kubectl
- helm

## Instalacion de argocd con helm
Adicionar el repo de argo a helm
```
helm repo add argo https://argoproj.github.io/argo-helm
```

recuperar los valores por defecto del helm chart para ver si hay que hacer un cambio

```
helm show values argo/argo-cd > argocd-values.yaml
```
instalar argocd
```
helm install my-argocd argo/argo-cd -n argocd --create-namespace
```
Recuperar password para usuario admin
```
kubectl get customresourcedefinitions.apiextensions.k8s.io | grep argo
```
Crear un porforward para tener el acceso
```
kubectl port-forward service/my-argocd-server -n argocd 8080:443
```

Acceder mediante el link  http://localhost:8080

Ahi crear un proyecto con los siguientes parametros

PROJECT: default
CLUSTER: in-cluster (https://kubernetes.default.svc)
NAMESPACE: default   
REPO URL: https://github.com/jupa1986/ejemploArgocd
TARGET REVISION: HEAD
PATH: .

Crear
