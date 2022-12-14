# CURSO DE DOCKER 馃悑

# Virtualizacion
Permite atacar en simult谩neo los tres problemas del desarrollo de software profesional.

## Problemas de la virtualizacion

- PESO: En el orden de los GBs. Repiten archivos en com煤n. Inicio lento.
- COSTO DE ADMINISTRACION: Necesita mantenimiento igual que cualquier otra computadora.
- MULTIPLES DE FORMATO: VDI, VMDK, VHD, raw, etc

## Containerizaci贸n

El empleo de contenedores para construir y desplegar software.

Flexibles
Livianos
Portables
Bajo acoplamiento
Escalables
Seguros

## Virtualizacion vs Containerizaci贸n

Virtualizaci贸n: A diferencia de un contenedor, las m谩quinas virtuales ejecutan un sistema operativo completo, incluido su propio kernel.
Containerizaci贸n: Un contenedor es un silo aislado y ligero para ejecutar una aplicaci贸n en el sistema operativo host. Los contenedores se basan en el kernel del sistema operativo host (que puede considerarse la fontaner铆a del sistema operativo), y solo puede contener aplicaciones y algunas API ligeras del sistema operativo y servicios que se ejecutan en modo de usuario.

# Qu茅 es y c贸mo funciona Docker

![](https://i.imgur.com/spx30aQ.png)

![](https://i.imgur.com/TRYEMSr.png)

*Componentes DENTRO del circulo de Docker:*

Docker daemon: Es el centro de docker, el coraz贸n que gracias a el, podemos comunicarnos con los servicios de docker.

REST API: Como cualquier otra API, es la que nos permite visualizar docker de forma 鈥済r谩fica鈥?.

Cliente de docker: Gracias a este componente, podemos comunicarnos con el coraz贸n de docker (Docker Daemon) que por defecto es la l铆nea de comandos.
Dentro de la arquitectura de Docker encontramos:

- Contenedores: Es la raz贸n de ser de Docker, es donde podemos encapsular nuestras imagenes para llevarlas a otra computadora, o servidor, etc.

- Imagenes: Son las encapsulaciones de x contenedor. Podemos correr nuestra aplicaci贸n en Java por medio de una imagen, podemos utilizar Ubuntu para correr nuestro proyecto, etc.

= Volumenes de datos: Podemos acceder con seguridad al sistema de archivos de nuestra m谩quina.

- Redes: Son las que permiten la comunicaci贸n entre contenedores.

# Primeros pasos: hola mundo

Nota: Antes de correr nuestro primer contenedor hay que asegurarnos de agregar un usuario para correr sin root

```
$ sudo groupadd docker
$ sudo usermod -aG docker name_user
$ newgrp docker

```

Comando para correr nuestro primer contenedor 馃榾

``` 
    docker run hello-world 
```

# Conceptos fundamentales de Docker: contenedores

Es una agrupaci贸n de procesos.

Es una entidad l贸gica, no tiene el limite estricto de las m谩quinas virtuales, emulaci贸n del sistema operativo simulado por otra m谩s abajo.

Ejecuta sus procesos de forma nativa.

Los procesos que se ejecutan adentro de los contenedores ven su universo como el contenedor lo define, no pueden ver mas all谩 del contenedor, a pesar de estar corriendo en una maquina m谩s grande.

No tienen forma de consumir m谩s recursos que los que se les permite. Si esta restringido en memoria ram por ejemplo, es la 煤nica que pueden usar.

A fines pr谩cticos los podemos imaginar c贸mo maquinas virtuales, pero NO lo son. M谩quinas virtuales livianas.

Docker corre de forma nativa solo en Linux.

Sector del disco: Cuando un contenedor es ejecutado, el daemon de docker le dice, a partir de ac谩 para arriba este disco es tuyo, pero no puedes subir mas arriba.

Docker hace que los procesos adentro de un contenedor este aislados del resto del sistema, no le permite ver m谩s all谩.

Cada contenedor tiene un ID 煤nico, tambi茅n tiene un nombre.

# Comprendiendo el estado de Docker

Saber que contenedores estan correindo en el deamon de docker 

```
    docker ps
```

Ver todos los contenedores de docker , nota: cuando realizamos un docker run , estamos creando un nuevo contenedor y lo ejecuta

```
    docker ps -a 
```

Para ver la informaci贸n de un contenedor 

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




