# Automatizando todo el ciclo de vida
El objetivo de este último laboratorio es mostrar como podemos automatizar el ciclo de vida completo del desarrollo, sin tener que pasar por tareas manuales como hemos estado haciendo con anterioridad. La idea detrás de esto es que desde un commit a la rama maestra de nuestro proyecto, se genere una nueva imagen que contiene el código fuente modificado, se realicen las pruebas unitarias(No parte de esta serie de laboratorios) y finalmente se haga el deployment en un entorno de ejecución para contenedores como lo es Oracle Container Cloud Service.

## Creación del archivo requerido para la orquestación
El archivo que van a crear debe encontrarse en la carpeta *RESTServer* del repositorio y se debe llamar "wercker.yml". A continuación tienen el código del archivo:

```yaml
box: python:2.7
build:
  steps:    
    - internal/docker-build: 
        dockerfile: Dockerfile 
        image-name: my-new-image # temporary name used to refer to this image in a subsequent step
    - internal/docker-push:
            cmd: 0.0.0.0 8080
            image-name: my-new-image
            tag: participant<NUMERO PARTICIPANTE>
            ports: "8080"
            username: $DOCKER_USERNAME
            password: $DOCKER_PASSWORD
            repository: $DOCKER_REPO
            registry: https://phx.ocir.io/v2
deploy-to-kubernetes:
    box: python:2.7
    steps:

    - bash-template
    - script:
        name: Prepare Kubernetes files
        code: |
          mkdir -p $WERCKER_OUTPUT_DIR/kubernetes
          mv kubernetes_*.yml $WERCKER_OUTPUT_DIR/kubernetes
    
    - kubectl:
        name: deploy to kubernetes
        server: $OKE_MASTER
        token: $OKE_TOKEN
        insecure-skip-tls-verify: true
        command: apply -f $WERCKER_OUTPUT_DIR/kubernetes/
   
    - kubectl:
        name: set deployment timeout
        server: $OKE_MASTER
        token: $OKE_TOKEN
        insecure-skip-tls-verify: true
        command: patch deployment/restserver<NUMERO PARTICIPANTE> -p '{"spec":{"progressDeadlineSeconds":60}}'

    - kubectl:
        name: check deployment status
        server: $OKE_MASTER
        token: $OKE_TOKEN
        insecure-skip-tls-verify: true
        command: rollout status deployment/restserver<NUMERO PARTICIPANTE>

```

Este archivo lo vamos a generar y luego entregar directamente a la rama *RESTServer* de su repositorio.

```
git add wercker.yml
git commit -m 'Creacion de archivo wercker.yml'
git push origin master

El proximo paso es logearnos a nuestra cuenta en Wercker.com y generar una nueva aplicación. (Si no tenemos cuenta podemos abrir una)

![Container](https://github.com/tmaragno/workshops/blob/master/images/700_Image_3.png)
![Container](https://github.com/tmaragno/workshops/blob/master/images/700_Image_4.png)

La nueva aplicación estará amarrada a nuestro repositorio creado en Developer Cloud Service. Para esto debemos seleccionar la opción y introducir los datos de nuestro ambiente.

![Container](https://github.com/tmaragno/workshops/blob/master/images/700_Image_5.png)

El URL del ambiente se le compartirá en la sesión. Un ejemplo del ambiente está a continuación:
```URL
https://alticedevcs-nvidal.developer.ocp.oraclecloud.com/alticedevcs-nvidal
```

Seleccionamos el repositorio deseado y seguimos los pasos hasta el final como se muestra en las imágenes a continuación.

![Container](https://github.com/tmaragno/workshops/blob/master/images/images_short/600short01.png)


Llenamos los datos de repo y usuario que se compartieron durante el workshop.

![Container](https://github.com/tmaragno/workshops/blob/master/images/700_Image_6.png)
![Container](https://github.com/tmaragno/workshops/blob/master/images/700_Image_7.png)
![Container](https://github.com/tmaragno/workshops/blob/master/images/700_Image_8.png)

Una vez que estamos en la página principal de nuestra aplicación, podemos elegir si queremos que Wercker nos guie en la generación del archivo ".yml" dependiendo del lenguaje de programación que tengamos. Sin embargo como esto ya lo hicimos arriba, vamos a decirle que queremos ejecutar un build con un "wercker.yml" existente.

![Container](https://github.com/tmaragno/workshops/blob/master/images/700_Image_9.png)
![Container](https://github.com/tmaragno/workshops/blob/master/images/700_Image_10.png)

El primer build falló, ya que tenemos unas variables de entorno definidas en nuestro archivo que debemos definir en el flujo de Wercker. Debemos introducir las credenciales requeridas para acceder a nuestro repositorio en Docker Hub. Para esto abrimos el primer pipeline denominado build y las agregamos como se muestra en las imagenes a continuación.

![Container](https://github.com/tmaragno/workshops/blob/master/images/700_Image_11.png)
![Container](https://github.com/tmaragno/workshops/blob/master/images/700_Image_12.png)

La imágen a continuación lista las variables de entorno que debemos configurar. Los valores de los campos secretos los pueden encontrar en la carpeta de recursos.

![Container](https://github.com/tmaragno/workshops/blob/master/images/images_short/600short02.png)

Luego de configurado las variables con nuestros datos volvemos a ejecutar el workflow.

![Container](https://github.com/tmaragno/workshops/blob/master/images/700_Image_14.png)
![Container](https://github.com/tmaragno/workshops/blob/master/images/700_Image_15.png)

Una vez culminado deberíamos tener la ejecución en verde. Esto lo que hizo fue generar una nueva imagen con el código que se encuentra resguardado en la rama maestra del repositorio y realizar el push a nuestro repositorio de Docker desde el cuál Oracle Container Cloud Service va a tomar la imagen para crear el contenedor. Espero que ya estén viendo como todo se relaciona. El último paso es detener el contenedor para forzar el reinicio del mismo para que se vuelva a crear con la nueva versión de la imagen. Para esto agregamos un paso adicional al workflow. Para esto abrimos la pestaña "Workflow" y agregamos un nuevo "Pipeline".

![Container](https://github.com/tmaragno/workshops/blob/master/images/700_Image_16.png)
![Container](https://github.com/tmaragno/workshops/blob/master/images/700_Image_17.png)

La imágen a continuación muestra un ejemplo de como configurar el nuevo pipeline que se encargará de detener el contenedor que está corriendo. (Podemos discutir en la sesión que significa exactamente este paso)

![Container](https://github.com/tmaragno/workshops/blob/master/images/images_short/600short03.png)

Nuevamente, el paso del pipeline para detener el contenedor requiere algunas variables de entorno para poder ejecutar. Estas las definimos de la misma forma que antes, sin embargo la imagen muestra un ejemplo.

![Container](https://github.com/tmaragno/workshops/blob/master/images/images_short/600short06.png)

Para que este pipeline se ejecute, debemos agregarlo al "Workflow" que tenemos definido. Para esto regresamos a la pestaña "Workflow" (paso 2 de la imagen anterior) y lo agregamos como se muestra en las imágenes a continuación.

![Container](https://github.com/tmaragno/workshops/blob/master/images/700_Image_20.png)
![Container](https://github.com/tmaragno/workshops/blob/master/images/images_short/600short04.png)

Ahora para la gran final! Vamos a realizar un cambio al código del servidor REST. El extracto a continuación tiene los comandos que se deben ejecutar uno a uno.

```sh
vi server.js
```

Los cambios del archivo se muestran abajo. Vamos a agregar nuestro nombre en el status:

```JS
var express = require('express');
var app = express();

var PORT = process.env.PORT || 8081;

app.get('/status', function (req, res) {
	res.set('Content-Type', 'application/json');
	res.end('{"status": {"message": "Hi! All working here! <SU NOMBRE AQUI>"}}');
})

app.get('/sum', function (req, res) {
        var num1 = parseInt(req.query.num1);
        var num2 = parseInt(req.query.num2);
	var result = num1 + num2;
        res.set('Content-Type', 'application/json');
        res.end('{"result": {"operation":"' +num1+"+"+num2+'", "result":'+result+'}}');
})

server = app.listen(PORT, function () {

   var host = server.address().address
   var port = server.address().port

   console.log("The magic happens here! Server listening at http://%s:%s", host, port)

})

```

Finalmente debemos entregar los cambios al repositorio como hemos hecho antes. A continuación el extracto con los comandos a ejecutar uno a uno.

```sh
git add server.js
git commit -m 'Cambios realizados al servidor para laboratorio.'
git push origin master
```

En el momento que se realiza el commit, podemos ver que se dispara una nueva corrida en Wercker. Una vez terminada esta corrida, si vamos a la consola de Oracle Container Cloud Service, podemos observar como se detiene el contenedor y después de un momento inicia la creación nuevamente del mismo. Las imágenes a continuación ilustran un ejemplo basado en mi corrida.

![Container](https://github.com/tmaragno/workshops/blob/master/images/images_short/600short05.png)

Finalmente si ejecutamos nuevamente el servicio como hicimos antes podemos ver como cambió el código con los cambios que realizaron. 

# FIN



