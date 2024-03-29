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
    docker 
```


ponerle un nombre a un contenedor con la opcion --name
y renombrar un contenedor 

```
    docker run --name hola1 hello-world

    docker rename hola1 nombre_formal
```

Eliminar los contenedores que ya no utilizamos, 
prune nos elimina todos los contenedores

```
    docker rm id/nombre_contenedor
    docker container prune
```




