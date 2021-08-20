---
layout: page
title: 8 Otras tecnologías
permalink: /otras-tecnologias/
parent: Desarrollo Web en Entorno Servidor
nav_order: 8
---
# 8. Otras tecnologías

En esta sección vamos a hacer un repaso rápido a otros lenguajes para desarrollo web del lado del servidor diferentes de PHP.

Será solo una pasada superficial, para que te hagas una idea de qué aspecto tienen estos lenguajes y veas que, en lo sustancial, no difieren mucho unos de otros. Esto quiere decir que, si te manejas bien con PHP, podrás pasarte a cualquiera de estos lenguajes con muy poco esfuerzo y en solo unos días.

## 8.1. Common Gateway Interface (CGI)

CGI es la solución más antigua para el desarrollo web en el lado del servidor.

En la década de 1990, cuando se empezó a pensar en la posibilidad de crear página dinámicas generadas por el servidor a partir de los recursos del mismo (típicamente, una base de datos), los primeros intentos utilizaron las tecnologías presentes en ese momento en los servidores web.

Todos los servidores tenían un compilador de C/C++, así que alguien pensó: ¿por qué no escribimos las aplicaciones web en C/C++, las compilamos y hacemos que el ejecutable se pueda invocar vía web?

Para lograr esto último, se utilizó CGI (Common Gateway Interface).

CGI es una interfaz entre los servidores web y las aplicaciones que se ejecutan en el servidor. Estas aplicaciones pueden estar construidas en cualquier lenguaje (no solo C/C++). A CGI, eso le da igual. Solo define la forma de transferir información en ambos sentidos.

La figura siguiente muestra la forma en la que se ejecutan programas en el servidor a través de CGI. Si lo observas con atención, verás que no difiere demasiado de la forma en la que trabaja PHP, porque cualquier petición tiene 4 pasos:
1. Se recibe la petición de un cliente web.
2. El servidor web recibe la peticion y, a través del interfaz CGI, le pide al sistema operativo que ejecute el programa correspondiente.
3. La salida del programa se redirige al servidor web. De esto se encarga, nuevamente, el interfaz CGI.
4. El servidor devuelve al cliente el resultado de la ejecución del programa.

XXX esquema

### 8.1.1. Entonces, ¿en qué se diferencia CGI de PHP?

Lo primero, CGI no es un lenguaje de programación. Eso ya lo hemos dicho. Es un ***interfaz*** entre el servidor web y el sistema operativo para poder ejecutar cualquier programa escrito en cualquier lenguaje a través de la web.

Puede parecer una solución perfecta, ¿verdad? Pero, si fuera así, ¿por qué no se sigue usando de forma masiva? ¿Por qué se abandonó en favor de PHP u otros de los lenguajes que vamos a ver más adelante?

La respuesta breve es: CGI tiene un serio problema de rendimiento.

Cada vez que se recibe una petición de un cliente, se crea un nuevo proceso en el servidor para ejecutar el programa en cuestión. Este proceso necesita un espacio de memoria para colocar su código fuente y sus datos, y esto recursos solo se liberan cuando el servidor termina de responder al cliente. Esta creación de procesos independientes implica una carga importante para el servidor, por lo cual esta modalidad de generación de contenido dinámico no es muy escalable.

Por su parte, PHP (y otras soluciones que veremos más adelante) no crean un proceso independiente para cada petición recibida, sino que un mismo macro-proceso se encarga de gestionarlas todas. En términos de escalabilidad, esta opción es mucho mejor. Así que, cuando los servidores empezaron a recibir muchas visitas simultáneas, CGI comenzó a abandonarse. Sencillamente, ningún servidor podía soportar grandes volúmenes de peticiones.

Existen algunas alternativas para solucionar este problema de CGI, como mantener un sólo proceso CGI en memoria que se encargue de procesar todas las peticiones (técnica conocida como FastCGI y que, de hecho, se sigue utilizando en la actualidad, incluso para ejecutar PHP en el servidor), pero resulta más complejo de configurar y operar, e implica algunos problemas de seguridad. En cualquier caso, estos detalles de configuración del servidor son cosas que competen más a los administradores de sistemas que a los desarrolladores.


## 8.2. Perl

A partir de este punto, veremos varios lenguajes alternativos a PHP (es decir, su "competencia") siguiendo siempre el mismo esquema:
* Primero, enumeraremos las características y filosofia del lenguaje.
* Luego explicaremos a grandes rasgos cómo hay que configurar el servidor para poder usar ese lenguaje para desarrollo web.
* Después mostraremos la sintaxis básica del lenguaje.
* Por último, escribiremos dos ejemplos completos en cada lenguaje: un sencillo "hola, mundo" y un programa algo más complejo que lanza una validación de login mediante ajax. En este segundo caso, la parte del cliente será siempre la misma, y solo cambiaremos la parte del servidor. Eso te permitirá apreciar las diferencias entre unos lenguajes y otros. Enseguida te darás cuenta de que esas diferencias son mínimas.

### 8.2.1. Características del lenguaje Perl

Fecha de aparición: 1987.

Perspectivas: 
* Uso decreciente. 
* Apto para tareas pequeñas y rápidas. 
* Cuenta con desarrolladores muy fieles y experimentados. Documentación muy extensa.
* Soporte amplio en cualquier servidor.

Filosofía de Perl:
* Versión mejorada del shell scripting de Unix.
* Pensado para procesamiento rápido de archivos de texto y automatización de tareas de administración del sistema.
* Favorece la programación ágil, rápida y sucia de scripts. 
* Énfasis en las expresiones regulares.
* Multiparadigma.
* En combinación con CGI, se popularizó para aplicaciones web antes de la aparición de PHP.

### 8.2.2. Configuración necesaria en el servidor

Para utilizar Perl en un servidor Apache o similar, necesitaremos:

1. Instalar el intérprete Perl (usr/bin/perl).
2. Activar los módulos perl y/o cgi de Apache y configurar el handler para CGI.
3. Instalar módulos Perl adicionales para acceso a bases de datos, etc.

Se puede ejecutar el intérprete Perl de forma nativa en Apache, o bien hacerlo a través de CGI. Lo primero es más difícil de configurar y raramente se encuentra en hostings web compartidos.

### 8.2.3. Sintaxis básica de Perl

Las variables en Perl no se declaran, tienen tipado dinámico y son globales por defecto.

```perl
$var = valor;
print "La variable var vale $variable";
```

Algunos operadores:

* Comparación: lt, gt, le, ge, eq, ne... 
* Asignación: =

Algunas estructuras de control:

```perl
while (condicion) {
  Acciones
}


if (condicion) {
  Acciones-1
}
else {
  Acciones-2
}
```

### 8.2.4. Entrada / salida

Entrada de datos estándar:

```perl
chop ( $variable = <STDIN> );
```

Lectura de datos desde un formulario HTML:

```perl
use CGI;
my $cgi = CGI->new;
my $username = $cgi->param("username");
```

Salida:

```perl
print "cadena $variable cadena..."; 
```

### 8.2.5. Bibliotecas, funciones y clases

Para utilizar una biblioteca o ***package***, como se denominan en Perl, se emplea la palabra **use**:

```perl
use nombre-biblioteca;
```

Las bibliotecas se empaquetan en archivos con extensión .pm (***Perl Modules***). Dentro de ellas, puede haber una colección de funciones o métodos que se declaran así:

```perl
package nombre-biblioteca;

Sub nombre-funcion (argumentos) {
   Acciones
}
```

Estas funciones pueden usarse desde fuera de la biblioteca con esta sintaxis:

```perl
use nombre-biblioteca;

nombre-biblioteca::nombre-funcion(argumentos);
```

Los ***packages*** también pueden usarse para construir clases (o algo parecido) de las que luego se pueden instanciar objetos. Más o menos así:

```perl
  package nombre-de-la-clase;

  sub new {
      # Este es el método constructor
      my $self = {};      # Array para los atributos
      $self->{VAR1} = 0;  # Un atributo
      $self->{VAR2} = 9;  # Otro atributo
  }

  sub otro-método{
       # Aquí van el resto de métodos de la clase
  }
  sub DESTROY {
       # Método destructor
  }
  1    # Para que el intérprete Perl no se queje al interpretar este archivo
```

Como puedes observar, Perl está lleno de peculiaridades que muchos consideran anticuadas o, como mínimo, poco elegantes. Observa si no la forma que tiene de crear los atributos de instancia, los caprichosos nombres de los métodos (a veces en minúscula, a veces en mayúscula) o la necesidad de terminar el ***package*** con un 1 para que el intérprete Perl lo considere un script válido.

Por último, para instanciar un objeto de esta clase:

```perl
use nombre-de-la-clase;
$objeto = nombre-de-la-clase->new();
```

### 8.2.6. Ejemplo 1 en Perl: Hola mundo

```perl
#!/usr/bin/perl
print "Content-type: text/html\n\n";
print "<html><title>Hola mundo</title><body>";
print "Hola, mundo";
print "</body></html>";
```

### 8.2.7. Ejemplo 2 en Perl: login con comprobación de email por Ajax

Este segundo ejemplo, como hemos explicado más arriba, consistirá en un formulario de login que comprobará el nombre de usuario y la contraseña mediante una petición Ajax.

#### Formulario HTML

El formulario de login es un simple código HTML que será idéntico en todos los ejemplos que veremos en el resto de este capítulo, así que solo lo mostraremos aquí por primera vez.

```html
<form id="loginForm" name="loginForm" method="post" action="">
  <fieldset>
    <p>
      <label for="username">Nombre de usuario</label>
      <br />
      <input type="text" id="username" name="username" class="text" size="20" />
    </p>
    <p>
      <label for="password">Contraseña</label>
      <br />
      <input type="password" id="password" name="password" class="text" size="20" />
    </p>
    <p>
      <button type="submit">Login</button>
    </p>
  </fieldset>
</form>
```

#### Script jQuery

El script que lanza la petición Ajax (cuyo código puede ir en el mismo archivo que el formulario) será ***casi*** idéntico en todos los ejemplos: solo cambiará el nombre del script al que se lanza la petición.

En nuestro caso actual, es script lo hemos llamado **login.pl** (la extensión .pl denota que se trata de un script escrito en lenguaje Perl). Como es lógico, en ejemplos posteriores, tendrías que cambiar el nombre de ese archivo por el que corresponda (login.py si estamos usando Python, login.rb si estamos usando Ruby, etc).

Para no repetirnos innecesariamente, no volveremos a mostrar tampoco el código de este script en los ejemplos sucesivos.

Observa que Javascript está esperando que el servidor responda con un JSON que puede llevar estos tres datos en su interior:
* data.error: Un string con un texto de error en caso de que el usuario o la contraseña sean incorrectos.
* data.success: Un string con un texto de éxito en caso de que el usuario y la contraseña sean correctos.
* data.userId: Un entero con el ID del usuario logueado (solo en caso de éxito).

```javascript
$(document).ready(function(){
  $("form#loginForm").submit(function() { 
    var username = $('#username').attr('value'); // Obtenemos el username
    var password = $('#password').attr('value'); // Obtenemos la password

    if (username && password) { // Los valores de username y password no están vacíos
      $.ajax({
        type: "GET",
        url: "login.pl", 
        dataType: "json",
        data: "username=" + username + "&password=" + password,
        success: function(data){
          if (data.error) { // El servidor ha devuelto un error de login
            $('div#loginResult').text("data.error: " + data.error);
            $('div#loginResult').addClass("error");
          } 
          else {            // El servidor ha hecho el login correctamente
            $('form#loginForm').hide();
            $('div#loginResult').text("data.success: " + data.success 
              + ", data.userid: " + data.userid);
            $('div#loginResult').addClass("success");
          } 
        } 
      }); 
    } 
    else {
      $('div#loginResult').text("Debe escribir su nombre de usuario y su contraseña");
      $('div#loginResult').addClass("error");
    } 
    $('div#loginResult').fadeIn();
    return false;
  });
});
```

#### Script Perl en el lado del servidor (login.pl)

Este sería el script en Perl que respondería a la petición Ajax anterior.

Observa que, a pesar de la peculiar sintaxis de Perl, la estructura del algoritmo es idéntica a la que usaríamos si lo escribiéramos en PHP:
1. Recuperamos los datos del formulario (username y password)
2. Conectamos con la base de datos
3. Lanzamos la consulta contra la tabla de usuarios
4. En función del resultado de la consulta, preparamos nuestro JSON de respuesta al cliente
5. Devolvemos el JSON al cliente

```perl
#!/usr/bin/perl -T
use CGI;
use DBI;
use strict;
use warnings;

# read the CGI params
my $cgi = CGI->new;
my $username = $cgi->param("username");
my $password = $cgi->param("password");

# connect to the database
my $dbh = DBI->connect("DBI:mysql:database=mydb;host=localhost;port=2009",  
  "mydbusername", "mydbpassword") 
  or die $DBI::errstr;

# check the username and password in the database
my $statement = qq{SELECT id FROM users WHERE username=? and password=?};
my $sth = $dbh->prepare($statement)
  or die $dbh->errstr;
$sth->execute($username, $password)
  or die $sth->errstr;
my ($userID) = $sth->fetchrow_array;

# create a JSON string according to the database result
my $json = ($userID) ? 
  qq{{"success" : "login is successful", "userid" : "$userID"}} : 
  qq{{"error" : "username or password is wrong"}};

# return JSON string
print $cgi->header(-type => "application/json", -charset => "utf-8");
print $json;
```



## 8.3. Python

### 8.3.1. Características del lenguaje Python

Fecha de aparición: 1991

Perspectivas: 

* Uso creciente. 
* Es el sustituto natural de Perl para el desarrollo rápido de scripts. 
* También usado en grandes proyectos como alternativa a PHP.
* Menos extendido que PHP, pero comunidad con muchos desarrolladores profesionales (mejor relación señal/ruido)
* Muchas bibliotecas de terceros → flexibilidad

Filosofía:

* Es la versión “limpia” de Perl. Pensado para escribir scripts de forma rápida y limpia.
* Énfasis en la legibilidad: Python es casi pseudocódigo (código “pythonico” → v. “El Zen de Python”)
* Interpretado. Tipado dinámico. Fuertemente tipado.
* Expresiones regulares heredadas de Perl.
* Multiparadigma: imperativo, O.O., funcional.

### 8.3.2. Configuración necesaria en el servidor

Para hacer funcionar Python en un servidor Apache o similar, es necesario:

1. Instalar el intérprete Python (/usr/bin/python). El más extendido es CPhyton.
2. Activar los módulos python y/o cgi de Apache y configurar el handler de Apache para CGI.
3. Instalar módulos adicionales (p. ej: para acceso a bases de datos) si es necesario.

Python puede funcionar de forma nativa integrado en Apache o a través de CGI. Lo primero es más rápido; lo segundo, más frecuente.


### 8.3.3. Sintaxis básica de Python

Las variables en Python no se declaran obligatoriamente: tienen tipado dinámico y son locales por defecto.

```python
varariable = valor;
print "La variable var vale %s" (variable);
```

En Python hay muchos tipos de datos complejos predefinidos: listas, tuplas, diccionarios...

Algunos operadores son:

* Comparación: <, >, <=, >=, ==, != 
* Asignación: =

Y estas son algunas estructuras de control. **¡Cuidado! ¡El código debe indentarse OBLIGATORIAMENTE!** No existen las llaves ({ y }) en Python. ¡La indentación (o sangrado) marca los bloques!

```python
while condicion:
  Acciones

if condicion:
  Acciones-1
else:
  Acciones-2
```

### 8.3.4. Entrada / Salida

La entrada de datos por teclado puede hacerse con raw_input():

```python
variable = raw_input("Texto")
```

Pero a nosotros nos interesa hacer entrada de datos a través de un formulario HTML. Esto se hace así:

```python
import cgi
form = cgi.FieldStorage()
campo = form["campo"].value
```

En cuanto a la salida de datos, se usa ***print*** con cadenas de formato, seguida de una lista de variables. Cada elemento de la cadena de formato marcado con un % se sustituirá por una variable de la lista, en el mismo orden en el que estén escritas. Por ejemplo:

```python
print "cadena %s cadena %s ..." (variable1, variable2) 
```

El símbolo %s significa que en esa posición irá un String. Otras posibilidades son %d (enteros) o %f (float). Esta forma de especificar las cadenas de formato está directamente tomada del lenguaje C.

En Python existen muchas otras formas de hacer una salida de datos, pero ***print*** es lo suficientemente potente como para que puedas utilizarla para cualquier cosa imaginable en una aplicación web.

### 8.3.5. Bibliotecas, funciones y clases

En Python hay tres niveles de agrupación de bibliotecas:

* Módulos: un módulo es un fichero con código Python en su interior. Puede ser una clase o un puñado de funciones sueltas, por ejemplo.
* Paquetes (*packages*): un paquete es un directorio que contiene varios módulos. También puede contener subpaquetes. Los paquetes se instalan y desinstalan con un gestor de paquetes (como *pip*, que viene a ser como *composer* en PHP).
* Bibliotecas (*libraries*): una biblioteca es cualquier fragmento de código reutilizable que se puede incluir en otros proyectos. Las bibliotecas pueden ser paquetes o no. Existe una *Python Standard Library* que contiene todas las funciones básicas de Python y viene preinstalada con el *core* del lenguaje.

Podemos incluir una librería en nuestro proyecto Python usando la palabra *import*:

```python
import mi-librería
```

Como hemos dicho, dentro de cada módulo puede haber clases o subrutinas sueltas. Una subrutina (procedimiento o función) se declara así en Python (observa de nuevo como la indentación o sangrado es fundamental porque marca el comienzo y final de los bloques de código):

```python
def mi-funcion(param1, param2, etc):
    # Aquí va el código de la función
    [return valor1, varlor2...]
```

En cuanto a las clases, la sintaxis para declararlas y muy similar a PHP, Java o C++ (recordando que, en Python, no se usan las llaves sino la indentación):

```python
class MyClass:
    
    un_atributo = valor
    otro_atributo = valor

    # Esto es un constructor
    def __init__(self):
        self.un_atributo = 0
 

    def un_metodo(parámetros):
        return lo_que_sea
```

### 8.3.6. Ejemplo 1 en Python: Hola mundo

```python
#!/usr/bin/python
print "Content-type: text/html\n\n"
print "<html><body>"
print "<h1>Hola, mundo</h1>"
print "</body></html>"
```

### 8.3.7. Ejemplo 2 en Python: login con comprobación de email por Ajax

Repetimos ahora el ejemplo del login con comprobación de usuario y contraseña mediante Ajax, pero no mostraremos de nuevo el código del formulario ni de la llamada Ajax. Para ver ese código, revisa la sección que dedicamos al lenguaje Perl. Allí solo tendrás que cambiar el nombre del script (login.pl) por login.py.

El código de ese script sí que cambia, claro. Esta es la versión del mismo escrita en Python:

```python
#!/usr/bin/python

import cgi
import MySQLdb 

# Capturamos los valores del formulario
form = cgi.FieldStorage()
usuario = form["username"].value;
password = form["password"].value;

print "Usuario = ", usuario, " Pass = ", password

# Lanzamos la consulta contra la base de datos
db=MySQLdb.connect(host='localhost', user='yo-que-sé', passwd='vete-a-saber', db='lo-que-sea')
cursor=db.cursor()
num_rows = cursor.execute("SELECT id FROM users WHERE username = '%s' AND password = '%s';", (usuario, password))
userid = cursor.fetchone()

# return JSON string
print "Content-type: application/json\n"
if num_rows == 0:
   print "{'error': 'Usuario o contrase&ntilde;a incorrectos'}"
else:
   print "{'success': 'El usuario y la contrase&ntilde;a son v&aacute;lidos', 'userid': '%d'", userid
```


## 8.4. .NET

XXX

### 8.4.1. Características de .NET

Fecha de aparición: 1996 (ASP) / 2002 (.NET)

Perspectivas: 

* Alternativa de Microsoft a JSP para desarrollo de grandes proyectos, donde PHP se queda pequeño.
* Componentes exclusivos en el servidor y altas prestaciones. 
* Coste más elevado y problemas de seguridad endémicos.

Filosofía:

* Framework de código cerrado y propietario.
* Tecnología multilenguaje. Suele correr con VBS (Visual Basic Script), pero puede hacerlo con otros. 
* Puede funcionar como PHP, embebido dentro de HTML.
* ASP.Net incluye controles de servidor exclusivos de Microsoft (equivalentes a los ActiveX del lado del cliente)

### 8.4.2. Configuración necesaria en el servidor

Instalar Microsoft IIS (Internet Information Server). Viene de serie en los Windows Server.
Puede ejecutarse con un módulo de apache (mono), pero es mucho más lento.
Cada lenguaje tiene su servidor. Si quieres PHP, usa Apache. Si quieres JSP, usa Tomcat. Si quieres ASP, usa IIS.

### 8.4.3. Sintaxis básica de .NET con VBasic

Embeber el código ASP (VBS) en HTML
<html>
  <head>...</head>
  <body>
    Este texto se ha generado desde HTML<br/>
    <%
      response.write("Y este se ha generado con ASP")
    %
  </body
</html>

No es necesario declarar las variables de tipo simple, pero puede hacerse:
Dim i,j,k As Integer

Algunos operadores:
Comparación: <, >, <=, >=, =, <> 
Asignación: =

Algunas estructuras de control
do while (condicion) 
  Acciones
loop


if (condicion) then
  Acciones-1
else 
  Acciones-2
end if

### 8.4.4. Entrada / Salida

// Leer datos de un formulario (GET):
variable = request.QueryString("campo");
// Leer datos de un formulario (POST):
variable = request.Form("campo");

// Salida:
response.write ("cadena" + variable + "cadena2"); 

### 8.4.5. Bibliotecas, funciones y clases

Subrutinas
sub nombre(parametros)
    Acciones;
end sub

Bibliotecas
<% @Import Namespace="Biblioteca" %>



### 8.4.6. Ejemplo 1 en VBasic: Hola mundo

<%
   response.write("<html><body>")
   response.write("<h1>Hola, mundo</h1>")
   response.write("</body></html>")
%>


### 8.4.7. Ejemplo 2 en VBasic: login con comprobación de email por Ajax

url: "/ruta/al/script.asp", // URL of the ASP script

Script ASP en el lado del servidor (login.asp)

<% 
# connect to the database
strDSN= "DRIVER={MySQL ODBC 3.51 driver}; Server=localhost; Database=prueba; User=root;  
         Password=xxxx"
con = Server.CreateObject("ADODB.Connection")
con.Open strDSN

# retrieve the form params
name = request.Form("username");
pass = request.Form("password");

# check username and password in the database
rs = con.Execute("SELECT id FROM users WHERE user = '" + name + 
                 "' AND password = '" + pass + "'");

# generate ouput JSON string
if (rs.eof)
   Response.Write "{'error': 'Username or password not valid'}"
else
   Response.Write "{'success': 'Authentication is OK', 'userid': "+ rs("id") + "}");

con.close
%>

## 8.5. JSP

### 8.5.1. Características del lenguaje JSP

Fecha de aparición: 1995

Perspectivas: 

* Usado para proyectos grandes y complejos, donde PHP (y otros lenguajes de scripting) se quedan pequeños.
* El lenguaje de programación es Java, es decir, lo conoce cualquier programador. 
* Velocidad de ejecución superior a la de otros lenguajes semi-interpretados.

Filosofía:

* Adaptación natural de Java al lado del servidor.
* Orientado a objetos. Multiplataforma. Fuertemente tipado. 
* Puede embeberse dentro de HTML, como PHP.
* El código Java se precompila en un Servlet y se deja cargado en la memoria del servidor. Las peticiones subsiguientes se ejecutan así mucho más rápidas.

### 8.5.2. Configuración necesaria en el servidor

Instalar Tomcat. Es el servidor de referencia para la tecnología JSP. 
JSP se puede ejecutar como CGI, pero resulta mucho más lento.

### 8.5.3. Sintaxis básica de JSP

Embeber el código JSP en HTML
<html>
  <head>...</head>
  <body>
    Este texto se ha generado desde HTML<br/>
    <%
      out.println("Y este se ha generado con JSP");
    %>
  </body>
</html>

Las variables se declaran como en cualquier programa Java:
int var = 5;
out.print("La variable var vale " + var);

Algunos operadores:
Comparación: <, >, <=, >=, ==, != 
Asignación: =

Algunas estructuras de control
while (condicion) {
  Acciones
}


if (condicion) {
  Acciones-1
}
else {
  Acciones-2
}

### 8.5.4. Entrada / Salida

// Leer datos de un formulario:
variable = request.getParameter("campo");

// Salida:
out.println ("cadena" + variable + "cadena2"); 

### 8.5.5. Bibliotecas, funciones y clases

Clases y métodos
class mi-clase extends clase-madre {
   public|private|protected tipo nombre(params) {
       Acciones;
   }
}

Módulos
import modulo;

### 8.5.6. Ejemplo 1 en JSP: Hola mundo

<%
   out.println("<html><body>");
   out.println("<h1>Hola, mundo</h1>");
   out.println("</body></html>");
%>

### 8.5.7. Ejemplo 2 en JSP: login con comprobación de email por Ajax

url: "/ruta/al/script.jsp", // URL of the JSP script

Script JSP en el lado del servidor (login.jsp)
<% @page import="java.sql.*"

# connect to the database
Connection conex = null;
Statement st = null;
Class.forName("org.gjt.mm.mysql.Driver");
conex = DriverManager.getConnection("jdbc:mysql://servidor", "user", "pass");

# retrieve the form params
name = request.getParameter("username");
pass = request.getParameter("password");

# check username and password in the database
st = conex.createStatement();
ResultSet = st.executeQuery("SELECT id FROM users WHERE user = '" + name + 
            "' AND password = '" + pass + "'");

# generate ouput JSON string
if (st.EOF)
   out.println("{'error': 'Username or password not valid'}");
else
   out.println("{'success': 'Authentication is OK', 'userid':"+ ResultSet.getInt() + "}");
conex.close()
%>




## 8.6. Ruby

### 8.6.1. Características del lenguaje Ruby

Fecha de aparición: 1995

Perspectivas: 

* Uso y popularidad creciente.
* Base de programadores fiel y especializada.
* Excelente relación señal/ruido.
* Aún tiene que resolver algunas cosas:
* El lenguaje todavía está en fase de importantes cambios.
* Tiene peor rendimiento que Python o PHP.
* Muchos módulos (gemas) están mal documentados.

Filosofía:

* Completa – y verdaderamente – orientado a objetos. Todo es un objeto.
* Admite otros paradigmas ocultos bajo los objetos. 
* “Rápido y fácil”. Es un lenguaje divertido: de programadores para programadores. 
* Curva de aprendizaje larga pero nunca abrupta.
* Lenguaje de scripting Unix: expresiones regulares.
* En combinación con Rails, ideal para desarrollo web MVC rápido y basado en prototipos.

**¿Y Ruby on Rails?**

Rails es un framework para desarrollar aplicaciones web MVC con Ruby.
Apareció en 2004 y gustó tanto que otros frameworks para otros lenguajes (como CodeIgniter para PHP) copiaron su forma de trabajar:
Abundantes capas de abstracción para evitar tareas de bajo nivel, como ActiveRecord.
Scaffolding
Integración con Ajax mediante jQuery, Prototype o Script.aculo.us
CoC & DRY (Convention over Configuration & Don't Repeat Yourself)


### 8.6.2. Configuración necesaria en el servidor

Instalar el intérprete Ruby en el sistema.
Instalar el módulo de Ruby (mod_ruby) y/o el módulo cgi (mod_cgi) para Apache.
Configurar el manejador de Apache para CGI.
Instalar módulos adicionales para Ruby (como cgi o mysql) si son necesarios.
Como en el caso de Perl o Python, Ruby puede correr de forma nativa en Apache (más rápido pero menos frecuente) o como script CGI.

### 8.6.3### 8.6.4. . Sintaxis básica de Ruby

No es necesario declarar las variables. El tipado es dinámico (duck)
Todo es un objeto, incluso números enteros o valores constantes:
5.isEven?
"cadena".lenght
variable_cadena.chop!
Algunos operadores:
Comparación: <, >, <=, >=, =, != 
Asignación: =

Algunas estructuras de control
while condicion 
  Acciones
end


if condicion
  Acciones-1
else 
  Acciones-2
end

Sin embargo, el uso de bucles clásicos casi siempre puede sustituirse por iteradores sobre objetos:

variable_array.do_each
   ...
end


num_rows.times do
   ...
end

### 8.6.4. Entrada / Salida

// Leer datos de un formulario
require "cgi"
cgi = CGI.new
variable = cgi["campo"];

// Salida:
print "cadena", variable, "cadena2", ... 

### 8.6.5. Bibliotecas, funciones y clases

class nombre_clase < clase-madre
    def nombre(parametros)
       Acciones;
    end
end

Bibliotecas (gemas)
include "modulo"
require "modulo"

### 8.6.6. Ejemplo 1 en Ruby: Hola mundo

#!/usr/bin/ruby

print "Content-Type: text/html\n\n"
print "<html><body>"
print "<h1>Hola, mundo</h1>"
print "</body></html>"

### 8.6.7. Ejemplo 2 en Ruby: login con comprobación de email por Ajax

url: "/cgi-bin/login.rb", // URL of the Ruby script

Script Ruby en el lado del servidor (login.rb)
#!/usr/bin/ruby
require "mysql"
require "cgi"

begin
    # connect to the database
    con = Mysql.new 'server', 'db-user', 'db-password', 'db-name'

    # retrieve the form params
    cgi = CGI.new
    name = cgi["username"]
    pass = cgi["password"]

    # check username and password in the database
    res = con.query("SELECT id FROM users WHERE user = '#{name}' AND password = '#{pass}'")

    # generate ouput JSON string
    print "Content-type: application/json\n\n"
    if res.num_rows == 0
       print %Q!{"error": "Username or password not valid"}!
    else
       row = res.fetch_hash
       print %Q!{"success": "Authentication is OK", "userid": "#{row['id']}" }!
    end
    con.close if con    
end



## 8.7. NodeJS

TODO

### 8.7.1. Características del lenguaje NodeJS


Fecha de aparición: XXX

Perspectivas: 

* TODO

Filosofía:

* TODO

### 8.7.2. Configuración necesaria en el servidor

TODO

### 8.7.3. Sintaxis básica de NodeJS

TODO

### 8.7.4. Entrada / Salida con NodeJS

TODO

### 8.7.5. Bibliotecas, funciones y clases

TODO

### 8.7.6. Ejemplo 1 en NodeJS: Hola mundo

TODO

### 8.7.7. Ejemplo 2 en NodeJS: login con comprobación de email por Ajax

TODO

## 8.8. Y otras tecnologías aún más extrañas

Además de los lenguajes que hemos visto, existen otras alternativas a PHP para desarrollar aplicaciones web en el lado del servidor.
A continuación mostramos una lista con alguna de estas alternativas (no están todas las que son, pero sí son todas las que están) para quien quiera profundizar aún más en el asunto:

### 8.2.1. ColdFusion

ColdFusion es la alternativa de Adobe. ColdFusion es al mismo tiempo un servidor de aplicaciones y un lenguaje de programación. Utiliza elementos <...> para insertar su código en la página web y, lógicamente, interacciona de manera óptima con otros productos de Adobe, como Flash. Los archivos tienen extensión .cfm. Se diseñó para tener un rendimiento muy elevado (por ejemplo, aprovecha bien la presencia de múltiples procesadores en el servidor) 

### 8.2.2. WebDNA

WebDNA es un lenguaje especialmente diseñado para hacer scripting del lado del servidor (no como PHP, Perl, Python o Ruby, que fueron pensados para otros propósitos). Especialmente rápido en la interacción con bases de datos. Utiliza etiquetas encerradas entre corchetes [...] para intercalar su código con HTML. 

### 8.2.3. Erlang

Se trata de un lenguaje para desarrollo de aplicaciones concurrentes (es decir, en las que varios procesos se ejecutan simultáneamente, cooperando en la resolución de un problema). Fue diseñado para sistemas en tiempo real. Se está empezando a usar en el lado del servidor cuando las aplicaciones tienen necesidades de procesamiento brutales. 

### 8.2.4. Otros SSJS

(SSJS = Server Side JavaScript): hace mucho tiempo que se especula con la posibilidad de programar scripts del lado del servidor en JavaScript. Al fin y al cabo, JS es un lenguaje dominado por cualquier desarrollador web. No existe por ahora ninguna solución estandarizada: a veces, el JS se traduce a Java para ejecutarlo como JSP, otras veces se compila a código nativo del servidor (como hace NodeJS), otras veces se instala un plugin en el servidor para ejecutarlo nativamente, o bien se reduce su uso sólo a generar y procesar información JSON, etc. JS en el lado del servidor necesita siempre de librerías adicionales para acceder a los recursos del servidor (p.ej: bases de datos) 
