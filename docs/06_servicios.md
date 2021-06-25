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

### 6.2.2. El protocolo SOAP

#### Ejemplo 1: Consulta de una BD de marcas y modelos de coches.

Vamos a programar un servicio web muy sencillo capaz de servir a los clientes que nos lo pidan un listado de las marcas de coches que existen y otro con los modelos registrados que pertenecen a una marca en concreto.

El servidor, por lo tanto, necesita dos funciones:

* ObtenerMarcas
* ObtenerModelos($marca)

El cliente, como es lógico, debe conocer cómo utilizar el servidor. Esto puede hacerse mediante el protocolo WSDL (que ya veremos un poco después) por otras vías más tradicionales: documentación de la API, guía del desarrollador, manual de usuario...

En estos ejemplos, tanto el servidor como el cliente estarán escritos en PHP. Por supuesto, puede usarse cualquier otro lenguaje para ello, en particular en el lado del cliente. Para saber cómo hacer un cliente SOAP en otros lenguajes, consulta la documentación de tu lenguaje preferido.

Pues bien, **en el lado del servidor** necesitaremos crear un objeto de tipo SoapServer:

```php
$soapS = new SoapServer("fichero WSDL");
```

Como aún no vamos a usar fichero WSDL XXX



Para crear un cliente
$soapC = new SoapClient(“fichero WSDL”);
Si no tenemos WSDL:
$soapS = new SoapServer(null, “URI del servidor”);
$soapC = new SoapClient(null, “URI del servidor y del servicio”);


El servidor se crea con una clase que contenga los métodos necesarios:

class GestionAutomoviles
{
  public function ObtenerMarcas()
  {
    ....
    return $marcas;
  }

  public function ObtenerModelos($marca)
  {		
    ....
    return $modelos;
  }
}


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
  }
  
  
  Ahora registramos el servicio usando la clase SoapServer de PHP, y asignándole la clase anterior:

<?php
   include 'GestionAutomoviles.class.php';
   $soap = new SoapServer(null, array('uri' => 'http://localhost/'));
   $soap->setClass('GestionAutomoviles');
   $soap->handle();
?>

A este archivo lo llamaremos webservice.php


Un cliente PHP puede usar ahora el servicio así:

<?php
   $client = new SoapClient(null, array('uri' => 'http://localhost/',
       'location' => 'http://localhost/<ruta>/webservice.php'));
   $marcas = $client->ObtenerMarcas();
   foreach($marcas as $key => $value )
      echo $value;   
?>






Ejemplo 2: Un servicio que devolverá una lista de libros de una biblioteca.
Empaquetaremos el id, el título y el ISBN con JSON:
Es más ligero que XML
Y más sencillo de crear y procesar
Tampoco usaremos WSDL (descripción del servicio).

Creamos el servidor (archivo libros.class.php):

class libros
{
      private function getLibrosJSON()
      {
         $sql = "SELECT l.* ";  
         $sql .= " FROM libros AS l ";
         $db = new dbAbstract();  // Suponemos que existe una capa
                                  // de abstracción de datos
         return json_encode($db->consulta($sql));
     }
     
     
     Registramos el servidor (archivo libros.server.php):

<?php
   include 'libros.class.php';
   $soap = new SoapServer(null, array('uri' => 'http://localhost/'));
   $soap->setClass('libros');
   $soap->handle();
?>


Creamos un cliente:

<?php
   $client = new SoapClient(null, array('uri' => 'http://localhost/',
       'location' => 'http://localhost/.../libros.server.php'));
   $listaLibros = $libros->getLibrosJSON();
?>

Ahora el cliente dispone en $listaLibros de información con estructura compleja recibida del servidor (id, titulo, isbn) y empaquetada en formato JSON.





Ejemplo 3: Servicio de alculadora
El servicio proporcionará dos funciones: 
sumar (op1, op2)
restar (op1, op2)
Ahora sí usaremos WSDL para definir el servicio y que los clientes sepan cómo usarlo.

Código del sevidor
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

Código del cliente
<?php
 $clienteSOAP =
   new SoapClient('http://ejemplo.com/test/wsdl/aritmetica.wsdl');
 
 $resultado_suma = $clienteSOAP->sumar(2.7, 3.5);
 $resultado_resta = $clienteSOAP->restar(2.7, 3.5);
 
 echo "la suma de 2.7 mas 3.5 es: " . $resultado_suma . "<br/>";
 echo "la diferencia de 2.7 menos 3.5 es: " . $resultado_resta . "<br/>";
?>

Documento WSDL: mensajes
  <message name="AritmeticaPeticion">
    <part name="operando1" type="xsd:float" />
    <part name="operando2" type="xsd:float" />
  </message>
 
  <message name="AritmeticaRespuesta">
    <part name="respuesta" type="xsd:float" />
  </message>

Documento WSDL: operaciones
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

Documento WSDL: enlaces
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
  
  Documento WSDL: servicio
  <service name="AritmeticaServicio">
    <port name="AritmeticaPort" binding="tns:AritmeticaBinding">
      <soap:address location="http://ejemplo.com/test/wsdl/aritmetica_server.php" />
    </port>
  </service>
  
### UDDI

Es un intento de la industria por estandarizar repositorios de servicios, de manera que cualquier cliente pueda descubrirlos y usarlos.
Está en un punto muerto desde 2006, cuando Microsoft e IBM decidieron abandonarlo.


## REST

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



