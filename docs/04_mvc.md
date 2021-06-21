---
layout: page
title: 4 Arquitectura MVC
permalink: /mvc/
nav_order: 4
has_children: false
parent: Desarrollo Web en Entorno Servidor
---
# 4. Arquitectura MVC

Cuando hablamos de arquitectura de una aplicación web nos referimos a la estructura básica que la sustenta, como los pilares de un edificio en construcción. Si quitas las paredes, las ventanas, las puertas, los azulejos de la cocina... todavía pueden distinguirse las formas fundamentales, ¿verdad?

En este tema, hablaremos mucho de la arquitectura más popular en aplicaciones web (llamada MVC; no te preocupes, pronto se convertirá en tu mejor amiga). Pero, antes, vamos a darle una vuelta al término "arquitectura", porque en aplicaciones web se usa con dos significados distintos que conviene que tengas claros para no hacerte un lío. 

## 4.1 Arquitecturas FÍSICAS multinivel (multitier)

Hablamos indistintamente de "arquitectura de una aplicación web" para referirnos a dos cosas distintas: la arquitectura física y la arquitectura lógica. Y ahí empiezan los líos.

Vamos a intentar desliarnos antes de apretar el nudo.

Una **arquitectura física de varios niveles** (multinivel o multitier, en inglés) consiste en un conjunto de ordenadores conectados a una red que ejecutan de forma conjunta una aplicación.

El ejemplo más sencillo es la arquitectura cliente-servidor, la más popular en aplicaciones web sencillas: una máquina cliente y una máquina servidor ejecutan alternativamente fragmentos del código, proporcionando al usuario final la sensación de una aplicación unificada. 

![Arquitectura en 2 niveles](/assets/images/04-arquitectura-2-niveles.png)

Por supuesto, nada impide que tengamos más de dos máquinas colaborando en red par ejecutar una aplicación web. Podemos tener, por ejemplo, un cliente, un servidor web y un servidor de bases de datos (estos dos últimos en dos máquinas físicas diferentes). Esto sería una arquitectura de 3 niveles físicos.

La arquitectura de N niveles tendría este aspecto:

![Arquitectura en N niveles](/assets/images/04-arquitectura-N-niveles.png)

## 4.2 Arquitecturas LÓGICAS multicapa (multilayer)

Ahora viene la vuelta de tuerca: la arquitectura de una aplicación también puede referirse a sus capas (layers) lógicas. Es decir, a las capas de software que nosotros, como desarrolladores, crearemos.

Dividir una aplicación en capas que colaboran entre sí por medio de interfaces bien definidos no es una idea nueva, ni pertenece exclusivamente al ámbito de la programación web. Pero la mayor parte de las aplicaciones web hacen uso de este mecanismo de abstracción.

La idea es dividir nuestra aplicación en capas de niveles de abstracción cada vez mayor. La capa superior (la más abstracta) es la que interacciona con el usuario: ahí se implementará nuestro interfaz de usuario, o lo que en aplicaciones web se llama *front-end*.

La capa inferior (la menos abstracta) es la que está en contacto con el hardware de la máquina. Bueno, con el hardware no: debajo de ella habrá otras capas que ya no pertenecen a nuestra aplicación y que se encargarán de ello: el sistema operativo, el servidor, el gestor de bases de datos, o lo que sea. Pero nuestra capa inferior será la que interactúe con esas otras capas que escapan a nuestros dominios y que están en contacto con la máquina.

Esta división en capas de abstracción, que puede parecer al neófito una complicación innecesaria, tiene un montón de ventajas y por eso se usa en cualquier aplicación un poco más complicada que "Hola, mundo".

### 4.2.1. Ventajas de las arquitecturas multicapa

Las arquitecturas multicapa permiten varias cosas que no pueden hacerse con los códigos monolíticos. Entre otras:

* Desarrollar en paralelo cada capa (mayor rapidez de desarrollo).
* Aplicaciones más robustas (gracias al encapsulamiento. ¿Te suena? ¡Programación orientada a objetos!).
* Matenimiento más sencillo.
* Más flexibilidad para añadir módulos.
* Más escalabilidad para aumentar rendimiento.

### 4.2.1. Esquema Modelo-Vista-Controlador (MVC)

Y por fin llegamos a la palabreja: Modelo-Vista-Controlador o MVC. ¿Qué narices es esto?

Tan solo una arquitectura multicapa estandarizada. Una arquitectura de 3 capas, para ser exactos.

Este es el esquema de una arquitectura en 3 capas. Recuerda: cada capa ejecuta una parte de la solución, y entre ellas colaboran para formar la aplicación completa. La capa superior interactúa con el usuario; la capa inferior, con la máquina (donde dice "hardware", debería decir "cualquier cosa menos abstracta que nuestro programa"). Tienes permiso para imaginar cada capa como una clase con sus métodos y atributos.

![Arquitectura en 3 capas](/assets/images/04-arquitectura-3-capas.png)

Pues bien, si a esas tres les ponemos nombres exóticos como modelo, vista y controlador, y remeneamos un poco el esquema, ya lo tenemos: la arquitectura MVC.

![Arquitectura MVC](/assets/images/04-arquitectura-mvc.png)

Es decir, la arquitectura MVC solo es un caso particular de la arquitectura en 3 capas.

¿Y ya está? Bueno, no. Ahora tienes que aprender qué signfica *en realidad* esta palabrería.

Para que tengas una idea completa del asunto, ahora tienes que aprender qué parte de la aplicación se ejecuta en cada una de las capas. Pero es más simple de lo que parece. Y lo maravilloso es que el 99,99% de las aplicaciones web encajan como un guante en esta arquitectura. Es decir, apenas tendremos que hacer trabajo de diseño previo, porque, si es una aplicación web, ya sabemos qué clases tendremos que construir: los que nos indique la arquitectura MVC.

Antes de entrar en profundidad, un breve apunte: por supuesto, nada impide construir arquitecturas con más de 3 capas. De hecho, nosotros vamos a usar una variante del MVC en el que se añade una capa adicional por debajo del modelo, es decir, una arquitectura con 4 capas. Pero ya llegaremos a eso.


### 4.2.2. Otras arquitecturas multicapa
Modelo de capas mejorado con una capa de entidades

XXX esquema

### 4.2.3. Características de las arquitecturas multicapa
Funcionalidades transversales presentes en todas las capas:
Seguridad
Escalabilidad
Rendimiento
Comunicaciones
Control de calidad

## 4.3. Arquitecturas orientadas a los servicios (SOA)
Permiten comunicar sistemas diferentes mediante protocolos bien definidos en XML.

XXX esquema

Los estudiaremos en un tema posterior.

## 4.4. Patrones de software

Los patrones de software: Soluciones comprobadas a problemas comunes en el desarrollo de software.
Características de un patrón:
Debe haber sido comprobado en otros sistemas.
Debe ser fácilmente reutilizable.
Debe ser aplicable a diferentes circunstancias.
Debe estar bien documentado.

### 4.4.1. Documentación típica de un patrón de software:
Nombre.
Problema que resuelve.
Contexto en el que es aplicable.
Fuerzas, objetivos y restricciones.
Solución que propone.
Ejemplos.
Contexto resultante.
Exposición razonada.
Otros patrones relacionados.

### 4.4.2. Tipos de patrones:
De arquitectura (p. ej: MVC)
De diseño
De creación de objetos
De estructura de clases
De comportamiento
De dialectos
De interacción o interfaz de usuario
De análisis
De dominio

### 4.4.3. Ejemplo de patrón: el patrón Singleton

Ejemplo de patrón: el patrón Singleton
Algunos recursos en una aplicación son de tal naturaleza que sólo puede existir una instancia de ese tipo de recurso. Por ejemplo, la conexión a la base de datos a través de un manejador de base de datos. A veces interesa compartir un manejador de base de datos para que el resto de recursos no tengan que conectarse y desconectarse continuamente de la BD, y sólo debería existir una instancia de ese manejador.
El patrón Singleton cubre esta necesidad. Un objeto es “singleton” si la aplicación puede generar una y sólo una instancia del mismo. 

<?php
require_once("DB.php");

class DatabaseConnection
{
  public static function get()
  {
    static $db = null;
    if ( $db == null )
      $db = new DatabaseConnection();
    return $db;
  }
  
  private $_handle = null;

  private function __construct()
  {
    $dsn = 'mysql://root:password@localhost/photos';
    $this->_handle =& DB::Connect( $dsn, array() );
  }
  
  public function handle()
  {
    return $this->_handle;
  }
}

print( "Handle = ".DatabaseConnection::get()->handle()."\n" );
print( "Handle = ".DatabaseConnection::get()->handle()."\n" );
?>

## 4.5. El patrón MVC en la práctica

Mostrar lista de artículos de un blog

### 4.5.1. Código monolítico

<?
  $db = new mysqli('localhost', 'usuario', 'clave', 'dbname');
  $resultado=$db->query('SELECT fecha, titulo FROM articulo');
?>
<h1>Listado de Artículos</h1>
<table>
     <tr> <th>Fecha</th> <th>Titulo</th> </tr>
<?php
  while ($fila = $resultado->fetch_array())  {
      echo "<tr>";
      echo "<td> ".$fila['fecha']." </td>";
      echo "<td> ".$fila['titulo']." </td>";
      echo "</tr>";
  }
  echo "</table>";
  $db->close();
?>

### 4.5.2. Primera mejora: controlador + vista

Dividir el código en:
Un controlador.
Una vista.

<?
  // Este es el controlador (esta aplicación solo realiza una acción)

  $db = new mysqli('localhost', 'usuario', 'clave', 'dbname');
  $resultado=$db->query('SELECT fecha, titulo FROM articulo');

  $articulos = array();
  while ($fila = $resultado->fetch_array())  {
      $articulos[] = $fila;
  }

  $db->close();
?>





include('vista.php');
?>

<!-- Esta es la vista -->

<h1>Listado de Articulos</h1>
<table>
     <tr> <th>Fecha</th> <th>Titulo</th> </tr>
<?php foreach($articulos as $articulo): ?>
    <tr>
        <td><?php echo $articulo['fecha']?></td>
        <td><?php echo $articulo['titulo']?></td>
    </tr>
<?php endforeach;?>
</table>

### 4.5.3. Segunda mejora: modelo, vista y controlador

Dividir el código en:
Un controlador.
Una vista.
Un modelo.

// Este es el controlador (solo realiza una acción)

include('articulos.php');	// En este archivo estará el modelo
$articulos = Articulos::getAllArticulos();

require('vista.php');		// En este archivo estará la vista




<?php
class Articulos {
  public function getArticulos()
  {
    $db = new mysqli('localhost', 'usuario', 'clave', 'dbname');
    $resultado=$db->query('SELECT fecha, titulo FROM articulo');

    $articulos = array();
    while ($fila = $resultado->fetch_array())  {
        $articulos[] = $fila;
    }

    $db->close();

    return $articulos;
  }
}
?>





<h1>Listado de Articulos</h1>
<table>
     <tr> <th>Fecha</th> <th>Titulo</th> </tr>
<?php foreach($articulos as $articulo): ?>
    <tr>
        <td><?php echo $articulo['fecha']?></td>
        <td><?php echo $articulo['titulo']?></td>
    </tr>
<?php endforeach;?>
</table>


### 4.5.4. Tercera mejora: añadiendo capa de abstracción de datos


Dividir el código en:
Un controlador.
Una vista.
Un modelo en dos capas:
Capa de abstracción de datos.
Capa de acceso a datos.



class DbAbstract {
  private $db;
  function crearConexion($servidor, $usuario, $clave, $dbname) {
    $db = new mysqli($servidor, $usuario, $clave, $dbname);
  }

  function cerrarConexion() {
    if ($db) $db->close();
  }

  function consulta($consulta) {
    $res = $db→query($consulta);
    $resArray = array();
    if ($res) {
      $resArray = $res->fetch_all();
    }
    return $resArray;
  }
  ...etc… (añadimos cualquier función que acceda directamente a MySQL)
}




include "DbAbstract.php";

class Articulos {

  public function getAllArticulos() {
    $db = new dbAbstract();
    $db->crearConexion('localhost', 'usuario', 'clave','dbName');
    $articulos = $db->cosulta('SELECT fecha, titulo FROM articulo');
    $db->cerrarConexion();
    return $articulos;
  }

}

### 4.5.5. Cuarta mejora: transformación en clases y objetos reutilizables



Implementar el código siguiendo el paradigma de orientación a objetos.
Crear clase Controlador.
Crear clase Vista.




$controlador = new Controlador();
$controlador->main();






include ("Vista.php");
include ("Articulos.php");

class Controlador {

   public function main() {
      $estado = (isset($_REQUEST['do']) ? $_REQUEST['do'] ; "formLogin");

      switch ($estado) {
         case "formLogin": ...
         case "checkLogin": ...
         case "showAllArticles":
             $articulos = Articulos::getAllArticulos();
             Vista::show("showAllArticles");
             break; 
         case "...etc…": ...
      }
    }
}













<?php

class Vista
{
   public function show($nombreVista) {
      include("header.php");
      include("$nombreVista.php");
      include("footer.php");
   }
}

?>









   <h1>Listado de Articulos</h1>
   <table>
        <tr> <th>Fecha</th> <th>Titulo</th> </tr>
   <?php foreach($articulos as $articulo): ?>
       <tr>
           <td><?php echo $articulo['fecha']?></td>
           <td><?php echo $articulo['titulo']?></td>
       </tr>
   <?php endforeach;?>
   </table>
   <?php
    }
}


include "DbAbstract.php";

class Articulos {

  public function getAllArticulos() {
    $db = new dbAbstract();
    $db->crearConexion('localhost', 'usuario', 'clave','dbName');
    $articulos = $db->cosulta('SELECT fecha, titulo FROM articulo');
    $db->cerrarConexion();
    return $articulos;
  }

}









class DbAbstract {
  private $db;
  function crearConexion($servidor, $usuario, $clave, $dbname) {
    $db = new mysqli($servidor, $usuario, $clave, $dbname);
  }

  function cerrarConexion() {
    if ($db) $db->close();
  }

  function consulta($consulta) {
    $res = $db→query($consulta);
    $resArray = array();
    if ($res) {
      $resArray = $res->fetch_all();
    }
    return $resArray;
  }
  ...etc… (añadimos cualquier función que acceda directamente a MySQL)
}




