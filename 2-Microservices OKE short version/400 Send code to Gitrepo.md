# GIT y completación de actividades
En este laboratorio vamos a subir el código fuente y los DockerFiles a los repositorios que les proporciona el instructor. Realizaremos los siguientes pasos:
- Entrega del código fuente a una rama de desarrollo

# Entrega del código a una rama de desarrollo
En primer lugar abrimos el terminal en la maquina asignada y ejecutamos los siguientes comandos en orden, uno por uno. En comentario (Texto que empieza con el symbolo #) se coloca una breve explicación de lo que hace el comando.

![Open Terminal](https://github.com/tmaragno/workshops/blob/master/images/500_Image_1.png)

```shell
#Inicializamos la carpeta para que sea considerada un repositorio git
git init
#Ignoramos las dependencias
vi .gitignore
#en el archivo agregamos la siguiente linea
node_modules
#Agregamos el repositorio remoto en Developer Cloud Service como un repositorio remoto
git remote add origin <URL del repositorio en developer cloud service DEL PARTICIPANTE>
#Vamos a marcar todos los archivos en la carpeta para que sean entregados.
git add –A
#Se genera un conjunto de cambios con el mensaje deseado
git commit -m "Entrega version .1 del servidor"
#Enviamos el conjunto de cambios al repositorio en la nube.
git push origin master
```

##FIN






