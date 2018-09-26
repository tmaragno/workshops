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
#Enviamos el conjunto de cambios al repositorio en la nube.
git push origin <nombre de la nueva rama>
```
Para obtener el URL del repositorio, podemos navegar a la página principa de nuestro proyecto en Developer Cloud Servie y copiarla. La imágen a continuación muestra donde se encuentra.

![Open Terminal](https://github.com/tmaragno/workshops/blob/master/images/500_Image_2.png)

Para ver como quedó el código podemos abrir la sección "Code" en developer cloud service.

![Open Terminal](https://github.com/tmaragno/workshops/blob/master/images/500_Image_3.png)

Como pueden ver, inicialmente no vemos nuestro código. Esto es ya que se encuentra en una rama distinta creada por nosotros. La imagen a continuación muestra como podemos cambiar la rama que estamos viendo.

![Open Terminal](https://github.com/tmaragno/workshops/blob/master/images/500_Image_4.png)

Deberíamos tener algo parecido a esto:

![Open Terminal](https://github.com/tmaragno/workshops/blob/master/images/500_Image_5.png)

NOTA IMPORTANTE: Vamos a repetir los mismos pasos para el cliente.

## Promoción de código a distintos ambientes
A continuación el desarrollador va a solicitar una revisión y que su código se una a la rama maestra del código. Esto se realiza a través de un "Merge Request" en Developer Cloud Service.

En primer lugar vamos a solicitar el "Merge Request".

![Open Terminal](https://github.com/tmaragno/workshops/blob/master/images/500_Image_6.png)

Seleccionamos el repositorio de interés, la rama destino y la origen. Al seleccionar las ramas deberían aparecer los "commits" que podemos unir y que serán parte de la revisón.

![Open Terminal](https://github.com/tmaragno/workshops/blob/master/images/500_Image_7.png)

A continuación podemos enlazar una actividad asignada a nosotros a este merge request para enlazar el plan con los cambios que se realizaron.

![Open Terminal](https://github.com/tmaragno/workshops/blob/master/images/500_Image_8.png)

En el último paso del asistente podemos colocar una descripción en formato "Markdown" para darle mayor información al revisor de los cambios realizados. En la pestaña "preview" podemos previsualizar como se verá nuestro comentario.

![Open Terminal](https://github.com/tmaragno/workshops/blob/master/images/500_Image_9.png)

Como estamos haciendo todo bajo el mismo usuario, se abrirá la ventana para aprobar la solicitud y todo el detalle asociado a esta solicitud. Pueden revisar el contenido de la solictitud en cada una de las pestañas. El revisor puede ver los archivos con cambios y la tarea asociada junto a los comentarios del desarrollador. Una vez revisado todo puede decidir si aprobar, rechazar, agregar comentarios y finalmente unir el código a la rama principal.

![Open Terminal](https://github.com/tmaragno/workshops/blob/master/images/500_Image_10.png)

Al presionar en "Merge", se le presenta un asistente en donde puede unir el código de distintas formas. Vamos a realizar un commit normal, podemos asociar un comentario y finalmente decidir si eliminamos la rama de desarrollo y si queremos que automaticamente se resuelva la tarea asociada.

![Open Terminal](https://github.com/tmaragno/workshops/blob/master/images/500_Image_11.png)

Si regresamos a la sección "Code" podemos ver que la rama maestra ahora tiene nuestro código.

![Open Terminal](https://github.com/tmaragno/workshops/blob/master/images/500_Image_12.png)

NOTA: Si hay suficiente tiempo se pueden repetir los mismos pasos para el cliente.

##FIN






