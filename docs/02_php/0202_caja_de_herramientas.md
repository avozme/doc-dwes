---
layout: page
title: 2.2 Caja de herramientas
permalink: /php/caja-de-herramientas
nav_order: 2
has_children: false
parent: 2 Introducción a PHP
grand_parent: Desarrollo Web en Entorno Servidor
---

## 2.2. Caja de herramientas para desarrollar de aplicaciones web
{: .no_toc }

- TOC
{:toc}

Para desarrollar apliaciones web necesitamos una caja de herramientas bastante completa. Algunas herramientas son fundamentales, como el martillo o el destornillador de una caja de herramientas convencional. Otras, en cambio, son optativas y dependerán del trabajo que vayamos a realizar y de nuestras propias preferencias como desarrolladores.

En esta sección vamos a hacer un repaso de las herramientas fundamentales, las que no pueden faltar en tu caja de herramientas. Algunas ya las conoces y otras las aprenderemos a manejar a lo largo de este curso. Se trata de:

* DHTML (HTML, CSS y Javascript)
* PHP u otro lenguaje de script de servidor (Python, Ruby, Perl, etc)
* MySQL / MariaDB u otro SGBD que permita acceso remoto.

### 2.2.1. HTML

DHTML (Dynamic HTML) no es un lenguaje como tal, sino que, como probablemente sabes ya, es la conjunción de tres lenguajes:

* HTML
* CSS
* JavaScript

DHTML y PHP son los lenguajes que nos van a permitir ejecutar programas en el servidor y acceder a sus recursos a través de páginas web, pero existen otras posibles combinaciones como:

* DHTML con ASP
* DHTML con JSP
* DHTML con Python, Ruby, Perl, etc.

HTML significa "HyperText Markup Language" (Lenguaje de Etiquetas de Hipertexto). Como sin duda sabrás, se trata de un lenguaje para formatear documentos:

* Permite definir el tipo de letra, tamaño, formato y color de los textos.
* Permite insertar imágenes y otro contenido multimedia.
* Permite crear listas, tablas, enumeraciones...
* Permite crear enlaces entre secciones del mismo documento, o enlaces con otros documentos (hipertexto)

HTML **NO** es un lenguaje de programación: no permite programar algoritmos. Pero sí permite incrustar otros lenguajes de programación en su interior, aumentando así su potencia.

Los trozos de código embebidos dentro de HTML se denominan ***scripts***.

#### Brevísima historia de HTML

* En 1990 se crea HTML (procedente de un lenguaje anterior, SGML) junto con la World Wide Web, para formatear los documentos de la www.
* Se amplía en sucesivas versiones hasta la 3.0, que no consiguió éxito debido a las limitaciones de los navegadores de la época.
* Comienza la guerra de navegadores: Microsoft y Netscape sacan sus propios “dialectos” de HTML y destrozan en estándar.
* A partir de HTML 4 se intenta unir las características de los dos, pero el resultado es demasiado complejo.
* Se hace evidente que hay que hacer una “limpieza” de HTML
   * Así surge XHTML, la versión XML de HTML, mucho más estricta y formal, con menos añadidos pero igual de potente.

Las versiones actuales de HTML son:

* HTML 4.01 transicional: HTML clásico, con todos los elementos del HTML antiguo. En la actualidad está obsoleto, pero aún quedan muchas páginas antiguas que lo utilizan.
* HTML 4.01 estricto: también llamado XHTML, no permite usar los elementos HTML desaprobados, tales como definición de formatos. También se considera obsoleto.
* HTML5: elimina definitivamente los elementos antiguos del lenguaje e incorpora algunos nuevos para completar la asimilación con XML. Es el estándar actual.
* La especificación para HTML6 (o HTML Next) está actualmente en desarrollo.

### 2.2.3. CSS

CSS significa "Cascade Style Sheet" (Hojas de estilo en cascada).

CSS es un lenguaje para la definición de los formatos utilizados en una página web. Sólo permite definir el formato (es decir, el aspecto) de la página, no su contenido.

Al definir los formatos en otra parte, se pueden reutilizar a lo largo de una o incluso de varias páginas: si cambiamos la definición CSS del formato, se cambian automáticamente los formatos de todas las páginas que usen esa definición.

El objetivo último de CSS es **separar completamente el formato de la página de su contenido**.

CSS 2.1 se usaba con HTML 4. CSS3 se usa con HTML5 y se considera el estándar actual. Está soportado universalmente, aunque, como sin duda habrás sufrido en tus carnes, los diferentes navegadores pueden interpretar de forma ligeramente distinta algunas definiciones CSS.

### 2.2.4. Javascript

JavaScript es un lenguaje interpretado que puede ser incrustado dentro del código HTML de una página web.

El código JavaScript puede interactuar y modificar cualquier parte del documento HTML, por lo que dota a las páginas web de dinamismo e interactividad.

**JavaScript no es Java**, por mucho que su nombre se parezca. También su sintaxis puede recordar un poco a Java en algunas ocasiones. Pero déjame que te lo repita de nuevo: Javascript no es Java.

La implementación de JavaScript de cada navegador es distinta, obteniéndose resultados que no siempre son iguales, por desgracia para los desarrolladores. Por ejemplo:

* V8 = motor JS de Chrome
* WebKit = motor JS de Safari
* Rhino = motor JS de Mozilla Firefox
* WebKit = motor JS de Microsoft Edge

### 2.2.5. PHP

PHP es un acrónimo recursivo. Significa “PHP Hypertext Preprocessor”

Sí, así es el sentido del humor de los informáticos. Qué le vamos a hacer.

Es un lenguaje de programación de propósito general. Junto con librerías como PHP-Qt o PHP-GTK, puedes programar con él cualquier aplicación de escritorio.

Pero, por circunstancias más debidas al azar que a otra cosa, se empezó a usar para desarrollo web al comienzo de la web 2.0, y hoy en día se utiliza casi exclusivamente para ese propósito.

Cuando se usa en desarrollo web, PHP aparece embebido dentro de documentos HTML.

#### Características de PHP

* PHP permite conectarse con múltiples bases de datos: MySQL, MariaDB, Oracle, PostgreSQL, SQL Server, DB2, etc. También puede conectar por ODBC.
* Se parece mucho a otros lenguajes de tercera generación y orientados a objeto (en particular a C/C++ y, por tanto, a Java). Su curva de aprendizaje para los que ya saben programar es muy plana.

#### Brevísima historia de PHP

* Surge en 1995 como extensión de CGI (otro lenguaje para acceso a funciones del servidor)
* PHP3 (1998) tuvo un gran éxito comercial.
* PHP4 (2000) es la versión más extendida (por desgracia): la mayoría de los scripts en PHP que circulan por la red están escritos en esta versión obsoleta.
* PHP5 (2004) tiene soporte para orientación a objetos y una biblioteca de clases bastante bien diseñada. Por lo tanto, desde esta versión PHP pasa de ser un lenguaje estructurado (3GL) a ser un lenguaje orientado a objetos.
* PHP6 empezó a desarrollarse en 2007 y se canceló en 2014.
* PHP7 introdujo novedades menores y estuvo vigente hasta 2020. En el momento de escribi esto (junio de 2021) es la versión dominante en la mayoría de los servidores web.
* PHP8 es la última versión (8.0.7 en junio de 2021). Las versiones PHP4 y PHP5 se consideran obsoletas e inseguras. Aún existe soporte para PHP7, pero todas las nuevas aplicaciones se deberían escribir pensando en PHP8.

#### Lo nuevo en PHP 8

PHP 8 no tiene demasiadas novedades con respecto a PHP 7, como este no las tenía con respecto a PHP 5.

Debes tener en cuenta que el mayor salto evolutivo se produjo entre PHP 4 y PHP 5. A partir de ahí, y para principiantes como nosotros, la cosa no ha cambiado demasiado.

Algunas de las novedades más destacables de PHP 8 son:

* Mejoras importantes de rendimiento, con la aparición de JIT (Just in Time Compiler), un compilador de PHP que trabaja de forma transparente al programador para incrementar la velocidad de ejecución.
* Mejoras menores en el manejo de las clases y métodos abstractos.
* Simplificación en la declaración de atributos.
* Posibilidad de usar arrays con índices negativos.
* Etc

#### Ventajas de PHP sobre otros lenguajes

* Es un lenguaje libre y abierto.
* Es muy eficiente.
* Es ejecutable en (casi) cualquier servidor.
* Cuenta con una excelente documentación y miles de foros y sitios donde consultar dudas.
* La curva de aprendizaje es baja si ya sabes programar.
* Existen mogollón de entornos de desarrollo para PHP, para todos los gustos.
* Fácil interoperatibilidad con otros sistemas, en particular con bases de datos.
* Comunidad muuuy grande.
* Aunque llevan décadas diciendo que es un lenguaje moribundo, lo cierto es que sigue siendo líder del mercado de aplicaciones web.

#### Inconvenientes de PHP

* Fallos de diseño (corregidos en su mayoría a partir de PHP 5), como:
   * Los métodos para acceso a bases de datos cambian según el SGBD usado.
   * Nombres de funciones inconsistentes.
   * No es completamente orientado a objetos.
   * Tipado confuso y, a veces, impredecible.
* Grandes (e incompatibles) cambios entre versiones.
* Pérdida lenta pero constante de cuota de mercado.
* Pésima relación señal/ruido en la web: ¡hay demasiados *malos* desarrolladores en PHP!

### 2.2.6. MariaDB

Otra de las herramientas básicas de nuestra caja de herramientas es el gestor de bases de datos relacionales (SGBD).

MySQL / MariaDB es el SGBD líder del mercado de las aplicaciones web. Nos permitirá conectarnos a la base de datos y ejecutar sentencias SQL de forma remota al visitar una aplicación web.

Existen otras posibilidades, desde luego, como:
* SQL Server
* Oracle
* PostgreSQL
* SQLite

También está la posibilidad de usar base de datos no relacionales, como MongoDB, Cassandra o Redis. PHP puede conectarse también a estos sistemas, pero la forma de trabajar es diferente que con bases de datos relacionales. Como estas últimas son, de lejos, las predominantes en el mercado, nos centraremos en ellas.

#### Características de MariaDB

* MariaDB es un gestor de bases de datos relacional multiusuario y multiplataforma.
* Permite mútiples conexiones remotas.
* Es software libre.
* Existen librerías para acceder a MariaDB desde muchos lenguajes: C/C++, Java, PHP, Perl, Pascal... Además, hay drivers ODBC.
* Está muy extendida en aplicaciones web, generalmente en combinación con PHP.
* Cuenta un interfaz gráfico programado en PHP, llamado PHPMyAdmin, que se ejecuta en el navegador web. Por supuesto, se puede usar cualquier otro cliente compatible con MySQL, como MySQL Workbench.

#### Brevísima historia de MariaDB

* MySQL surgió como un proyecto OpenSource en Suecia en 1995.
* El objetivo era lograr un SGBD rápido y fiable que cumpliera con el estándar SQL.
* Las primeras versiones (que se denominaron mSQL) eran muy ineficientes.
* La popularización de PHP y su ganancia en eficiencia a partir de la versión 3 la han hecho muy popular en la actualidad.
* Tras su adquisición por Oracle, se intentó relegar al segmento medio-bajo en el mercado de los SGBD y surgió un fork: MariaDB.
* Versión más reciente (junio 2021): MariaDB 10.5.10

