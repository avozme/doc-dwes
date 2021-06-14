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

Casi todas las aplicaciones web incluyen un subsistema de autenticación de usuarios (ACL = Access Control Login).
Ese subsistema suele estar basado en este diseño de base de datos:

XXX esquema

## 3.2. Cookies

Las cookies son variables que se guardan en el ordenador del cliente.

Sintaxis:
bool setcookie ( string $name [, string $value [, int $expire = 0 [, string $path [, string $domain [, bool $secure = false [, bool $httponly = false ]]]]]] )

Ejemplo:
setcookie("TestCookie", $value, time()+3600); 

Para acceder al valor de una cookie:
$_COOKIE["NombreCookie"];

Ejemplo:
echo "La cookie TestCookie vale ".$_COOKIE["TestCookie"];

## 3.3. Sesiones

Las sesiones sirven para guardar variables en el servidor.
Esas variables sólo son accesibles para el cliente que creó esa sesión.

Sintaxis:
session_start();
$_SESSION["variable"] = $valor;

Algunas funciones para manejar sesiones:

// Abre una sesión o la retoma si ya estaba abierta
session_start();
// Cierra una sesión abierta y destruye sus variables
session_destroy();
// Devuelve el ID de la sesión
session_id();
// Destruye todas las variables de sesión
session_unset();

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

## 3.5. Técnicas de ataque frecuentes

### 3.5.1. Captura de ID de sesión

El ID de sesión se pasa entre páginas de forma transparente a través de cookies o de la URL (con POST). Un atacante puede leer el ID de sesión en el paquete http y acceder a las variables de sesión.
Solución:
Combinar las variables de sesión con cookies o con entradas en la base de datos.
No confiar en variables de sesión para información sensible.

### 3.5.2. Inyección de SQL

Se inserta código SQL en campos de formulario. Este código actúa sobre la BD, dando información al atacante sobre su estructura y contenido, o permitiéndole destruir datos.
Soluciones:
Usar filtros de SQL (MySQLi incluye algunos, como real_scape_string())
Utilizar usuarios de MySQL sin privilegios destructivos (¡root solo en fase de desarrollo!)
Filtrar los datos de entrada de los formularios.

### 3.5.3. XSS (cross site scripting)
Se inyecta código JavaScript a través de la URL, de un formulario o de algún otro elemento externo.
Ese código JS redirecciona a otra página o tiene algún otro efecto indeseado.
Soluciones
Filtrar todos los datos externos.
Usar listas blancas de datos válidos.

### 3.5.4. CSRF (cross site request forgery)
Consiste en que un usuario accede a partes no permitidas de la aplicación insertando datos maliciosos en la URL o en un formulario.
Soluciones:
Utilizar POST en lugar de GET para no dar pistas.
Generar tokens únicos para cada petición.
Filtrar los datos de entrada.

### 3.5.5. DT (directory transversal)
El atacante accede a ficheros fuera del directorio público (htdocs o public_html) mediante rutas relativas (../../ejemplo.php)
Sucede cuando la página que se va a cargar se envía como un parámetro en la URL (index.php?page=ejemplo.php)
Soluciones:
Filtrar el formato de las páginas enviadas por la URL, o tener una lista de páginas válidas.

### 3.5.6. RFI (remote file inclusion)
Consiste en acceder al sistema de ficheros del servidor mediante inyección de código malicioso en la URL o en un formulario (por ejemplo, con el comando exec de SQL)
Soluciones:
Filtrar datos de entrada.
Tener una lista de páginas válidas.


