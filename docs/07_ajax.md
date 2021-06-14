---
layout: page
title: 7 Ajax
permalink: /ajax/
parent: Desarrollo Web en Entorno Servidor
nav_order: 7
---
# 7. Ajax

## 7.1. ¿Qué es Ajax?

Ajax = Asynchronous Javascript And XML
Ajax es una tecnología JS para ejecutar la aplicación web en el cliente (o gran parte de ella) y lanzar peticiones al servidor para refrescar la información mostrada.
Las peticiones al servidor se lanzan y reciben en segundo plano (= de forma asíncrona)
Ajax permite actualizar las páginas sin necesidad de recargarlas por completo, lo que mejora la usabilidad y velocidad de respuesta.

## 7.2. Cómo enviar peticiones Ajax al servidor

### 7.2.1. Peticiones sin datos al servidor

peticion_http = new XMLHttpRequest();
peticion_http.onreadystatechange = procesa_respuesta;
peticion_http.open('GET', 'http://servidor/recurso', true);
peticion_http.send(null);


function procesa_respuesta() {
    if(peticion_http.readyState == 4) {
      if(peticion_http.status == 200) {
        alert(peticion_http.responseText);
      }
    }
}

### 7.2.2. Peticiones con datos al servidor (GET)

var cp = document.getElementById("codigo_postal");
var telefono = document.getElementById("telefono");
 
query_string = "&codigo_postal=" + encodeURIComponent(cp.value) +
               "&telefono=" + encodeURIComponent(telefono.value);

peticion_http = new XMLHttpRequest();
peticion_http.onreadystatechange = procesa_respuesta;
peticion_http.open('GET', 'http://servidor/scrip.php', true);
peticion_http.send(query_string);

function procesa_respuesta() { .... }

### 7.2.3. Peticiones con datos al servidor (POST)
var cp = document.getElementById("codigo_postal");
var telefono = document.getElementById("telefono");
 
query_string = "&codigo_postal=" + encodeURIComponent(cp.value) +
               "&telefono=" + encodeURIComponent(telefono.value);

peticion_http = new XMLHttpRequest();
peticion_http.onreadystatechange = procesa_respuesta;
peticion_http.open("POST", "http://servidor/script.php", true);
peticion_http.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
peticion_http.send(query_string);

function procesa_respuesta() { .... }

### 7.2.4. Peticiones con datos al servidor (XML)
var cp = document.getElementById("codigo_postal");
var telefono = document.getElementById("telefono");
xml = "<datos>" +
      "<cp>" + cp + </cp>" + <telefono> + telefono + </telefono> +
      "</datos>";

peticion_http = new XMLHttpRequest();
peticion_http.onreadystatechange = procesa_respuesta;
peticion_http.open("POST", "http://servidor/script.php", true);
peticion_http.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
peticion_http.send(xml);

function procesa_respuesta() { .... }

## 7.3. Cómo recibir la respuesta del servidor

### 7.3.1. Recepción de datos XML

Recepción de datos XML
function procesaRespuesta() {
  if(peticion_http.readyState == 4) {
    if(peticion_http.status == 200) {
      var xml = peticion_http.responseXML;
      var datos = xml.getElementsByTagName("datos")[0];
      var telefono = datos.getElementsByTagName("telefono")[0].
                     firstChild.nodeValue;
      var cp = datos.getElementsByTagName("cp")[0].
               firstChild.nodeValue;
 
      document.getElementById("respuesta").innerHTML = 
             "Codigo postal = " + codigo_postal + "<br/>" + 
             "Telefono = " + telefono;
    }
  }
}

### 7.3.2. Recepción de datos JSON
function procesaRespuesta() {
  if(http_request.readyState == 4) {
  if(http_request.status == 200) {
    var json = http_request.responseText;
    var objeto_json = eval("("+json+")");
    var telefono = objeto_json.datos.telefono;
    var codigo_postal = objeto_json.datos.cp;
    document.getElementById("respuesta").innerHTML = 
             "Codigo postal = " + codigo_postal + "<br/>" + 
             "Telefono = " + telefono;
    }
  }
}

## 7.4. Ajax y jQuery

El uso de jQuery facilita enormemente la programación de llamadas Ajax al servidor.
jQuery ofrece varias funciones para hacer llamadas Ajax:
$.ajax() → La más configurable pero también la más compleja.
$.get() → Para lanzar peticiones GET sencillas.
$.post() → Para lanzar peticiones POST sencillas
$.load() → Para lanzar peticiones GET y cargar la respuesta en una capa.

Función $.ajax()
$.ajax({
  url: '/ruta/hasta/script.php',
  type: 'POST',
  async: true,
  data: 'parametro1=valor1&parametro2=valor2',
  success: función_procesa_respuesta,
  error: función_procesa_error
});

Funciones $.get() y $.post
$.get(url, datos, funcion_manejadora);
$.post(url, datos, funcion_manejadora);

Ejemplo:
$.get('/ruta/hasta/script.php',
      { user: 'juanperez03' },
      function(user) {
         alert('Hola, ' + user);
      }
);


Función $.load()
Inserta el resultado del script del servidor en el elemento seleccionado con $:
$('#info').load('/ruta/hasta/pagina.php');

Variación “IfModified”:

$.getIfModified('/ruta/hasta/script.php');
$.postIfModified('/ruta/hasta/script.php');
$('#info').loadIfModified('/ruta/hasta/script.php');


## 7.5. Ajax y Laravel

Enrutador /routes/web.php
Route::post('miJqueryAjax','AjaxController@miMetodo');

Ten en cuenta que:
No es imprescindible crear un controlador específico para atender las peticiones Ajax. Puedes usar métodos de tus controladores habituales.
Las peticiones Ajax pueden llegar por GET, POST o cualquier otro método. De hecho, el servidor no tiene modo de saber si han llegado por Ajax o no.

Controlador /app/controllers/AjaxController.php
class AjaxController extends Controller {
   public function miMetodo() {
     ...aquí va mi código... 
     $result = json_encode($mis_variables);
     echo $result;
   }
}

O mejor todavía:
class AjaxController extends Controller {
   public function miMetodo() {
      $msg = "This is a simple message.";
      return response()->json($mis_variables);
   }
}

Ten en cuenta que:
La salida de una petición Ajax suele ser JSON, pero podría ser otra cosa: HTML, XML, o un simple carácter como “0” o “1”.
Para responder a una petición Ajax no se debe renderizar una vista, sino que basta con un echo en el controlador.

Agregar el token CSRF a las peticiones (1/2)
Las peticiones enviadas por POST a Laravel deben llevar el token CSRF o serán rechazadas.
El token debe agregarse a cada petición, así:
$.ajax({
     method: "POST",
     url: "mi-url",
     data: {
         "_token": "{{ csrf_token() }}",
     },
     ...etc... 
});

Agregar el token CSRF a las peticiones (2/2)
También puede agregarse automáticamente el token CSRF a todas las peticiones haciendo esto en el header de nuestro layout:
   <meta name="csrf-token" content="{{ csrf_token() }}">
   <script type="text/javascript">
      $.ajaxSetup({
          headers: {
             'X-CSRF-TOKEN': $('meta[name="csrf-token"]').attr('content')
          }
      });
   </script>
A partir de ahora, podremos hacer las peticiones Ajax normalmente, porque el token CSRF se añadirá él solito a cada petición Ajax.




