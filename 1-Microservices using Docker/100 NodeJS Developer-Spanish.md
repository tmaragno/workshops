# Desarrollo de un servidor NodeJS
A continuación se proporcionan los pasos a seugir para demostrar la funcionalidad de Docker y como se puede emplear para construir una aplicación levemente acoplada siguiendo un patrón de diseño de microservicios. En primer lugar y objetivo de esta guia será el desarrollo de un servidor de servicios web REST que retorna el resultado de una operación matemática muy compleja. ;)

## Desarrollar la aplicación NodeJS
Instale NodeJS usando los siguiente comando
```sh
cd /etc/yum.repos.d
curl -sL https://rpm.nodesource.com/setup_8.x | sudo -E bash -
sudo yum install nodejs
```

Cree un directorio en la maquina virtual denominado *RESTServer* como se muestra a continuación.
```sh
mkdir RESTServer
```
A continuación debemos crear un archivo denominado *package.json* que contenga el contenido descrito abajo.
```sh
vi package.json
```
Para poder editar el archivo presionar la siguiente combinación de teclas *i* *pegue el json abajo* y luego *esc*
```json
{
    "name": "rest_server",
    "version": "1.0.0",
    "description": "NodeJS server",
    "author": "Primer Nombre <tuemail@email.com>",
    "main": "restserver.js",
    "scripts": {
        "start": "node server.js"
    },
    "dependencies": {
        "express": "latest"
    }
}
```
Para cerrar y guardar el archivo presionar las siguientes teclas en orden. *:* luego *w* luego *q* finalizando con *enter*

Repetir el mismo procedimiento para crear un archivo denominado *server.js*
```sh
vi server.js
```
Y pegar el siguiente contenido. (Teclas: *i* luego pegan y luego *esc*)
```javascript
var express = require('express');
var app = express();

var PORT = process.env.PORT || 8081;

app.get('/status', function (req, res) {
        res.set('Content-Type', 'application/json');
        res.end('{"status": {"message": "Hi! All working here!"}}');
})

server = app.listen(PORT, function () {

   var host = server.address().address
   var port = server.address().port

   console.log("The magic happens here! Server listening at http://%s:%s", host, port)

})
```
Para cerrar y guardar el archivo nuevamente presionan la combinación de teclas en orden *:* luego *w* luego *q* y finalizar presionando *enter*

El siguiente paso es ejecutar el servidor y verificar que esté funcionando. 
```sh
npm i

node server.js 
```
Ahora prombamos si todo funciona. Por favor abra un explorador (Firefox por ejemplo) y pruebe abriendo la siguiente dirección: http://localhost:8081/status<br/>
El resultado debería ser el siguiente:
```json
{"status": {"message": "Hi! All working here!"}}
```
Finalmente vamos a crear un segundo método GET que nos permita sumar dos números. De allí ustedes pueden agregarle el código que quieran - si así lo desean.  
  
Después del cierre del paréntesis del método `app.get('/status', function (req, res) {` inserte el siguiente snippet de código:

```javascript
app.get('/sum', function (req, res) {
        var num1 = parseInt(req.query.num1);
        var num2 = parseInt(req.query.num2);
        var result = num1 + num2;
        res.set('Content-Type', 'application/json');
        res.end('{"result": {"operation":' +num1+"+"+num2+', "result":'+result+'}}');
})
```
Salir nuevamente con la misma combinación de teclas. (*:* luego *w* luego *q* luego *enter*)

Pruebe el servicio recién construido en la siguiente dirección: <br/>
http://localhost:8081/sum?num1=2&num2=2

El programa completo debería verse de la siguiente forma:
```javascript
var express = require('express');
var app = express();

var PORT = process.env.PORT || 8081;

app.get('/status', function (req, res) {
        res.set('Content-Type', 'application/json');
        res.end('{"status": {"message": "Hi! All working here!"}}');
})

app.get('/sum', function (req, res) {
        var num1 = parseInt(req.query.num1);
        var num2 = parseInt(req.query.num2);
        var result = num1 + num2;
        res.set('Content-Type', 'application/json');
        res.end('{"result": {"operation":' +num1+"+"+num2+', "result":'+result+'}}');
})

server = app.listen(PORT, function () {

   var host = server.address().address
   var port = server.address().port

   console.log("The magic happens here! Server listening at http://%s:%s", host, port)


})

```
#The End - por ahora