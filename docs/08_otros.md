---
layout: page
title: 8 Otras tecnologías
permalink: /otras-tecnologias/
parent: Desarrollo Web en Entorno Servidor
nav_order: 8
---
# 8. Otras tecnologías

## 8.1. Common Gateway Interface (CGI)

CGI es la definición de la interfaz entre los servidores web y las aplicaciones que se ejecutan en el servidor. Estas aplicaciones pueden estar construidas en cualquier lenguaje como Perl, C, scripting de unix, Python o cualquier otro. CGI sólo define la forma de transferir información en ambos sentidos.

En el diagrama siguiente vemos el esquema general en que se ejecutan programas en el servidor a través de CGI. Las invocaciones se llevan a cabo a través del llenado de un formulario con los parámetros que se envían al programa que corresponda. Por lo tanto, el primer paso es el acceso al formulario en donde se definen los campos, y el programa que se ejecutará cuando se envíen los datos. El segundo paso es justamente el envío de los datos. El tercer paso es la invocación de la ejecución del programa referenciado (en el ejemplo, “programa 1”). Esta invocación es hecha por el servidor web, quien le traspasa los datos recibidos del cliente. Los programas CGI generan una salida, típicamente un documento HTML, que será enviado al cliente como paso final (cuarto).

XXX esquema

Ventajas e inconvenientes de CGI
El interfaz CGI permite que cualquier programa ejecutable en el servidor pueda usarse para generación dinámica de páginas web. Por eso fue la primera alternativa utilizada para este tipo de páginas. Además, está disponible en muchos servicios de hosting web y es relativamente fácil de configurar.
Sin embargo, tiene un serio problema de rendimiento: cada vez que se envían los datos de un formulario se crea un nuevo proceso en el servidor para ejecutar el programa en cuestión, quien genera una respuesta que se envía a través del servidor HTTP al browser, luego de lo cual se elimina el proceso creado. Esta creación de procesos implica una carga importante para el servidor, por lo cual esta modalidad de generación de contenido dinámico no es muy escalable.
Existen algunas alternativas para solucionar este problema, como mantener un sólo proceso CGI en memoria que se encargará de procesar todas las peticiones (técnica conocida como FastCGI), pero resulta más complejo de configurar y operar, e implica algunos problemas de seguridad.

Variables de entorno CGI 
La comunicación desde el browser al servidor con los datos del formulario se puede hacer en dos modalidades, a través de variables de entorno (GET) o a través de la línea de comando (POST). Estos datos están disponibles en la variable QUERY_STRING en los envíos con GET y en la entrada estándar en los envíos con POST. Adicionalmente existe un conjunto de variables de entorno que existen en ambas modalidades:
    • SERVER_SOFTWARE    Devuelve el nombre y la versión del software del servidor de información que contesta la petición de usuario (y ejecuta el programa cgi). 
    • SERVER_NAME    Devuelve nombre de host del servidor, el alias DNS, o la dirección IP como aparecería en las URL autoreferenciadas.
    • GATEWAY_INTERFACE    Devuelve la revisión de la especificación CGI con que el servidor puede trabajar. Formato: CGI/revisión.
    • SERVER_PROTOCOL    Da el nombre y revisión del protocolo de información con el que la petición de usuario viene. Formato: protocolo/revisión. 
    • SERVER_PORT         Devuelve el número de puerto por el cual fue enviada la petición. 
    • REQUEST_METHOD    Devuelve el método por el cual la petición fue enviada. Para HTTP serán "GET", "HEAD", "POST", etc
    • PATH_INFO        La información extra sobre el path, tal como es dada por el cliente. En otras palabras, podemos acceder a los scripts por su pathname virtual, seguido de alguna información extra. Esa información extra es enviada como PATH_INFO. La información será decodificada por el servidor si viene de una URL antes de pasarla al script CGI.
    • PATH_TRANSLATED    El servidor proporciona una versión traducida del PATH_INFO, que transforma el path virtual al físico.
    • SCRIPT_NAME    Path virtual al script que va a ejecutar, usado para autoreferenciar URL.
    • QUERY_STRING    La información que sigue al signo ‘?’ en la URL que referencia al script. Es la información de la pregunta. No deberá ser decodificada de ningún modo. Esta variable será activada cuando hay una petición de información, sin hacer caso de la decodificación de la línea de comandos. 
    • REMOTE_HOST    El nombre de host que realiza la petición. Si el servidor no posee esta información activará REMOTE_ADDR y dejará esta desactivada.
    • REMOTE_ADDR    La dirección IP del host remoto que realiza la petición. 
    • AUTH_TYPE    Si el servidor soporta autentificación de usuario , y el script está protegido, esta es el método de autentificación específico del protocolo para validar el usuario. 
    • REMOTE_USER    Si el servidor soporta autentificación de usuario , y el script está protegido, este será el nombre de usuario con el que se ha autentificado. 
    • REMOTE_IDENT    Si el servidor HTTP soporta autentificación RFC 931 , entonces está variable se activará con el nombre del usuario remoto obtenido por el servidor. Esta varible solo se utilizará durante el login. 
    • CONTENT_TYPE    Para peticiones que tienen información añadida, como HTTP POST y PUT, este será el tipo de datos contenido. 
    • CONTENT_LENGTH    La longitud del contenido tal como es dado por el cliente.
La forma de acceder a estas variables, lógicamente, dependerá del lenguaje que estemos usando. Cada lenguaje proporcionará sus propias librerías para hacer uso de CGI y facilitar el desarrollo de aplicaciones CGI.

Respuesta al cliente
La respuesta se envía a través de la salida estandar y puede ser cualquier cosa comprensible por el navegador web. Para el caso de texto HTML (que es lo más habitual), se debe comenzar enviando el string:
Content-Type: text/html
...seguido de una línea en blanco. Detrás del texto “Content-Type:” puede colocarse cualquier tipo MIME reconocible por el navegador.

## 8.2. Perl

### 8.2.1. Características del lenguaje Perl

Fecha de aparición: 1987
Última revisión: 5.30.1 (nov 2019)
Perspectivas: 
Uso decreciente. 
Apto para tareas pequeñas y rápidas. 
Cuenta con desarrolladores muy fieles y experimentados. Documentación muy extensa.
Soporte amplio en cualquier servidor.

Filosofía
Versión mejorada del shell scripting de Unix.
Pensado para procesamiento rápido de archivos de texto y automatización de tareas de administración del sistema.
Favorece la programación ágil, rápida y sucia de scripts. 
Énfasis en las expresiones regulares.
Multiparadigma.
En combinación con CGI, se popularizó para aplicaciones web antes de la aparición de PHP.

### 8.2.2. Configuración necesaria en el servidor

Instalar el intérprete Perl (usr/bin/perl).
Activar los módulos perl y/o cgi de Apache y configurar el handler para CGI.
Se puede ejecutar el intérprete Perl de forma nativa en Apache, o bien hacerlo a través de CGI.
Lo primero es más difícil de configurar y raramente se encuentra en hostings web compartidos.
Instalar módulos Perl adicionales para acceso a bases de datos, etc.

### 8.2.3. Sintaxis básica de Perl

Las variables no se declaran, tienen tipado dinámico y son globales por defecto.
$var = valor;
print "La variable var vale $variable";

Algunos operadores:
Comparación: lt, gt, le, ge, eq, ne... 
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

Entrada / salida

# Entrada de datos estándar:
chop ( $variable = <STDIN> );

# Lectura de datos desde un formulario HTML:
use CGI;
my $cgi = CGI->new;
my $username = $cgi->param("username");

# Salida:
print "cadena $variable cadena..."; 

Subprogramas
# Comentarios
Sub nombre-rutina (argumentos) {
   Acciones
}

Bibliotecas
use biblioteca

### 8.2.4. Ejemplo 1 en Perl: Hola mundo

#!/usr/bin/perl
print "Content-type: text/html\n\n";
print "<html><title>Hola mundo</title><body>";
print "Hola, mundo";
print "</body></html>";


### 8.2.5. Ejemplo 2 en Perl: login con comprobación de email por Ajax

Formulario HTML

<form id="loginForm" name="loginForm" method="post" action="">
  <fieldset>
    <legend>Enter information</legend>
    <p>
      <label for="username">Username</label>
      <br />
      <input type="text" id="username" name="username" class="text" size="20" />
    </p>
    <p>
      <label for="password">Password</label>
      <br />
      <input type="password" id="password" name="password" class="text" size="20" />
    </p>
    <p>
      <button type="submit" class="button positive">
       <img alt="ok" src=
       "http://www.blueprintcss.org/blueprint/plugins/buttons/icons/tick.png" /> 
       Login
      </button>
    </p>
  </fieldset>
</form>

Script AJAX/jQuery

$(document).ready(function(){
  $("form#loginForm").submit(function() { // loginForm is submitted
    var username = $('#username').attr('value'); // get username
    var password = $('#password').attr('value'); // get password

    if (username && password) { // values are not empty
      $.ajax({
        type: "GET",
        url: "/cgi-bin/login.pl", // URL of the Perl script
        contentType: "application/json; charset=utf-8",
        dataType: "json",
        // send username and password as parameters to the Perl script
        data: "username=" + username + "&password=" + password,
        // script call was *not* successful
        error: function(XMLHttpRequest, textStatus, errorThrown) { 
          $('div#loginResult').text("responseText: " + XMLHttpRequest.responseText 
            + ", textStatus: " + textStatus 
            + ", errorThrown: " + errorThrown);
          $('div#loginResult').addClass("error");
        }, // error 
        // script call was successful 
        // data contains the JSON values returned by the Perl script 
        success: function(data){
          if (data.error) { // script returned error
            $('div#loginResult').text("data.error: " + data.error);
            $('div#loginResult').addClass("error");
          } // if
          else { // login was successful
            $('form#loginForm').hide();
            $('div#loginResult').text("data.success: " + data.success 
              + ", data.userid: " + data.userid);
            $('div#loginResult').addClass("success");
          } //else
        } // success
      }); // ajax
    } // if
    else {
      $('div#loginResult').text("enter username and password");
      $('div#loginResult').addClass("error");
    } // else
    $('div#loginResult').fadeIn();
    return false;
  });
});


Script Perl en el lado del servidor (login.pl)

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




## 8.3. Python

### 8.3.1. Características del lenguaje Python
Fecha de aparición: 1991
Última revisión: 3.8.1 (dic 2019)
Perspectivas: 
Uso creciente. 
Es el sustituto natural de Perl para el desarrollo rápido de scripts. 
También usado en grandes proyectos como alternativa a PHP.
Menos extendido que PHP, pero comunidad con muchos desarrolladores profesionales (mejor relación señal/ruido)
Muchas bibliotecas de terceros → flexibilidad

Filosofía
Es la versión “limpia” de Perl. Pensado para escribir scripts de forma rápida y limpia.
Énfasis en la legibilidad: Python es casi pseudocódigo (código “pythonico” → v. “El Zen de Python”)
Interpretado. Tipado dinámico. Fuertemente tipado.
Expresiones regulares heredadas de Perl.
Multiparadigma: imperativo, O.O., funcional.

### 8.3.2. Configuración necesaria en el servidor

Instalar el intérprete Python (/usr/bin/python). El más extendido es CPhyton.
Activar los módulos python y/o cgi de Apache y configurar el handler de Apache para CGI.
Python puede funcionar de forma nativa integrado en Apache o a través de CGI.
Lo primero es más rápido, lo segundo más frecuente.
Instalar módulos adicionales (p. ej: para acceso a bases de datos) si es necesario.

### 8.3.3. Sintaxis básica de Python

Las variables no se declaran obligatoriamente, tienen tipado dinámico y son locales por defecto.
varariable = valor;
print "La variable var vale %s" (variable);
Tiene muchos tipos de datos complejos predefinidos: listas, tuplas, diccionarios...
Algunos operadores:
Comparación: <, >, <=, >=, ==, != 
Asignación: =


Algunas estructuras de control

¡El código debe indentarse OBLIGATO-RIAMENTE!

La indentación marca el final del bloque

while condicion:
  Acciones



if condicion:
  Acciones-1
else:
  Acciones-2
  
  
  Entrada / salida

# Entrada de datos estándar:
variable = raw_input("Texto")

# Lectura de datos de un formulario HTML:
import cgi
form = cgi.FieldStorage()
campo = form["campo"].value

# Salida:
print "cadena %s cadena %s ..." (variable1, variable2) 

Subprogramas
# Comentarios
def nombre-rutina (argumentos):
   Acciones
   [return valor1, varlor2...]

Módulos
import modulo

### 8.3.4. Ejemplo 1 en Python: Hola mundo

#!/usr/bin/python
print "Content-type: text/html\n\n"
print "<html><body>"
print "<h1>Hola, mundo</h1>"
print "</body></html>"

### 8.3.5. Ejemplo 2 en Python: login con comprobación de email por Ajax

url: "/cgi-bin/login.py", // URL of the Python script


Script Python en el lado del servidor (login.py)
#!/usr/bin/python

import cgi
import MySQLdb 

# read the CGI params
form = cgi.FieldStorage()
usuario = form["username"].value;
password = form["password"].value;

print "Usuario = ", usuario, " Pass = ", password

# check the username and password in the database
db=MySQLdb.connect(host='localhost',user='root',passwd='root',db='perl')
cursor=db.cursor()
num_rows = cursor.execute("SELECT id FROM users WHERE username = '%s' AND password = '%s';", (usuario, password))
userid = cursor.fetchone()

# return JSON string
print "Content-type: application/json\n"
if num_rows == 0:
   print "{'error': 'Usuario o contrase&ntilde;a incorrectos'}"
else:
   print "{'success': 'El usuario y la contrase&ntilde;a son v&aacute;lidos', 'userid': '%d'", userid



## 8.4. .NET

### 8.4.1. Características de .NET

Fecha de aparición: 1996 (ASP) / 2002 (.NET)
Última revisión: 4.7.1 (oct 2017)
Perspectivas: 
Alternativa de Microsoft a JSP para desarrollo de grandes proyectos, donde PHP se queda pequeño.
Componentes exclusivos en el servidor y altas prestaciones. 
Coste más elevado y problemas de seguridad endémicos.

Filosofía
Framework de código cerrado y propietario.
Tecnología multilenguaje. Suele correr con VBS (Visual Basic Script), pero puede hacerlo con otros. 
Puede funcionar como PHP, embebido dentro de HTML.
ASP.Net incluye controles de servidor exclusivos de Microsoft (equivalentes a los ActiveX del lado del cliente)

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

Entrada / Salida

// Leer datos de un formulario (GET):
variable = request.QueryString("campo");
// Leer datos de un formulario (POST):
variable = request.Form("campo");

// Salida:
response.write ("cadena" + variable + "cadena2"); 

Subrutinas
sub nombre(parametros)
    Acciones;
end sub

Bibliotecas
<% @Import Namespace="Biblioteca" %>



### 8.4.4. Ejemplo 1 en VBasic: Hola mundo

<%
   response.write("<html><body>")
   response.write("<h1>Hola, mundo</h1>")
   response.write("</body></html>")
%>


### 8.4.5. Ejemplo 2 en VBasic: login con comprobación de email por Ajax

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
Última revisión: Java 11 (ago 2012)
Perspectivas: 
Usado para proyectos grandes y complejos, donde PHP (y otros lenguajes de scripting) se quedan pequeños.
El lenguaje de programación es Java, es decir, lo conoce cualquier programador. 
Velocidad de ejecución superior a la de otros lenguajes semi-interpretados.

Filosofía
Adaptación natural de Java al lado del servidor.
Orientado a objetos. Multiplataforma. Fuertemente tipado. 
Puede embeberse dentro de HTML, como PHP.
El código Java se precompila en un Servlet y se deja cargado en la memoria del servidor. Las peticiones subsiguientes se ejecutan así mucho más rápidas.

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

Entrada / Salida

// Leer datos de un formulario:
variable = request.getParameter("campo");

// Salida:
out.println ("cadena" + variable + "cadena2"); 

Clases y métodos
class mi-clase extends clase-madre {
   public|private|protected tipo nombre(params) {
       Acciones;
   }
}

Módulos
import modulo;

### 8.5.4. Ejemplo 1 en JSP: Hola mundo

<%
   out.println("<html><body>");
   out.println("<h1>Hola, mundo</h1>");
   out.println("</body></html>");
%>

### 8.5.5. Ejemplo 2 en JSP: login con comprobación de email por Ajax

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
Última revisión: 2.6.1 (feb 2013)
Perspectivas: 
Uso y popularidad creciente.
Base de programadores fiel y especializada.
Excelente relación señal/ruido.
Aún tiene que resolver algunas cosas:
El lenguaje todavía está en fase de importantes cambios.
Tiene peor rendimiento que Python o PHP.
Muchos módulos (gemas) están mal documentados.

Filosofía
Completa – y verdaderamente – orientado a objetos. Todo es un objeto.
Admite otros paradigmas ocultos bajo los objetos. 
“Rápido y fácil”. Es un lenguaje divertido: de programadores para programadores. 
Curva de aprendizaje larga pero nunca abrupta.
Lenguaje de scripting Unix: expresiones regulares.
En combinación con Rails, ideal para desarrollo web MVC rápido y basado en prototipos.

### 8.6.2. Configuración necesaria en el servidor

Instalar el intérprete Ruby en el sistema.
Instalar el módulo de Ruby (mod_ruby) y/o el módulo cgi (mod_cgi) para Apache.
Configurar el manejador de Apache para CGI.
Instalar módulos adicionales para Ruby (como cgi o mysql) si son necesarios.
Como en el caso de Perl o Python, Ruby puede correr de forma nativa en Apache (más rápido pero menos frecuente) o como script CGI.

### 8.6.3. ¿Y Ruby on Rails?

¿Y Ruby on Rails?
Rails es un framework para desarrollar aplicaciones web MVC con Ruby.
Apareció en 2004 y gustó tanto que otros frameworks para otros lenguajes (como CodeIgniter para PHP) copiaron su forma de trabajar:
Abundantes capas de abstracción para evitar tareas de bajo nivel, como ActiveRecord.
Scaffolding
Integración con Ajax mediante jQuery, Prototype o Script.aculo.us
CoC & DRY (Convention over Configuration & Don't Repeat Yourself)

### 8.6.4. Sintaxis básica de Ruby

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

Entrada / Salida

// Leer datos de un formulario
require "cgi"
cgi = CGI.new
variable = cgi["campo"];

// Salida:
print "cadena", variable, "cadena2", ... 

Clases y métodos
class nombre_clase < clase-madre
    def nombre(parametros)
       Acciones;
    end
end

Bibliotecas (gemas)
include "modulo"
require "modulo"

### 8.6.5. Ejemplo 1 en Ruby: Hola mundo

#!/usr/bin/ruby

print "Content-Type: text/html\n\n"
print "<html><body>"
print "<h1>Hola, mundo</h1>"
print "</body></html>"

### 8.6.6. Ejemplo 2 en Ruby: login con comprobación de email por Ajax

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

TODO

### 8.7.2. Configuración necesaria en el servidor

TODO

### 8.7.3. Sintaxis básica de NodeJS

TODO

### 8.7.4. Ejemplo 1 en NodeJS: Hola mundo

TODO

### 8.7.5. Ejemplo 2 en NodeJS: login con comprobación de email por Ajax

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
