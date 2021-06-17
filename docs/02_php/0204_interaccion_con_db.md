---
layout: page
title: 2.4 Interacción con la base de datos
permalink: /php/interaccion-con-php
nav_order: 4
has_children: false
parent: 2 Introducción a PHP
grand_parent: Desarrollo Web en Entorno Servidor
---

## 2.4. Interacción entre MariaDB y PHP
{: .no_toc }

- TOC
{:toc}

A partir de ahora, vamos a referirnos a MySQL/MariaDB indistintamente. Este será el gestor de bases de datos relacionales que vamos a usar a lo largo del curso. La adaptación a otros gestores, en cualquier caso, es muy simple.

MySQL/MariaDB es un SGBD profesional, por lo que la interacción con él busca ser eficiente y segura, pero no necesariamente fácil.

Hay básicamente tres métodos de utilizar MySQL:

* **A través de la línea de comandos:**

   Iniciamos una sesión en MySQL con:
   
   ```
   $ mysql -h servidor -u nombre_usuario -p
   ```

   Y luego tenemos a nuestra disposición montones de comandos para hacer cosas con la base de datos, incluyendo cualquier instrucción válida en SQL.

* **A través de una aplicación con interfaz gráfico como PHPMyAdmin**, una aplicación web escrita en PHP que proporciona un interfaz muy cómodo para trabajar con MySQL o MariaDB.

* **A través de un programa escrito en PHP** o algún otro lenguaje con posibilidad de acceso a MySQL. Este método de acceso será el que nosotros practicaremos a lo largo del curso. Por ahora, vamos a ver lo fundamental.

### 2.4.1. MySQL/MariaDB con PHP4

El modo en que se accedía a bases de datos en PHP4 era mediante bibliotecas de funciones diferentes para cada SGBD.

Este tipo de codificación está obsoleta y se desaconseja su uso. Ya no tiene soporte oficial, por lo que no se resolverán futuros problemas de seguridad o estabilidad.

**Lo mostramos aquí para que sepáis lo que NO se debe hacer.** 

**Encontraréis mucho código de esta naturaleza en la red que DEBE SER EVITADO.**

#### Acceso a MySQL con PHP4 (¡OBSOLETO!)

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

### 2.4.2. MySQL/MariaDB con PHP5+

Desde PHP5, se utiliza una biblioteca de clases para acceder a los diferentes SGBDs.

Todos los nuevos desarrollos deberían usar las bibliotecas de clases y prescindir de las viejas librerías de funciones.

*Vuelvo a repetirlo: mucho código de ejemplo de PHP que circula por la red es PHP4 y DEBE SER EVITADO.*

#### Conectar a MySQL con PHP5+

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

La ejecución de consultas (SELECT) produce la devolución de un conjunto de registros. Esos registros se manejan en PHP con un cursor. Observa cómo se hace en este ejemplo:

```html
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
```

