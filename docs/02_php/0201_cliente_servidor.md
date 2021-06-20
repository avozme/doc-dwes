---
layout: page
title: 2.1 Programación cliente-servidor
permalink: /php/programacion-cliente-servidor
nav_order: 1
has_children: false
parent: 2 Introducción a PHP
grand_parent: Desarrollo Web en Entorno Servidor
---

## 2.1. Programación cliente-servidor
{: .no_toc }

- TOC
{:toc}

En los primeros tiempos de Internet, no se ejecutaban programas en el servidor. Solo se pedían páginas estáticas más o menos elaboradas que había sido grabadas en el servidor por un administrador de sistemas. A esto se le denomina web 1.0.

A alguien se le ocurrió la idea de que los propios visitantes podrían también crear contenido. Ese contenido se guardaría en el servidor (en archivos o en una base de datos) y posteriormente podría recuperarse para generar con él una web dinámica, que no existía previamente y que nadie, en realidad, ha tecleado.

Esa web dinámica estaría generada por un programa ejecutado en el servidor, un programa cuya salida sería HTML válido, comprensible por el navegador que la reciba. A esto se le denomina web 2.0 y supuso una revolución tan grande como el propio nacimiento de Internet.

### 2.1.1. Un poco de jerga informática

Antes de continuar, tienes que asegurarte de que comprendes bien el significado de algunos términos:

* Un **servidor** es un programa que se ejecuta en una máquina conectada a una red y que permanece dormido hasta que una petición procedente de la red lo despierta. Entonces, el programa hace algo (consulta datos, elabora un cálculo, lo que sea) y devuelve su resultado por la red.
* Por extensión, un servidor también es cualquier ordenador donde se ejecute un programa servidor. Es decir, usamos la misma palabra para referirnos a un programa y al ordenador donde se ejecuta ese programa. Mala idea, ya lo sé, pero es lo que hay.
* El **cliente** es el programa que envía esas peticiones al programa servidor para despertarlo. También es el programa que recoge el resultado devuelto por el servidor.
* Por extensión, la máquina donde se ejecuta un programa cliente también se llama cliente.

Pues bien, en programación web, nuestro cliente es el **navegador web** (también llamado cliente web). Cualquier navegador del universo conocido entra en esta categoría (excepto, tal vez, Internet Explorer).

Y un servidor es cualquier máquina de la red donde se esté ejecutando un programa servidor web como Apache, Nginx, Tomcat, IIS y otros cuando viejos amigos que irás conociendo a lo largo de este curso.

### 2.1.2. Una petición web en la época 1.0

Ahora que tienes claro qué es un servidor y un cliente web, puedes comprender el siguiente esquema.

En él, se ilustra lo que ocurre cuando un cliente web (recuerda: tu navegador) envía al servidor la peiticón de una **página estática**. 

El servidor, en este caso, se limita a enviar al cliente el documento HTML tal cual está almacenado en su disco duro, sin cambiar una sola coma.

![Ejemplo de servicio www](/assets/images/02-servicio-www-1.jpg)

### 2.1.3. Una petición web en la época 2.0

Con la web 2.0 la cosa cambia bastante porque aparecen las **páginas dinámicas**, aunque tendrás que fijarte bien en el esquema para apreciar la diferencia, ¿verdad?

Quédate con lo importante: en este esquema, el cliente web no pide un documento HTML, sino *un programa*, que puede estar escrito en PHP o algún otro lenguaje, eso es lo de menos. 

Ese programa se ejecuta en el servidor, y *el resultado de esa ejecución* es lo que recibe el cliente, *no el programa en sí*.

![Ejemplo de servicio www](/assets/images/02-servicio-www-2.jpg)

Así es como funcionan las aplicaciones web.
