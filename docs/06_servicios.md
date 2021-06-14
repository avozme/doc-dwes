---
layout: page
title: 6 Servicios web
permalink: /servicios-web/
parent: Desarrollo Web en Entorno Servidor
nav_order: 6
---
# 6. Servicios web

## 6.1. ¿Qué es un servicio web?

¿Qué es un servicio web?
Es una forma de permitir que las aplicaciones se comuniquen independientemente de la plataforma.
Las aplicaciones intercambian mensajes generalmente mediante XML o JSON.
Hay dos estándares principales en la industria para implementar servicios web: SOAP y REST.

Diferencia entre un servicio web y una aplicación web
Un servicio web está pensado para que lo use otra aplicación (el cliente), no un ser humano.
Por ese motivo, carece de interfaz de usuario y no produce salidas HTML legibles.
Los servicios web suelen producir salidas XML o JSON, pensadas para que los clientes las procesen.

## 6.2. SOAP

¿Qué es SOAP?
SOAP (Single Object Access Protocol) es un mecanismo para la implementación, descripción y publicación de servicios en red.
SOAP establece el modo en el que deben comportarse el cliente y el servidor para hablar entre sí, así como la forma en la que el servidor debe dar a conocer sus servicios.
Es un mecanismo orientado al proceso, a diferencia de REST, que está orientado a los datos.

La pila de protocolos de SOAP

XXX imagen

Ejemplo de intercambio de mensajes SOAP

XXX imagen



  
Ejemplo 1: Consulta de una BD de marcas y modelos de coches.
Existirán dos funciones:
ObtenerMarcas
ObtenerModelos($marca)
No usaremos fichero WSDL (descripción del servicio)
El cliente debe conocer cómo utilizar el servidor por otras vías más tradicionales: documentación de la API, guía del desarrollador, manual de usuario...

Objetos SoapServer y SoapClient:
Para crear un servidor:
$soapS = new SoapServer(“fichero WSDL”);
Para crear un cliente:
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



