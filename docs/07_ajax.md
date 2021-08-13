---
layout: page
title: 7 Ajax
permalink: /ajax/
parent: Desarrollo Web en Entorno Servidor
nav_order: 7
---
# 7. Ajax

## 7.1. Un poco de introducción al asunto

## 7.1.1. ¿Qué es Ajax?

**Ajax** significa **Asynchronous Javascript And XML**.

Qué bien, ¿no?

¿Y eso qué quiere decir?

Ajax es una tecnología javascript para lanzar y recibir las peticiones al servidor en segundo plano. La página sigue funcionando con normalidad mientras la petición al servidor se resuelve: el usuario puede interactuar con ella y la página responde y no se queda *congelada* a la espera de que el servidor conteste.

**Todo eso es lo que significa "de forma asíncrona"**.

Esta forma de trabajar, que puede parecer una chorrada, se creó para que las páginas dieran la impresión de ser más ágiles de lo que en realidad eran (sobre todo en una época en la que las redes eran más lentas y los servidores podían tardar bastante en responder).

En la actualidad, Ajax ha permitido algo que parecía impensable hace una década: que gran parte de la página se ejecute en el cliente y que se pidan al servidor solo los fragmentos de la página que necesitan ser actualizados. Ajax permite actualizar las páginas sin necesidad de recargarlas por completo, lo que mejora la usabilidad y velocidad de respuesta, y cambia radicalmente nuestra forma de programar una aplicación web.

### 7.1.2. Ajax no sirve, en realidad, para nada

Esa es la pura verdad.

Puedes programar una aplicación web completa, compleja y profesional sin hacer una sola petición Ajax.

Pero Ajax mejora el rendimiento y la experiencia del usuario. Puedes sustituir unas pocas peticiones convencionales por peticiones Ajax sin cambiar demasiado en tu aplicación. Por ejemplo, para borrar un recurso, puedes lanzar la petición DESTROY por Ajax y actualizar tu vista para eliminar el recurso del documento HTML cuando el servidor responda.

Esto es fácil de hacer. Y muy recomendable. Te aconsejo empezar a trastear con Ajax de este modo.

### 7.1.3. Y, sin embargo, Ajax ha cambiado la forma en la que desarrollamos aplicaciones web

Como algo que, en realidad, no sirve para nada ha logrado cambiar la forma en la que desarrollamos aplicaciones web puede parecer un misterio a simple vista, pero existe una razón muy simple para ello:

La mayoría de las aplicaciones web se pasan todo el tiempo haciendo lo mismo: accediendo a recursos de una base de datos para consultarlos, crearlos, modificarlos o borrarlos, todo ello mediante un interfaces de usuario básicamente semejantes. Es decir, el interfaz de usuario para crear, modificar y borrar productos de una base de datos es prácticamente el mismo que el que se usa para crear, modificar y borrar proveedores, por decir algo.

Así que alguien se preguntó: ¿por qué estamos programando todo el tiempo lo mismo?

Ajax nos permite hacer algo muy ingenioso para evitar este engorro: diseñar un interfaz de usuario genérico y vacío, solo compuesto por contenedores preparados para nutrirse de datos del servidor.

Por ejemplo, podemos diseñar un típico interfaz de usuario HTML que nos muestre una lista de recursos (productos, proveedores, o lo que sea) junto con los botones de "Update" y "Delete", además de un botón de "Add new". Pero ese interfaz estará vacío, y mediante Ajax lo cargaremos con productos, con proveedores o con lo que necesitemos. Crearemos el interfaz una vez y lo podemos reutilizar miles de veces, para todo tipo de recursos.

Este tipo de aplicaciones, también llamadas **SPA (Single-page applications)**, necesitan una arquitectura algo distinta de la que usamos en las aplicaciones web tradicionales, además de una librería en el lado del cliente para ayudarnos en la creación de contenedores genéricos (librerías como **Angular**, **React** o **Vue.js**). Aunque excede a nuestros propósitos profundizar en estas librerías, hemos visto algunos fundamentos sobre el uso de Vue.js con Laravel en el capítulo dedicado a Laravel. Consútalo si quieres profundizar en esta forma de uso masivo de Ajax.

En lo que sigue de este capítulo, utilizaremos Ajax de forma puntual en el entorno de una aplicación web convencional con arquitectura MVC.

## 7.2. Cómo enviar peticiones Ajax al servidor

### 7.2.1. Peticiones sin datos al servidor

La forma más sencilla (y primitiva) de usar Ajax es lanzar una petición asíncrona al servidor sin que el usuario de la web se percate de ello (porque se hará en segundo plano). El servidor no sabrá si la petición se lanzó en primer o en segundo plano y, en realidad, no le importa: él se limitará a atender la petición.

Para lanzar una petición mediante Ajax usando JavaScript tradicional (luego veremos cómo hacerlo con jQuery, que simplifica bastante el proceso), necesitamos crear un objeto de tipo XMLHttpRequest. Este objeto nos permitirá controlar todo el proceso de envío de la petición, recepción de la posible respuesta y control de los errores que hayan podido ocurrir.

Observa detenidamente este fragmento de código JavaScript:

```javascript
peticion_http = new XMLHttpRequest();
peticion_http.onreadystatechange = procesa_respuesta;
peticion_http.open('GET', 'http://servidor/recurso');
peticion_http.send(null);


function procesa_respuesta() {
    if(peticion_http.readyState == 4) {
      if(peticion_http.status == 200) {
        alert(peticion_http.responseText);
      }
    }
}
```

En las cuatro primeras líneas se crea el objeto de tipo XMLHttpRequest y luego se hacen tres cosas clave con él:
1. Se le indica qué función se debe ejecutar cuando el servidor responda. Recuerda que esta función se ejecutará también en segundo plano, sin que el usuario de la página se percate de que está sucediendo algo.
2. Se le indica qué recurso del servidor se quiere invocar (típicamente, una URL). Para ello se usa el método open(). Ahí también se indica el método de envío de datos al servidor (GET o POST), incluso si no se envían datos al servidor en absoluto, como en este ejemplo.
3. Por último, se lanza la petición al servidor con el método send(). El argumento "null" debe sustituirse por los datos que se envían al servidor mediante GET en caso de que los hubiera.

Eso deja lista la petición. JavaScript permanecerá a la escucha en segundo plano hasta que el servidor responda. Cuando lo haga, se ejecutará la función procesa_respuesta().

En esa función se hacen tres cosas muy importantes:
XXX

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




