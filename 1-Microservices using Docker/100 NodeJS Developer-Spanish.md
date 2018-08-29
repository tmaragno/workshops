# Desarrollo de un servidor NodeJS
A continuación se proporcionan los pasos a seugir para demostrar la funcionalidad de Docker y como se puede emplear para construir una aplicación levemente acoplada siguiendo un patrón de diseño de microservicios. En primer lugar y objetivo de esta guia será el desarrollo de un servidor de servicios web REST que retorna el resultado de una operación matemática muy compleja. ;)

## Desarrollar la aplicación NodeJS
1. Instale NodeJS usando el siguiente comando

1. Cree un directorio en la maquina virtual denominado *RESTServer* como se muestra a continuación.
```sh
mkdir RESTServer
```
1. A continuación debemos crear un archivo denominado *package.json* que contenga el contenido descrito abajo.
```sh
vi package.json
```

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
        "express": "^4.16.1"
    }
}
```

1. 

