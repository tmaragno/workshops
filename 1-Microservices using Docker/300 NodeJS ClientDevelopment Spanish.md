# Desarrollo de un cliente que consume la operación del primer servicio
En este laboratorio vamos a construir un servicio REST que hace uso de la suma que construimos en el primer taller. Para esto vamos a crear un archivo denominado *client.js* dentro de una nueva carpeta. El servicio será muy parecido, sin embargo podrán ver como podemos ir construyendo una arquitectura basada en microservicios. 

## Desarrollar el cliente NodeJS
En primer lugar vamos a colocar la tarea en Developer Cloud Service para indicar que el trabajo se encuentra en progreso. En la pantalla principal del proyecto, navege hacia la sección "Issues" como se puede ver en la imagen

![Issue in progress](https://github.com/tmaragno/workshops/blob/master/images/300_Image_1.png)

Repetimos los pasos que hicimos en el lab 200 pero ahora con la otra tarea.

El desarrollo del cliente es muy parecido al taller anterior. Si seguimos dentro de la carpeta del taller anterior, debemos salirnos antes de empezar. Crear una nueva carpeta para el cliente.
```shell
mkdir RESTClient
```
A continuación, crear el archivo *package.json* como se ilustra a continuación.
```json
{
    "name": "rest_client",
    "version": "1.0.0",
    "description": "NodeJS Client",
    "author": "Primer Nombre <tuemail@email.com>",
    "main": "client.js",
    "scripts": {
        "start": "node client.js"
    },
    "dependencies": {
        "express": "latest",
        "node-rest-client": "latest"
    }
}
```
Como pueden ver, utilizaremos la misma librería *express* para exponer la funcionalidad como un servicio web, sin embargo también utilizaremos la librería *node-rest-client* para consumir el otro servicio. A continuación tenemos que instalar estos paquetes utilizando el mismo comando que en el taller anterior.
```shell
npm i
```
No voy a pasar paso a paso nuevamente por cada una de las secciones, sin embargo revisen el código para que lo entiendan. A continuación pueden conseguir el código para el cliente.
```javascript
var express = require('express');
var app = express();
var Client = require('node-rest-client').Client;
var client = new Client();

var PORT = process.env.PORT || 8082;

app.get('/status', function (req, res) {
        res.set('Content-Type', 'application/json');
        res.end('{"status": {"message": "Hi! Second service working here!"}}');
})

app.get('/div', function (req, res) {
	var num1 = parseInt(req.query.num1);
	var num2 = parseInt(req.query.num2);
       client.get("http://localhost:8081/sum?num1="+req.query.num1+"&num2="+req.query.num2, function (data, response) {
			var result = num1/num2;
			res.set('Content-Type', 'application/json');
			res.end('{"result": {"result":'+result+'}}');
		});
})

server = app.listen(PORT, function () {

   var host = server.address().address
   var port = server.address().port

   console.log("The magic happens here! Server listening at http://%s:%s", host, port)

})
```
Dense cuenta como cambia el número de puerto de donde está escuchando este segundo microservicio. Finalmente para probarlo asegurense que está corriendo el servicio del primer taller y ejecuten el siguiente URL en su explorador: http://localhost:8082/div?num1=10&num2=1 <br/>
El resultado debería ser el siguiente:
```json
{"result": {"result":10}}
```
# Fin parte 2
