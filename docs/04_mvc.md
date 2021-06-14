---
layout: page
title: 4 Arquitectura MVC
permalink: /mvc/
nav_order: 4
has_children: false
parent: Desarrollo Web en Entorno Servidor
---
# 4. Arquitectura MVC

## 4.1 Arquitecturas FÍSICAS multinivel (multitier)

Arquitectura en 2 niveles:

XXX esquema

Arquitectura en 3 niveles:

XXX esquema

## 4.2 Arquitecturas LÓGICAS multicapa (multilayer)

Ventajas:
Desarrollos paralelos en cada capa
Aplicaciones robustas (encapsulamiento)
Matenimiento más sencillo
Más flexibilidad para añadir módulos
Más escalabilidad para aumentar rendimiento

### 4.2.1. Esquema Modelo-Vista-Controlador (MVC)

XXX esquema

Arquitectura en 3 capas
Es una generalización del patrón MVC.

XXX esquema

Hay que decidir qué componentes hay, sus funciones, y en qué capa y qué nivel físico encaja cada uno.

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




