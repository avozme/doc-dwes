---
layout: page
title: 1.1 Algunas cosas que debes saber sobre los CMS
permalink: /cms/algunas-cosas-que-debes-saber
nav_order: 1
has_children: false
parent: 1 Sistemas gestores de contenido (CMS)
grand_parent: Desarrollo Web en Entorno Servidor
---


## 1.1. Algunas cosas que debes saber sobre los CMS
{: .no_toc }

- TOC
{:toc}

### 1.1.1. Inconvenientes de desarrollar una web desde cero

Desarrollar sitios web programándolos desde cero (o más o menos desde cero, porque la mayor parte de las veces se parte de librerías existentes) tiene varias ventajas, como, por ejemplo:

* Permite sacar el máximo partido tanto del servidor como de los clientes.
* Nos da un control absoluto sobre el sitio web que estamos desarrollando.
* Nos posibilita ajustarnos al máximo a los requerimientos y crear aplicaciones a medida.

Pero también tiene inconvenientes:

* La creación de un sitio desde cero es un proceso muy largo.
* Las ampliaciones y actualizaciones del sitio también resultan lentas y costosas.
* Ambas tareas (creación y actualización) requieren personal altamente cualificado, con conocimientos de todas las tecnologías implicadas. Es decir, desarrolladores web. Y eso cuesta dinero.

Y, cuando los inconvenientes superan a las ventajas, muchas personas se pasan al CMS.

### 1.1.2. Cómo funciona un CMS

**Un CMS (Content Management System)** es una aplicación web que se ejecuta en un servidor y se controla desde un navegador (cliente), y que nos permite:

* Crear a través del navegador un sitio web completamente nuevo en muy poco tiempo.
* Administrar fácilmente todo lo relacionado con el sitio web: usuarios, privilegios, contenido, apariencia, menús, etc.
* Y todo ello sin tener conocimientos de HTML, CSS, PHP ni el resto de tecnologías (ojo: no es necesario, pero sí conveniente)

El CMS guarda el **contenido** del sitio web en una **base de datos**.

Cuando se solicita una página, un programa escrito en PHP (o en otro lenguaje de servidor) busca el contenido de esa página en la BD y la genera dinámicamente, enviándola al navegador (cliente).

Además, otro conjunto de programas permiten agregar nuevo contenido, modificar el contenido existente, crear usuarios, gestionar privilegios, etc. Todo ello altera los datos existentes en la BD, que a su vez alteran la forma en la que el usuario percibe la página cuando la visita.

Al sitio web en sí se le denomina a veces ***front-end***. El front-end, en este sentido es lo que ve el visitante de la web.

A las páginas de adminsitración del sitio se les llama a veces ***back-end*** o ***dashboard*** (panel de administración). El back-end sólo es accesible a algunos usuarios (administradores, editores, etc). El CMS siempre necesita, por ello, un control de acceso de usuarios o login.

¡Cuidado! Los términos front-end y back-end son confusos. En términos de programación, a menudo se denomina ***front-end*** a la salida de una aplicación web, es decir, al interfaz de usuario, y ***back-end*** a la parte de la aplicación que interactúa con los recursos del servidor (como la base de datos). En este otro sentido, el front-end está escrito en HTML, CSS, JavaScript u otros lenguajes del lado del cliente y el back-end está escrito en PHP, Java, Python u otros lenguajes del lado del servidor.

### 1.1.3. Tipos de CMS

Hay un montón (¡pero un montón!) de CMS, y cada uno tiene sus propias características, puntos fuertes y puntos débiles.

Podemos clasificarlos según su método de distribución:

* Código abierto y software libre.
* Código propietario.

Pero suele ser más útil clasificarlos por su funcionalidad:

* CMS genéricos (para cualquier tipo de sitio web)
* CMS para blogs.
* CMS para foros.
* CMS para wikis.
* CMS para e-learning (aprendizaje por internet)
* CMS para e-commerce (comercio electrónico)
* CMS para publicaciones digitales (periódicos, revistas...)

**Los CMS actuales son fuertemente incompatibles.**

Cada uno utiliza un interfaz distinto, bases de datos completamente diferentes para almacenar la información, módulos incompatibles, etc.

Existen algunas iniciativas para lograr que los servicios desarrollados en un CMS puedan utilizarse en otros, pero todavía están en un estadio muy inicial.

Lo que sí existen son familias de CMS relacionados entre sí que pueden compartir algunas características, generalmente porque unos CMS han derivado de otros.

### 1.1.4. Algunos CMS importantes

Los CMS propietarios no han podido competir con los CMS libres. Por ello, han evolucionado hacia soluciones cloud computing completas, como Microsoft Azure, Google Cloud o Amazon Web Services (AWS).

Entre los verdaderos CMS abundan las soluciones opensource o software libre. Por ejemplo:

* Para blogs:

   * WordPress
   * Calepin
   * Scriptogram
   * Jekyll
   * Anchor
   * Etc.

* Para wikis:

   * MediaWiki
   * WikkaWIki
   * DokuWiki
   * Etc.

* Para foros:

   * phpBB
   * MyBB
   * VBulletin
   * Simple Machines Forum
   * Etc.

* Para e-learning:

   * Moodle
   * WebCT
   * Mahara
   * Claroline
   * Etc.

* Para e-commerce:

   * PrestaShop
   * Magento
   * OsCommerce
   * Zen Cart
   * Etc.
   
* Otros CMS específicos:
   * eGroupWare: para groupware (desarrollo colaborativo)
   * ownCloud: almacenamiento de archivos.
   * Coppermine: galerías de imágenes.
   * PyASC: galerías de arte.

Muchos de estos CMS desaparecerán, se fundirán con otros o se dividirán en varios proyectos desde que yo escriba estas líneas hasta que tú las leas. Lo mejor es que eches un vistazo a alguna lista actualizada de CMS, como [esta de Wikipedia](https://en.wikipedia.org/wiki/List_of_content_management_systems).

### 1.1.5. Instalación de un CMS

IMPORTANTE: la instalación puede diferir de un CMS a otro, pero, más o menos, todos necesitan los mismos pasos.

Hay que leer cuidadosamente las instrucciones de instalación, que encontrarás en la web del desarrollador.

Los pasos que suelen ser habituales en casi todos los CMS:

1. Descargar la última versión del programa de la web del desarrollador.
2. Asegurarse de que el servidor cumple los prerrequisitos para ejectuar el CMS (versión de Apache, PHP, MySQL u otro software necesario)
3. Subir el CMS por al servidor (por ftp, vía web o como tu proveedor de hosting te lo permita).
4. Crear la base de datos.
5. Lanzar la instalación del CMS. Esto suele hacerse cargando una dirección concreta en tu navegador.
6. Adapar el archivo de configuración (suele llamarse config.php, config.inc, o algo similar). En los CMS más elaborados este paso no es necesario, pues el programa de instalación se encarga de generar un archivo de configuración válido.
7. A veces, hay que modificar los permisos de algún directorio y/o archivo.
8. Instalar el paquete de idioma español (si está disponible)

### 1.1.6. Explotación de un CMS

IMPORTANTE: la explotación puede diferir notablemente de un CMS a otro, pero, en general, todo tienen una serie de elementos en común.

Hay que leer cuidadosamente las instrucciones de uso, que encontrarás en la web del desarrollador.

Pasos que suelen ser habituales en casi todos los CMS, una vez realizada la instalación:

1. Asignar una password de alta seguridad al usuario administrador que se crea por defecto.
2. Crear otros usuarios y asignarles privilegios.
3. Editar la página de inicio del sitio web.
4. Cambiar la plantilla (apariencia) del sitio.
5. Instalar módulos de ampliación (si es necesario).
6. Crear el contenido y/o revisar el contenido creado por otros usuarios.

