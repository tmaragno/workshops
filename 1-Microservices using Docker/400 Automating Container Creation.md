# Automatización
Parte de la filosofía de construir aplicaciones basadas en microservicios es automatizar absolutamente todos los pasos del ciclo de vida de desarrollo. Eso incluye los pasos manuales que realizamos anteriromente para crear las imágenes Docker. Para este paso utilizaremos una herramienta de Oracle denominada Wercker.

## Creación de los pipelines para automatizar la creación de las imágenes
En primer lugar vamos a hacer un Docker push de las imágenes que creamos en los laboratorios anteriors a nuestro usuario en Docker Hub. Esto lo realizamos ejecutando los siguientes comandos.
```shell
docker login
docker push <username>/node-server:latest
docker push <username>/node-client:latest
```
Si entramos a nuestro espacio en Docker Hub, podremos ver las imagenes que acabamos de entregar. (www.dockerhub.com)
![alt text](https://github.com/tmaragno/workshops/blob/master/images/dockerhub.PNG "Docker hub image")
