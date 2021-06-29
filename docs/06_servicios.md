---
layout: page
title: 6 Servicios web
permalink: /servicios-web/
parent: Desarrollo Web en Entorno Servidor
nav_order: 6
---
# 6. Servicios web

## 6.1. ¿Qué es un servicio web?

Como dijimos al estudiar el patrón MVC, esta arquitectura no es la única manera de plantear las aplicaciones web. En este tema vamos a hablar de otra manera en la que las aplicaciones web funcionan muy frecuentemente: como simples servicios.

### 6.1.1. Una definición de servicio web

Un **servicio web** es una forma de permitir que una aplicación cliente y una aplicación servidor se comuniquen entre sí e intercambien información independientemente de la plataforma en la que cada una se ejecute.

Los mensajes que las aplicaciones se intercambiar generalmente tienen formato XML o JSON.

Hay dos estándares principales en la industria para implementar servicios web: **SOAP** y **REST**.

### 6.1.2. Diferencias entre servicios web y aplicaciones web

Llegados a este punto, puede que estés pensando: "Vale, pero ¿en qué se diferencia todo esto de una aplicación web MVC? ¿No intercambian también el cliente y el servidor información independientemente de la plataforma en la que se ejecuta cada uno?".

Pues sí, pero hay algunas **diferencias fundamentales entre un servicio web y una aplicación web**:

* Una aplicación web está diseñada para que un ser humano interactúe con ella a través de un interfaz DHTML. Un servicio web, en cambio, está pensado para que lo use otra aplicación (el cliente), no un ser humano.
* Por ese motivo, los servicios web carecen de interfaz de usuario y no produce salidas HTML legibles. Es decir, un servicio web **no tiene vistas**.
* En cambio, los servicios web suelen producir salidas XML o JSON, pensadas para que los clientes las procesen. Una aplicación web solo hace esto cuando responde a una petición Ajax, algo que veremos más adelante.

Por lo demás, un servicio web puede tener una arquitectura *aproximadamente* MVC, y digo *aproximadamente* porque el servicio web, como acabo de contarte, carece de vistas. Pero puede seguir conservando sus controladores y sus modelos. Los controladores se encargarán de convertir los datos de los modelos a JSON o XML y devolverlos al cliente.

## 6.2. SOAP

**SOAP (Single Object Access Protocol)** es un mecanismo estandarizado para la implementación, descripción y publicación de servicios en red.

SOAP establece el modo en el que deben comportarse el cliente y el servidor para hablar entre sí, así como la forma en la que el servidor debe dar a conocer sus servicios.

Es un mecanismo orientado al proceso, a diferencia de REST, que está orientado a los datos y que veremos después.

### 6.2.1. La pila de protocolos de SOAP

El estándar SOAP define una serie de protocolos de niveles de abstracción crecientes. Esta colección de protocolos suele denominarse **pila de protocolos SOAP**, y son los siguientes:

XXX imagen

Vamos a explicar brevemente en qué consiste cada protocolo de la pila, y lo vamos a hacer, como en otras ocasiones, por medio de un ejemplo en lugar de perdernos en largas y farragosas explicaciones.

### 6.2.2. Los protocolos SOAP y WSDL

Para ver cómo funciona el protocolo SOAP (el más importante de la pila de protocolos SOAP, como ya te habrás imaginado por su nombre), utilizaremos tres ejemplos:

* En el primero, veremos cómo construir un servidor que duelva colecciones de datos en forma de array.
* En el segundo, veremos cómo puede un servidor devolver datos con estructura más compleja formateados con JSON.
* En el tercero, veremos un servidor extremadamente simple con un fichero WSDL.

#### Ejemplo 1: Consulta de una BD de marcas y modelos de coches.

Vamos a programar un servicio web muy sencillo capaz de servir a los clientes que nos lo pidan un listado de las marcas de coches que existen y otro con los modelos registrados que pertenecen a una marca en concreto.

El servidor, por lo tanto, necesita dos funciones:

* ObtenerMarcas
* ObtenerModelos($marca)

El cliente, como es lógico, debe conocer cómo utilizar el servidor. Esto puede hacerse mediante el protocolo WSDL (que ya veremos un poco después) por otras vías más tradicionales: documentación de la API, guía del desarrollador, manual de usuario...

En estos ejemplos, tanto el servidor como el cliente estarán escritos en PHP. Por supuesto, puede usarse cualquier otro lenguaje para ello, en particular en el lado del cliente. Para saber cómo hacer un cliente SOAP en otros lenguajes, consulta la documentación de tu lenguaje preferido.

**En el lado del servidor** necesitaremos crear un objeto de tipo SoapServer y definir los métodos a los que el servidor va a responder.

Vamos a empezar por los métodos. Crearemos un fichero (por ejemplo, llamado **GestionAutomoviles.class.php**) en cuyo interior escribiremos una clase con los métodos que necesitemos. Para nuestro ejemplo de marcas y modelos de coches, podrías ser algo así:

El servidor se crea con una clase que contenga los métodos necesarios:

```php
class GestionAutomoviles
{
  public function ObtenerMarcas()
    {
      $db = new mysqli(<datos-de-la-conexión>);

      $marcas = array();
      if( $db )
      {
        $result = $db->query('select id, marca from marcas');
        while( $row = $result->fetch_array() )
          $marcas[$row['id']] = $row['marca'];
        $db->close();
      }

      return $marcas;
    }
    
    public function ObtenerModelos($marca)
    {		
      $db = new mysqli(<datos-de-la-conexión>);
      $marca = intVal($marca);
      $modelos = array();

      if( $marca !== 0 )
      {
        $result = $db->query('select id, modelo from modelos
                                where marca = ' . $marca );
        while( $row = $result->fetch_array() )
            $modelos[$row['id']] = $row['modelo'];
      }
      $db->close();
      return $modelos;
    }}
```

Ahora, en otro archivo aparte, que llamaremos, por ejemplo, *webservice.php*, *registramos el servicio* usando la clase SoapServer de PHP y asignándole la clase anterior GestionAutomoviles. Así:

```php
<?php
   include 'GestionAutomoviles.class.php';
   $soap = new SoapServer(null, array('uri' => 'http://localhost/'));
   $soap->setClass('GestionAutomoviles');
   $soap->handle();
?>
```

El constructor de SoapServer tiene dos argumentos:
* El fichero WSDL donde se describe el servicio. Como aún no vamos a usar fichero WSDL, ese argumento lo dejaremos, de momento, a null.
* La URL donde el servidor va a estar escuchando. Puede ser el directorio raíz de nuestro servidor o cualquier subdirectorio o archivo.

Por último, y para comprobar que nuestro servidor SOAP funciona bien, necesitamos crear un secillo cliente que consuma ese servicio. Como hemos dicho antes, esta parte también la vamos a programar en PHP, aunque podría hacerse en cualquier otro lenguaje con soporte SOAP.

**En la parte cliente**, necesitamos crear un objeto de tipo SoapClient:

```php
$soapS = new SoapServer(null, "URI del servidor");
```

Nuevamente, el primer argumento del constructor es el fichero WSDL. Como aún no trabajamos con ellos, lo dejamos a null. Si tuviéramos fichero WSDL, no necesitaríamos indicar la URI del servidor, porque el propio fichero WSDL lo establecería de forma inequívoca.

Una vez hecho eso, podemos consumir los servicios del cliente. Por ejemplo: 

```php
<?php
   $client = new SoapClient(null, array('uri' => 'http://localhost/',
       'location' => 'http://localhost/<ruta>/webservice.php'));
   $marcas = $client->ObtenerMarcas();
   foreach($marcas as $key => $value )
      echo $value;   
?>
```

Observa cómo hemos indicado la localización del servidor: en un array, indicamos su ubicación y la ruta de acceso al fichero que maneja el servicio (en nuestro ejemplo, webservice.php).

#### Ejemplo 2: Lista de libros de una biblioteca.

El ejemplo anterior funciona porque tanto cliente como servidor trabajan en PHP. Pero si el cliente no fuera PHP, podría tener problemas al recibir los datos de respuesta del servidor, que son arrays PHP.

Lo más adecuado cuando se responden datos complejos es enviarlos en algún formato de intercambio de información, como XML o JSON.

En este nuevo ejemplo, vamos a crear un servidor que nos devuelva la lista de libros de una biblioteca (lo que incluirá el id, el título y el ISBN de cada libro) empaquetada en un string JSON.

De momento, tampoco usaremos WSDL (fichero de descripción del servicio).

**Servidor** (archivo *libros.class.php*):

```php
class libros
{
      private function getLibrosJSON()
      {
         $sql = "SELECT * FROM libros";
         $db = new dbAbstract();  // Suponemos que existe una capa
                                  // de abstracción de datos
         return json_encode($db->consulta($sql));
     }
     ...aquí irían más métodos que pudiera tener el servidor
}
     
     
Registramos el servidor en otro archivo (que llamaremos *libros.server.php*):

```php
<?php
   include 'libros.class.php';
   $soap = new SoapServer(null, array('uri' => 'http://localhost/'));
   $soap->setClass('libros');
   $soap->handle();
?>
```

**Cliente**

De nuevo, lo vamos a crear en PHP, aunque no sea lo más habitual. Al ser un programa PHP, tendrás que ejecutarlo contra un servidor web, o bien directamente desde la línea de comandos. 

```php
<?php
   $client = new SoapClient(null, array('uri' => 'http://localhost/',
       'location' => 'http://localhost/libros.server.php'));
   $listaLibros = $libros->getLibrosJSON();
?>
```

A partir de ahí, el cliente dispondrá en $listaLibros de la información recibida del servidor (id, titulo, isbn de todos los libros) empaquetada en formato JSON.

#### Ejemplo 3: Servicio de calculadora

Este será un servicio mucho más simple y hasta un poco tontorrón, pero no te lo tomes a mal: solo es un ejemplo.

El servicio simple y tontorrón proporcionará dos métodos:

* sumar (op1, op2) --> Devuelve la suma de op1 y op2
* restar (op1, op2) --> Devuelve la diferencia entre op1 y op2

Ahora sí usaremos WSDL para definir el servicio y que los clientes sepan cómo usarlo. Así, a través de un ejemplo simple (y tontorrón) podrás conocer cuál es la estructura de estos ficheros.

**Servidor**

El código del servidor es extremadamente simple. Fíjate en que ahora, el crear el objeto SoapServer, sí indicamos el archivo WSDL:

```php
<?php
   $server = new SoapServer("aritmetica.wsdl");
 
   function sumar($operando1,$operando2){
      return $operando1+$operando2;
   }
 
   function restar($operando1,$operando2){
      return $operando1-$operando2;
   }
 
   $server->AddFunction("sumar");
   $server->AddFunction("restar");
   $server->handle();
?>
```

**Cliente**

```php
<?php
 $clienteSOAP =
   new SoapClient('http://ejemplo.com/test/wsdl/aritmetica.wsdl');
 
 $resultado_suma = $clienteSOAP->sumar(2.7, 3.5);
 $resultado_resta = $clienteSOAP->restar(2.7, 3.5);
 
 echo "la suma de 2.7 mas 3.5 es: " . $resultado_suma . "<br/>";
 echo "la diferencia de 2.7 menos 3.5 es: " . $resultado_resta . "<br/>";
?>
```

**Documento WSDL**

El documento WSDL es un archivo de texto alojado en el servidor donde se describen todos los aspectos del servicio:

* Los mensajes que se pueden intercambiar entre el cliente y el servidor.
* Los argumentos y tipos de datos de esos mensajes.
* Las operaciones y sus tipos
* Las rutas donde puede encontrarse el servidor

Se trata de un documento en formato XML que resulta bastante farragoso de leer, así que tómatelo con calma (ahora entiendes por qué hemos elegido un servicio tan simple como el de este ejemplo para ver su archivo WSDL: si usáramos un servicio más realista, el archivo resultaría un monstruo de miles de líneas). Aquí lo tienes:

```xml
  <message name="AritmeticaPeticion">
    <part name="operando1" type="xsd:float" />
    <part name="operando2" type="xsd:float" />
  </message>
 
  <message name="AritmeticaRespuesta">
    <part name="respuesta" type="xsd:float" />
  </message>

  <portType name="AritmeticaPort">
    <operation name="sumar">
      <input message="tns:AritmeticaPeticion" />
      <output message="tns:AritmeticaRespuesta" />
    </operation>
    <operation name="restar">
      <input message="tns:AritmeticaPeticion" />
      <output message="tns:AritmeticaRespuesta" />
    </operation>
  </portType>

  <binding name="AritmeticaBinding" type="tns:AritmeticaPort">
    <soap:binding style="rpc" />
    <operation name="sumar">
        <soap:operation soapAction="urn:Aritmetica#sumar" />
        <input>
          <soap:body use="encoded" namespace="urn:Aritmetica" />
        </input>
        <output>
          <soap:body use="encoded" namespace="urn:Aritmetica" />
        </output>
    </operation>
    <operation name="restar">
        <soap:operation soapAction="urn:Aritmetica#restar" />
        <input>
          <soap:body use="encoded" namespace="urn:Aritmetica"/>            		</input>
       <output>
          <soap:body use="encoded" namespace="urn:Aritmetica"/>                   </output>
    </operation>
  </binding>
  
  <service name="AritmeticaServicio">
    <port name="AritmeticaPort" binding="tns:AritmeticaBinding">
      <soap:address location="http://ejemplo.com/test/wsdl/aritmetica_server.php" />
    </port>
  </service>
```

Escribir los documentos WSDL a mano es casi imposible. Y hacerlo sin cometer errores, es imposible del todo. Para eso existen herramientas automatizadas que toman el archivo con la clase que contiene los métodos del servicio y generan automáticamente el archivo WSDL.

Puedes encontrar estas herramientas de creación automática del archivo WSDL en cualquier IDE avanzado (como Netbeans o Eclipse) y también en mucho sitios web.

Por lo tanto, no es un documento que vayas a tener que redactar tú, ni siquiera que leer tú: se trata de una descripción del servicio escrita por y para programas informáticos. Por eso no tiene un formato demasiado legible para un humano.
  
### 6.2.3. UDDI

Este protocolo, que también forma parte de la pila SOAP, es mucho más fácil de explicar.

La explicación es esta: olvídate de él. Fin.

Ha sido fácil, ¿no?

Por si esta explicación necesita alguna aclaración adicional, te cuento que UDDI fue un intento de la industria por estandarizar repositorios de servicios, de manera que cualquier cliente pudiera lanzar una petición a la red para descubrirlos y usarlos.

Imagina que tienes una web que necesita conocer la previsión del tiempo en una zona, la que sea. Puedes localizar un servicio web que te proporcione esa información (ya sea de forma gratuita o mediante una suscripción, eso es irrelevante). Hay, de hecho, muchos servidores que ofrecen este servicio, empezando por el de la Agencia Estatal de Meteorología.

Para usar ese servicio, tienes que conocer el servidor que lo ofrece y luego bucear en su API para avieriguar cómo narices debes pedirle la información y en qué formato te la va a devolver. Y, una vez hecho eso, ya estás listo para programar tu cliente y consumir ese servicio.

Pues bien: el servicio UDDI buscaba implementar una manera para que el servidor publicara el tipo de servicio que está ofertando y los clientes pudieran escanear la red en busca de esos servicios, para luego seleccionar uno y lanzar peticiones contra él, todo ello de forma más o menos transparente al programador.

Era una idea interesante, ¿verdad? Pero murió hace mucho. De hecho, entró en punto muerto en el año 2006, cuando Microsoft e IBM decidieron abandonarlo.

Así que, lo dicho: aunque en teoría el protocolo UDDI forma parte de la pila SOAP, puedes actuar como si no existiera.

## 6.3. REST

XXX

¿Qué es REST?
REST (Representational State Transfer) es un mecanismo de intercambio de información entre clientes y servidores de una red.
A diferencia de SOAP, está orientado a los datos, esto eso, proporciona siempre los mismos tipos de acceso a los recursos, sin posibilidad de definir nuevas operaciones.
Por esa razón se dice que REST está orientado a los datos mientras que SOAP está orientado a los procesos.

Las 7 operaciones REST
Un servidor REST (también llamado RESTful) debe implementar estas siete operaciones de acceso a cada tipo de recurso:

XXX lista operaciones

REST vs SOAP
SOAP es más flexible: permite definir nuevas operaciones sobre los recursos, mientras que REST está limitado a las 7 operaciones predefinidas.
REST es mucho más sencillo de usar e implementar: las operaciones son bien conocidas y no es necesario describirlas (WSDL) ni publicarlas de ningún modo.
Para la mayor parte de las aplicaciones, REST es más que suficiente, y de ahí su mayor implantación en la actualidad.

Cómo implementar un servidor RESTful
Para implementar un servidor RESTful, basta con:
Crear una arquitectura MVC para los recursos/datos que deseemos servir.
Con Laravel, esto se puede conseguir con el comando:
$ php artisan make:controller --resource <controlador>
En lugar de mostrar los recursos en una vista, los mostraremos mediante JSON con un sencillo echo. (Recuerda que esa salida la recibirá el cliente, no un ser humano)

Es importante respetar los nombres de las peticiones HTTP, así como los verbos (GET, POST, etc), puesto que serán los que el cliente utilice.



