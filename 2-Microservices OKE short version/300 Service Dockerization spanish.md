# Dockerizar los servicios creados
A continuación vamos a generar una imagen Docker para cada uno de los servicios que hicimos anteriormente. De esta forma podemos iniciar rápidamente contenedores basados en estas imágenes. Sino tienen cuenta en *Docker Hub*, es bueno que la vayan creando ya que la van a necesitar para los siguientes pasos. 

## Dockerizando el servidor NodeJS
En primer lugar tenemos que crear un archivo denominado *Dockerfile* en la carpeta del servidor nodejs (RESTServer).

```shell
vi Dockerfile
```

Vamos a crear esta imagen usando como fundación la imagen ya disponible en Docker Hub que contiene Node versión 8. Iniciamos la edición del archivo presionando la tecla *i* y colocamos el siguiente texto:

```docker
FROM node:8
```

El proximo paso es definir un directorio de trabajo dentro del contenedor. Esto lo hacemos utilizando el comando:

```docker
WORKDIR /usr/src/server
```

La imagen ya tendrá nodejs instalado, por ende tenemos que copiar los archivos que necesitamos al contenedor. Copiamos el archivo *package.json* para luego instalar todas las dependencias. Esto lo hacemos ejecutando los siguientes dos comandos:

```docker
COPY package*.json ./

RUN npm install
```

Finalmente copiamos el código fuente de nuestro servidor node al contenedor definiendo el siguiente comando en nuestro Dockerfile.

```docker
COPY . .
```

Los contenedores Docker por defecto están aislados del mundo exterior. Dado que estamos construyendo un servicio web, tenemos que permitir la comunicación entre el mundo exterior y su contenedor. Lo ideal sería hacerlo a través de variables de entorno (como está definido en el código) para para mantenerlo simple vamos a exponer el puerto que necesitamos.

```docker
EXPOSE 8081
```

Finalmente el contenedor necesita ejecutar algo. La última línea del Dockerfile en nuestro caso debe ser el comando de ejecución del servidor. 

```docker
CMD [ "npm", "start" ]
```

El docker file completo se ve de esta forma:

```docker
FROM node:8

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 8081
CMD [ "npm", "start" ]
```

Terminamos nuevamente guardando el archivo y cerrando el editor *vi* presionando *esc* seguido de la combinación de teclas *:wq* y *enter*
 
Como no queremos que copie las dependecias locales y solo el código fuente, vamos a crear un archivo *.dockerignore* que va a permitir que se ignoren ciertas partes de la estructura del directorio.

```shell
vi .dockerignore
```

En este archivo colocamos lo siguiente:

```docker
node_modules
npm-debug.log
```

Guarde y cierre el archivo (*esc*, luego *:wq* y *enter)*.
 
El próximo paso es crear la imagen. Esto lo realizamos de la siguiente forma (no se olviden del punto al final).

```shell
sudo docker build -t participant<NUMERO PARTICIPANTE>/node-server .
```

Si listamos las imagenes locales que tenemos deberíamos ver la que acabamos de crear. Podemos listar las imagenes locales uando el siguiente comando.

```shell
sudo docker images

REPOSITORY               TAG                 IMAGE ID            CREATED             SIZE
<your username>/node-server     latest              ebb132c36bc6        24 seconds ago      678MB
```

Se procede a correr un contenedor desde esa imagen. Esto lo hacemos de la siguiente forma, reemplazando ```<your username>``` con su usuario de *Docker Hub*:

```shell
sudo docker run -p 8081:8081 -d --name server <your username>/node-server
```

La columna *STATUS* nos dice si está corriendo o no. <br/>
Podemos ver si está corriendo ejecutando el comando:
```shell
sudo docker ps
```
y si queremos ver el log del servicio, podemos ejecutar:

```shell
sudo docker logs <container id>
```

donde container id lo sacan del comando anterior. Si todo está arriba podemos probar nuevamente desde el browser y verificar que el servicio responde.

```
Si listan los contenedores que tienen corriendo(*docker ps*), debería verse algo como a continuación:
```shell
CONTAINER ID        IMAGE                  COMMAND             CREATED             STATUS              PORTS                    NAMES
3ede7da7a304        tmaragno/node-server   "npm start"         4 minutes ago       Up 4 minutes        0.0.0.0:8081->8081/tcp   server
```

Prueben nuevamente lo servicios y asegurense que todo siga funcionando.

# Fin parte 3


