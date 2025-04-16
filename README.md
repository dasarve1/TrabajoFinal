# TrabajoFinal
-------------------------------------

# Comandos utilizados

## Construcción de la imagen
docker build -t trabajofinal:1.0.1 .

## Iniciar el contenedor
docker run -d -p 8080:8080 -e ASPNETCORE_ENVIRONMENT=Development --name contenedor_trabajofinal trabajofinal:1.0.1 .

## Preparación de la imagen
docker tag trabajofinal:1.0.1 dasarve1/trabajofinal:1.0.1

## Enviar la imagen hacia dockerhub
docker push dasarve1/trabajofinal:1.0.1

## Instalación o actualización de los templates de chart
helm install[upgrade] trabajofinal-helm ./diplomadoarq-helm

## Empaquetar el chart
helm package ./diplomadoarq-helm

## Creación del index para chart
helm repo index . --url https://dasarve1.github.io/helm-charts

## Creación del namespace para argo
kubectl create namespace argocd

## Instalar argoCD
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

## Verificación de pods creados en el namespace de argocd
kubectl get pods -n argocd

## Inicializar el servidor de argoCD
kubectl port-forward svc/argocd-server -n argocd 8082:443

## Obtener la clave de administrador de argoCD
kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 --decode