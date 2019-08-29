# Desarrollo de un servidor NodeJS
A continuación se proporcionan los pasos a seguir para ilustrar la funcionalidad de Docker y como se puede emplear para construir una aplicación levemente acoplada siguiendo un patrón de diseño de microservicios. En primer lugar y objetivo de esta guia será el desarrollo de un servidor de servicios web REST que retorna el resultado de una operación matemática muy compleja. ;)

## Desarrollar el servidor NodeJS
Para empezar volvemos a nuestra maquina virtual en la nube.
<br/>
En caso de no estar instalado, instale NodeJS usando los siguiente comando
```sh
#para ver si está instalado ejecutar node -v
cd /etc/yum.repos.d
curl -sL https://rpm.nodesource.com/setup_8.x | sudo -E bash -
sudo yum install nodejs
```
Luego instale git para el control de versiones
```sh
sudo yum install git
```
Cree un directorio en la maquina virtual denominado *RESTServer* como se muestra a continuación.
```sh
cd $HOME
mkdir RESTServer
```
A continuación debemos crear un archivo denominado *package.json* que contenga el contenido descrito abajo.
```sh
cd RESTServer
vi package.json
```
Para poder editar el archivo hay que entrar en modo de editar (presione *i* ), luego *pegue el json abajo (right-click)*
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
Para cerrar y guardar el archivo presionar las siguientes teclas en orden, *:* luego *w*  y luego *q* (*:wq*) finalizando con *enter*

Repetir el procedimiento anterior para crear un archivo denominado *server.js* en la carpeta *RESTServer*:
```sh
vi server.js
```
Y pegar el siguiente contenido. (tecla *i* seguido de *right-click*)
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
Para cerrar y guardar el archivo, presione *esc* seguido por la combinación de teclas *:* luego *w* y luego *q* ( :wq ) y finalizar presionando *enter*

El siguiente paso es ejecutar el servidor y verificar que esté funcionando. 
```sh
npm i

node server.js 
```
Ahora probamos si todo funciona. Por favor abra un navegador de su preferencia (Firefox por ejemplo) y pruebe abriendo la siguiente dirección: http://<ip address asignada>:8081/status<br/> NOTA: Reemplazar el texto entre <> por la dirección de su VM asignada.
El resultado debería ser el siguiente:
```json
{"status": {"message": "Hi! All working here!"}}
```
Finalmente vamos a crear un segundo método GET que nos permita sumar dos números. De allí ustedes pueden agregarle el código que quieran - si así lo desean.  
  
Después del cierre del paréntesis del método `app.get('/status', function (req, res) {` inserte el siguiente "snippet" de código:

```javascript
app.get('/sum', function (req, res) {
        var num1 = parseInt(req.query.num1);
        var num2 = parseInt(req.query.num2);
        var result = num1 + num2;
        res.set('Content-Type', 'application/json');
        res.end('{"result": {"operation":"' +num1+"+"+num2+'", "result":'+result+'}}');
})
```
Guardar y salir nuevamente con la combinación de teclas (*esc* seguido de *:wq*).

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
        res.end('{"result": {"operation": "' +num1+"+"+num2+'", "result":'+result+'}}');
})

server = app.listen(PORT, function () {

   var host = server.address().address
   var port = server.address().port

   console.log("The magic happens here! Server listening at http://%s:%s", host, port)


})

```

#The End - por ahora
