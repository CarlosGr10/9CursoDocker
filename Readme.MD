# CURSO DE DOCKER 🐋

# Virtualizacion
Permite atacar en simultáneo los tres problemas del desarrollo de software profesional.

## Problemas de la virtualizacion

- PESO: En el orden de los GBs. Repiten archivos en común. Inicio lento.
- COSTO DE ADMINISTRACION: Necesita mantenimiento igual que cualquier otra computadora.
- MULTIPLES DE FORMATO: VDI, VMDK, VHD, raw, etc

## Containerización

El empleo de contenedores para construir y desplegar software.

Flexibles
Livianos
Portables
Bajo acoplamiento
Escalables
Seguros

## Virtualizacion vs Containerización

Virtualización: A diferencia de un contenedor, las máquinas virtuales ejecutan un sistema operativo completo, incluido su propio kernel.
Containerización: Un contenedor es un silo aislado y ligero para ejecutar una aplicación en el sistema operativo host. Los contenedores se basan en el kernel del sistema operativo host (que puede considerarse la fontanería del sistema operativo), y solo puede contener aplicaciones y algunas API ligeras del sistema operativo y servicios que se ejecutan en modo de usuario.

# Qué es y cómo funciona Docker

![](https://i.imgur.com/spx30aQ.png)

![](https://i.imgur.com/TRYEMSr.png)

*Componentes DENTRO del circulo de Docker:*

Docker daemon: Es el centro de docker, el corazón que gracias a el, podemos comunicarnos con los servicios de docker.

REST API: Como cualquier otra API, es la que nos permite visualizar docker de forma “gráfica”.

Cliente de docker: Gracias a este componente, podemos comunicarnos con el corazón de docker (Docker Daemon) que por defecto es la línea de comandos.
Dentro de la arquitectura de Docker encontramos:

- Contenedores: Es la razón de ser de Docker, es donde podemos encapsular nuestras imagenes para llevarlas a otra computadora, o servidor, etc.

- Imagenes: Son las encapsulaciones de x contenedor. Podemos correr nuestra aplicación en Java por medio de una imagen, podemos utilizar Ubuntu para correr nuestro proyecto, etc.

= Volumenes de datos: Podemos acceder con seguridad al sistema de archivos de nuestra máquina.

- Redes: Son las que permiten la comunicación entre contenedores.

# Primeros pasos: hola mundo

Nota: Antes de correr nuestro primer contenedor hay que asegurarnos de agregar un usuario para correr sin root

```
$ sudo groupadd docker
$ sudo usermod -aG docker name_user
$ newgrp docker

```

Comando para correr nuestro primer contenedor 😀

``` 
    docker run hello-world 
```

# Conceptos fundamentales de Docker: contenedores

Es una agrupación de procesos.

Es una entidad lógica, no tiene el limite estricto de las máquinas virtuales, emulación del sistema operativo simulado por otra más abajo.

Ejecuta sus procesos de forma nativa.

Los procesos que se ejecutan adentro de los contenedores ven su universo como el contenedor lo define, no pueden ver mas allá del contenedor, a pesar de estar corriendo en una maquina más grande.

No tienen forma de consumir más recursos que los que se les permite. Si esta restringido en memoria ram por ejemplo, es la única que pueden usar.

A fines prácticos los podemos imaginar cómo maquinas virtuales, pero NO lo son. Máquinas virtuales livianas.

Docker corre de forma nativa solo en Linux.

Sector del disco: Cuando un contenedor es ejecutado, el daemon de docker le dice, a partir de acá para arriba este disco es tuyo, pero no puedes subir mas arriba.

Docker hace que los procesos adentro de un contenedor este aislados del resto del sistema, no le permite ver más allá.

Cada contenedor tiene un ID único, también tiene un nombre.

# Comprendiendo el estado de Docker

Saber que contenedores estan correindo en el deamon de docker 

```
    docker ps
```

Ver todos los contenedores de docker , nota: cuando realizamos un docker run , estamos creando un nuevo contenedor y lo ejecuta

```
    docker ps -a 
```

Para ver la información de un contenedor 

```
    docker inspect id/nombre
```


ponerle un nombre a un contenedor con la opcion --name
y renombrar un contenedor 

```
    docker run --name hola1 hello-world

    docker rename hola1 nombre_formal
```

Eliminar los contenedores que ya no utilizamos, 
prune nos elimina todos los contenedores que estan parados

```
    docker rm id/nombre_contenedor
    docker container prune
```


# El modo interactivo


```
    docker run ubuntu
    docker run -it ubuntu
```

# Ciclo de vida de un contenedor (segundo plano)

Cuando un proceso falla, el contenedor se detiene

El modo detach , el contenedor corre en segundo plano

```
    docker run --name hey -d ubuntu tail -f /dev/null
```

Entrar al contenedor con el comando exec

```
    docker exec -it id/contenedor shell
```

Dentro del contenedor de docker podemos ejecutar el siguinte comando

```
    ps -aux
```

Otra forma de parar los contenedores 

```
    docker inspect --format '{{.State.Pid}}' id/contenedor
    
    kill numero_pid
```

# Exponiendo contenedores (Puertos)

Para enfocarnos en este ejemplo utilizamos nginx
la bandera -p es de publish, que es la que expone el pueto del contenedor
del lado izquierdo es la de nuetra maquina y el lado derecho es la del contenedor
**-p puertoMáquna:puertoContenedor**

```
    docker run -d --name proxy -p 8080:80 nginx
```

![](https://i.imgur.com/Xat2Lst.png)

Ver los logs del contenedor

```
    docker logs -f proxy
```


#  Bind mounts

Utilizaremos mongodb 

```
    docker run -d --name db mongo
```

dentro del contenedor utilizamos

```
    $ mongogs
    $ show dbs
    $ use banco
    $ db.users.insert({"nombre":"carlos"})
    $ db.users.find()
```

Cuando salimos del contenedor nos damos cuenta que no guardo informacion
lo que hacemos es montar un bind mount

creamos una carpeta y despues ejecutamos el sig. comando

```
    docker run -d --name db -v /home/garcia/Contenedores/dockerdata/mongodata:/data/db mongo
```

# Volúmenes

La diferencia con bind mount es que uno requiere una carpeta fuera del contenedor
y los volumenes son respaldos que maneja docker virtualmente


Listar los volumenes

```
    docker volume ls
```

Crear volumenes

```
    docker volume create nombre_volumen
```

Montar los volumenes

tiene dos parametros mount , 

- src: el el volumen que se le va a montar
- dst: la ruta del contenedor donde se va montar ese volumen 

```
    docker run --name  db -d --mount src=dbdata,dst=/data/db mongo
```

Inspeccionar los volumenes

```
    docker inspect nombre_volumen
```

# Insertar y extraer archivos de un contenedor

### Agregando unn archivo de local hacia el servidor

Creamos un contenedor y creamos un directorio

```
    docker run -it --name test ubuntu
    docker exec -it test bash
    mkdir testing
```

Creamos un archivo , y lo copiamos dentro del contenedor

```
    touch prueba.txt
    docker cp prueba.txt test:/testing/tes.txt
```

### Obteniendo un directorio del contenedor

```
    docker cp test:/testing localtesting
```

# Conceptos fundamentales de Docker: imágenes

Las imagenes son como plantillas o moldes donde hacemos la construccion de contenedores
estas tienen blibliotecas y librerias

Podemos bajar diferentes imagenes de ubuntu en Dockerhub

```Dockerfile
    FROM ubuntu:latest

    RUN touch /usr/src/hola-docker.txt

    RUN chmod 777 /opt

    RUN mkdir /opt/backup1

    RUN mkdir /opt/backup2

    RUN mkdir /opt/app
```

Comando para construir nuestras imagenes
```
    docker build -t ubuntu:lubuntu .
```

Creamos carpetas para montar nuestros volumenes
```
    docker run -it -d -v /home/garcia/Contenedores/imagenes/backup/b1:/opt/backup1 -v /home/garcia/Contenedores/imagenes/backup/b2:/opt/backup2 -v /home/garcia/Contenedores/imagenes/backup/b3:/opt/app --name cool ubuntu:lubuntu
```

# El sistema de capas

El dockerfile sus capas son las lineas que ejecutamos 

```
    docker history ubuntu:lubuntu
```

La importancia de entender el sistema de capas consiste en la optimización de la construcción del contenedor para reducir espacio ya que cada comando en el dockerfile crea una capa extra de código en la imagen.

Agregando Capas

Con docker commit se crea una nueva imagen con una capa adicional que modifica la capa base.

para ver los layers de la imagenes podemos utiliar docker ![dive](https://github.com/wagoodman/dive)


# Usando Docker para desarrollar aplicaciones

```
    git clone https://github.com/platzi/docker

    docker build -t platziapp .

    docker run --rm -p 3000:3000 platziapp 
    
    (creo el contenedor y cuando se detenga se borra, lo publica el puerto 3000)
    -- rm es una bandera para ejecutar un contenedor , pero cuando se apage lo elimina
```

Instrucciones del Dockerfile

- FROM -> La imagen de referencia que vamos a montar

- COPY -> Copia los archivos de nuestro local hacia el contenedor

- WORKDIR -> Es el punto donde va a trabajar los comandos del dockerfile

- RUN -> Es ajecutar un comando

- EXPOSE -> Se pueda acceder a este cotenedor desde este puerto

- CMD -> Definir el comando predeterminado que se ejecutará cuando se inicie un contenedor a partir de la imagen Docker construida


# Aprovechando el caché de capas para estructurar correctamente tus imágenes

Layer cache -> no vuelve a costruir sobre algo nuevo

Si cambiamos la base (FROM) es no entra el layer cache ya que instala todo de nuevo

Elegir bien los archivos a copiar hacia el contenedor

Para optimizar el Dockerfile y no estar ejecutando build constantemente, lo ejecutamos como un bind mount

```
    docker run --rm -p 3000:3000 -v $(pwd)/index.js:/usr/src/index.js platziapp
```








