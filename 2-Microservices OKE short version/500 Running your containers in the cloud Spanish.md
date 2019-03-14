# Entorno de Ejecución
En nuestro ejemplo tenemos una simplificación en donde únicamente corremos 1 contenedor. Esto no es un caso real. Cargas empresariales van a contar con cientos de contenedores corriendo en simultáneo, lo cuál aumenta la complejidad de administración. Para simplificar esto, Oracle crea su infraestructura para gestionar y correr contenedores Docker llamada Oracle Container Engine for Kubernetes.

Oracle Container Engine for Kubernetes ofrece a los equipos de Desarrollo y Operaciones los beneficios de una "contenedorización" Docker fácil y segura al crear y desplegar aplicaciones.<br>/

Oracle Container Engine for Kubernetes:

-Proporciona una interfaz fácil de usar para administrar el entorno de Kubernetes

-Permite a los desarrolladores conectarse fácilmente a sus registros Docker privados (para que puedan traer sus propios contenedores')

-Permite a los desarrolladores enfocarse en la construcción de imágenes de aplicaciones en contenedores y en los flujos de Integración Continua / Entrega Continua (CI / CD), no en el aprendizaje de tecnologías complejas de orquestación

## Instalar la línea de comandos de Oracle Compute Infrastructure y Kubectl
```sh
sudo vi /etc/yum.repos.d/kubernetes.repo
```
El archivo debe verse como a continuación:
```sh
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
```

Para instalar las herramientas de Kubernetes ejecutar el siguiente comando:
```sh
sudo yum install -y kubelet kubeadm kubectl
```

Para probar que la instalación fue exitosa vamos a ejecutar el siguiente comando. Igualmente les coloco un ejemplo de un resultado esperado.
```sh
kubectl version

Client Version: version.Info{Major:"1", Minor:"13", GitVersion:"v1.13.4", GitCommit:"c27b913fddd1a6c480c229191a087698aa92f0b1", GitTreeState:"clean", BuildDate:"2019-02-28T13:37:52Z", GoVersion:"go1.11.5", Compiler:"gc", Platform:"linux/amd64"}
The connection to the server localhost:8080 was refused - did you specify the right host or port?
```

Para instalar las herramientas de línea de comandos de Oracle Cloud Infrastructure, realizamos los siguientes pasos.

```sh
cd $HOME

sudo yum install -y oracle-epel-release-el7
sudo yum install -y python36

bash -c "$(curl -L https://raw.githubusercontent.com/oracle/oci-cli/master/scripts/install/install.sh)"
```
Usar los valores por defecto para la instalación y esperar que termine.

Ahora vamos a inicializar y configurar las herramientas de línea de comandos para OCI.

##Conectarnos al Cluster creado
Primero vamos a crear una carpeta en donde configuramos todo los relacionado a nuestro cluster Kubernetes. 
```sh
cd $HOME
mkdir -p .kube
```
En esta carpeta va a estar el archivo de configuración que creamos con el siguiente comando. Asegurense de utilizar las llaves que serán suministradas por el instructor.
```sh
oci setup config.
```
Los datos solicitados los pueden encontrar en el archivo parameters.md en la carpeta Resources.

```sh
oci ce cluster create-kubeconfig --cluster-id ocid1.cluster.oc1.phx.aaaaaaaaafqtimdfg5sdkzjymyzwmmzyge4taytcga4gcmjxhcqtgnzqmmyd --file $HOME/.kube/config --region us-phoenix-1 
```

Finalmente tenemos que expotar la variable de entorno que indicará la ruta en donde se encuentra el archivo de configuración generado.

```sh
export KUBECONFIG=$HOME/.kube/config
```

Para verificar el correcto funcionamiento de lo que hicimos anteriormente ejecutamos el siguiente comando que nos mostrará los nodos qué estan corriendo en el Oracle Cloud.

```sh
kubectl get nodes

NAME              STATUS   ROLES   AGE   VERSION
129.146.134.112   Ready    node    94d   v1.11.1
129.146.61.156    Ready    node    94d   v1.11.1
129.146.70.125    Ready    node    94d   v1.11.1
```
Para poder crear contenedores basados vamos a crear un template donde definimos los parámetros para el servicio que vamos a desplegar en el cluster Kubernetes. A continuación coloco el template que les permitirá desplegar el servicio en el cluster.

```yaml
# This template file will have its environment variables expanded
# and the .template extension removed by the bash-template Wercker step.
# See wercker.yml.
 
apiVersion: apps/v1
kind: Deployment
metadata:
  name: restserver<NUMERO PARTICIPANTE>
  labels:
    commit: participant<NUMERO PARTICIPANTE>
spec:
  replicas: 3
  selector:
    matchLabels:
      app: restserver<NUERO PARTICIPANTE>
  template:
    metadata:
      labels:
        app: restserver
        commit: participant<NUMERO PARTICIPANTE>
    spec:
      containers:
      - name: restserver
        image: phx.ocir.io/gse00014124/workshoprepo:participant<NUMERO PARTICIPANTE>
        ports:
          - containerPort: 8081
      imagePullSecrets:
      - name:  demosecret
```
Para crear la app ejecutamos el siguiente comando:

```sh
kubectl create -f .\kubernetes_deployment.yml.template
```

Podemos probar nuestro deployment usando la capacidad de port forwarding de kubectl, tal como se muestra en el ejemplo a continuación. En primer lugar obtenemos todos los "pods" que están corriendo en el cluster y luego realizamos el port forwarding para poder conectarnos a el.

```sh
kubectl get pods

NAME                                    READY   STATUS    RESTARTS   AGE
hello-k8s-deployment-6dcbb9998b-hwmhx   1/1     Running   0          104d
quickstart-se-55f88c4d5c-ntx82          1/1     Running   0          29d
registry-ui-6cf8bd69dc-rrkl8            1/1     Running   0          85d
restserver01-6d7bb6d48-7q8tw            1/1     Running   0          26m
restserver01-6d7bb6d48-8jz2d            1/1     Running   0          26m
restserver01-6d7bb6d48-m58b5            1/1     Running   0          26m
restserver02-9874bd9c5-fcr5t            1/1     Running   0          11s
restserver02-9874bd9c5-j7m7p            1/1     Running   0          11s
restserver02-9874bd9c5-vn2kx            1/1     Running   0          11s

kubectl port-forward <nombre POD> 8081:8081
```

Para probar nuestro servicio podemos volver a ejecutarlo pero esta vez usando localhost ya que estamos haciendo un port-forwarding de nuestra maquina al cluster Kubernetes.

```url
http://localhost:8082/status
```

Finalizamos este laboratorio haciendo un git commit y un git push para subir todos los archivos a nuestro repositorio para poder iniciar nuestro próximo laboratorio. A continuación se listan los ejemplos para realizar esto.

```sh
git add .
git commit -m "MENSAJE QUE QUEREMOS COLOCAR DESCRIPTIVO DE LOS CAMBIOS"
git push origin rama <NUMERO PARTICIPANTE>
```
#FIN




