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

