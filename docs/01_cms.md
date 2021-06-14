---
layout: page
title: 1 Sistemas gestores de contenido (CMS)
permalink: /cms/
nav_order: 1
has_children: false
parent: Desarrollo Web en Entorno Servidor
---
# 1. CMS: Sistemas gestores de contenido

## 1.1. Desarrollo web clásico vs desarrollo web con CMS

Desarrollar sitios web usando HTML, CSS, JavaScript, PHP, etc. tiene muchas ventajas:

* Permite sacar el máximo partido de las posibilidades de Internet.
* Nos da un control absoluto sobre el sitio web que estamos desarrollando.

Pero también tiene inconvenientes:

* La creación de un sitio desde cero es un proceso muy largo.
* Las ampliaciones y actualizaciones del sitio también resultan lentas y costosas.
* Ambas tareas (creación y actualización) requieren personal altamente cualificado, con conocimientos de todas las tecnologías implicadas (HTML, CSS, PHP, Ajax, etc).

Si los inconvenientes superan a las ventajas, es conveniente usar un CMS.

**Un CMS (Content Management System)** es una aplicación web que se ejecuta en un servidor y se controla desde un navegador (cliente), y que nos permite:

* Crear a través del navegador un sitio web completamente nuevo en muy poco tiempo.
* Administrar fácilmente todo lo relacionado con el sitio web: usuarios, privilegios, contenido, apariencia, menús, etc.
* Y todo ello sin tener conocimientos de HTML, CSS, PHP ni el resto de tecnologías (ojo: no es necesario, pero sí conveniente)

## 1.2. Cómo funciona un CMS

El CMS guarda el **contenido** del sitio web en una **base de datos**.

Cuando se solicita una página, un programa escrito en PHP (o en otro lenguaje de servidor) busca el contenido de esa página en la BD y la genera dinámicamente, enviándola al navegador (cliente).

Además, otro conjunto de programas permiten agregar nuevo contenido, modificar el contenido existente, crear usuarios, gestionar privilegios, etc. Todo ello altera los datos existentes en la BD, que a su vez alteran la forma en la que el usuario percibe la página cuando la visita.

Al sitio web en sí se le denomina a veces ***front-end***. El front-end, en este sentido es lo que ve el visitante de la web.

A las páginas de adminsitración del sitio se les llama a veces ***back-end*** o ***dashboard*** (panel de administración). El back-end sólo es accesible a algunos usuarios (administradores, editores, etc). El CMS siempre necesita, por ello, un control de acceso de usuarios o login.

¡Cuidado! Los términos front-end y back-end son confusos. En términos de programación, a menudo se denomina ***front-end*** a la salida de una aplicación web, es decir, al interfaz de usuario, y ***back-end*** a la parte de la aplicación que interactúa con los recursos del servidor (como la base de datos). En este otro sentido, el front-end está escrito en HTML, CSS, JavaScript u otros lenguajes del lado del cliente y el back-end está escrito en PHP, Java, Python u otros lenguajes del lado del servidor.

## 1.3. Tipos de CMS

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

## 1.4. Algunos CMS importantes

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

## 1.5. Instalación de un CMS

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

## 1.6. Explotación de un CMS

IMPORTANTE: la explotación puede diferir notablemente de un CMS a otro, pero, en general, todo tienen una serie de elementos en común.

Hay que leer cuidadosamente las instrucciones de uso, que encontrarás en la web del desarrollador.

Pasos que suelen ser habituales en casi todos los CMS, una vez realizada la instalación:

1. Asignar una password de alta seguridad al usuario administrador que se crea por defecto.
2. Crear otros usuarios y asignarles privilegios.
3. Editar la página de inicio del sitio web.
4. Cambiar la plantilla (apariencia) del sitio.
5. Instalar módulos de ampliación (si es necesario).
6. Crear el contenido y/o revisar el contenido creado por otros usuarios.

## 1.7. Wordpress

Wordpress es sin duda el campeón actual de los CMS. Algunas estadísticas afirman que el 90% de los sitios web de internet está hecho con Wordpress. Probablemente son estadísticas un poco infladas, pero la importancia de este CMS es innegable y cualquier desarrollador web debe conocerlo, aunque sea para odiarlo.

Wordpress es un CMS enfocado a la creación de blogs, aunque, en su estadio actual, permite crear casi cualquier tipo de sitio web: tiendas online, portales, revistas digitales, álbumes de imágenes o recursos de cualquier tipo... 

Está desarrollado en PHP bajo licencia GPL y se ha convertido. Tiene detrás una enorme comunidad de desarrolladores y diseñadores, que se encargan de actualizarlo y de crear plugins y temas para la comunidad.

### 1.7.1. Características principales de Wordpress

* La estética, tanto de resultado como del código fuente, es fundamental para los desarrolladores de WordPress. 
* Las entradas publicadas son ordenadas por fecha, aunque esto se puede modificar. 
* La estructura y diseño visual del sitio depende del sistema de plantillas. 
* La filosofía de Wordpress apuesta decididamente por la elegancia, la sencillez y las recomendaciones del W3C pero depende siempre de la plantilla. 
* Separa el contenido y el diseño en XHTML y CSS, aunque, como se ha dicho, depende de la plantilla que se esté usando. 
* La gestión y ejecución corre a cargo del sistema de administración con los plugins y los widgets que usan las plantillas. 

### 1.7.2. Funcionalidades de Wordpress

Wordpress hace magia. Así de sencillo.

Si te vas a convertir en desarrollador/a web, Wordpress es tu peor enemigo, porque permite que cualquier usuario medio, sin tener ni idea de programación, pueda crear un sitio web solvente y de aspecto profesional en una tarde.

No te voy a engañar: a ti te llevaría meses programar algo parecido desde cero.

Pero Wordpress también tiene sus limitaciones, y cuando sus usuarios las descubren, necesitan a un programador que sepa meterse en las tripas de Wordpress para retorcérselas. Ahí es donde entrarás tú.

De modo que sí: Wordpress es tu peor enemigo, pero puede convertirse en tu mejor aliado.

Para eso, tienes que conocer qué es capaz de hacer y qué no. Entre sus asombrosas funciones podemos contar estas:

* Fácil instalación, actualización y personalización. 
* Posibilidad de actualización automática del sistema implementada en la versión 2.7. 
* Múltiples autores o usuarios, junto con sus roles o perfiles que establecen distintos niveles de permisos desde la versión 2.0). 
* Múltiples blogs o bitácoras (desde la versión 1.6). 
* Capacidad de crear páginas estáticas (a partir de la versión 1.5). 
* Permite ordenar artículos y páginas estáticas en categorías, subcategorías y etiquetas ("tags"). 
* Cuatro estados para una entrada ("post"): Publicado, Borrador, Esperando Revisión (nuevo en Wordpress 2.3) y Privado (sólo usuarios registrados), además de uno adicional: Protegido con contraseña. 
* Editor WYSIWYG "What You See Is What You Get" en inglés, "lo que ves es lo que obtienes" (desde la versión 2.0). 
* Publicación mediante email. 
* Importación desde Blogger, Blogware, Dotclear, Greymatter, Livejournal, Movable Type y Typepad, Textpattern y desde cualquier fuente RSS. Se está trabajando para poder importar desde pMachine y Nucleus además de la importación a través de scripts o directamente de base de datos. 
* Guardado automático temporizado del artículo como Borrador (A partir de la versión 2.2). 
* Permite comentarios y herramientas de comunicación entre blogs (Trackback, Pingback, etc). 
* Permite "permalinks" (enlaces permanentes y fáciles de recordar) mediante mod_rewrite. 
* Distribución de los artículos mediante RDF, RSS 0.92, RSS 2.0 y Atom 1.0. 
* Distribución de las discusiones (mediante RSS 2.0 y ATOM 1.0). 
* Gestión y distribución de enlaces. 
* Subida y gestión de adjuntos y archivos multimedia. 
* Admite plugins para aumentar aún más la fucionalidad, a riesgo de convertirlo en una "monstruo de Frankenstein" hecho a pegotes.
* Admite plantillas y "Widgets" para éstas. 
* Búsqueda en entradas y páginas estáticas y Widget de casa para búsqueda integrada de google desde la versión 2.5.[5] 
    
### 1.7.3. Plantillas de Wordpress

Las plantillas (themes) de Wordpress son diseños CSS que sirven para establecer la apariencia y estructura del blog. Algunas también modifican parte del panel de administración. 

Hay una gran comunidad oficial, tanto profesional como de usuarios, dedicada al diseño de estas plantillas. Puedes encontrarlas tanto en el sitio de Wordpress (comprobadas y aprobadas oficialmente) como en sitios web de terceros. Muchas son gratuitas, otras de pago y, la mayoría, tienen una versión gratuita con funciones adicionales de pago.

Las posibilidades de las plantillas, tanto a nivel de diseño, estructura o gestión, son tan grandes que prácticamente permiten tener desde un simple blog hasta un portal web fuertemente personalizable.

Hay un gran campo de trabajo en las plantillas de Wordpress para un desarrollador web. Más adelante veremos como crear plantillas nuevas, algo que también te servirá para modificar plantillas existentes. 

### 1.7.4. Widgets

Los widgets son pequeñas aplicaciones que proporcionan nuevas funcionalidades a un programa o que permiten un acceso rápido a funcionalidades usadas con frecuencia.

Pueden ser vistosos como, por ejemplo, relojes en pantalla, calculadoras, calendarios o nubes de tags; o pueden ser discretos pero útiles como, por ejemplo, un cuadro con enlaces de interés o con un contador del número de visitas.

Wordpress incorpora un sistema de widgets para sus plantillas que ofrece numerosas posibilidades y flexibilidad para el diseño y estructura de sus blogs. Cada plantilla puede soportar un número diferente de Widgets.

### 1.7.5. Plugins

Hay una monstruosa cantidad de plugins que potencian el uso de Wordpress y que lo convierten en un CMS prácticamente de propósito general. Encontrarás un plugin para casi cualquier cosa que se te ocurra.

Pero (siempre hay un pero) con los plugins se corre el riesgo de empezar a parchear Wordpress hasta convertirlo en un amasijo informe de código puesto a pegotones. Muchos sitios web montados con Wordpress se vuelven ingobernables (y extraordinariamente lentos y pesados en la carga) por la gran cantidad de plugins que tienen activados.

Otro problema de los plugins es que pueden provocar incontables problemas con las actualizaciones del sistema.

En el ámbito de los plugins también hay mucho trabajo potencial para un futuro desarrollador/a web como tú: tanto para crear plugins nuevos y adaptados a las necesidades del cliente como para optimizar y racionalizar el uso de plugins existentes en los sitios que ya están en funcionamiento.

Por último, y al igual que ocurría con las plantillas, tienes que saber que muchos plugins son gratuitos, otros son de pago, y otros tienen versiones gratuitas que se vuelven de pago cuando queremos utilizar sus características más atractivas.

XXX

Fallos de seguridad
Las críticas más frecuentes a WordPress se han centradoalrededor de su seguridad. En mayo de 2007, por ejemplo, un estudio reveló que el 98% de los blogs basados en WordPress eran vulnerables a ataques. Parece ser que la arquitectura de la aplicación hacen difícil escribir código que sea seguro frente a vulnerabilidades de inyección SQL, entre otros.

### Plantillas de Wordpress

Fuentes:
    • esandra.com/crear-plantilla-wordpress-desde-cero
    • manuelvicedo.com/guias/personalizar-wordpress-plantillas
Las plantillas de WordPress
Existen muchos sitios web donde adquirir plantillas de WordPress de gran valor añadido. Algunas son gratuitas, otras de pago, y otras tienen versiones gratuitas incompletas o parcialmente desactivadas, y versiones de pago que permiten usar todas las funcionalidades. 
Pero, a veces, queremos ir un paso más allá y desarrollar nuestro propio tema. Para ello, se puede usar un framework como Thematic o de partir de un tema básico, pensado para desarrollo, como Bones o Basic.
Sin embargo, la mayor parte de las veces es mucho mejor desarrollar un tema de WordPress desde cero, pues así conseguiremos adaptarlo exactamente a lo que estamos buscando, evitando llamar a un montón de funciones innecesarias para las prestaciones que necesitamos. Además, así tendremos el control abosluto sobre los archivos y contenidos de la plantilla.
Dónde localizar las plantillas instaladas
Suponiendo que tenemos WordPress instalado y en correcto funcionamiento en un servidor (local o remoto, da lo mismo), lo primero que tendremos que hacer es ir a la carpeta que contiene los temas de WordPress. Esta carpeta se encuentra en las siguiente ruta: carpetawordpress -> wp-content -> themes, siendo carpetawordpress el directorio donde tenemos instalado WordPress dentro del htdocs del servidor.
Dentro de themes veremos una carpeta para cada tema de WordPress. Ahí tendremos que crear una nueva carpeta con el nombre de nuestro nuevo tema.
A partir de ahora supondremos que estamos creando un nuevo tema llamado mitema, con lo que que dentro de themes tendremos que crear un directorio llamado mitema.
Archivos de un tema de WordPress
WordPress funciona por módulos. Por ejemplo, para insertar el footer en una página habremos de llamar al archivo footer.php, en caso de que exista. Y lo mismo con el header, la barra lateral, etc.
Así, un tema de WordPress puede estar formado por muchos archivos, pero para que un tema de WordPress funcione, sólo necesitará dos archivos: index.php y style.css. Está claro que con sólo estos dos archivos tendremos un tema muy básico y de ir por casa, pero, a fin de cuentas, será considerado por WordPress un tema válido si estos dos archivos están bien configurados.
Con esto estamos también diciendo que para que un tema de WordPress sea reconocido por WordPress deberá incluir sí o sí estos dos archivos index.php y style.css. Con que falte la hoja de estilos o el archivo index.php WordPress no reconocerá la carpeta mitema como un tema de WordPress.
En las siguientes páginas vamos a desarrollar un tema más completo que nos sirva de base para otros proyectos. Y raramente crearemos un tema de WordPress que no contenga una cabecera, un footer y una barra lateral, como mínimo. Tampoco vamos aquí a desarrollar un tema complejo con funciones avanzadas, pero sí que queremos tener lo necesario para crear un tema decente con el que poder desarrollar proyectos más complejos.
Así, vamos a desarrollar un tema con la mayoría de archivos y carpetas habituales en otros temas para WordPress profesionales. Son los siguientes:
    • /images. Carpeta con las imágenes del tema.
    • /js. Carpeta con los archivos de JavaScript
    • style.css. Hoja de estilos del tema. Obligatoria para que el tema funcione.
    • index.php. Obligatorio para que el tema funcione. Por defecto será la página principal.
    • screenshot.png. Muestra la imagen en miniatura que se verá en el panel de administración en Apariencia -> Temas.
    • favicon.ico. La imagen que se verá en el navegador y al guardar el marcador.
    • header.php. Módulo que contiene la cabecera del tema.
    • sidebar.php. La barra lateral del tema.
    • footer.php. Módulo que contiene el pie de página del tema.
    • single.php. Este archivo especifica cómo se verá una entrada.
    • page.php. Este archivo especifica cómo se verá una página estática.
    • category.php. Muestra cómo se ve la página de resultados de una categoría.
    • tag.php. Muestra cómo se ve la página de resultados de una etiqueta.
    • search.php. Muestra cómo se ve la página de resultados de búsqueda.
    • functions.php. Archivo con las funciones genéricas de nuestro tema de WordPress.
En la plantilla que vamos a desarrollar utilizaremos prácticamente todos estos archivos, para que veamos que no es tan complejo como de entrada pueda parecer. 
A partir de ahí, es fundamental tener la capacidad de crear un buen código HTML y CSS para obtener resultados profesionales, pero, lo que es el tema de WordPress en sí, se reduciría a desarrollar estos archivos.
Para no perdernos en la inmensidad y hacer fácil lo supuestamente difícil, vamos a aplicar la técnica del divide y vencerás. 
Crear una nueva plantilla en WordPress en 11 pasos
Paso 1: Crear el archivo style.css
El primer paso va a consistir en crear dentro de la carpeta mitema el archivo style.css. Es recomendable utilizar un buen editor de textos para desarrollo web, como Sublime Text 2 o Notepad++, pero puedes hacerlo incluso con el Bloc de Notas de Windows si te va la marcha.
Dentro del archivo style.css, en la parte superior deberemos incluir esta información:
	/*
	Theme Name: Mitema
	Theme URI: el lugar donde vayas a alojar el tema 
                 para ponerlo a disposición de la comunidad
	Description: La descripción del tema
	Author: Tu nombre y apellidos
	Author URI: la web profesional del creador del tema
            Version: 1.0
	*/

Fíjate que este fragmento de texto está comentado con /* ... */. Todos los datos que ponemos aquí van a aparecer junto al tema en Apariencia -> Temas. 
A conitnuación, si vamos a utilizar HTML5, es conveniente insertar normalize.css. Lo podemos importar o bien incrustar aquí.
A partir de aquí, podemos ya crear nuestro propio código de CSS.
Paso 2: Imágenes y JavaScript
Este tema lo vamos a desarrollar con HTML5. Vamos a utilizar Modernizr, una librería de JavaScript que detecta las capacidades de HTML5 y CSS3 del navegador. También haremos uso de Respond, otra librería JavaScript que sirve para que Internet Explorer sepa interpretar los media queries de CSS3.
Por supuesto, puede crearse un tema sin estas librerías, pero las usaremos para ilustrar cómo se puede incrustar JavaScript en una plantilla WP.
Crearemos las carpetas images y js dentro de la carpeta mitema, y en js pondremos una copia de las librerías Modernizr y Respond bajadas directamente de las webs de los desarrolladores.
En la carpeta images colocaremos más adelantes todas las imágenes que vayamos necesitando para nuestro CSS. Ten en cuenta que el screenshot.png y el favicon.ico se han de ubicar en la raíz del tema y no dentro de la carpeta images.
Paso 3: Crear la cabecera del tema
El archivo header.php contiene la cabecera de nuestro tema. Es aquí donde pondremos nuestro logo, menú principal y aquello que aparezca en la parte superior de nuestro tema. Veamos un código posible para header.php:
	<!DOCTYPE html>
	<html <?php language_attributes(); ?>>
	<head>
	  <meta charset= <?php bloginfo( 'charset' ); ?>">
	  <title><?php wp_title(); ?></title>
	  <!-- Definir viewport para dispositivos web móviles -->
	  <meta name="viewport" content="width=device-width, minimum-scale=1">
	  <link rel="shortcut icon" href="<?php echo get_stylesheet_directory_uri(); ?>/favicon.ico" />
	  <link rel="stylesheet" media="all" href="<?php bloginfo( 'stylesheet_url' ); ?>" />
	  <link rel="pingback" href="<?php bloginfo( 'pingback_url' ); ?>" />
	  <?php wp_head(); ?>
	</head>
	<body>
	  <div class="wrapper">
	    <header>
	      <h1><a href="<?php echo get_option('home'); ?>"><?php bloginfo('name'); ?></a></h1>
	      <hr>
	      <?php wp_nav_menu( array('menu' => 'Main', 'container' => 'nav' )); ?>
	    </header>

Lo primero que hemos hecho ha sido declarar el doctype, en este caso para HTML5. Seguidamente hemos abierto la etiqueta html indicando que seleccione los atributos de idioma de la instalación de WordPress. Dentro de head hemos usado bloginfo( 'charset' ); para que seleccione la codificación predeterminada de nuestra instalación de WordPress. La función wp_title() selecciona y muestra el título especificado en Ajustes -> General del panel de administración de WordPress.
En el caso de estar diseñando un tema responsive, especificaremos el viewport. Para mostrar la URL al favicon.ico le habremos de indicar la ruta a la carpeta mitema de la instalación de WordPress, y para ello llamafremos a la función de PHP get_stylesheet_directory_uri();:
	link rel="shortcut icon" href="<?php echo get_stylesheet_directory_uri(); ?>/favicon.ico" />
Otro modo de acceder a mitema será:
	<script src="<?php bloginfo('stylesheet_directory'); ?>/js/respond.min.js"></script>
Aquí hemos accedido al directorio de mitema con bloginfo('stylesheet_directory');.
Finalmente incluiremos la función wp_head de WordPress, necesaria par que muchos plugins y funcionalidades de WordPress funcionen. A partir de aquí cerramos la etiqueta head y empezamos con los contenidos de body.
Quizás aquí te estés preguntando por que incluir el body en header.php y no en index.php. La razón es sencilla: los contenidos de la cabecera del tema van a estar en todas las páginas, por lo que al incluirlo aquí, evitamos duplicar código y el mantenimiento del tema va a ser mucho más sencillo. Así, dentro de las etiquetas de header incluiremos nuestra cabecera. En este ejemplo, hemos puesto el nombre del sitio web con un enlace a la página de inicio:
	<h1><a href="<?php echo get_option('home'); ?>"><?php bloginfo('name'); ?></a></h1>
Insertar el menú de navegación
Fíjate que en la etiqueta header hemos escrito esta línea:
	<?php wp_nav_menu( array('menu' => 'Main', 'container' => 'nav' )); ?>
Bien, para que esto funcione, primero deberemos añadir al archivo functions.php este código:
	<?php
	// Registro del menú de WordPress
	add_theme_support( 'nav-menus' );
	if ( function_exists( 'register_nav_menus' ) ) {
	    register_nav_menus(
	        array(
	          'main' => 'Main'
	        )
	    );
	}
	?>
Este código lo que hace es crear un menú llamado “Main” que nos aparecerá en el panel de administración de WordPress en Apariencia -> Menús. Lo que esté código dice es que si existe una función llamada register_nav_menus, que entonces cree un nuevo menú de navegación llamado Main. Hemos añadido la función de WordPRess add_theme_support() para indicar que en este tema queremos poder crear menús dinámicos.
A partir de aquí, simplemente habremos de ir a Apariencia -> Menús y crear nuestro menú y guardarlo, como con cualquier otro theme.
Con esto ya tenemos la cabecera del tema creada junto con su menú de navegación. Recuerda que para añadir páginas al menú de WordPress, primero hay que crear las páginas o no podremos hacerlo.
Si quieres crear un menú de navegación complejo, que sea responsive, incluya imágenes, mapas, submenús y entradas, puedes usar el plugin WordPress Ubermenu. Es un plugin de pago, pero ahorra un montón de horas de codificación y trabajo.
Paso 4: Crear la barra lateral
La mayoría de temas de WordPress incluyen una barra lateral que no tiene por qué aparecer en todas las páginas del tema. En las barras laterales acostumbramos a poder añadir widgets, por lo que se van a tener que habilitar para widgets. Para ello, abriremos nuestro archivo functions.php e incluiremos esta función:
	<?php
	     //  Main Sidebar
	     if(function_exists('register_sidebar'))
	          register_sidebar(array(
	          'name' => 'Main Sidebar',
	           'before_widget' => '<hr>',
	            'after_widget' => '',
	          'before_title' => '<h3>',
	          'after_title' => '</h3>',
	     ));
	?>

Al hacer esto, si vamos a Apariencia -> Widgets, veremos que nos aparece una nueva zona de widgets llamada Main Sidebar. 
Una vez creada la zona lista para widgets, vamos a tener que llamarla dentro del archivo sidebar.php. Creamos este archivo y escribimos:
	<section id="sidebar">
	  <?php if ( !function_exists('dynamic_sidebar') || !dynamic_sidebar('Main Sidebar') ) : ?>
	  <?php endif; ?>
	</section>

Hemos utilizado un id teniendo en cuenta que en este tema sólo va a existir una barra lateral, pero si quieres crear más, quizás prefieras crear una clase. Con esto ya tenemos creada la barra lateral lista para widgets.
Paso 5: Crear el footer
Hasta aquí hemos creado la cabecera y la barra lateral. Ahora vamos a crear el footer para después integrarlo todo en index.php. Recordemos que WordPress funciona por módulos, con lo que lo que estamos haciendo ahora es crear los módulos necesarios para que nuestra página de inicio, en este caso index.php, se muestre correctamente.
El archivo footer.php quedaría así:
	<footer>
	  <p>&amp;amp;amp;copy; <?php bloginfo('name'); ?>, <?=date('Y');?>. Mi primer tema.</p>
	</footer>
	</div> <!-- Fin de wrapper -->
	<?php wp_footer(); ?>
	</body>
	</html>

Fíjate que wrapper engloba tanto el header como el footer. Si queremos un header o un footer que se extienda toda la pantalla, deberemos mover las posiciones de los div que abren y cierran wrapper.
Aquí aparece la función wp_footer, que al igual que pasaba con wp_header, no debemos olvidarla. Estas funciones son lo que se llaman hooks y son necesarias para que funcionen los plugins que instalemos.
En el caso de wp_footer va a ser además necesaria si queremos ver la barra de administración de WordPress. No serás el primero que se vuelve loco buscando el por qué no aparece la barra de administración hasta que descubre que es porque no ha llamado a este hook de WordPress.
Paso 6: Crear la página principal
En este tema la página principal se va a corresponder a los contenidos de index.php. Así, creamos el archivo index.php tal y como se indica a continuación.
	<?php get_header(); ?>
	  <section id="main">
	  </section> <!-- Fin de main -->
	    <?php  get_sidebar()?>
	  <?php get_footer(); ?>

Observa estas tres funciones:
get_header();
get_sidebar();
get_footer();

Lo que hace get_header() es insertar los contenidos del archivo header.php en el lugar donde se encuentra esta función. Lo mismo pasa con get_sidebar() para los contenidos de sidebar.php y get_footer() para los contenidos de footer.php. Eso es lo que significa que WordPress funciona por módulos.
Paso 6. El loop de WordPress
La potencia de WordPress reside en el loop. ¿Qué es el loop? Es el bucle que muestra las entradas almacenadas en la base de datos de WordPress de la forma en que nosotros lo programemos. Es gracias al loop de WordPress que podemos ver un listado de entradas.
Este es un ejemplo del código del loop:
	<?php if (have_posts()) :  while (have_posts()) : the_post(); ?>
	    <h2><a href="<?php the_permalink(); ?>"><?php the_title(); ?></a></h2>
	   <small>Publicado el <?php the_time('j/m/Y') ?> por <?php the_author_posts_link() ? </small>
	    <?php the_excerpt(); ?>
	  <?php endwhile; else: ?>
	    <p><?php _e('No hay entradas .'); ?></p>
	  <?php endif; ?>

Vayamos a explicarlo paso a paso. En la primera línea tenemos:
	<?php if(have_posts()) : ?><?php while(have_posts()) : the_post(); ?>

Lo que aquí le estamos diciendo a WordPress es que mire si hay alguna entrada disponible, esto lo hacemos con if(have_posts()). Fíjate en el if, significa que sólo ejecute el resto si esta condición se cumple, esto es, que exista algún post. Lo siguiente que le decimos es que mientras haya entradas, esto es, while(have_posts()), que seleccione cada uno de los posts: the_post().
Una vez ha seleccionado el post, lo siguiente es que le vamos a indicar cómo ha de mostrar los contenidos del post.
Así pues, ahora mostraremos el título de la entrada con una enlace a la misma:
	<h3  class="title"><a href="<?php the_permalink() ?>" rel="bookmark" title="Enlace permanente a <?php the_title_attribute(); ?>"><?php the_title(); ?></a></h3>

La función the_permalink() se encarga de encontrar el enlace permanente a la entrada, para que podamos ir a la misma. Y la función the_title() mostrará en pantalla el título de la entrada.
Si queremos que debajo del título se vean datos como la fecha de publicación, la categoría, el autor, etc., se lo tendremos que especificar a continuación:
	<small>Publicado el <?php the_time('j/m/Y') ?> por <?php the_author_posts_link() ?></small>

La función the_time() muestra la fecha de publicación y en el paréntesis podemos definir el formato de la fecha entre comillas. Con la función the_author_posts_link() estamos mostrando el nombre del autor con un enlace a su página de autor.
Si queremos mostrar las etiquetas, lo haremos con la función the_tags(), y si lo quisiéramos hacer es mostrar la categoría de la entrada, utilizaríamos la función the_category().
Seguidamente, con la función the_excerpt() mostraremos el resumen de la entrada. Si no hemos creado un resumen, se mostrará la primera parte de la entrada.
Para cerrar el loop, llamamos este código:
	<?php endwhile; else: ?>
	  <p><?php _e('No hay entradas .'); ?></p>
	<?php endif; ?>
Así, en el caso que no haya entradas, se mostrará el mensaje de “No hay entradas”.
Paso 7. Añadir thumbnails al loop
Si queremos añadir thumbnails al loop como sucede en muchos portales WP, lo que haremos es lo siguiente: vamos al archivo functions.php y añadimos este código:
	<?php
	//Habilitar thumbnails
	add_theme_support('post-thumbnails');
            set_post_thumbnail_size(150, 150, true);
	?>

Con este código hemos habilitado los thumbnials o imágenes destacadas de nuestras entradas y hemos establecido un tamaño para las mismas de 150 por 150 píxeles. Una vez hecho esto, modificaremos nuestro loop como sigue:
	<?php if (have_posts()) :  while (have_posts()) : the_post(); ?>
	    <h2><a href="<?php the_permalink(); ?>"><?php the_title(); ?></a></h2>
	   <small>Publicado el <?php the_time('j/m/Y') ?> por <?php the_author_posts_link() ?>  </small>
	   <div class="thumbnail">
	      <?php
	          if ( has_post_thumbnail() ) {
	                the_post_thumbnail();
          }
	      ?>
	   </div>
	      <?php the_excerpt(); ?>
	  <?php endwhile; else: ?>
	    <p><?php _e('No hay entradas .'); ?></p>
	  <?php endif; ?>

Fíjate que hemos añadido:
	<?php
	       if ( has_post_thumbnail() ) {
	             the_post_thumbnail();
	        }
	 ?>
if ( has_post_thumbnail() ) significa que compruebe si la entrada en cuestión tiene una imagen destacada asignada y en caso afirmativo, le decimos que la muestre con the_post_thumbnail();.
A partir de aquí, si queremos, por ejemplo, que el extracto quede en línea con la imagen destacada, lo haremos a través del CSS.
Con esto ya hemos creado nuestra página principal, con su cabecera, zona de contenidos con las últimas entradas, barra lateral y pie de página. Podríamos seguir complicándolo. Por ejemplo: podríamos añadir una paginación de las entradas. Tendrás que buscar información sobre cada cosa que quieras añadir a tu loop o, mejor aún, descargar el código de plantillas que lo hacen y curiosear las tripas del código. Recuerda que raramente hace falta reinventar la rueda.
Paso 8. Resultados de la búsqueda
Los resultados de la búsqueda se especifican en el archivo search.php. He aquí un ejemplo:
	<?php get_header(); ?>
	    <section id="main">
	  <h2>Resultados de la búsqueda</h2>
	         <?php if (have_posts()) :  while (have_posts()) : the_post(); ?>
	      <h2><a href="<?php the_permalink(); ?>"><?php the_title(); ?></a></h2>
	     <small>Publicado el <?php the_time('j/m/Y') ?> por <?php the_author_posts_link() ?>  </small>
	     <div class="thumbnail">
	        <?php
	            if ( has_post_thumbnail() ) {
	                  the_post_thumbnail();
	            }
	        ?>
	     </div>
	        <?php the_excerpt(); ?>
	 
	 <?php endwhile; ?>
	<?php if (function_exists("pagination")) {
	    pagination($additional_loop->max_num_pages);
	} ?>
	<?php  else: ?>
	<div class="entry"><?php _e('Lo sentimos, no hay resultados con este término de búsqueda.'); ?></div>
	<?php endif; ?>
	</section> <!-- Fin de main -->
	<?php  get_sidebar()?>
	<?php get_footer(); ?>

Fíjate que se parece mucho a index.php. Esta página es la que va a mostrar los resultados de una búsqueda en cuestión. Así, vamos a necesitar que aparezca un buscador en nuestra plantilla. Un buen sitio para colocarlo puede ser el sidebar. Iremos a nuestro archivo sidebar.php y justo antes de la función que habilita la zona de widgets en el sidebar, incluimos este código:
	<form method="get" id="searchform" action="<?php bloginfo('url'); ?>/">
	  <input type="text" placeholder="Buscar…" value="<?php the_search_query(); ?>" name="s" id="s" />
	  <button type="submit" class="icon-only"  id="searchsubmit"></button>
	</form>
Con esto tenemos un campo de búsqueda en nuestra barra lateral. Para que se visualice como queremos, simplemente hará falta crear el código CSS necesario.
Paso 9. Configurar vista de las entrada (posts)
La página del post es aquella donde vamos a ver una entrada individual. Vamos a poder definir cómo se ve, incluir o no comentarios, etc.
El archivo single.php puede ser más o menos así:

	<?php get_header(); ?>
	    <section id="main">
	        <article id="single">
	          <?php if(have_posts()) : ?><?php while(have_posts()) : the_post(); ?>
	            <h2><a href="<?php the_permalink() ?>" rel="bookmark" title="Enlace permanente a <?php the_title_attribute(); ?>"><?php the_title(); ?>. </a></h2>
	              <small> Publicado por <?php the_author_posts_link() ?>  el <?php the_time('j/m/Y') ?>. Categoría: <?php the_category(', '); ?> </small><br>
	          <div class="post">
	 
	             <?php the_content(); ?>
	        </div>
	<?php endwhile; ?>
	<?php endif; ?>
	  </article> <!-- Fin de single -->
	  </section> <!-- Fin de main -->
	  <?php  get_sidebar()?>
	<?php get_footer(); ?>

Si has llegado hasta aquí, te resultará fácil comprender el archivo. Faltaría añadir el poder poner comentarios en cadena y las entradas relacionadas. En el loop utilizamos the_excerpt() para mostrar el extracto de la entrada, mientras que aquí utilizamos la función the_content() para que se muestre el contenido de la entrada.
Por supuesto, esto se puede complicar hasta el infinito. A modo de ejemplo, mostraremos cómo podríamos mostrar las entradas relacionadas. Bastaría con añadir este código justo después de mostrar el contenidos de la entrada:
	    <?php
	    $tags = wp_get_post_tags($post->ID);
	    if ($tags) {
	      $tag_ids = array();
	      foreach($tags as $individual_tag) $tag_ids[] = $individual_tag->term_id;
	      $args=array(
	      'tag__in' => $tag_ids,
	      'post__not_in' => array($post->ID),
	      'showposts'=>5, // Number of related posts that will be shown.
	      'caller_get_posts'=>1
	      );
	    $my_query = new wp_query($args);
	      if( $my_query->have_posts() ) {
	        echo '<h3>Artículos relacionados</h3><ul>';
	        while ($my_query->have_posts()) {
	          $my_query->the_post();
	          ?>
	          <li><a href="<?php the_permalink() ?>" rel="bookmark" title="Permanent Link to <?php the_title_attribute(); ?>"><?php the_title(); ?></a></li>
	        <?php
	        }
	        echo '</ul>';
	      }
	         wp_reset_query();
	    }
	?>

Paso 10: Habilitar y mostrar comentarios
Para permitir los comentarios en una entrada, añadiremos este código a nuestro archivo functions.php:
	
       // Permitir comentarios encadenados
	function enable_threaded_comments(){
	    if (is_singular() AND comments_open() AND (get_option('thread_comments') == 1)) {
	       wp_enqueue_script('comment-reply');
	    }
	}
	add_action('get_header', 'enable_threaded_comments');

Y en single.php, justo antes de la línea que contiene el endwhile añadiremos:
	<div class="comentarios">
	  <?php comments_template(); ?>
	</div>

Es el CSS lo que visualmente nos va a permitir que se vean los comentarios encadenados. Aquí, un ejemplo:
	.commentlist li {
	  list-style: none !important;
	}
	.comment-body {
	  padding: 15px;
	}
	.comment-author {
	  margin-top: 5px;
	}
	.reply,  .commentmetadata {
	  font-size: 0.9em;
	}
	.depth-1, .depth-2, .depth-3, .depth-4 {
	  border: 1px solid #eaeaea;
	  border-radius: 4px;
	}
	.depth-1, .depth-3 {
	  background-color: #fafafa;
	}
	.depth-2, .depth-4 {
	   background-color: #fff;
	}
	.comment-author-eSandra {
	  border: 3px solid #eaeaea;
	  border-left:3px solid #fbc356;
	}
	.depth-1 {
	   margin: 20px 0;
	}
	/* Respuesta a comentarios*/
	.depth-2 {
	  margin:2% 5% !important;
	}
	.depth-3 {
	   margin: 2% 7% !important;
	}
	.depth-4 {
	  margin:2% 5% 4% 10% !important;
	}
	#comment, #author, #email {
	  border-radius: 4px;
	  border:2px solid #ccc;
	}

Paso 11: Crear la página de categorías y etiquetas
Las páginas de category.php y etiquetas.php son prácticamente iguales. Simplemente añadiremos antes del loop:
	<?php $post = $posts[0];  ?>
	  <?php  if (is_category()) { ?>
	  <?php } elseif( is_tag() ) { ?>
	    <h2>Etiqueta &amp;amp;amp;#8216;<?php single_tag_title(); ?>&amp;amp;amp;#8217;</h2>
	  <?php } elseif (is_day()) { ?>
	    <h2>Archivo para <?php the_time('F jS Y'); ?>:</h2>
	  <?php  } elseif (is_month()) { ?><h2>Archivo para <?php the_time('F, Y'); ?>:</h2>
	  <?php } elseif (is_year()) { ?>
	    <h2>Archivo para <?php the_time('Y'); ?>:</h2>
	  <?php /} elseif (is_author()) { ?>
	    <h2>Archivo del autor </h2>
	  <?php } elseif (isset($_GET['paged']) &amp;amp;amp;&amp;amp;amp; !empty($_GET['paged'])) { ?>
	    <h2>Archivos del blog</h2>
	<?php } ?>

Haremos lo mismo si queremos crear una página con nuestros archivos.
Y ahora, ¿qué?
La creación de plantillas no termina aquí, claro. Solo hemos dado los primeros pasos y sentado unas bases lo más sólidas posible. La API de WordPress es muy amplia, a menudo confusa y casi siempre redundante. Especializarse en el desarrollo para WordPress es una tarea de largo recorrido que no puede aprenderse en unas cuantas horas. Pero, si has llegado hasta aquí, ya has hecho, probablemente, lo más difícil.
No obstante, vamos a apuntar algunas ideas para ampliar nuestra primera plantilla.
Otros archivos de la plantilla
Hemos visto cómo crear un tema de WordPress desde cero. Debería ser suficiente para tener una buena base para desarrollar un tema de WordPress desde cero. 
Se pueden añadir otros archivos, como page.php para mostrar páginas estáticas, author.php para mostrar la página de "acerca de", o 404.php para crear nuestra propia página de error, pero con todo lo anteior no deberías tener dificultad para crearlos.
Plantillas de página
El archivo page.php del tema especifica cómo se verán todas las páginas, pero puedes crear nuevas plantillas para páginas y, desde el propio editor de páginas, asignar a cada página una plantilla diferente.
Las plantillas de página son muy utilizadas para generar contenidos especiales en un sitio WordPress, ya que pueden ser asignadas a una página en particular en lugar de a toda una colección de contenidos (como ocurre con las entradas). 
Los temas WordPress pueden tener tantas plantillas de página como desees, y son bastante útiles para cuando deseas crear alguna página con detalles especiales.
Crear nuevas plantillas es una tarea muy sencilla, ya que se comportan igual que cualquier otro archivo dentro de un tema WordPress. Para hacerlo, tienes que localizar el archivo page.php de tu tema. Después debes crear una copia de este archivo, el cual puedes nombrar como mejor prefieras. Aquí debes tener cuidado de no utilizar uno de los nombres de archivo utilizados por la jerarquía de WordPress, como single-post.php, o archive.php. Para evitar cualquier problema, lo mejor es siempre añadir algún prefijo personalizado y crear un nombre de archivo como template-blog.php.
Cuando tengas tu nuevo archivo creado y renombrado, ábrelo. Dentro del archivo vamos a añadir la siguiente cabecera al principio de todo:
<?php /* Template Name: MIPLANTILLA */ ?>

Esta cabecera servirá para indicarle a WordPress que el archivo en cuestión se trata de una plantilla, y por tanto incluirla entre la lista de plantillas disponibles al editar una página. Recuerda cambiar MIPLANTILLA por cualquier otro nombre, aunque preferiblemente uno que sea descriptivo. Para que WordPress detecte tu nueva plantilla bastará con incluirla entre los demás archivos del tema, junto a page.php.
Estas plantillas son excelentes para añadir personalizaciones que afecten a un número determinado de páginas. Son especialmente útiles cuando necesites crear algo fuera de lo normal, como quitar la barra lateral o crear un listado de posts.
Herencia de plantillas en WordPress
Por último, presentamos un diagrama de las relaciones que existen entre los archivos típicos de una plantilla Wordpress. Recuerda que el único obligatorio (además de styles.css) es index.php, y que una plantilla compleja puede tener otros archivos adicionales a los que aquí se muestran (como las plantillas de página)

XXX esquema

### Plugins de Wordpress

www.cristalab.com/tutoriales/como-crear-un-plugin-para-wordpress-c54308l/
Los plugins de WordPress
En las siguientes páginas vamos a crear un sencillo plugin para Wordpress que pueda servir de base para desarrollos posteriores más realistas.
El plugin se llamará "Saludo" y contendrá algunas funciones para saludar que nos servirán para ilustrar el funcionamiento del sistema de plugins de WordPress.
Crear un plugin nuevo
Para crear el plugin "Saludo" basta con crear un archivo llamado saludo.php en una carpeta llamada tambiéb "saludo" y ubicada en carpeta_raiz/wp-content/plugins/
Dentro del archivo saludo.php, escribiremos el comentario de cabecera para que WordPress lo reconozca como un plugin válido (igual que sucede con las plantillas). Es importante respetar la sintaxis:

<?php
   /*
      Plugin Name: nombre del plugin
      Plugin URI: url oficial de tu maravilloso plugin
      Description: que carajos hace tu plugin
      Version: numero de intentos para que esta cosa resulte
      Author: Nombre del mono programador
      Author URI: url del mono programador
   */
   
   /*
      esto aparecerá directamente en el panel de 
      administración de plugins
   */ 
?>

Bastará con esto para que WordPress reconozca el plugin.
Añadir funciones al plugin
Vamos a crear nuestra primera función con un código algo complejo pero de gran rendimiento. Todo se escribirá en el mismo archivo saludo.php:

<?php
   // Aquí van los comentarios de la cabecera que vimos antes
   function saludo(){
      echo 'hola mundo';   
   }
?>

Instalar y desinstalar el plugin
Para poder instalar y desinstalar el plugin desde el panel de administracion de WP, es necesario crear dos funciones en saludo.php: una para instalar y otra para desinstalar. Estas funciones, por ahora, las dejaremos vacías.
Además, al final del archivo saludo.php hay que usar la funcion de WP add_action() para indicar las funciones que activar y desactivan el plugin.

<?php
   ...
   function saludo_instala(){
      //   Por ahora la dejamos vacía
   }
   function saludo_desinstala(){
      //   Por ahora la dejamos vacía
   }   
// Ojo con la sintaxis de la funcion add_action!
add_action('activate_saludo/saludo.php','saludo_instala');
add_action('deactivate_saludo/saludo.php', 'saludo_desinstala');
?>

Cómo usar las funciones del plugin
Ahora ya puedes usar tu maravilloso y complejo plugin, sólo debes colocar en la sección de tu plantilla que estimes conveniente la siguiente línea:

<?php saludo(); ?>
Configurar el plugin desde el panel de administración
Ahora nos toca crear un item dentro del panel de administración que nos permita modificar las opciones de este plugin. El ítem lo crearemos dentro del menú opciones, y para esto programaremos tres funciones:
    • saludo_panel(): donde incluiremos el html que será expresado en nuestro panel, como a mí no me gusta mezclar html dentro de la programación usaremos la función include() a modo de template .
    • saudo_add_menu(): donde se usará a su vez la función de WP add_options_page.
    • saludo_add_action(): para desencadenar todo esto usaremos esta función que es también parte del API de WP.

<?php
   ...
   
   function saludo_panel(){      
      include('template/panel.html');
   }
   function saludo_add_menu(){   
      if (function_exists('add_options_page')) {
         //add_menu_page
         add_options_page('saludo', 'saludo', 8, basename(__FILE__), 'saludo_panel');
      }
   }
   if (function_exists('add_action')) {
      add_action('admin_menu', 'saludo_add_menu'); 
   } 
      
   ...
?>

Además, necesitaremos un formulario html para poder visualizar la pantalla de configuración. Crearemos algo muy sencillo. Por supuesto, se puede mejorar con un poco de HTML y CSS. Lo escribiremos en el archivo "template/panel.html":

<form method="post" action="" id="saludo">
<label for="saludo_inserta" accesskey="s">Inserte su saludo<input type='text' id='saludo_inserta'  name='saludo_inserta' value='' /></label>
<input type='submit' name='' value='enviar' />
</form>

Por último, modificaremos la función saludo_panel() para poder visualizar nuestros avances:

<?php
   ...   
   function saludo_panel(){      
      include('template/panel.html');
   }
   echo "<h1>{$_POST['saludo']}</h1>";
   ...
?>

Podemos probar que todo funciona escribiendo algo en el formulario y pulsando Enviar.
Acceder a la BD desde nuestro plugin
Vamos a ver cómo se puede usar la BD de WordPress desde un plugin.
Para ello, antes debemos desinstalar el plugin desde el panel de control, para poder modificar la función de instalación y ejecutarla más adelante de nuevo.
Las funciones de WP que manejan la DB se llaman con una variable global denominada $wpdb con: global $wpdb.

<?php
...

function saludo_instala(){
   global $wpdb; // <-- sin esto no funcionara nada con la DB no cambies nada
   $table_name= $wpdb->prefix . "saludos";
   $sql = " CREATE TABLE $table_name(
      id mediumint( 9 ) NOT NULL AUTO_INCREMENT ,
      saludo tinytext NOT NULL ,
      PRIMARY KEY ( `id` )   
   ) ;";
   $wpdb->query($sql);
   $sql = "INSERT INTO $table_name (saludo) VALUES ('Hola Mundo');";
   $wpdb->query($sql);
}   

function saludo_desinstala(){
   global $wpdb; 
   $tabla_nombre = $wpdb->prefix . "saludos";
   $sql = "DROP TABLE $tabla_nombre";
   $wpdb->query($sql);
}   
   
...
?>

Por supuesto, hay que agregar los datos a la DB desde nuestro panel en opciones/saludo, para lo cual modificaremos la función saludo_panel()


<?php
...

function saludo_panel(){
   include('template/panel.html');         
   global $wpdb; 
   $table_name = $wpdb->prefix . "saludos";
   if(isset($_POST['saludo_inserta'])){   
         $sql = "INSERT INTO $table_name (saludo) VALUES ('{$_POST['saludo_inserta']}');";
         $wpdb->query($sql);
   }
}
      
...
?>

Ahora que ya podemos insertar saludos en nuestra BD, sólo nos queda poder mostrarlos en nuestra función saludo(). Para esto extraeremos un saludo de manera aleatoria a nuestra BD:

<?php
...

function saludo(){
   global $wpdb; 
   $table_name = $wpdb->prefix . "saludos";
   $saludo= $wpdb->get_var("SELECT saludo FROM $table_name ORDER BY RAND() LIMIT 0, 1; " );
   include('template/saludo.html');      
}
   
...
?>

Ahora modificaremos nuestro saludo.html para que imprima la variable $saludo:

<h1><?php echo $saludo;?></h1>


Para terminar vamos modificar el html de nuestro panel para que se adapte al html del administrador de WP:

 <div class="wrap"> 
   <form method="post" action="">
      <fieldset>
         <legend>Ingresar Nuevo Saludo</legend>
         <label for="saludo" accesskey="s">Inserte su saludo<input type='text' id='saludo_inserta'  name='saludo_inserta'  /></label>
         <input type='submit' name='' value='enviar' />
      </fieldset>
   </form>
</div>

Ya tenemos listo nuestro plugin. Por supuesto, del mismo modo podríamos eliminar o modificar registros, y hacer todo lo que fuera necesario con la base de datos.


## 1.8. Moodle
Moodle es un sistema de gestión de contenidos (CMS) orientado a crear comunidades de aprendizaje en línea. Este tipo de plataformas tecnológicas también se conoce como LMS (Learning Management System). Está publicado con licencia GPL (es decir: es software libre). Está programado en lenguaje PHP y puede usar diferentes gestores de bases de datos para almacenar el contenido: MySQL o PostgreSQL son los más habituales, pero también es posible utilizar Oracle o SQL Server.
Características generales de Moodle
    • Su arquitectura y herramientas son apropiadas para la educación a distancia, así como también para complementar el aprendizaje presencial. 
    • Tiene una interfaz de navegador de tecnología sencilla, ligera, y compatible. 
    • La instalación es sencilla, requiriendo tan solo una plataforma que soporte PHP y la disponibilidad de una base de datos. 
    • Se ha puesto énfasis en una seguridad sólida en toda la plataforma: todos los formularios son revisados, las cookies cifradas, etc. 
    • La mayoría de las áreas de introducción de texto (materiales, mensajes de los foros, entradas de los diarios, etc.) pueden ser editadas usando un editor WYSIWYG. 
Algunos módulos de Moodle
En Moodle, los contenidos se organizan en categorías llamadas "módulos". Cada módulo tiene sus propias características y está orientado a un tipo de actividad distinta: cuestionarios en línea, lecciones, tareas para que los alumnos suban, etc.
Módulo de Tareas
    • Puede especificarse la fecha final de entrega de una tarea y la calificación máxima que se le podrá asignar. 
    • Los estudiantes pueden subir sus tareas (en cualquier formato de archivo) al servidor. Se registra la fecha en que se han subido. 
    • Se permite enviar tareas fuera de tiempo, pero el profesor puede ver claramente el tiempo de retraso. 
    • Para cada tarea en particular, puede evaluarse a la clase entera (calificaciones y comentarios) en una única página con un único formulario. 
    • Las observaciones del profesor se adjuntan a la página de la tarea de cada estudiante y se le envía un mensaje de notificación. 
    • El profesor tiene la posibilidad de permitir el reenvío de una tarea tras su calificación (para volver a calificarla). 
Módulo de consulta
Es como una votación. Puede usarse para votar sobre algo o para recibir una respuesta de cada estudiante (por ejemplo, para pedir su consentimiento para algo).
    • El profesor puede ver una tabla que presenta de forma intuitiva la información sobre quién ha elegido qué. 
    • Se puede permitir que los estudiantes vean un gráfico actualizado de los resultados. 
Módulo foro
Hay diferentes tipos de foros disponibles: exclusivos para los profesores, de noticias del curso y abiertos a todos.
    • Todos los mensajes llevan adjunta la foto del autor. 
    • Las discusiones pueden verse anidadas, por rama, o presentar los mensajes más antiguos o los más nuevos primero. 
    • El profesor puede obligar la suscripción de todos a un foro o permitir que cada persona elija a qué foros suscribirse de manera que se le envíe una copia de los mensajes por correo electrónico. 
    • El profesor puede elegir que no se permitan respuestas en un foro (por ejemplo, para crear un foro dedicado a anuncios). 
    • El profesor puede mover fácilmente los temas de discusión entre distintos foros. 
Módulo Cuestionario
    • Los profesores pueden definir una base de datos de preguntas que podrán ser reutilizadas en diferentes cuestionarios. 
    • Las preguntas pueden ser almacenadas en categorías de fácil acceso, y estas categorías pueden ser "publicadas" para hacerlas accesibles desde cualquier curso del sitio. 
    • Los cuestionarios se califican automáticamente, y pueden ser recalificados si se modifican las preguntas. 
    • Los cuestionarios pueden tener un límite de tiempo a partir del cual no estarán disponibles. 
    • El profesor puede determinar si los cuestionarios pueden ser resueltos varias veces y si se mostrarán o no las respuestas correctas y los comentarios 
    • Las preguntas y las respuestas de los cuestionarios pueden ser mezcladas (aleatoriamente) para disminuir las copias entre los alumnos. 
    • Las preguntas pueden crearse en HTML y con imágenes. 
    • Las preguntas pueden importarse desde archivos de texto externos. 
    • Las preguntas pueden tener diferentes métricas y tipos de captura. 
Módulo recurso
    • Admite la presentación de un importante número de contenido digital, Word, Powerpoint, Flash, vídeo, sonidos, etc. 
    • Los archivos pueden subirse y manejarse en el servidor, o pueden ser creados sobre la marcha usando formularios web (de texto o HTML). 
    • Pueden enlazarse aplicaciones web para transferir datos. 
Módulo encuesta
    • Se proporcionan encuestas ya preparadas (COLLES, ATTLS) y contrastadas como instrumentos para el análisis de las clases en línea. 
    • Se pueden generar informes de las encuestas los cuales incluyen gráficos. Los datos pueden descargarse con formato de hoja de cálculo Excel o como archivo de texto CSV. 
    • La interfaz de las encuestas impide la posibilidad de que sean respondidas sólo parcialmente. 
    • A cada estudiante se le informa sobre sus resultados comparados con la media de la clase. 
Módulo Wiki
    • El profesor puede crear este modulo para que los alumnos trabajen en grupo en un mismo documento. 
    • Todos los alumnos podrán modificar el contenido incluido por el resto de compañeros. 
    • De este modo cada alumno puede modificar el wiki del grupo al que pertenece, pero podrá consultar todos los wikis. 
    
    
## 1.9. Prestashop

TODO


