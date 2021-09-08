---
layout: page
title: 2.3 Sintaxis de PHP
permalink: /php/sintaxis-de-php
nav_order: 3
has_children: false
parent: 2 Introducción a PHP
grand_parent: Desarrollo Web en Entorno Servidor
---

## 2.3. La sintaxis de PHP
{: .no_toc }

- TOC
{:toc}

### 2.3.1. Cómo embeber PHP dentro de HTML

El código PHP se escribe incrustado dentro de un documento de texto mediante estas etiquetas:

```html
<?php .... ?>
```

La siguiente sintaxis está obsoleta desde PHP7. Si la encuentras en alguna web, huye de allí lo más rápido que puedas:

```html
<script language= "php"> ... </script>
```
**Este archivo debe tener extensión .php, *nunca .html***

Cuando el servidor web encuentre un archivo con extensión .html, lo enviará al cliente sin mirar ni siquiera lo que hay en su interior.

En cambio, cuando el servidor web encuentre un archivo con extensión .php, lo abrirá y buscará las etiquetas <?php ... ?>, y ejecutará el código que haya dentro antes de enviar el resultado al cliente. El resto del archivo, es decir, lo que esté fuera de las etiquetas de PHP, se enviará al cliente sin modificar.

### 2.3.2. Comentarios

Los comentarios de PHP se pueden escribir de varias formas:

```php
// Comentario de una línea
#  Comentario de una línea
/* Comentario de una o varias líneas */
```

### 2.3.3. Operadores

Los operadores en PHP son iguales que los de Java, que, a su vez, los heredó de C/C++:

* Asignación: $a = 3;
* Comparación:  ==, <=, >=, !=, <=>, etc.
* Operadores aritméticos: +, -, *, /, %...
* Operadores lógicos: &&, \|\|, !

### 2.3.4. Variables

Las variables de una función/clase/método PHP son siempre **locales**, es decir, sólo están disponibles en esa función/clase/método, salvo que se indique otra cosa.

Si se definen variables fuera de una función, serán **globales** a todo el fichero actual, pero no pueden usarse en el código ubicado en otros ficheros. Existen maneras de lograr que una variable sea global a todo el código, pero, vamos... ¿en serio quieres hacer eso?

(Nota anticipatoria: hay ciertas situaciones en las que una aplicación web *necesita* variables globales, pero ya lo veremos en su momento. Por ahora, solo recuerda que usar variables globales es una pésima práctica de programación).

El **identificador** de variable siempre debe empezar por $. Esta es una peculiaridad de PHP que al principio descoloca un poco.

En PHP, no es necesario declarar las variables: al inicializarlas queda especificado el tipo. A partir de PHP7 pueden indicarse los tipos predefinidos (int, float, string...), pero solo es algo optativo.

Ejemplos:

```php
$a = 4;                  // Variable entera (PHP5+)
int $a = 4;              // Variable entera (PHP7+)
$media = 52.75;          // Variable real
$texto = "Hoy es lunes"; // Variable string
```

Cualquier variable puede **cambiarse de tipo** con la función **setType()**:

```php
$a = "10";                 // a es una cadena
setType($a, "integer");    // a se convierte a entero
```

El tipado de PHP es débil, así que puedes encontrarte expresiones donde se mezclan tipos. PHP hará las conversiones que le parezca oportunas, con resultados a veces imprevisibles, por lo que no es buena idea recurrir a estas estratagemas a menos que sepas muy bien lo que estás haciendo y el resultado que obtendrás. Por ejemplo:

```php
$a = 3;                // a es un integer
$b = "Hoy es lunes";   // b es un string
$c = $a + $b;          // ¡Esto funciona, pero ¿a que no predices bien el resultado?
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

Vamos a hacer un repaso muy rápido por las estructuras de control de PHP. Si ya conoces otros lenguajes como Java, todas te resultarán familiares.

#### Condicionales

El condicional doble tiene la sintaxis habitual:

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

Por supuesto, la parte del ```else``` puede eliminarse si no la necesitas, y obtendrías un condicional simple.

#### Bucle while

El bucle de *tipo while* tiene este aspecto:

```php
while (condición)
{
acciones;
}
```

#### Bucle repeat

El bucle de *tipo repeat*, es decir, con la condición al final, tiene esta sintaxis:

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

XXX

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

