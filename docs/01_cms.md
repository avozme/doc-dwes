---
layout: page
title: 1 Sistemas gestores de contenido (CMS)
permalink: /cms/
nav_order: 1
has_children: false
parent: Desarrollo Web en Entorno Servidor
---
# 1. CMS: Sistemas gestores de contenido

## 1.1. Desarrollo web clásico vs CMS

Desarrollar sitios web usando HTML, CSS, JavaScript, PHP, etc. tiene muchas ventajas:
Permite sacar el máximo partido de las posibilidades de Internet.
Nos da un control absoluto sobre el sitio web que estamos desarrollando.
Pero también tiene inconvenientes:
La creación de un sitio desde cero es un proceso muy largo.
Las ampliaciones y actualizaciones del sitio también resultan lentas y costosas.
Ambas tareas (creación y actualización) requieren personal altamente cualificado, con conocimientos de todas las tecnologías implicadas (HTML, CSS, PHP, Ajax, etc).
Si los inconvenientes superan a las ventajas, es conveniente usar un CMS.
Un CMS (Content Management System) es un programa, escrito generalmente en PHP, que se ejecuta en un servidor web y se controla desde un navegador (cliente), permitiéndonos:
Crear a través del navegador un sitio web completamente nuevo en muy poco tiempo.
Administrar fácilmente todo lo relacionado con el sitio web: usuarios, privilegios, contenido, apariencia, menús, etc.
Y todo ello sin tener conocimientos de HTML, CSS, PHP ni el resto de tecnologías (ojo: no es necesario, pero sí conveniente)

## 1.2. Cómo funciona un CMS

El CMS guarda el contenido del sitio web en una base de datos.
Cuando se solicita una página, un script PHP busca el contenido de esa página en la BD y la genera dinámicamente, enviándola al navegador (cliente).
Además, otro conjunto de scripts PHP permiten agregar nuevo contenido, modificar el contenido existente, crear usuarios, gestionar privilegios, etc.
Al sitio web en sí se le suele denominar front-end. El front-end es lo que ve el visitante de la web.
A las páginas de adminsitración del sitio se les llama back-end o dashboard. El back-end sólo es accesible a algunos usuarios.
El CMS necesita, por ello, un control de acceso de usuarios o login.

## 1.3. Tipos de CMS

Hay un montón de CMS, y cada uno tiene sus propias características, puntos fuertes y puntos débiles.
Podemos clasificarlos según su método de distribución:
Código abierto y software libre.
Código propietario.
Pero suele ser más útil clasificarlos por su funcionalidad:
CMS genéricos (para cualquier tipo de sitio web)
CMS para blogs.
CMS para foros.
CMS para wikis.
CMS para e-learning (aprendizaje por internet)
CMS para e-commerce (comercio electrónico)
CMS para publicaciones digitales (periódicos, revistas...)


Los CMS actuales son fuertemente incompatibles
Cada uno utiliza un interfaz distinto, bases de datos completamente diferentes para almacenar la información, módulos incompatibles, etc.
Existen algunas iniciativas para lograr que los servicios desarrollados en un CMS puedan utilizarse en otros, pero todavía están en un estadio muy inicial.
Lo que sí existen son familias de CMS relacionados entre sí que pueden compartir algunas características, generalmente porque unos CMS han derivado de otros.

## 1.4. Algunos CMS

Los CMS propietarios no han podido competir con los CMS libres.
Por ello, han evolucionado hacia soluciones cloud computing completas, como:
Microsoft Azure
Apple iCloud
Google Cloud Platform
Amazon Web Services
Apache CloudStack
Etc.

Para blogs:
WordPress
Calepin
Scriptogram
Jeckyll
Anchor
Etc.
Para wikis:
MediaWiki
WikkaWIki
DokuWiki
Etc.

Para foros:
phpBB
MyBB
VBulletin
Simple Machines Forum
Etc.
Para e-learning:
Moodle
WebCT
Mahara
Claroline
Etc.

Para e-commerce:
PrestaShop
Magento
OsCommerce
Zen Cart
Etc.
Otros CMS específicos:
eGroupWare: para groupware (desarrollo colaborativo)
ownCloud: almacenamiento de archivos.
Coppermine: galerías de imágenes.
PyASC: galerías de arte.
Lista actualizada de CMS en Wikipedia.

## 1.5. Instalación de un CMS

IMPORTANTE: la instalación puede diferir notablemente de un CMS a otro.
Hay que leer cuidadosamente las instrucciones de instalación, que encontrarás en la web del desarrollador.
Pasos que suelen ser habituales en casi todos los CMS:
Descargar la última versión del programa de la web del desarrollador.
Asegurarse de que el servidor cumple los prerrequisitos para ejectuar el CMS (versión de Apache, PHP, MySQL u otro software necesario)
Subir el CMS por ftp al servidor.
Crear la base de datos.
Lanzar la instalación del CMS.
Adapar el archivo de configuración (suele llamarse config.php, config.inc, o algo similar). En los CMS más elaborados este paso no es necesario, pues el programa de instalación se encarga de generar un archivo de configuración válido.
A veces, hay que modificar los permisos de algún directorio y/o archivo.
Instalar el paquete de idioma español (si está disponible)

## 1.6. Explotación de un CMS

IMPORTANTE: la explotación puede diferir notablemente de un CMS a otro.
Hay que leer cuidadosamente las instrucciones de uso, que encontrarás en la web del desarrollador.
Pasos que suelen ser habituales en casi todos los CMS, una vez realizada la instalación:
Asignar una password de alta seguridad al usuario administrador que se crea por defecto.
Crear otros usuarios y asignarles privilegios.
Editar la página de inicio del sitio web.
Cambiar la plantilla (apariencia) del sitio.
Instalar módulos de ampliación (si es necesario).
Crear el contenido y/o revisar el contenido creado por otros usuarios.
