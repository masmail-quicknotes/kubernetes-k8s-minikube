# kubernetes-k8s-minikube

- [¿Qué es minikube?](#que-es-minikube)
- [Como Instalar Minikube](#como-instalar-minikube)
- [Empezando con Minikube](#empezando-con-minikube)
- [Comandos iniciales Kubernetes](#comandos-kubernetes)
- [Listado Comandos Kubernetes](#listado-comandos-kubernetes)

***

# Que es Minikube

Minikube es un entorno de kubernetes con un sólo master y un sólo worker en la misma máquina. Para realizar pruebas de laboratorio va genial.

# Como Instalar Minikube

### Antes de empezar 

La virtualización VT-x o AMD-v debe estar habilitada en la BIOS de tu ordenador. En Linux, puedes comprobar si la tienes habilitada buscando 'vmx' o 'svm' en el fichero /proc/cpuinfo:
> egrep --color 'vmx|svm' /proc/cpuinfo

Y es necesario tener Hypervisor p.e. VirtualBox.  
> sudo apt install virtualbox

## Instalando Minikube en Ubuntu

> curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube \
> sudo cp minikube /usr/local/bin && rm minikube

# Empezando con minikube

Si habías instalado previamente minikube, y ejecutas:
> minikube start

Y dicho comando devuelve un error:
> machine does not exist

Necesitas eliminar permanentemente los siguientes archivos de configuración:
> rm -rf ~/.minikube

Para verificar el estado de Minikube:
> minikube status

Para eliminar el cluster Minikube y arrancarlo en modo debug:
> minikube delete \
> minikube start --v=7 --alsologtostderr \
> minikube status

# Comandos kubernetes

Para facilitar la gestión del kubectl crearemos un comando alias:
> alias kubectl="minikube kubectl --"

Versión del kubectl:
> kubectl version

Obtener estado de los nodos:
> kubectl get nodes \
> NAME       STATUS   ROLES    AGE     VERSION \
> minikube   Ready    master   2m51s   v1.19.4

Obtener listado de los services:
> kubectl get svc

Obtener listado de los pods:
> kubectl get pods -A -owide

# Listado Comandos kubernetes

**kubectl commands:**
> kubectl get nodes \
> kubectl get pod \
> kubectl get services \
> kubectl create deployment nginx-depl --image=nginx \
> kubectl get deployment \
> kubectl get replicaset \
> kubectl edit deployment nginx-depl 

**debugging:**
> kubectl logs {pod-name} \
> kubectl exec -it {pod-name} -- bin/bash

**create mongo deployment:**
> kubectl create deployment mongo-depl --image=mongo \
> kubectl logs mongo-depl-{pod-name} \
> kubectl describe pod mongo-depl-{pod-name}

**delete deployment:**
> kubectl delete deployment mongo-depl \
> kubectl delete deployment nginx-depl

**create or edit config file:**
> vim nginx-deployment.yaml \
> kubectl apply -f nginx-deployment.yaml \
> kubectl get pod \
> kubectl get deployment \

**delete with config:**
> kubectl delete -f nginx-deployment.yaml \

**Metrics:** The kubectl top command returns current CPU and memory usage for a cluster’s pods or nodes, or for a particular pod or node if specified.
> kubectl top 

***

### URL referencia: 

- <https://kubernetes.io/es/docs/tasks/tools/install-minikube/>
- <https://www.youtube.com/watch?v=X48VuDVv0do&list=WL&index=8>
- <https://gitlab.com/nanuchi/youtube-tutorial-series/-/blob/master/basic-kubectl-commands/cli-commands.md>
