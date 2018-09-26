# GIT y completación de actividades
En este laboratorio vamos a subir el código fuente y los DockerFiles a los repositorios que hemos creado en el laboratorio 100. Realizaremos los siguientes pasos:
- Entrega del código fuente a una rama de desarrollo
- Solicitaremos un "Merge Request" para verificar y promocionar los cambios de la rama de desarrollo a la maestra.
- Marcaremos como completada nuestra tarea

# Entrega del código a una rama de desarrollo
En primer lugar abrimos el terminal en la máquina virtual y ejecutamos los siguientes comandos en orden, uno por uno. En comentario (Texto que empieza con el symbolo #) se coloca una breve explicación de lo que hace el comando.

![Open Terminal](https://github.com/tmaragno/workshops/blob/master/images/500_Image_1.png)

```shell
#Inicializamos la carpeta para que sea considerada un repositorio git
git init
#Agregamos el repositorio remoto en Developer Cloud Service como un repositorio remoto
git remote add origin <URL del repositorio en developer cloud service>
#Jalamos todo lo que hay en la rama maestra para tener ambos repositorios al iguales.
git pull origin master
#Nos movemos a una rama nueva para no entregar cambios no probados a la maestra que usualmente contiene la última versión del código productivo.
git checkout -b <nombre de la nueva rama>
#Vamos a marcar todos los archivos en la carpeta para que sean entregados.
git add –A
#Se genera un conjunto de cambios con el mensaje deseado
git commit -m "Entrega version .1 del servidor"
#Enviamos el conjunto de cambios al repositorio en la nube
git push origin REQThomas
```

