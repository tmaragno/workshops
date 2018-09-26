# Configuración inicial del espacio de trabajo para el equipo
En este laboratorio inicial vamos a actuar como el líder del equipo/proyecto y configuraremos el espacio de trabajo. Crearemos los siguientes artefactos:
- Repositorio para el Servidor que se desarrollará
- Repositorio para el cliente que se desarrollará
- Tareas para las distintas personas del equipo de trabajo asociadas al producto que se va a construir
- Un "Sprint" para manejar el proyecto utilizando metodologías ágiles

## Creación del proyecto
Una vez creada la instancia de developer cloud service, ingresamos a su consola y creamos un nuevo proyecto tal como se muestra en la figura a continuación.

![New Project](https://github.com/tmaragno/workshops/blob/master/images/100_Image_1.png)

Los detalles para el proyecto se muestran en las imágenes a continuación. No es obligatorio utilizar los mismos nombres, sin embargo si cambian los nombres y usan sus propios, deben referirse a estos a lo largo del laboratorio.

![New Project](https://github.com/tmaragno/workshops/blob/master/images/100_Image_2.png)

![New Project](https://github.com/tmaragno/workshops/blob/master/images/100_Image_3.png)

![New Project](https://github.com/tmaragno/workshops/blob/master/images/100_Image_4.png)

![New Project](https://github.com/tmaragno/workshops/blob/master/images/100_Image_5.png)

## Creación de los repositorios para el código
Para poder controlar el código fuente, vamos a crear dos repositorios git dentro de Developer Cloud Service. Un repositorio va a contener el código para el servidor y el segundo va a contener el código para el cliente. Para crear el primer repositorio, desde la página principal de nuestro proyecto, vamos a presionar el botón "Create Repository" como se muestra en la imágen a continuación:

![New Repo](https://github.com/tmaragno/workshops/blob/master/images/100_Image_6.png)

En el asistente que se presenta a continuación, seguir las instrucciones y llenar los datos como se muestra en las imágenes. Vamos a crear un repositorio denominado "ServerRepo" y lo vamos a inicializar con un archivo README.md en donde generalmente se incluyen descripciones e instrucciones sobre el código que se encuentra en el repositorio.

![New Repo](https://github.com/tmaragno/workshops/blob/master/images/100_Image_7.png)

NOTA IMPORTANTE: Repetimos los mismos pasos para crear un repositorio denominado "ClientRepo" 

##Creación de tareas para el desarrollo
En Developer Cloud Service podemos asociar todo esfuerzo de desarrollo, cambio, defecto o incidente a una tarea o historia. De esta forma obtenemos la trazabilidad completa de los cambios y adiciones que se realizan en el código fuente. Developer Cloud Service está diseñado para poder manejar proyectos de desarrollo de software basados en metodologías ágiles como lo son SCRUM y Kanban. No es objetivo de este taller entrar en detalle de estas metodologías, sin embargo vamos a mostrar como la herramienta puede apoyarlas.<br/>
<br/>
En primer lugar vamos a proceder a crear 2 historias (Terminología scrum) o tareas para describir el código que vamos a construir en los laboratorios 200 y 300. El primer paso es abrir la pestaña "Issues"

![New Issues](https://github.com/tmaragno/workshops/blob/master/images/100_Image_8.png)

Luego crear un nuevo issue para documentar la creación de un servidor para servicios web REST usando NodeJS como se muestra en las imágenes a continuación:

![New Issues](https://github.com/tmaragno/workshops/blob/master/images/100_Image_9.png)
![New Issues](https://github.com/tmaragno/workshops/blob/master/images/100_Image_10.png)
![New Issues](https://github.com/tmaragno/workshops/blob/master/images/100_Image_11.png)
![New Issues](https://github.com/tmaragno/workshops/blob/master/images/100_Image_12.png)
![New Issues](https://github.com/tmaragno/workshops/blob/master/images/100_Image_13.png)

NOTA IMPORTANTE: Repitamos estos pasos para crear una segunda tarea para crear el cliente que consumirá este servicio REST que ofrece el servidor. Al final vamos a tener estas dos historias como se muestra en la imágen a continuación:

![New Issues](https://github.com/tmaragno/workshops/blob/master/images/100_Image_14.png)

El próximo paso es crear un "Sprint" para gestionar el proyecto y los esfuerzos de desarrollo siguiendo la metodología SCRUM. Abra la pestaña "Agile" como se muestra en la imagen anterior y luego presione el botón "New Board" y siga los pasos que se muestran en las imágenes a continuación.

![New Issues](https://github.com/tmaragno/workshops/blob/master/images/100_Image_15.png)
![New Issues](https://github.com/tmaragno/workshops/blob/master/images/100_Image_16.png)
![New Issues](https://github.com/tmaragno/workshops/blob/master/images/100_Image_17.png)
![New Issues](https://github.com/tmaragno/workshops/blob/master/images/100_Image_18.png)

Antes de empezar debemos seleccionar de todo el "Backlog" o actividades/issues que tenemos identificados para el proyecto las que vamos a trabajar en este primer "Sprint". Para efectos del taller solamente tenemos dos, así que las seleccionamos las dos. Esto se realiza arrastrando las historias hacia el espacio arriba como se muestra en la imagen.

![New Issues](https://github.com/tmaragno/workshops/blob/master/images/100_Image_19.png)

Finalmente, iniciamos el sprint. Siga las instrucciones en las imagenes a continuación.

![New Issues](https://github.com/tmaragno/workshops/blob/master/images/100_Image_20.png)
![New Issues](https://github.com/tmaragno/workshops/blob/master/images/100_Image_21.png)
![New Issues](https://github.com/tmaragno/workshops/blob/master/images/100_Image_22.png)
![New Issues](https://github.com/tmaragno/workshops/blob/master/images/100_Image_23.png)

Con esto finalizamos el laboratorio 100.

## FIN


