# Entorno de Ejecución
En nuestro ejemplo tenemos una simplificación en donde únicamente corremos en la maquina virtual 2 contenedores. Esto no es un caso real. Cargas empresariales van a contar con cientos y hasta miles de contenedores corriendo en simultáneo, lo cuál aumenta la complejidad de administración. Para simplificar esto, Oracle crea su infraestructura para gestionar y correr contenedores Docker llamada Oracle Container Cloud Service.

Oracle Container Cloud Service (también conocido como Oracle Cloud Infrastructure Container Service Classic) ofrece a los equipos de Desarrollo y Operaciones los beneficios de una "contenedorización" Docker fácil y segura al crear y desplegar aplicaciones.<br>/

Oracle Container Cloud Service:

-Proporciona una interfaz fácil de usar para administrar el entorno Docker

-Proporciona ejemplos listos para usar de servicios en contenedores y pilas de aplicaciones que se pueden implementar con un solo clic

-Permite a los desarrolladores conectarse fácilmente a sus registros Docker privados (para que puedan 'traer sus propios contenedores')

-Permite a los desarrolladores enfocarse en la construcción de imágenes de aplicaciones en contenedores y en los flujos de Integración Continua / Entrega Continua (CI / CD), no en el aprendizaje de tecnologías complejas de orquestación

## Importar las imagenes a Container Cloud Service
El primer paso es importar las imágenes que creamos y tenerlas listas como servicios para poder aprovisionar rapidamente el servidor REST cuando necesitemos. En primer lugar vamos a navegar a la consola de servicio para Container Cloud Service. 

![Container](https://github.com/tmaragno/workshops/blob/master/images/600_Image_1.png)
![Container](https://github.com/tmaragno/workshops/blob/master/images/600_Image_2.png)

Iniciamos sesión con las credenciales que definimos al principio del taller.

![Container](https://github.com/tmaragno/workshops/blob/master/images/600_Image_3.png)

La pagina principal muestra el estado general de nuestro ambiente. La salud de los contenedores, los hosts físicos que realizan la ejecución de los contenedores y los pools de recursos que hemos definido. De aquí podemos ver rápidamente si hay algun problema y como se esta comportando mi arquitectura basada en microservicios.<br/>

El primer paso que realizaremos es abrir la pantalla que nos muestra los servicios que tenemos disponibles.

![Container](https://github.com/tmaragno/workshops/blob/master/images/600_Image_4.png)

En esta pantalla podemos ver todos los servicios que tenemos a disposición y de los cuales podemos crear nuevos contenedores. Para crear uno nuevo presionamos el botón "New Service".

![Container](https://github.com/tmaragno/workshops/blob/master/images/600_Image_5.png)

Para crear un nuevo servicio vamos a introducir los datos para la imagen del servidor REST que ya tenemos en el Docker Hub. Las pantalla a continuación muestran el proceso de creación. En nuestro caso es bastante sencillo, solo debemos especificar un nombre, descripción, la imagen y los puertos que deseamos disponibilizar.

![Container](https://github.com/tmaragno/workshops/blob/master/images/600_Image_6.png)
![Container](https://github.com/tmaragno/workshops/blob/master/images/600_Image_7.png)
![Container](https://github.com/tmaragno/workshops/blob/master/images/600_Image_8.png)
![Container](https://github.com/tmaragno/workshops/blob/master/images/600_Image_9.png)

Ahora que tenemos un servicio asociado a nuestra imagen en Docker Hub, podemos empezar a crear contenedores y desplegarlos en distintos pools de recursos para garantizar la disponibilidad de nuestro servicio.

![Container](https://github.com/tmaragno/workshops/blob/master/images/600_Image_10.png)

Al presionar "Deploy" se nos presenta una pantalla solicitando datos de configuración para el despliegue. En nuestro caso podemos dejar los valores por defecto ya que contamos con un solo host para hacer los despliegues. Si tuvieramos multiples nodos trabajadores (Worker nodes en inglés) pudieramos definir reglas para distribuir multiples instancias del mismo contenedor.

![Container](https://github.com/tmaragno/workshops/blob/master/images/600_Image_11.png)
![Container](https://github.com/tmaragno/workshops/blob/master/images/600_Image_12.png)

Una vez listo, podrémos ver detalles de ejecución del contenedor y del host en el cúal está corriendo. Si presionamos sobre el enlace del host podrémos ver todos los contenedores que están corriendo allí, la "salud" del host y la de sus contenedores al igual que pausar, detener e iniciarlos.

![Container](https://github.com/tmaragno/workshops/blob/master/images/600_Image_13.png)
![Container](https://github.com/tmaragno/workshops/blob/master/images/600_Image_14.png)

Finalmente si utilizamos la dirección ip del contenedor, podemos ejecutar una invocación al servicio REST tal como lo hicimos en el laboratorio 200. 

![Container](https://github.com/tmaragno/workshops/blob/master/images/600_Image_15.png)

Si hay tiempo suficiente pueden repetir estos pasos para el cliente también.

#FIN





