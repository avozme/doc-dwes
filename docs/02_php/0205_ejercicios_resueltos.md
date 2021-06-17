---
layout: page
title: 2.5 Ejercicios resueltos
permalink: /php/ejercicios-resueltos
nav_order: 5
has_children: false
parent: 2 Introducción a PHP
grand_parent: Desarrollo Web en Entorno Servidor
---


## 2.5. Ejercicios resueltos de PHP
{: .no_toc }

- TOC
{:toc}

En esta sección vamos a mostrar algunos ejemplos sencillos de aplicaciones web muy, muy básicas programadas con PHP. La última de ellas incluye un acceso a una base de datos.

Mira con detenimiento el código y asegúrate de entenderlo. Para empezar a programar con PHP, no hay nada mejor que echar un vistazo a algunos programas fáciles que luego puedas utilizar como plantilla para los tuyos.

### 2.5.1. Tabla de multiplicar

Vamos a escribir un programa en PHP que pida un número al usuario y muestre su tabla de multiplicar hasta el 25 en una tabla HTML de 5 por 5 casillas.

En la siguiente solución utilizaremos un solo archivo para implementar tanto el formulario HTML como la recogida de datos del formulario más el cálculo de la tabla de multiplicar. Observa como se usa la función isset() para averiguar si estamos enviando los datos del formulario o si, por el contrario, acabamos de lanzar la aplicación y tenemos que mostrar ese formulario al usuario.

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <title></title>
  </head>
  <body>

	<?php
	if (!isset($_REQUEST["numero"])) {
		// Si no tenemos un número pasado por GET, mostramos el formulario
		echo "<form action='03-tabla2.php' method='GET'>
		Introduce un número:
		<input type='text' name='numero'>
		<br>
		<input type='submit'>
		</form>";
	}
	else {
		// Ya tenemos número pasado por GET. Vamos a procesarlo.
		$n = $_REQUEST["numero"];
		echo "<table border='1'>";
		echo "<tr><td colspan='5'>Tabla de multiplicar del número $n</td></tr>";
		echo "<tr>";
		for ($i = 1; $i <= 25; $i++) {
			if (($i-1) % 5 == 0) echo "</tr><tr>";
			echo "<td>$n x $i = " . $n * $i . "</td>";
		}
		echo "</tr>";
		echo "</table>";
	}
	?>

  </body>
</html>
```

### 2.5.2. Juego del número secreto

Vamos a escribir una aplicación web en PHP para jugar al número secreto. 

El juego consiste en lo siguiente: el ordenador "pensará" un número al azar entre 1 y 100 y el jugador tendrá que averiguarlo. Cada vez que el jugador haga un intento, la aplicación le indicará si el número secreto es mayor o menor que el número introducido. 

Cuando el jugador por fin acierte, la aplicación le dará la enhorabuena y le indicará cuántos intentos ha necesitado para averiguar el número secreto.

Vamos a ver dos soluciones para este programa. En la primera, utilizaremos variables de la URL para mantener vivos los datos del programa. En la segunda, utilizaremos variables de sesión para lograr el mismo efecto de forma mucho más limpia.

#### Juego del número secreto: solución sin variables de sesión

Este juego necesita que algunas variables, como el número secreto (variable $aleatorio) o el número de intentos (variable $intentos) persistan entre una solicitud al servidor y la siguiente.

Para lograrlo, haremos que el script se envíe a sí mismo el valor de esas variables. Es una solución poco elegante que se dejó de usar hace años, pero que ilustra perfectamente cuál es el primer problema al que nos enfrentamos al desarrollar aplicaciones web: que se ejecutan en el servidor "a tirones", un trozo cada vez, y para el servidor cada uno de esos trozos es un programa independiente, aunque el usuario tenga la sensación de que forman una aplicación coherente. 

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <title></title>
  </head>
  <body>

	<?php
		if (!isset($_REQUEST["numero"])) {
			if (!isset($_REQUEST["aleatorio"])) {
				$intentos = 0;
				$aleatorio = rand(1,100);
			} else {
				$aleatorio = $_REQUEST["aleatorio"];
				$intentos = $_REQUEST["intentos"];
			}
			echo "<form action='05-numero-secreto.php' method='get'>
				Adivina mi número:
				<input type='text' name='numero'><br>
				<input type='hidden' name='aleatorio' value='$aleatorio'>
				<input type='hidden' name='intentos' value='$intentos'>
				<br>				
				<input type='submit'>
				</form>";
		} else {
			$n = $_REQUEST["numero"];
			$aleatorio = $_REQUEST["aleatorio"];
			$intentos = $_REQUEST["intentos"];
			$intentos++;
			echo "Tu número es: $n<br>";
			if ($n > $aleatorio) {
				echo "Mi número es MENOR";
			}
			else if ($n < $aleatorio) {
				echo "Mi número es MAYOR";
			}
			else {
				echo "<p>ENHORABUENA, HAS ACERTADO</p>";
				echo "Has necesitado $intentos intentos";
			}
			echo "<br><a href='05-numero-secreto.php?aleatorio=$aleatorio&intentos=$intentos'>Sigue jugando...</a>";
		}

	?>
```

#### Juego del número secreto: solución con variables de sesión

En esta solución, se ha sustituido la chapuza de las variables pasadas por URL por **variables de sesión**.

Aunque las veremos con más detalle en el siguiente tema, te puedo adelantar que las variables de sesión permiten almacenar datos persistentes entre sucesivas ejecuciones de scripts desde el mismo cliente.

Es decir, el servidor **recuerda** el valor de determinadas variables para que ese programa ejecutado a tirones se comporte como un todo unificado de cara al usuario.

Observa detenidamente cómo se usan las variables de sesión con PHP mediante el array global $_SESSION.

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <title></title>
  </head>
  <body>

	<?php
		session_start();

		if (!isset($_REQUEST["numero"])) {
			if (!isset($_REQUEST["aleatorio"])) {
				$_SESSION["intentos"] = 0;
				$_SESSION["aleatorio"] = rand(1,100);
			} else {
				$aleatorio = $_SESSION["aleatorio"];
				$intentos = $_SESSION["intentos"];
			}
			echo "<form action='05-numero-secreto-v2.php' method='get'>
				Adivina mi número:
				<input type='text' name='numero'><br>
				<br>				
				<input type='submit'>
				</form>";
		} else {
			$n = $_REQUEST["numero"];
			$aleatorio = $_SESSION["aleatorio"];
			$intentos = $_SESSION["intentos"];
			$intentos++;
			echo "Tu número es: $n<br>";
			if ($n > $aleatorio) {
				echo "Mi número es MENOR";
				echo "<br><a href='05-numero-secreto-v2.php'>Sigue jugando...</a>";
			}
			else if ($n < $aleatorio) {
				echo "Mi número es MAYOR";
				echo "<br><a href='05-numero-secreto-v2.php'>Sigue jugando...</a>";
			}
			else {
				echo "<p>ENHORABUENA, HAS ACERTADO</p>";
				echo "Has necesitado $intentos intentos";
				$intentos = 0;
				unset($_SESSION["aleatorio"]);
				echo "<br><a href='05-numero-secreto-v2.php'>Jugar de nuevo</a>";
			}
			$_SESSION["intentos"] = $intentos;
		}

	?>
</body>
</html>
```

### 2.5.3. Biblioteca

Este es un ejemplo muy importante por dos razones:

1. Porque es nuestra primera aplicación web "de verdad", con una base de datos detrás
2. Porque volveremos sobre ella varias veces para hacerle sucesivas mejoras, hasta dejarla presentable.

Se trata de escribir una aplicación web en PHP que gestione (de forma muy simplificada) una biblioteca.

La aplicación trabajará con una base de datos compuesta de solo dos tablas (ya te dije que estaría muy simplificada): libros y autores.

Esta aplicación nos permitirá, en principio, ver la lista de todos los libros disponibles, así como dar de alta libros nuevos y modificar o borrar los libros existentes. 

De momento no trabajaremos con los autores, pero sería fácil extenderla para que también nos dejase hacer altas, bajas y modificaciones de los autores.

Lee este código con especial atención (aunque sea un poco largo), y observa como utilizamos una variable muy especial llamada $action para saber qué tiene que hacer la aplicación en cada momento. Esa variable es el germen de la arquitectura modelo-vista-controlador con la que trabajaremos una y otra vez más adelante.

```php
<!-- BIBLIOTECA VERSIÓN 1
     Características de esta versión:
       - Código monolítico (sin arquitectura MVC)
       - Sin seguridad
       - Sin sesiones ni control de acceso
       - Sin reutilización de código
-->


<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html lang="es" xmlns="http://www.w3.org/1999/xhtml">

<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
</head>

<body>
    <?php

    $db = new mysqli("localhost:3386", "root", "bitnami", "biblioteca");

    if (isset($_REQUEST["action"])) {
        $action = $_REQUEST["action"];
    } else {
        $action = "mostrarListaLibros";  // Acción por defecto
    }

    switch ($action) {

            // --------------------------------- MOSTRAR LISTA DE LIBROS ----------------------------------------

        case "mostrarListaLibros":
            echo "<h1>Biblioteca</h1>";

            // Buscamos todos los libros de la biblioteca
            if ($result = $db->query("SELECT * FROM libros
                                        INNER JOIN escriben ON libros.idLibro = escriben.idLibro
                                        INNER JOIN personas ON escriben.idPersona = personas.idPersona
                                        ORDER BY libros.titulo")) {

                // La consulta se ha ejecutado con éxito. Vamos a ver si contiene registros
                if ($result->num_rows != 0) {
                    // La consulta ha devuelto registros: vamos a mostrarlos

                    // Primero, el formulario de búsqueda
                    echo "<form action='index.php'>
                                <input type='hidden' name='action' value='buscarLibros'>
                                <input type='text' name='textoBusqueda'>
                                <input type='submit' value='Buscar'>
                                </form><br>";

                    // Ahora, la tabla con los datos de los libros
                    echo "<table border ='1'>";
                    while ($fila = $result->fetch_object()) {
                        echo "<tr>";
                        echo "<td>" . $fila->titulo . "</td>";
                        echo "<td>" . $fila->genero . "</td>";
                        echo "<td>" . $fila->numPaginas . "</td>";
                        echo "<td>" . $fila->nombre . "</td>";
                        echo "<td>" . $fila->apellido . "</td>";
                        echo "<td><a href='index.php?action=formularioModificarLibro&idLibro=" . $fila->idLibro . "'>Modificar</a></td>";
                        echo "<td><a href='index.php?action=borrarLibro&idLibro=" . $fila->idLibro . "'>Borrar</a></td>";
                        echo "</tr>";
                    }
                    echo "</table>";
                } else {
                    // La consulta no contiene registros
                    echo "No se encontraron datos";
                }
            } else {
                // La consulta ha fallado
                echo "Error al tratar de recuperar los datos de la base de datos. Por favor, inténtelo más tarde";
            }
            echo "<p><a href='index.php?action=formularioInsertarLibros'>Nuevo</a></p>";
            break;

            // --------------------------------- FORMULARIO ALTA DE LIBROS ----------------------------------------

        case "formularioInsertarLibros":
            echo "<h1>Modificación de libros</h1>";

            // Creamos el formulario con los campos del libro
            echo "<form action = 'index.php' method = 'get'>
                    Título:<input type='text' name='titulo'><br>
                    Género:<input type='text' name='genero'><br>
                    País:<input type='text' name='pais'><br>
                    Año:<input type='text' name='ano'><br>
                    Número de páginas:<input type='text' name='numPaginas'><br>";

            // Añadimos un selector para el id del autor o autores
            $result = $db->query("SELECT * FROM personas");
            echo "Autores: <select name='autor[]' multiple='true'>";
            while ($fila = $result->fetch_object()) {
                echo "<option value='" . $fila->idPersona . "'>" . $fila->nombre . " " . $fila->apellido . "</option>";
            }
            echo "</select>";
            echo "<a href='index.php?action=formularioInsertarAutores'>Añadir nuevo</a><br>";

            // Finalizamos el formulario
            echo "  <input type='hidden' name='action' value='insertarLibro'>
					<input type='submit'>
				</form>";
            echo "<p><a href='index.php'>Volver</a></p>";

            break;

            // --------------------------------- INSERTAR LIBROS ----------------------------------------

        case "insertarLibro":
            echo "<h1>Alta de libros</h1>";

            // Vamos a procesar el formulario de alta de libros
            // Primero, recuperamos todos los datos del formulario
            $titulo = $_REQUEST["titulo"];
            $genero = $_REQUEST["genero"];
            $pais = $_REQUEST["pais"];
            $ano = $_REQUEST["ano"];
            $numPaginas = $_REQUEST["numPaginas"];
            $autores = $_REQUEST["autor"];

            // Lanzamos el INSERT contra la BD.
            echo "INSERT INTO libros (titulo,genero,pais,ano,numPaginas) VALUES ('$titulo','$genero', '$pais', '$ano', '$numPaginas')";
            $db->query("INSERT INTO libros (titulo,genero,pais,ano,numPaginas) VALUES ('$titulo','$genero', '$pais', '$ano', '$numPaginas')");
            if ($db->affected_rows == 1) {
                // Si la inserción del libro ha funcionado, continuamos insertando en la tabla "escriben"
                // Tenemos que averiguar qué idLibro se ha asignado al libro que acabamos de insertar
                $result = $db->query("SELECT MAX(idLibro) AS ultimoIdLibro FROM libros");
                $idLibro = $result->fetch_object()->ultimoIdLibro;
                // Ya podemos insertar todos los autores junto con el libro en "escriben"
                foreach ($autores as $idAutor) {
                    $db->query("INSERT INTO escriben(idLibro, idPersona) VALUES('$idLibro', '$idAutor')");
                }
                echo "Libro insertado con éxito";
            } else {
                // Si la inserción del libro ha fallado, mostramos mensaje de error
                echo "Ha ocurrido un error al insertar el libro. Por favor, inténtelo más tarde.";
            }
            echo "<p><a href='index.php'>Volver</a></p>";

            break;

            // --------------------------------- BORRAR LIBROS ----------------------------------------

        case "borrarLibro":
            echo "<h1>Borrar libros</h1>";

            // Recuperamos el id del libro y lanzamos el DELETE contra la BD
            $idLibro = $_REQUEST["idLibro"];
            $db->query("DELETE FROM libros WHERE idLibro = '$idLibro'");

            // Mostramos mensaje con el resultado de la operación
            if ($db->affected_rows == 0) {
                echo "Ha ocurrido un error al borrar el libro. Por favor, inténtelo de nuevo";
            } else {
                echo "Libro borrado con éxito";
            }
            echo "<p><a href='index.php'>Volver</a></p>";

            break;

            // --------------------------------- FORMULARIO MODIFICAR LIBROS ----------------------------------------

        case "formularioModificarLibro":
            echo "<h1>Modificación de libros</h1>";

            // Recuperamos el id del libro que vamos a modificar y sacamos el resto de sus datos de la BD
            $idLibro = $_REQUEST["idLibro"];
            $result = $db->query("SELECT * FROM libros WHERE libros.idLibro = '$idLibro'");
            $libro = $result->fetch_object();

            // Creamos el formulario con los campos del libro
            // y lo rellenamos con los datos que hemos recuperado de la BD
            echo "<form action = 'index.php' method = 'get'>
				    <input type='hidden' name='idLibro' value='$idLibro'>
                    Título:<input type='text' name='titulo' value='$libro->titulo'><br>
                    Género:<input type='text' name='genero' value='$libro->genero'><br>
                    País:<input type='text' name='pais' value='$libro->pais'><br>
                    Año:<input type='text' name='ano' value='$libro->ano'><br>
                    Número de páginas:<input type='text' name='numPaginas' value='$libro->numPaginas'><br>";

            // Vamos a añadir un selector para el id del autor o autores.
            // Para que salgan preseleccionados los autores del libro que estamos modificando, vamos a buscar
            // también a esos autores.
            $todosLosAutores = $db->query("SELECT * FROM personas");  // Obtener todos los autores
            $autoresLibro = $db->query("SELECT idPersona FROM escriben WHERE idLibro = '$idLibro'");             // Obtener solo los autores del libro que estamos buscando
            // Vamos a convertir esa lista de autores del libro en un array de ids de personas
            $listaAutoresLibro = array();
            while ($autor = $autoresLibro->fetch_object()) {
                $listaAutoresLibro[] = $autor->idPersona;
            }

            // Ya tenemos todos los datos para añadir el selector de autores al formulario
            echo "Autores: <select name='autor[]' multiple size='3'>";
            while ($fila = $todosLosAutores->fetch_object()) {
                if (in_array($fila->idPersona, $listaAutoresLibro))
                    echo "<option value='$fila->idPersona' selected>$fila->nombre $fila->apellido</option>";
                else
                    echo "<option value='$fila->idPersona'>$fila->nombre $fila->apellido</option>";
            }
            echo "</select>";

            // Por último, un enlace para crear un nuevo autor
            echo "<a href='index.php?action=formularioInsertarAutores'>Añadir nuevo</a><br>";

            // Finalizamos el formulario
            echo "  <input type='hidden' name='action' value='modificarLibro'>
                    <input type='submit'>
                  </form>";
            echo "<p><a href='index.php'>Volver</a></p>";

            break;

            // --------------------------------- MODIFICAR LIBROS ----------------------------------------

        case "modificarLibro":
            echo "<h1>Modificación de libros</h1>";

            // Vamos a procesar el formulario de modificación de libros
            // Primero, recuperamos todos los datos del formulario
            $idLibro = $_REQUEST["idLibro"];
            $titulo = $_REQUEST["titulo"];
            $genero = $_REQUEST["genero"];
            $pais = $_REQUEST["pais"];
            $ano = $_REQUEST["ano"];
            $numPaginas = $_REQUEST["numPaginas"];
            $autores = $_REQUEST["autor"];

            // Lanzamos el UPDATE contra la base de datos.
            $db->query("UPDATE libros SET
							titulo = '$titulo',
							genero = '$genero',
							pais = '$pais',
							ano = '$ano',
							numPaginas = '$numPaginas'
							WHERE idLibro = '$idLibro'");

            if ($db->affected_rows == 1) {
                // Si la modificación del libro ha funcionado, continuamos actualizando la tabla "escriben".
                // Primero borraremos todos los registros del libro actual y luego los insertaremos de nuevo
                $db->query("DELETE FROM escriben WHERE idLibro = '$idLibro'");
                // Ya podemos insertar todos los autores junto con el libro en "escriben"
                foreach ($autores as $idAutor) {
                    $db->query("INSERT INTO escriben(idLibro, idPersona) VALUES('$idLibro', '$idAutor')");
                }
                echo "Libro actualizado con éxito";
            } else {
                // Si la modificación del libro ha fallado, mostramos mensaje de error
                echo "Ha ocurrido un error al modificar el libro. Por favor, inténtelo más tarde.";
            }
            echo "<p><a href='index.php'>Volver</a></p>";
            break;

            // --------------------------------- BUSCAR LIBROS ----------------------------------------

        case "buscarLibros":
            // Recuperamos el texto de búsqueda de la variable de formulario
            $textoBusqueda = $_REQUEST["textoBusqueda"];
            echo "<h1>Resultados de la búsqueda: \"$textoBusqueda\"</h1>";

            // Buscamos los libros de la biblioteca que coincidan con el texto de búsqueda
            if ($result = $db->query("SELECT * FROM libros
					INNER JOIN escriben ON libros.idLibro = escriben.idLibro
					INNER JOIN personas ON escriben.idPersona = personas.idPersona
					WHERE libros.titulo LIKE '%$textoBusqueda%'
					OR libros.genero LIKE '%$textoBusqueda%'
					OR personas.nombre LIKE '%$textoBusqueda%'
					OR personas.apellido LIKE '%$textoBusqueda%'
					ORDER BY libros.titulo")) {

                // La consulta se ha ejecutado con éxito. Vamos a ver si contiene registros
                if ($result->num_rows != 0) {
                    // La consulta ha devuelto registros: vamos a mostrarlos
                    // Primero, el formulario de búsqueda
                    echo "<form action='index.php'>
								<input type='hidden' name='action' value='buscarLibros'>
                            	<input type='text' name='textoBusqueda'>
								<input type='submit' value='Buscar'>
                          </form><br>";
                    // Después, la tabla con los datos
                    echo "<table border ='1'>";
                    while ($fila = $result->fetch_object()) {
                        echo "<tr>";
                        echo "<td>" . $fila->titulo . "</td>";
                        echo "<td>" . $fila->genero . "</td>";
                        echo "<td>" . $fila->numPaginas . "</td>";
                        echo "<td>" . $fila->nombre . "</td>";
                        echo "<td>" . $fila->apellido . "</td>";
                        echo "<td><a href='index.php?action=formularioModificarLibro&idLibro=" . $fila->idLibro . "'>Modificar</a></td>";
                        echo "<td><a href='index.php?action=borrarLibro&idLibro=" . $fila->idLibro . "'>Borrar</a></td>";
                        echo "</tr>";
                    }
                    echo "</table>";
                } else {
                    // La consulta no contiene registros
                    echo "No se encontraron datos";
                }
            } else {
                // La consulta ha fallado
                echo "Error al tratar de recuperar los datos de la base de datos. Por favor, inténtelo más tarde";
            }
            echo "<p><a href='index.php?action=formularioInsertarLibros'>Nuevo</a></p>";
            echo "<p><a href='index.php'>Volver</a></p>";
            break;

            // --------------------------------- ACTION NO ENCONTRADA ----------------------------------------

        default:
            echo "<h1>Error 404: página no encontrada</h1>";
            echo "<a href='index.php'>Volver</a>";
            break;
    } // switch

    ?>

</body>

</html>
```
```
