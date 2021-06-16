---
layout: page
title: 2 Introducción a PHP
permalink: /php/
nav_order: 2
has_children: false
parent: Desarrollo Web en Entorno Servidor
---
# 2. Introducción a PHP
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>


## 2.1. Programación cliente-servidor

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

## 2.2. Caja de herramientas para desarrollar de aplicaciones web

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

## 2.3. La sintaxis de PHP

### 2.3.1. Cómo embeber PHP dentro de HTML

El código PHP se escribe incrustado dentro de un documento de texto mediante estas etiquetas:

```html
<?php .... ?>
```

La sintaxis clásica está obsoleta desde PHP 7:

```html
<script language= "php"> ... </script>
```
Este archivo debe tener extensión .php.

El servidor ejecuta el código PHP que encuentre dentro del archivo, mientras que el código HTML es enviado al cliente sin modificar.

### 2.3.2. Comentarios

```php
// Comentario de una línea
#  Comentario de una línea
/* Comentario de una o varias líneas */
```

### 2.3.3. Operadores

* Operadores: son iguales que los de C/C++:
* Asignación: 	$a = 3;
* Comparación:  ==, <=, >=, !=, <=>, etc.
* Operadores aritméticos: +, -, *, /, %...
* Operadores lógicos: &&, ||, !

### 2.3.4. Variables

Las variables de una función/clase/método PHP son siempre **locales**, es decir, sólo están disponibles en esa función/clase/método, salvo que se indique otra cosa.

Si se definen variables fuera de una función, serán globales a todo el fichero actual, pero no pueden usarse en el código ubicado en otros ficheros.

El **identificador** de variable siempre debe empezar por $. Esta es una peculiaridad de PHP que al principio descoloca un poco.

No es necesario declararlas: al inicializarlas queda especificado el tipo. A partir de PHP 7 pueden indicarse los tipos predefinidos (int, float, string...)
Ejemplos:

```php
$a = 4;                  // Variable entera (PHP 5)
int $a = 4;              // Variable entera (PHP 7+)
$media = 52.75;          // Variable real
$texto = "Hoy es lunes"; // Variable string
```

Cualquier variable puede **cambiarse de tipo** con la función **setType()**:

```php
$a = "10";                 // a es una cadena
setType($a, "integer");    // a se convierte a entero
```

Los **tipos de datos** predefinidos en PHP son:

* integer (entero)
* double (real)
* bool (booleano)
* string (cadena)
* array (pues eso)

### 2.3.5. Arrays

Los arrays en PHP son colecciones de variables del mismo o de distinto tipo identificadas por un índice. Se parecen más a los ArrayList de Java que a los arrays clásicos propiamente dichos.

```php
$a[1] = "lunes";
$a[2] = "martes";
$a[3] = "miércoles";
```

El índice no tiene por qué ser un número entero: puede ser un String (array asociativo):

```php
$a["ESP"] = "España";
$a["FRA"] = "Francia";
$a["POR"] = "Portugal";
```

### 2.3.6. Estructuras de control

#### Condicionales

```php
if (condición)
{
acciones-1;
}
else
{
acciones-2;
}
```

#### Bucle while

```php
while (condición)
{
acciones;
}
```

#### Bucle repeat

```php
do
{
acciones;
}
while (condición);
```

#### Bucles for y foreach

El bucle for controlado por contador es idéntico a C/C++ y Java:

```php
for (inicialización; condición; incremento)
{
acciones;
}
```

Hay una variedad de bucle for muy interesante: el bucle foreach para recorrido de arrays asociativos:

```php
foreach ($array as $índice=>$var)
{
acciones;
}
```

El bucle foreach se repite una vez para cada valor guardado en el array. Ese valor se asigna a la variable $var en cada repetición.


### 2.3.7. Funciones y procedimientos

Los subprogramas (funciones y procedimientos) se escriben en PHP con la misma palabra: function.

* Las **funciones** deben devolver un valor en su última línea con return. Si necesitas devolver varios valores, puedes empaquetarlos en un array.
* Los **procedimientos** no tienen return. Realizan su función y terminan.

Los **parámetros** de la función en PHP siembre se pasan por valor. 

Por ejemplo:

```php
function calcular_iva($base, $porcentaje)
{
   $total = $base * $porcentaje /100;
   return $total;
}
```

### 2.3.8. Clases y objetos (¡solo en PHP5 y PHP7!)

Las clases, métodos y atributos se declaran de forma muy semejante a C++ y Java:

```php
class miClase
{
    // Declaración de propiedades (atributos)
    public $var = 'soy una variable de clase';

    // Método constructor (siempre se llama __construct)
    public function __construct($valor) {
        $var = $valor;
    }

    // Declaración de métodos
    public function mostrarVar() {
        echo $this->var;
    }
    private function resetVar() {
       $this->var = '';
    }
}
```

Para instanciar un objeto de una clase, se usa la palabra new. El constructor puede llevar parámetros o no, como en Java. Por ejemplo:

```php
$miObjeto = new miClase('Estoy aprendiendo PHP');
$miObjeto->mostrarVar();
```

La salida de este programa sería "Estoy aprendiendo PHP".

### 2.3.9. Salida de datos

PHP puede hacer salidas de datos como cualquier otro lenguaje de programación: puede enviar texto a una impresora, datos a un fichero o puede dibujar ventanas y componentes en un entorno gráfico de usuario.

Pero cuando PHP se ejecuta como parte de una aplicación web, nada de eso tiene sentido: esa salida se produciría en el servidor, y nosotros no estamos allí para verla. Nosotros estamos en nuestro cliente (navegador web), pidiendo al servidor que ejecute un programa PHP.

Recuerda que, en este contexto, la salida PHP es siempre código HTML válido. Ese código HTML será recibido por tu navegador, interpretado y mostrado en la ventana del navegador.

Observa el uso de "echo" para producir una salida HTML desde este pequeño script PHP:

```html
<body>
 <?php 
     echo "Soy un script de PHP y estoy generando 
               código HTML. Para demostrarlo
               voy a escribir <b>esto en negrita</b>"
  ?>
</body>
```

### 2.3.10. Paso de parámetros por la URL

Las aplicaciones web pueden recibir parámetros a través de la propia URL de invocación del servidor.

Imagina que tenemos este link en un documento HTML:

```html
<a href="pagina.php?variable1=valor1&variable2=valor2&etc…">
```

Al hacer clic en él, pediremos al servidor que ejecute el programa cuyo código fuente está en el archivo "pagina.php", ¿verdad?

Pues bien, ese programa "pagina.php" puede acceder a las variables "variable1", "variable2", etc.

Esto se hace a traves del array global de PHP **$_GET**, que se indexa con el nombre de las variables. Así:

```php
<?php
echo "La variable 2 vale:".$_GET['variable2']."<br>";
?>
```

### 2.3.11. Entrada de datos a través de formulario (1)

Como PHP se ejecuta dentro de HTML, sólo puede recibir datos del usuario de la aplicación a través del navegador web.

Y sólo hay una forma de introducir datos en una página web: a través de un formulario.

Veámoslo con un ejemplo. Supongamos que hemos definido en HTML este sencillo formulario:

```html
<body>
<form method="post" action="destino.php">
Nombre<br/>
<input type="text" name="nombre"><br/>
Apellidos<br>
<input type="text" name="apellidos"><br/>
<input type="submit">
</form>
</body>
```

Al pulsar el botón "Enviar", se cargará el script destino.php en el servidor.

Ese script recibirá dos variables HTML llamadas nombre y apellido, con el valor que el usuario haya introducido en el formulario.

Para acceder a las variables HTML, se usa el array del sistema **$_POST**, indexándolo con el nombre de la variable:

```php
<?php 
     echo "La variable nombre vale".$_POST['nombre']."<br>" 
?>
```

Observa que $_POST es una variable semejante a $_GET. Puedes utilizar una u otra según el valor del atributo *method* de tu formulario HTML.

La variable **$_REQUEST** sirve tanto para POST como para GET. **Por eso será la que nosotros usaremos preferentemente en nuestros programas**.

## 2.4. Interacción entre MariaDB y PHP

MySQL es un SGBD profesional, por lo que la interacción con él busca ser eficiente y segura, pero no necesariamente fácil.

Hay básicamente tres métodos de utilizar MySQL:

* A través de la línea de comandos:
   Iniciamos una sesión en MySQL con:
   
```
$ mysql -h servidor -u nombre_usuario -p
```

   Y luego tenemos a nuestra disposición montones de comandos para hacer cosas con la base de datos, incluyendo cualquier instrucción válida en SQL.

* A través de una aplicación con interfaz gráfico como PHPMyAdmin, una aplicación web escrita en PHP que proporciona un interfaz muy cómodo para trabajar con MySQL o MariaDB.

* A través de un programa escrito en PHP o algún otro lenguaje con posibilidad de acceso a MySQL. Este método de acceso será el que nosotros practicaremos a lo largo del curso. Por ahora, vamos a ver lo fundamental.

### 2.4.1. Acceso a MySQL con PHP4

El modo en que se accedía a bases de datos en PHP4 era mediante bibliotecas de funciones diferentes para cada SGBD.

Este tipo de codificación está obsoleta y se desaconseja su uso. Ya no tiene soporte oficial, por lo que no se resolverán futuros problemas de seguridad o estabilidad.

**Lo mostramos aquí para que sepáis lo que NO se debe hacer.** 

**Encontraréis mucho código de esta naturaleza en la red que DEBE SER EVITADO.**

#### Acceso a MySQL con PHP4

PHP4 utiliza una biblioteca de funciones PHP cuyo nombre empieza por mysql_.

Por ejemplo, para insertar un registro en una BD MySQL, se hacía así:

```php
<?php
//Conectamos con MySQL
mysql_connect("URL","nombre_usuario","contraseña");

//Selección de la base de datos con la que vamos a trabajar
mysql_select_db("nombre_base_de_datos");

//Ejecucion de cualquier sentencia SQL válida
mysql_query("INSERT INTO clientes (nombre,telefono) VALUES ('$nombre','$telefono')");
?>
```

Y para ejecutar consultas (SELECT), se recogía el resultado en un cursor. Observa cómo se hacía en este ejemplo:

```php
<?php
//Nos conectamos con MySQL
mysql_connect(“URL","user","password");

//Seleccionamos la base de datos con la que vamos a trabajar
mysql_select_db("nombre_base_datos");

//Ejecutamos la consulta SQL
$result=mysql_query("SELECT * FROM Clientes");
?>

... continúa en la pág. siguiente ...

Consultas SQL con PHP4 (2/2)

... viene de la pág. anterior ...

<table align="center"><tr>
<th>Nombre</th>
<th>Teléfono</th></tr>
<?
//Mostramos los registros
while ($registro=mysql_fetch_array($result)) {
echo '<tr><td>'.$registro["nombre"].'</td>';
echo '<td>'.$registro["telefono"].'</td></tr>';
}
mysql_free_result($result)
?>
</table>
</body>
```

**RECUERDA: esta forma de operar con la base de datos está OBSOLETA y DEBE SER EVITADA.** Te la mostramos aquí solo para que sepas reconocerla si te la encuentras por las procelosas aguas de internet.

### 2.4.2. Acceso a MySQL con PHP5+

Desde PHP5, se utiliza una biblioteca de clases para acceder a los diferentes SGBDs.

Todos los nuevos desarrollos deberían usar las bibliotecas de clases y prescindir de las viejas librerías de funciones.

*Vuelvo a repetirlo: mucho código de ejemplo de PHP que circula por la red es PHP4 y DEBE SER EVITADO.*

#### Acceso a MySQL con PHP5+

Por ejemplo, para insertar un registro en una BD MySQL:

```php
<?php
// Conectamos con el servidor y abrimos la BD.
$conexdb = new mysqli('host','username','password','database');

// Aquí se ejecutaría cualquier sentencia SQL válida.
// Por ejemplo:
$conexdb->query("INSERT INTO clientes (nombre,telefono) VALUES ('$nombre','$telefono')");
?>
```

PHP proporciona varios mecanismos para acceder a bases de datos (¡demasiadas formas de hacer lo mismo!):

* **La extensión mysqli en su forma procedimental.**

   Es idéntica a la de PHP4, pero cambiando la palabra “mysql” por “mysqli”. 

   Por ejemplo, mysql_connect() cambia a mysqli_connect().

   Esta forma es apta para programadores perezosos y anticuados, que no quieren pasarse a la programación orientada a objetos.

* **La extensión mysqli en su forma orientada a objetos.**

   Es la que nosotros estamos usando y usaremos todo el curso.
   
* **La extensión PDO.**

   Se trata de una clase genérica que permite acceder a cualquier gestor de bases de datos mediante el mismo conjunto de métodos. En funcionalidad y rendimiento es idéntica a mysqli.

#### Consultas SQL con PHP5+
XXX
La ejecución de consultas (SELECT) produce la devolución de un conjunto de registros. Esos registros se manejan en PHP con un cursor. Observa cómo se hace en este ejemplo:
<body>
<?php
//Nos conectamos con MySQL
$db = new mysqli("URL","user","password", "database");

// Comprobamos que la conexión se ha realizado
if($db->connect_error){
   die("Error en la conexion : ".$db->connect_error);
}

//Ejecutamos la consulta SQL
$result=$db->query("SELECT * FROM Clientes");
?>
... continúa en la pág. siguiente ...

Consultas SQL con PHP5 y PHP7 (2/2)
           ... viene de la pág. anterior ...

<table align="center"><tr>
<th>Nombre</th>
<th>Teléfono</th></tr>
<?
//Mostramos los registros
while ($registro=$result->fetch_array()) {
echo '<tr><td>'.$registro["nombre"].'</td>';
echo '<td>'.$registro["telefono"].'</td></tr>';
}
$db->free($result);  // Libera memoria usada por cursor
$db->close();   // Cierra la conexión con el servidor
?>
</table>
</body>

## 2.5. Ejemplos de uso de PHP

Aviso previo: para hacer todos estos ejercicios debes tener un servidor Apache con soporte para PHP5 o PHP7 en funcionamiento. De momento, si trabajas con Windows o Mac, lo más cómodo es que tengas instalado XAMPP, WAMPP o MAMPP en tu ordenador. Si lo tuyo es Linux, instala Apache2, MySQL (o MariaDB) y phpMyAdmin desde los repositorios oficiales de tu distribución. 

Ejercicio 0: hola mundo
Comprueba que todo lo necesario para programar en PHP (editor, cliente ftp, servidor apache, etc.) funciona correctamente. Para hacerlo, escribe un sencillo script que genere el mensaje “Hola mundo”. Luego prueba a sustituirlo por una llamada a la función phpinfo(), para obtener información sobre la versión de PHP con la que estás trabajando en el servidor.
Ejercicio 1: positivo, negativo
Diseña un formulario –ejercicio01.html- con un campo de texto en el que puedas escribir números. Al pulsar el botón de enviar debe llamar a un script –ejercicio01.php- que debe decirnos si el número enviado fue positivo, cero o negativo.
A la página ejercicio01.php añádele un enlace HTML que permita volver a la página anterior. 
Ejercicio 2: tabla de multiplicar
Diseña un formulario –ejercicio02.html- con un campo de texto en el que puedas escribir números. Al pulsar el botón de enviar debe llamar a un script –ejercicio02.php- que mostrar la tabla de multiplicar del número introducido. A la página ejercicio02.php añádele un enlace HTML que permita volver a la página anterior. 
Ejercicio 3: tabla de multiplicar en forma de tabla
Modifica el ejercicio anterior para que la salida se produzca en una tabla HTML de 5 por 5 casillas. Deben aparecer, por lo tanto, los primeros 25 términos de la tabla de multiplicar. En la cabecera de la tabla coloca un encabezado que ocupe todo el ancho de la misma. Asigna los nombres ejercicio03.html y ejercicio03.php a los archivos.
Por ejemplo, si el número introducido es el 3, el resultado debe ser:
Tabla de multiplicar del número 3
3 x 1 = 3
3 x 2 = 6
3 x 3 = 9
3 x 4 = 12
3 x 5 = 15
3 x 6 = 18
3 x 7 = 21
3 x 8 = 24
3 x 9 = 27
3 x 10 = 30
3 x 11 = 33
3 x 12 = 36
3 x 13 = 39
3 x 14 = 42
3 x 15 = 45
3 x 16 = 48
3 x 17 = 51
3 x 18 = 54
3 x 19 = 57
3 x 20 = 60
3 x 21 = 63
3 x 22 = 66
3 x 23 = 69
3 x 24 = 72
3 x 25 = 75

Ejercicio 4: anagramas
Una palabra es un anagrama de otra si contiene las mismas letras colocadas en orden diferente. Por ejemplo, "CAVA" es un anagrama de "VACA", y viceversa.
El ejercicio consiste en escribir un programa en PHP que pida dos palabras y compruebe si la primera es un anagrama de la segunda.
Ejercicio 5: juego del número secreto
Construyamos ahora un programa PHP para jugar al típico juego del número secreto. El ordenador elegirá un número al azar entre 1 y 100, y luego nos pedirá que lo adivinemos. Si introducimos un número menor o mayor que el número secreto, el programa nos dará una pista (“el número secreto es mayor” o “el número secreto es menor”). Si acertamos, habremos ganado, y el programa nos dirá cuántos intentos hemos necesitado para adivinar el número.

Ejercicio 6: función potencia
Escribe una función PHP que reciba dos parámetros (A y B) y devuelva el valor de la potencia de A elevado a B (AB). Escribe también un programa PHP que haga uso de esa función para calcular potencias.
Ejercicio 7: devolución de arrays
Escribe un programa PHP que pida cinco números al usuario y los guarde en un array. Luego debe llamar a una función pasándole el array como parámetro, y la función calculará cuál de los cinco números es el mayor, cuál el menor y cuánto vale la media, devolviendo esos tres valores en otro array. Por último, se mostrarán en la pantalla el mayor, el menor y la media.
Ejercicio 8: formularios complejos
Crea un formulario (como el de la figura de más abajo) en un archivo ejercicio08.php. Al hacer clic en “Enviar”, debe lanzarse el script ejercicio08_accion.php. Este script debe comprobar que todos los datos del formulario han sido completados. Si no es así, mostrará un mensaje de error y volverá atrás. 
Luego comprobará si la edad es mayor o igual a 18 años. Si es menor, también mostrará un mensaje y volverá atrás. 
Si todo es correcto, mostrará los datos presentes del formulario en una tabla, junto con la fecha y la hora actual del sistema (ver segunda imagen)
Para hacer este ejercicio necesitarás algunas funciones de fecha y hora de PHP. Puedes consultar la referencia completa del lenguaje en la página oficial de PHP: www.php.net. Las funciones de fecha y hora están detalladas en http://www.php.net/manual/es/ref.datetime.php

## Algunos ejercicios avanzados de PHP

Ejercicio 1: Simon dice
“Simon dice” es un clásico juego de memoria que consiste en componer secuencias de cuatro colores cada vez más largas, y el jugador tiene que recordarlas y reproducirlas. Puedes encontrar muchas versiones de Simon en internet.
Nosotros vamos a construir una versión simplificada que muestre secuencias de números (aunque podríamos hacerlo con colores sólo complicándolo un poco). El programa mostrará un número entre 1 y 4 durante un instante, y luego borrará la pantalla y pedirá al usuario que lo repita. Después mostrará dos números aleatorios entre 1 y 4 (por ejemplo, 3 – 1), y luego el usuario los tendrá que repetir, y así hasta que el usuario falle al introducir los números.

Ejercicio 2: creación de tablas
Crea una base de datos nueva llamada Videoclub en MySQL. Puedes utilizar PHPMyAdmin para ello, aunque también podríamos hacerlo desde un programa PHP.
Luego, escribe un programa PHP llamado ejercicio09.php que sirva para crear las siguientes tablas del Videoclub (sólo usaremos tres por ahora). El programa debe informar de si las tablas se crearon correctamente o si ocurrió algún error al crearlas.
    • Películas (cod_película#, título, género, país, año, distribuidora)
    • Personas (cod_persona#, nombre, apellidos)
    • Actúan (cod_película#, cod_persona#)
Ejercicio 3: modificación de tablas
Escribe un programa PHP que, tras pulsar un botón que debe aparecer en la pantalla, realice en la base de datos del ejercicio anterior los siguientes cambios:
    • Eliminar el campo “distribuidora” a la tabla Películas.
    • Crear el campo “país” en la tabla Personas.
    • Crear las claves ajenas de la tabla Actúan. Es decir, que la tabla quede así: Actúan (cod_película#, cod_persona#)
Ejercicio 4: mantenimiento de tablas maestras
Crea un programa PHP para mantener la tabla Películas. El programa debe permitir:
    • Añadir nuevos registros, introduciendo todos los campos de la tabla.
    • Eliminar registros existentes, introduciendo el código de la película.
Ejercicio 5: consultas simples
Escribe un programa en PHP que permita buscar a una película cualquiera introduciendo su código. Debe mostrar todos los datos disponibles en la tabla Películas.
Ejercicio 6: consultas y actualizaciones
Combina los ejercicios 11 y 12 para que el mantenimiento de tablas también incluya la posibilidad de modificar registros existentes.
Primero, el usuario podrá buscar una película introduciendo su código, y el programa mostrará los datos correspondientes a ese registro (o un error si no existe). Luego, podrá modificarse cualquier campo del mismo.
Ejercicio 7: consultas complejas
Escribe un último programa PHP que permita consultar una película por código, por título o por género (en los dos últimos casos, la búsqueda puede producir varios resultados, de los que el usuario debe poder seleccionar el que desee). En la pantalla deben aparecer todos los datos de la película, incluyendo su reparto.
Ejercicio 8: biblioteca del instituto
La Biblioteca del IES Celia Viñas tiene guardado su fondo de libros en una base de datos con la siguiente estructura ER:
























Algunas entidades no son evidentes por sí mismas:
    • Funciones contiene las funciones que puede realizar un autor en un libro (autor principal, traductor, ilustrador, prologuista, etc.)
    • TiposFondo se refiere a los diferentes tipos de soporte que existen en la biblioteca: libro, DVD, cuadernillo, documentos sueltos, etc.
    • Aplicaciones contiene las áreas educativas a los que el libro va dirigido: matemáticas, literatura, astronomía, etc.
    • El atributo “principal” de la relación FondosAutores sirve para indicar cuál de los autores es el principal en una obra colectiva.

Las tablas que resultan de ese DER son:
Fondos (IdFondo#, Titulo, Subtitulo, LugarEdicion, IdTipoFondo, IdEditorial)
Editoriales (IdEditorial#, Editorial)
Autores (IdAutor#, Autor)
Ejemplares (IdEjemplar#, IdFondo, ISBN, FechaAlta, Sig1, Sig2, Sig3)
TiposFondo (IdTipoFondo#, TipoFondo)
Fondos_Autores (IdAutor#, IdFondo#, idFuncion#, Principal)
Funciones (IdFunción#, Función)
Géneros (IdGénero#, Género)
Fondos_Géneros (IdFondo#, IdGénero#)
Aplicaciones (IdAplicación#, Aplicación)
Fondos_Aplicaciones (IdFondo#, IdAplicación#)

Se quiere construir un pequeño programa para poder consultar los fondos de la biblioteca desde la página web del instituto. La consulta debe permitir buscar libros por título, autor, editorial, isbn, aplicación y género. El resultado será una lista de libros de los que el usuario podrá seleccionar uno para obtener la ficha completa del mismo (la ficha incuirá toda la información disponible en la BD para ese libro)
Después se podrá volver atrás para modificar la búsqueda o para hacer otra búsqueda nueva.
En el servidor del aula dispones de una réplica de la BD de la biblioteca para hacer las pruebas.



S

