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

#FIN





