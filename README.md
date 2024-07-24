# cluster-docker

Este proyecto despliega una aplicación Flask en un cluster de Kubernetes local utilizando Minikube.

## Requisitos previos

- Docker instalado y configurado
- Minikube instalado
- kubectl instalado y configurado
- Una cuenta en Docker Hub

## Configuración inicial

1. Clona este repositorio:
   ```
   git clone https://github.com/Dylan010/cluster-docker.
   cd cluster-docker
   ```

2. Modifica la imagen de Docker en `deployment.yaml`:
   Reemplaza `dy010101/desafio-13:latest` con tu propia imagen de Docker.

## Construcción y publicación de la imagen Docker

1. Construye la imagen Docker:
   ```
   docker build -t <TU_USUARIO_DOCKERHUB>/desafio-14:latest .
   ```

2. Publica la imagen en Docker Hub:
   ```
   docker login
   docker push <TU_USUARIO_DOCKERHUB>/desafio-14:latest
   ```

## Despliegue en Kubernetes

1. Inicia Minikube:
   ```
   minikube start
   ```

2. Aplica los manifiestos de Kubernetes:
   ```
   kubectl apply -f deployment.yaml
   kubectl apply -f service.yaml
   ```

3. Verifica el despliegue:
   ```
   kubectl get pods
   kubectl get services
   ```

4. Accede a la aplicación:
   ```
   minikube service desafio-14-service
   ```
   Este comando abrirá la aplicación en tu navegador predeterminado.

## Limpieza

Para eliminar todos los recursos creados:

1. Elimina los recursos de Kubernetes:
   ```
   kubectl delete -f deployment.yaml
   kubectl delete -f service.yaml
   ```

2. Detén Minikube:
   ```
   minikube stop
   ```

3. (Opcional) Elimina el cluster de Minikube:
   ```
   minikube delete
   ```

## Notas importantes

- Asegúrate de reemplazar `<TU_USUARIO_DOCKERHUB>` con tu nombre de usuario real de Docker Hub en todos los comandos y archivos relevantes.
- Si modificas el código de la aplicación, reconstruye la imagen Docker y actualiza la versión en `deployment.yaml` antes de volver a desplegar.
- Este proyecto utiliza una imagen base de Python 3.9. Si necesitas una versión diferente, modifica el `Dockerfile` según sea necesario.

## Solución de problemas

- Si los pods no inician, verifica los logs con:
  ```
  kubectl logs <NOMBRE_DEL_POD>
  ```
- Si el servicio no es accesible, verifica su configuración:
  ```
  kubectl describe service desafio-14-service
  ```

