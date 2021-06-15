---
layout: page
title: 1.2 Wordpress
permalink: /cms/wordpress
nav_order: 2
has_children: false
parent: 1 Sistemas gestores de contenido (CMS)
grand_parent: Desarrollo Web en Entorno Servidor
---


## 1.2. Wordpress
{: .no_toc }

- TOC
{:toc}

Wordpress es sin duda el campeón actual de los CMS. Algunas estadísticas afirman que el 90% de los sitios web de internet está hecho con Wordpress. Probablemente son estadísticas un poco infladas, pero la importancia de este CMS es innegable y cualquier desarrollador web debe conocerlo, aunque sea para odiarlo.

Wordpress es un CMS enfocado a la creación de blogs, aunque, en su estadio actual, permite crear casi cualquier tipo de sitio web: tiendas online, portales, revistas digitales, álbumes de imágenes o recursos de cualquier tipo... 

Está desarrollado en PHP bajo licencia GPL y se ha convertido. Tiene detrás una enorme comunidad de desarrolladores y diseñadores, que se encargan de actualizarlo y de crear plugins y temas para la comunidad.

### 1.2.1. Características principales de Wordpress

* La estética, tanto de resultado como del código fuente, es fundamental para los desarrolladores de WordPress. 
* Las entradas publicadas son ordenadas por fecha, aunque esto se puede modificar. 
* La estructura y diseño visual del sitio depende del sistema de plantillas. 
* La filosofía de Wordpress apuesta decididamente por la elegancia, la sencillez y las recomendaciones del W3C pero depende siempre de la plantilla. 
* Separa el contenido y el diseño en XHTML y CSS, aunque, como se ha dicho, depende de la plantilla que se esté usando. 
* La gestión y ejecución corre a cargo del sistema de administración con los plugins y los widgets que usan las plantillas. 

#### **Funcionalidades de Wordpress**

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
    
#### **Plantillas de Wordpress**

Las plantillas (themes) de Wordpress son diseños CSS que sirven para establecer la apariencia y estructura del blog. Algunas también modifican parte del panel de administración. 

Hay una gran comunidad oficial, tanto profesional como de usuarios, dedicada al diseño de estas plantillas. Puedes encontrarlas tanto en el sitio de Wordpress (comprobadas y aprobadas oficialmente) como en sitios web de terceros. Muchas son gratuitas, otras de pago y, la mayoría, tienen una versión gratuita con funciones adicionales de pago.

Las posibilidades de las plantillas, tanto a nivel de diseño, estructura o gestión, son tan grandes que prácticamente permiten tener desde un simple blog hasta un portal web fuertemente personalizable.

Hay un gran campo de trabajo en las plantillas de Wordpress para un desarrollador web. Más adelante veremos como crear plantillas nuevas, algo que también te servirá para modificar plantillas existentes. 

#### **Widgets**

Los widgets son pequeñas aplicaciones que proporcionan nuevas funcionalidades a un programa o que permiten un acceso rápido a funcionalidades usadas con frecuencia.

Pueden ser vistosos como, por ejemplo, relojes en pantalla, calculadoras, calendarios o nubes de tags; o pueden ser discretos pero útiles como, por ejemplo, un cuadro con enlaces de interés o con un contador del número de visitas.

Wordpress incorpora un sistema de widgets para sus plantillas que ofrece numerosas posibilidades y flexibilidad para el diseño y estructura de sus blogs. Cada plantilla puede soportar un número diferente de Widgets.

#### **Plugins**

Hay una monstruosa cantidad de plugins que potencian el uso de Wordpress y que lo convierten en un CMS prácticamente de propósito general. Encontrarás un plugin para casi cualquier cosa que se te ocurra.

Pero (¡siempre hay un pero!) con los plugins se corre el riesgo de empezar a parchear Wordpress hasta convertirlo en un amasijo informe de código puesto a pegotones. Muchos sitios web montados con Wordpress se vuelven ingobernables (y extraordinariamente lentos y pesados en la carga) por la gran cantidad de plugins que tienen activados.

Otro problema de los plugins es que pueden provocar incontables problemas con las actualizaciones del sistema.

En el ámbito de los plugins también hay mucho trabajo potencial para un futuro desarrollador/a web como tú: tanto para crear plugins nuevos y adaptados a las necesidades del cliente como para optimizar y racionalizar el uso de plugins existentes en los sitios que ya están en funcionamiento.

Por último, y al igual que ocurría con las plantillas, tienes que saber que muchos plugins son gratuitos, otros son de pago, y otros tienen versiones gratuitas que se vuelven de pago cuando queremos utilizar sus características más atractivas.

#### **Fallos de seguridad de Wordpress**

Las críticas más contundentes contra WordPress se han centrado en sus problemas de seguridad. En mayo de 2007, por ejemplo, un estudio reveló que el 98% de los blogs basados en WordPress eran vulnerables a ataques.

Todos los sistemas que se vuelven muy populares se vuelven inseguros por el simple hecho de que se multiplican los ataques contra ellos.

La receta para minimizar los posibles problemas de seguridad es sencilla: mantener Wordpress actualizado. No podemos hacer mucho más allá de eso.

### 1.2.2. Cómo crear y modificar una plantilla de Wordpress

(Esta sección está redactada a partir de esandra.com/crear-plantilla-wordpress-desde-cero y de manuelvicedo.com/guias/personalizar-wordpress-plantillas)

Vamos a ver que Wordpress dispone de una enorme API de funciones útiles para desarrollar nuestros propios temas y plugins. Y lo vamos a ver de forma práctica: creando nuestra propia plantilla desde cero.


#### **Las plantillas o temas de WordPress**

Como ya hemos dicho, existen muchos sitios web donde adquirir plantillas (themes) de WordPress de gran valor añadido. Algunas son gratuitas, otras de pago, y otras tienen versiones gratuitas incompletas o parcialmente desactivadas, y versiones de pago que permiten usar todas las funcionalidades. 

Pero, a veces, queremos ir un paso más allá y desarrollar nuestro propio tema. Para ello, se puede usar un framework como Thematic o partir de un tema básico, pensado para desarrollo. Existen muchos temas de ese tipo, algunos muy conocidos, como Bones o Basic.

A veces es mejor desarrollar un tema de WordPress desde cero, pues así conseguimos adaptarlo exactamente a lo que estamos buscando, evitando llamar a un montón de funciones innecesarias para las prestaciones que necesitamos. Además, así tendremos el control abosluto sobre los archivos y contenidos de la plantilla.

#### **Dónde localizar las plantillas instaladas**

Suponiendo que tenemos WordPress instalado y en correcto funcionamiento en un servidor (local o remoto, da lo mismo), lo primero que tendremos que hacer es ir al directorio que contiene los temas de WordPress. Este directorio se encuentra en las siguiente ruta: directoriowordpress -> wp-content -> themes, siendo directoriowordpress el directorio donde tenemos instalado WordPress dentro del htdocs del servidor.

Dentro del directorio themes veremos una carpeta para cada tema de WordPress. Ahí tendremos que crear una nueva carpeta con el nombre de nuestro nuevo tema.

A partir de ahora supondremos que estamos creando un nuevo tema llamado ***mitema***. Es decir, dentro de themes tendremos que crear un directorio llamado "mitema".

#### **Archivos de un tema de WordPress**

WordPress funciona por módulos. Por ejemplo, para insertar el footer en una página habremos de llamar al archivo footer.php, en caso de que exista. Y lo mismo con el header, la barra de navegación, etc.

Así, un tema de WordPress puede estar formado por muchos archivos, pero para que un tema de WordPress funcione, **sólo necesitará dos archivos: index.php y style.css**. Está claro que con sólo estos dos archivos tendremos un tema muy básico, pero será considerado por WordPress un tema válido si estos dos archivos están bien configurados.

Para que un tema de WordPress sea reconocido por WordPress deberá incluir sí o sí estos dos archivos, index.php y style.css. Si falta cualquiera de ellos, WordPress no reconocerá la carpeta mitema como un tema de WordPress.

A continuación vamos a desarrollar un tema más completo que nos sirva de base para otros proyectos. Y raramente crearemos un tema de WordPress que no contenga una cabecera, un footer y una barra lateral, como mínimo. Tampoco vamos aquí a desarrollar un tema complejo con funciones avanzadas, pero sí que queremos tener lo necesario para crear un tema decente con el que poder desarrollar proyectos más complejos.

Así, vamos a desarrollar un tema con la mayoría de archivos y carpetas habituales en otros temas para WordPress profesionales. Son los siguientes:

* /images. Carpeta con las imágenes del tema.
* /js. Carpeta con los archivos de JavaScript
* style.css. Hoja de estilos del tema. Obligatoria para que el tema funcione.
* index.php. Obligatorio para que el tema funcione. Por defecto será la página principal.
* screenshot.png. Muestra la imagen en miniatura que se verá en el panel de administración en Apariencia -> Temas.
* favicon.ico. La imagen que se verá en el navegador y al guardar el marcador.
* header.php. Módulo que contiene la cabecera del tema.
* sidebar.php. La barra lateral del tema.
* footer.php. Módulo que contiene el pie de página del tema.
* single.php. Este archivo especifica cómo se verá una entrada.
* page.php. Este archivo especifica cómo se verá una página estática.
* category.php. Muestra cómo se ve la página de resultados de una categoría.
* tag.php. Muestra cómo se ve la página de resultados de una etiqueta.
* search.php. Muestra cómo se ve la página de resultados de búsqueda.
* functions.php. Archivo con las funciones genéricas de nuestro tema de WordPress.

En la plantilla que vamos a desarrollar utilizaremos prácticamente todos estos archivos, para que veamos que no es tan complejo como de entrada pueda parecer.
 
A partir de ahí, es fundamental tener la capacidad de crear un buen código HTML y CSS para obtener resultados profesionales.

Para no perdernos en la inmensidad y hacer fácil lo supuestamente difícil, vamos a aplicar la técnica del divide y vencerás dividiendo la creación de la plantilla en 11 pasos

#### **Paso 1: Crear el archivo style.css**

El primer paso va a consistir en crear dentro de la carpeta "mitema" el archivo ***style.css***. 

Es recomendable utilizar un buen editor de textos para desarrollo web, como Sublime Text 2 o Notepad++, pero puedes hacerlo incluso con el Bloc de Notas de Windows si te va la marcha.

Dentro del archivo style.css, en la parte superior deberemos incluir esta información:

```css
	/*
	Theme Name: Mitema
	Theme URI: el lugar donde vayas a alojar el tema 
                 para ponerlo a disposición de la comunidad
	Description: La descripción del tema
	Author: Tu nombre y apellidos
	Author URI: la web profesional del creador del tema
            Version: 1.0
	*/
```

Fíjate que este fragmento de texto está comentado con /* ... */. Todos los datos que ponemos aquí van a aparecer junto al tema en Apariencia -> Temas.

A partir de aquí, podemos ya crear nuestro propio código de CSS.

#### **Paso 2: Imágenes y JavaScript**

Este tema lo vamos a desarrollar con HTML5. Vamos a utilizar Modernizr, una librería de JavaScript que detecta las capacidades de HTML5 y CSS3 del navegador. También haremos uso de Respond, otra librería JavaScript que sirve para que Internet Explorer sepa interpretar los media queries de CSS3. De ese modo, nuestro tema funcionará incluso en navegadores muy antiguos.

Por supuesto, puede crearse un tema sin estas librerías, pero las usaremos para ilustrar cómo se puede incrustar JavaScript en una plantilla WP.

Crearemos las carpetas "images" y "js" dentro de la carpeta "mitema".

En la carpeta "js" pondremos una copia de las librerías Modernizr y Respond bajadas directamente de las webs de los desarrolladores.

En la carpeta "images" colocaremos más adelantes todas las imágenes que vayamos necesitando para nuestro CSS. Ten en cuenta que dos archivos llamados ***screenshot.png*** y el ***favicon.ico*** se han de ubicar en la raíz del tema y no dentro de la carpeta images. Wordpress utilizará estos dos archivos para la previsualización del tema y para el icono de la página una vez que el tema se active.

#### **Paso 3: Crear la cabecera del tema y el menú de navegación**

El archivo header.php contiene la cabecera de nuestro tema. Es aquí donde pondremos nuestro logo, menú principal y aquello que aparezca en la parte superior de nuestro tema. Veamos un código posible para header.php:

```html
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
```

Si analizas el código, verás que, después del doctype, hemos abierto la etiqueta html indicando que seleccione los atributos de idioma de la instalación de WordPress.

Para el charset también hemos recurrido a una función de Wordpress, así como para el título de la página.

En el caso de estar diseñando un tema responsive, especificaremos el viewport.

Para mostrar la URL al favicon.ico le indicamos la ruta a la carpeta "mitema" de la instalación de WordPress. Eso se consigue con la función de Wordpress get_stylesheet_directory_uri().

Un poco más abajo se usa la función bloginfo() con el argumento 'stylesheet_directory', que tiene el mismo efecto que get_stylesheet_directory_uri().

Finalmente, se usa la función wp_head() de WordPress, necesaria par que muchos plugins y funcionalidades de WordPress funcionen. A partir de aquí cerramos la etiqueta head y empezamos con los contenidos de body.

Quizás aquí te estés preguntando por qué incluir el body en header.php y no en index.php. La razón es sencilla: los contenidos de la cabecera del tema van a estar en todas las páginas, por lo que al incluirlo aquí, evitamos duplicar código y el mantenimiento del tema va a ser mucho más sencillo. Así, dentro de las etiquetas de header incluiremos nuestra cabecera. En este ejemplo, hemos puesto el nombre del sitio web con un enlace a la página de inicio:

```html
	<h1><a href="<?php echo get_option('home'); ?>"><?php bloginfo('name'); ?></a></h1>
```

Fíjate que en la etiqueta header hemos escrito esta línea:

```php
	<?php wp_nav_menu( array('menu' => 'Main', 'container' => 'nav' )); ?>
```

Eso debería crear el menú de navegación, pero, para que funcione, primero deberemos añadir al archivo ***functions.php*** (que contiene las funciones propias del tema) este código:

```php
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
```

Este código lo que hace es crear un menú llamado "Main" que nos aparecerá en el panel de administración de WordPress en Apariencia -> Menús. Lo que este código dice es que si existe una función llamada register_nav_menus, entonces debe crearse un nuevo menú de navegación llamado Main. Además, la función de Wordpress add_theme_support() sirve para indicar que en este tema queremos poder crear menús dinámicos.

A partir de aquí, simplemente habremos de ir a Apariencia -> Menús y crear nuestro menú y guardarlo, como con cualquier otro theme.

Con esto ya tenemos la cabecera del tema creada junto con su menú de navegación. Recuerda que para añadir páginas al menú de WordPress, primero hay que crear las páginas o no podremos hacerlo.

#### **Paso 4: Crear la barra lateral**

La mayoría de temas de WordPress incluyen una barra lateral que no tiene por qué aparecer en todas las páginas del tema. En las barras laterales acostumbramos a poder añadir widgets, por lo que se van a tener que habilitar para widgets. Para ello, abriremos nuestro archivo ***functions.php*** e incluiremos esta función:

```php
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
```

Si activamos este tema y vamos a Apariencia -> Widgets, veremos que nos aparece una nueva zona de widgets llamada Main Sidebar. 

Una vez creada la zona lista para widgets, vamos a tener que llamarla dentro del archivo ***sidebar.php***, otro archivo típico de casi todas las plantillas. Creamos este archivo y escribimos:

```html
	<section id="sidebar">
	  <?php if ( !function_exists('dynamic_sidebar') || !dynamic_sidebar('Main Sidebar') ) : ?>
	  <?php endif; ?>
	</section>
```

Hemos utilizado un id teniendo en cuenta que en este tema sólo va a existir una barra lateral, pero si quieres crear más, quizás prefieras crear una clase. Con esto ya tenemos creada la barra lateral lista para widgets.

#### **Paso 5: Crear el footer**

Hasta aquí hemos creado la cabecera y la barra lateral. Ahora vamos a crear el footer para después integrarlo todo en index.php. 

Recuerda que WordPress funciona por módulos, y que los módulos son como piezas de un puzle: hasta ahora hemos ido creando esas piezas para luego montarlas todas en index.php.

El footer se crea, oh sorpresa, en un archivo llamado ***footer.php*** que puede quedarnos así:

```html
	<footer>
	  <p>&amp;amp;amp;copy; <?php bloginfo('name'); ?>, <?=date('Y');?>. Mi primer tema.</p>
	</footer>
	</div> <!-- Fin de wrapper -->
	<?php wp_footer(); ?>
	</body>
	</html>
```

Fíjate que la capa "wrapper" empieza en el header y termina en el footer. Si queremos un header o un footer que se extienda por toda la pantalla, deberemos mover las posiciones de los div que abren y cierran la capa "wrapper".

Aquí aparece la función wp_footer(), que es semejante a wp_header(). Estas funciones son lo que se llaman **hooks de Wordpress** y hacen funcionar los plugins que instalemos.

En el caso de wp_footer() va a ser, además, necesaria si queremos ver la barra de administración de WordPress. No serás el primero que se vuelve loco tratando de averiguar por qué no aparece la barra de administración hasta que descubre que es porque no ha llamado a este hook de WordPress.

#### **Paso 6: Crear la página principal**

En este tema, la página principal se va a corresponder a los contenidos de ***index.php***. Nuestro index tendrá este aspecto:

```html
	<?php get_header(); ?>
	  <section id="main">
	  </section> <!-- Fin de main -->
	    <?php  get_sidebar()?>
	  <?php get_footer(); ?>
```

Observa estas tres funciones: get_header(), get_sidebar() y get_footer():

* get_header() inserta los contenidos del archivo header.php en ese punto.
* get_sidebar() hace lo mismo con la barra lateral.
* get_footer() hace... bueno, ya te imaginas lo que hace, ¿verdad?

De modo que ya hemos montado nuestro puzle. Un puzle muy sencillito porque solo tiene tres piezas, vale. Pero ahora lo puedes complicar todo lo que quieras.

#### **Paso 7. El loop de WordPress**

En el ***loop*** reside toda la magia de Wordpress. 

¿Qué es el loop? Es un bucle (claro) en el que se muestram las entradas almacenadas en la base de datos de Wordpress. Y nosotros podemos decidir cómo se muestran esas entradas.

Este código de ejemplo de loop debe añadirse a continuación del anterior en ***index.php***:

```html
	<?php if (have_posts()) :  while (have_posts()) : the_post(); ?>
	    <h2><a href="<?php the_permalink(); ?>"><?php the_title(); ?></a></h2>
	   <small>Publicado el <?php the_time('j/m/Y') ?> por <?php the_author_posts_link() ? </small>
	    <?php the_excerpt(); ?>
	  <?php endwhile; else: ?>
	    <p><?php _e('No hay entradas .'); ?></p>
	  <?php endif; ?>
```

La primera línea es el auténtico loop:

```html
	<?php if(have_posts()) : ?><?php while(have_posts()) : the_post(); ?>
```

Wordpress mirará si hay alguna entrada disponible (if(have_posts())). Si es así, entramos en un bucle que se repite para todos los posts (while(have_posts())). Y, para cada post, se recupera su contenido de la base de datos (the_post()).

Una vez seleccionado el post, se muestra su información: la fecha de publicación (the_time()), los autores (the_author_posts_link()), el extracto (the_excerpt())... Si no hay posts, se muestra el mensaje de error "No hay entradas"

#### **Paso 8. Añadir thumbnails al loop**

Si queremos añadir thumbnails (imágenes destacadas) al loop como sucede en muchos portales WP, lo que haremos es lo siguiente: vamos al archivo functions.php y añadimos este código:

```html
	<?php
	//Habilitar thumbnails
	add_theme_support('post-thumbnails');
            set_post_thumbnail_size(150, 150, true);
	?>
```

Con este código hemos habilitado los thumbnials de nuestras entradas y hemos establecido un tamaño para las mismas de 150 por 150 píxeles. Una vez hecho esto, modificaremos nuestro loop como sigue:

```html
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
```

Observa que hemos añadido un par de líneas en las que se comprueba si el post tiene thumbnail y, en caso afirmativo, este se recupera.

La forma en la que queremos que se visualice todo esto debe establecerse mediante CSS, por supuesto.

Podríamos seguir añadiendo cosas al loop. Por ejemplo: podríamos añadir una paginación de las entradas. Encontrarás en la red mucha información sobre el tema, aunque lo más práctico es bajarse una plantilla sencillita ya hecha y curiosear en su código fuente.

#### **Paso 9. Resultados de la búsqueda**

Los resultados de la búsqueda se especifican en el archivo ***search.php***. He aquí un ejemplo:

```html
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
```

Fíjate que se parece mucho a index.php. 

Esta página es la que va a mostrar los resultados de una búsqueda en cuestión. Así, vamos a necesitar que aparezca un buscador en nuestra plantilla. Un buen sitio para colocarlo puede ser el sidebar. Iremos a nuestro archivo sidebar.php y justo antes de la función que habilita la zona de widgets en el sidebar, incluimos este código:

```html
	<form method="get" id="searchform" action="<?php bloginfo('url'); ?>/">
	  <input type="text" placeholder="Buscar…" value="<?php the_search_query(); ?>" name="s" id="s" />
	  <button type="submit" class="icon-only"  id="searchsubmit"></button>
	</form>
```

Con esto tenemos un campo de búsqueda en nuestra barra lateral. Para que se visualice como queremos, simplemente hará falta crear el código CSS necesario.

#### **Paso 10. Configurar la vista de las entradas (posts)**

La página del post es aquella donde vamos a ver una entrada individual, es decir, un post completo. 

Vamos a poder definir cómo se ve, incluir o no comentarios, etc.

El archivo donde se define esto se denomina ***single.php***, y puede ser más o menos así:

```html
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
```

Si has llegado hasta aquí, te resultará fácil comprender el archivo. Si en el loop utilizamos the_excerpt() para mostrar el extracto de la entrada, aquí utilizamos la función the_content() para recuperar el contenido completo de la entrada.

Por supuesto, esto se puede complicar hasta el infinito. A modo de ejemplo, mostraremos cómo podríamos mostrar las entradas relacionadas. Bastaría con añadir este código justo después de mostrar el contenidos de la entrada:

```html
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
```

#### **Paso 11: Habilitar y mostrar los comentarios**

Para permitir los comentarios en una entrada, añadiremos este código a nuestro archivo ***functions.php***:
	
```php
       // Permitir comentarios encadenados
	function enable_threaded_comments(){
	    if (is_singular() AND comments_open() AND (get_option('thread_comments') == 1)) {
	       wp_enqueue_script('comment-reply');
	    }
	}
	add_action('get_header', 'enable_threaded_comments');
```

Y en ***single.php***, justo antes de la línea del endwhile, añadiremos:

```html
	<div class="comentarios">
	  <?php comments_template(); ?>
	</div>
```

Nuevamente, será el CSS el que determine cómo se verán los comentarios. Aquí tienes un ejemplo de CSS para empezar a trabajar en él:

```css
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
```

#### **Paso 12: Crear la página de categorías y etiquetas**

Los archivos **category.php** y **tags.php** son prácticamente iguales. Simplemente añadiremos antes del loop:

```html
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
```


#### **¿Y ahora qué?**

Ya tienes una plantilla sencilla y funcional creada desde cero.

La creación de plantillas no termina aquí, claro. Solo hemos dado los primeros pasos y sentado unas bases lo más sólidas posible. La API de WordPress es muy amplia, a menudo confusa y casi siempre redundante. Especializarse en el desarrollo para WordPress es una tarea de largo recorrido que no puede aprenderse en unas cuantas horas. 

Pero, si has llegado hasta aquí, ya has hecho, probablemente, lo más difícil.

La mayoría de las plantillas tienen más archivos que la nuestra, como, por ejemplo:

* **page.php**, para mostrar páginas estáticas.
* **author.php**, para mostrar la página de "acerca de".
* **404.php**, para crear nuestra propia página de error "not found"

Por último, aquí tienes un diagrama de las relaciones que existen entre los archivos típicos de una plantilla Wordpress. Recuerda que el único obligatorio (además de styles.css) es index.php, y que una plantilla compleja puede tener otros archivos adicionales a los que aquí se muestran.

XXX esquema

### 1.2.3. Plugins de Wordpress

(El contenido de esta sección está adaptado de: www.cristalab.com/tutoriales/como-crear-un-plugin-para-wordpress-c54308l/)

#### **Los plugins de WordPress**

Los plugins, como en cualquier otro sistema, añaden funcionalidades a Wordpress. La arquitectura flexible de Wordpress permite realizar esa ampliación en casi cualquier sentido, dotando a Wordpress de esa capacidad polimórfica que lo hace tan útil en muchas circunstancias.

A partir de aquí vamos a crear un sencillo plugin para Wordpress que pueda servir de base para desarrollos posteriores más realistas.

El plugin se llamará "Saludo" y contendrá algunas funciones para saludar que nos servirán para ilustrar el funcionamiento del sistema de plugins de WordPress.

#### **Crear un plugin nuevo**

Para crear el plugin "Saludo" basta con crear un archivo llamado ***saludo.php*** en una carpeta llamada también "saludo" y ubicada a su vez en carpeta_raiz/wp-content/plugins/

Dentro del archivo saludo.php, escribiremos el comentario de cabecera para que WordPress lo reconozca como un plugin válido (igual que sucede con las plantillas). Es importante respetar la sintaxis.

```php
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
```

#### **Añadir funciones al plugin**

Vamos a crear nuestra primera función con un código algo más complejo. Todo lo que sigue se debe escribir en el mismo archivo ***saludo.php***.

```php
<?php
   // Aquí van los comentarios de la cabecera que vimos antes
   function saludo(){
      echo 'hola mundo';   
   }
?>
```

#### **Instalar y desinstalar el plugin**

Para poder instalar y desinstalar el plugin desde el panel de administracion de Wordpress, es necesario crear dos funciones en ***saludo.php***: una para instalar y otra para desinstalar. Estas funciones, por ahora, las dejaremos vacías.

Además, al final del archivo ***saludo.php*** hay que usar la funcion del API de Wordpress add_action() para indicar las funciones que activar y desactivan el plugin.

```php
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
```

#### **Cómo usar las funciones del plugin**

Ahora ya puedes usar tu maravilloso plugin. Sólo debes colocar en la sección de tu plantilla que estimes conveniente la siguiente línea:

```php
<?php saludo(); ?>
```

#### **Configurar el plugin desde el panel de administración**

Nos falta crear un item dentro del panel de administración que nos permita modificar las opciones de este plugin. El ítem lo daremos de alta dentro del menú "opciones", y para esto programaremos tres funciones más en nuestro archivo ***saludo.php***:

* saludo_panel(): aquí incluiremos el html que será expresado en nuestro panel. Para no mezclar html dentro del código, usaremos la función include() a modo de template.
* saludo_add_menu(): aquí usaremos a su vez la función de WP add_options_page.
* saludo_add_action(): para desencadenar todo esto usaremos esta función que es también parte del API de WP.

```php
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
```

Además, necesitaremos un formulario html para poder visualizar la pantalla de configuración en el panel de administración de Wordpress. Crearemos algo muy sencillo. Por supuesto, se puede mejorar con un poco de HTML y CSS. Lo escribiremos en el archivo ***template/panel.html***:

```html
<form method="post" action="" id="saludo">
<label for="saludo_inserta" accesskey="s">Inserte su saludo<input type='text' id='saludo_inserta'  name='saludo_inserta' value='' /></label>
<input type='submit' name='' value='enviar' />
</form>
```

Por último, modificaremos la función saludo_panel() para poder visualizar nuestros avances:

```php
<?php
   ...   
   function saludo_panel(){      
      include('template/panel.html');
   }
   echo "<h1>{$_POST['saludo']}</h1>";
   ...
?>
```

Podemos probar que todo funciona escribiendo algo en el formulario (pulsando "Enviar").

#### **Acceder a la BD desde nuestro plugin**

Vamos a ver cómo se puede acceder a la BD de WordPress desde un plugin.

Para ello, antes debemos desinstalar el plugin desde el panel de control. Solo así podremos modificar la función de instalación y ejecutarla más adelante de nuevo.

Las funciones de Wordpress que manejan la DB se llaman con una variable global denominada ***$wpdb***:

```php
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
```

Por supuesto, hay que agregar los datos a la DB desde nuestro panel en opciones/saludo, para lo cual modificaremos la función saludo_panel():

```php
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
```

¡Ahora que ya podemos insertar saludos en nuestra BD!

sólo nos queda poder mostrarlos en nuestra función saludo(). Para esto extraeremos un saludo de manera aleatoria a nuestra BD:

```
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
```

Ahora modifiquemos nuestro ***saludo.html*** para que imprima la variable $saludo:

```html
<h1><?php echo $saludo;?></h1>
```

Por último, vamos modificar el html de nuestro panel para que se adapte al html del administrador de WP y no quede tan feo:

```html
 <div class="wrap"> 
   <form method="post" action="">
      <fieldset>
         <legend>Ingresar Nuevo Saludo</legend>
         <label for="saludo" accesskey="s">Inserte su saludo<input type='text' id='saludo_inserta'  name='saludo_inserta'  /></label>
         <input type='submit' name='' value='enviar' />
      </fieldset>
   </form>
</div>
```

Con todo esto ya tenemos listo nuestro plugin.

Por supuesto, siguiendo la misma lógica podríamos eliminar o modificar registros o hacer cualquier otra operación que necesitásemos con la base de datos.


