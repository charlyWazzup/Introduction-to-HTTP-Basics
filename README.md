# HTTP (HyperText Transfer Protocol / Protocolo de transeferencia de Hypertexto)



#### Conceptos Básicos
* * * 





### Introducción
* * * 



## `La WEB`

Internet (o `La Web`) es un sistema masivo de información cliente/servidor distribuida como lo muestra el siguiente diagrama:

![Diagrama Internet](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/TheWeb.png)

Muchas aplicaciones son ejecutadas constantemente en la `WEB`, como lo son un _navegador web_, _correo electrónico_, _transferencia de archivos_, _transmición de audio y video_, etc. Para que exista una comunicación adecuada entre el `cliente` y el `servidor`, estas aplicaciones deben concordar en un protocolo específico como `HTTP`, `FTP`, `SMTP`, `POP`, etc.

## Protocolo de transferencia de HyperTexto (HTTP)

El `HTTP` es quizá el protocolo más popular utilizado en la _Internet_ (o la _WEB_).

* `HTTP` es un protocolo _asimetrico_ `solicitud/respuesta cliente/servidor` como se muestra en la siguiente imagen. Un cliente `HTTP` envia un mensaje de solicitud a servidor `HTTP`. Después, el servidor regresa un mensaje de respuesta. En otras palabras, `HTTP` es un protocolo `pull`. El cliente hace `pull` a la información de el servidor (en lugar de que el servidor haga `push` a la información que ira al cliente).

![Diagrama Solicitud/Respuesta](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP.png) 

* `HTTP` es un protocolo sin estado. En otras palabras, la solicitud actual no sabe lo que se ha hecho en solicitudes anteriores.

* `HTTP` permite la negociación de información y el tipo de representación de la misma, así pues, permite a los sistemas ser construidos independientemente de la información que ha sido transferida.

* Nota de _RFC2616_: `"El Protocolo de transferencia de Hypertexto (HTTP)` es un protocolo para los sistemas de información hypermedia, distrbuída y colaborativa. Es un protocolo genérico sin estado, el cual puede ser usado para varias tareas mas haya de su uso con el hypertexto, como por ejemplo, como nombre de servidores y sistemas distribuidos de manejo de objetos, extensión de metodos de solicitud, códigos de errores y cabeceras."

## Navegador

Cada vez que se introduce una URL desde nuestro navegador para obtener un recurso _WEB_ usando _HTTP_, por ejemplo, _http://nowhere123.com/index.html_, el navegador cambia la URL a un mensaje de solicitud y lo envia a un servidor _HTTP_. El servidor _HTTP_ interpreta el mensaje de solicitud y nos regresa un mensaje de respuesta, en el cual es el recurso que solicitamos o un mensaje de error. Este proceso se ilustra en la siguiente imagen:

![Diagrama Solicitud/Respuesta 2](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_Steps.png)

## Localizador Uniforme de Recursos (URL)

Una `URL` (Uniform Resource Locator / Localizador Uniforme de Recursos) es usado para identificar de forma exclusiva un recurso sobre la _WEB_. Las URL tienen la siguiente sintaxis: 

	protocol://hostname:port/path/and/file/name (protocolo://nombreDelHost/puerto/ruta-y-nombre-del-archivo



Una URL contiene 4 partes:

1. _Protocolo_: El protocolo a nivel de aplicación usado por el cliente y el servidor, como por ejemplo HTTP, FTP y TELNET.
2. _Hostname/nombre del host_: El nombre del dominio `DNS` (ej. www.nowhere123.com) o la dirección `IP` (ej. 192.128.1.2) de el servidor.
3. _Port/puerto_: El numero del puerto `TCP` que el servidor esta a la espera para peticiones entrantes de los clientes.
4. _Path-and-file-name/Ruta-y-nombre-del-archivo_: El nombre y localización del recurso solicitado desde los documentos del directorio base del servidor.

Por ejemplo, en la _URL_ http://www.nowhere123.com/docs/index.html, el protocolo de comunicación es HTTP y el nombre del host es www.nowhere123.com. El número del puerto no esta especificado en la URL, asi que toma el número por defecto, el cual es el puerto TCP 80 para HTTP. La ruta y nombre del archivo de el recurso a localizar es /docs/index.html.

Otros ejemplos de URL son:
	ftp://ftp.org/docs/test.txt
	mailto:user@test01.com
	news:soc.culture.Singpore
	telnet://nowhere123.com/

## Protocolo HTTP

Como hemos mencionado, ingresamos una URL en la caja de direcciones del navegador. El navegador traduce la URL en un mensaje de petición de acuerdo al protocolo especificado y envia el mensaje de petición al servidor.

Por ejemplo, el navegador traduce la URL http:://nowhere123.com/doc/index.html en el siguiente mensaje de petición:

	GET /docs/index.html HTTP/1.1
	Host: www.nowhere123.com
	Accept: image/gif, image/jpeg, */*
	Accept-Languaje: en-us
	Accept-Encoding: gzip, deflate
	User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
	(blank line)

Cuando este mensaje de petición alcanza el servidor, este puede realizar una de las siguientes acciones:

1. El servidor interpreta la petición recivida, mapea la petición en un _archivo_ debajo de el directorio de documentos del servidor y regresa el archivo pedido al cliente.
2. El servidor interpreta la petición recivida, mapea la petición en un _programa_ almacenado en el servidor, ejecuta el programa y regresa la salida del programa al cliente.
3. Si la petición no puede ser resuelta, el servidor regresa un mensaje de error.

Un ejemplo de mensaje de respuesta HTTP seria:

	**HTTP/1.1 200 OK**
	Date: Sun, 18 Oct 2009 08:56:53 GMT
	Server: Apache/2.2.14 (Win32)
	Last-Modified: Sat, 20 Nov 2004 07:16:26 GMT
	ETag: "10000000565a5-2c-3e94b66c2e680"
	Accept-Length: 44
	Connection: Close
	**Content-Type: text/html**
	X-Pad: avoid browser bug

	**<html><body><h1>It works!</h1></body></html>**

El navegador recive el mensaje de respuesta, interpreta el mensaje y muestra el contenido del mensaje en la ventana del navegador de acuerdo al tipo de contenido de la respuesta (como en _Content-Type_ respuesta de cabecera). El tipo de contenido mas común incluye "text/plain", "text/html", "image/jgep", "audio/mpeg", "video/mpeg", "application/msword" y "application/pdf".

En su estado vacio, un servidor HTTP no hace nada mas que esperar la dirección IP y el puerto especificado en la configuración de la petición entrante. Cuando una petición llega, el servidor analiza el mensaje de cabecera, aplica las reglas especificas de la configuración y toma acciones apropiadas. El control principal del Webmaster sobre el servidor web es mediante la configuración, la cual dera tratada con mas detalles en las siguientes secciones.

## HTTP Sobre TCP/IP

HTTP es un protocolo a nivel aplicación cliente-servidor. Normalmente corre sobre una conexión TCP/IP, como se ilustra en la siguiente imagen. (El HTTP no necesita correr en TCP/IP. Es solo un transporte de confianza. Cualquier protocolo de transporte que provea tal seguridad puede ser utilizado.)

![ISO OSI 7-layer network Image](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_OverTCPIP.png)

El TCP/IP (Transmission Control Protocol/Internet Protocol - Protocolo de control de transmición/ Protocolo de Internet) es un set de transporte de protocolos de maquinas para comunicarse unas con otras a través de la Net.

El IP (Internet Protocol/ Protocolo de Internet) es un protocolo de capa de red, trata con la direccion de la red y el routing. En una IP de red, cada maquina es asignada con una unica dirección de IP (ej. 165.1.2.3), y el software responsable para en enrutamiento del mensaje desde la IP de origen a la IP de destino. En la IPv4, la dirección IP consiste en 4 bytes, cada uno con rango de 0 a 255, separado por puntos, los cuales son llamados _quad-dotted form_. Este esquema soporta direcciones 4G en la red. La última IPv6 soporta mas direcciónes. Desde que memorizar el numero es dificil para mucha gente, un dominio con nombre, como www.nowhere123.com es usado en su lugar. El DNS (Domain Name Service /Servicio de nombre de dominio) traduce el nombre del dominio en la dirección IP. Una dirección IP especial 127.0.0.1 siempre referencia hacia nuestra propia máquina. Su nombre de dominio es "local host" y puede ser usada para testeo local.

El TCP es un protocolo de transferencia de capas, responsable de establecer una conexión entre dosmaquinas. El TCP consiste de 2 procolos: el TCP y el UDP (User Datagram Prackage). En el TCP, cada paquete tiene una secuencia de números y un conocimiento esperado. Un paquete sea retransmitido si no fue recibido. Un paquete enviado es garantizado en el TCP. UDP no garantiza la entrega del paquete. De cualquier manera, el UDP tiene menos sobrecalentamiento de red y puede ser utilizado para aplicaciones como transmición de audio y video.

Para cada IP, el TCP soporta hasta 65536 puertos, de el numero 0 al 65535. Una aplicación, como HTTP o FTP corre en un puerto particular de solicitudes entrantes. Del puerto 0 al 1023 son pre-asignados a protocolos populares, por ejemplo el HTTP al 80, el FTP al 21, Telnet al 23, etc.

Aunque para el TCP el puerto 80 esta preasignado a HTTP como puerto por default, no esta prohibido correr un servidor HTTP en otro puerto no asignado, especialmente para testear el servidor. También se pueden correr múltiples servidores HTTP en la misma maquina con diferentes números de puerto. Cuando un cliente solicita una URL sin un número de puerto especifico, el navegador  conectara al puerto por default, el 80.

## Especificaciónes del HTTP

Las especificaciónes del HTTP son ofrecidas por la W3C (World-wide Web Consortium). Existen dos versiones de HTTP actualmente, nombradas HTTP/1.0 y HTTP/1.1. La versión original, la HTTP/0.9 (1991), escrita por Tim Berners-Lee, es un protocolo simple para transferir datos brutos a través de Internet. El HTTP/1.0 (1996) permitía los mensajes MIME. El HTTP/1.0 no direcciona los problemas de los proxies, host virtuales, conección persistente y descarga de rango. Esto fue implementado en el HTTP/1.1 (1999).


## Servidor HTTP Apache o Servidor Tomcat Apache

Un servidor HTTP es necesario para estudiar el protocolo HTTP. El servidor Apache HTTP es popular en los servidores de producción de las industrias, producido por la Apache Software Foundation (ASF). ASF es una fundación de software open-source. El servidor Apache HTTP es gratuito con código fuente.

El primer servidor HTTP fué escrito por Tim Berners Lee en el CERN (European Center for Nuclear Reserach), que a su vez invento el HTML. Apache fue creado en la NCSA (National Center for Supercomputing Application). Probablemente Apache tomo su nombre de que consiste de código original más algunos parches, o por el nombre de las tribus Nativas Americanas.

## Mensajes de petición y respuesta en HTTP

Tanto el cliente como el servidor HTTP se comunican enviandose mensajes. El cliente envia un mensae de petición a el servidor. El servidor responde con un mensaje de respuesta.

Un mensaje HTTP consiste de un mensaje de cabecera y un cuerpo de mensaje opcional separados por una linea en blanco, como se ilustra a continuación:

![HTTP Messages Image](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_MessageFormat.png)

#### Mensaje de petición HTTP

El formato de un mensaje de petición HTTP es como se ilustra a continuación:

![HTTP Request Message](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_RequestMessage.png)

##### Linea de petición

La primer linea de la cabecera es llamada Linea de petición. Tiene la siguiente sintaxis:

	request-method-name request-URL HTTP-version

* request-method-name: El protocolo HTTP define un set de métodos de petición, por ejeplo _GET_, _POST_, _HEAD_, y _OPTIONS_.El cliente puede usar uno de estos métodos para enviar una petición al servidor.

* request-URL: Especifica el recurso solicitado.

* HTTP-version: Las versiones HTTP/1.0 y HTTP/1.1

Algúnos ejemplos de Lineas de petición: 

	GET /test.html HTTP/1.1
	HEAD /query.html HTTP/1.0
	POST /index.html HTTP/1.1

##### Cabeceras de petición

Las cabeceras de petición vienen en forma de pares de valores. Multiples valores, separados por comas, por ejemplo:
	
	request-header-name: request-header-value1, request-header-value2, ...

Ejemplos de cabeceras de petición:

	Host: www.xyz.com
	Connection: Keep-Alive
	Accept: image/gif, image/jpeg, */*
	Accept-Languaje: us-en, fr, cn


##### Ejemplo

El siguiente ejemplo muestra un mensaje de petición HTTP :

![REQUEST MESSAGE IMAGE](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_RequestMessageExample.png)

#### Mensaje de respuesta HTTP

El formato de un mensaje de respuesta HTTP es el siguiente:

![RESPONSE MESSAGE IMAGE](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_ResponseMessage.png)

##### Linea de Estatus

La primera linea es llamada Linea de estatus. Tiene la siguiente sintaxis:

	HTTP-version status-code reason-phrase

* HTTP-version: La versión de HTTP usada en esa sesión. La HTTP/1.0 o la HTTP/1.1.

* status-code: un número de 3 dígitos generado por el servdor como reflejo de una petición externa.

* reason-phrase: da una breve explicación de el código de estatus.

* Códigos de estatus comunes son por ejemplo "200 OK" , "404 Not Found", "403 Forbidden", "500 Internal Server Error"

Ejemplos de lineas de estatus: 

	HTTP/1.1 200 OK
	HTTP/1.0 404 Not Found
	HTTP/1.1 403 Forbidden

#### Cabeceras de respuesta

Las cabeceras de respuesta vienen en pares de valores:

	response-header-name: response-header-value1, responde-header-value2,...

Ejemplos de cabeceras de respuesta:

	Content-Type: text/html
	Content-Length: 35
	Connection: Keep-Alive
	Keep-Alive: timeout=15, max=100

El cuerpo del mensaje de respuesta contiene la información solicitada.

##### Ejemplo

La siguiente imagen muestra un mensaje de respuesta:

![RESPONSE MESSAGE EXAMPLE IMAGE](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_ResponseMessageExample.png)

### HTTP Request Methods

El protocolo HTTP define un set de metodos de solicitud. El cliente puede usar uno de estos metodos para enviar un mensaje de solicitud a un servidor HTTP. Estos metodos son:

* GET: El cliente utiliza GET para pedir un recurso web de un servidor.

* HEAD: El cliente utiliza HEAD para pedir la cabecera que un comando GET obtendria. Desde que la cabecera contiene la fecha de moficicación, este puede ser usado para checar el cache local.

* POST: Usado para postear la información en el servidor web.

* PUT: Le pregunta al servidor sobre la información almacenada.

* DELETE: Le pregunta al servidor sobre la información borrada.

* TRACE: Le pide al servidor un diagnostico de las acciones que toma.

* OPTIONS: Le pide al servidor regresar la lista de metodos de solicitud que soporta.

* CONNECT: Es usado para decirle a un proxy que haga una conexion a algun otro host y de manera simple replicar el contenido pero sin enviarlo al cache. Esto es muy usado para hacer una conexion SSL a traves de un proxy.

### *GET* Request Method

GET es el metodo de peticion mas comun en HTTP. Un cliente puede utilizar el metodo GET para pedir una pieza de un recurso desde un servidor HTTP. Un mensaje  de solicitud GET tiene la siguiente sintaxis:

	GET request-URI HTTP-version
	(optional request headers)
	(blank line)
	(optional request body)

* La palabra clave GET debe ir en Mayúsculas.
* request-URI: especifica la ruta en donde se encuentra el recurso solicitado, el cual debe comenzar de la raíz "/" del directorio base del documento.
* HTTP-version: Ambas, HTTP/1.0 o la HTTP/1.1. Este cliente nefocia el protocolo que se usara en la sesion. Por ejemplo, el cliente puede solicitar usar el HTTP/1.1. Si el servidor no soporta HTTP/1.1, debe informar al cliente que debe utilizar HTTP/1.0.
* El cliente usa cabeceras de petición opcionales (tal como _Accept_, _Accept-Language_, etc.) para negociar con el servidor y pedir que envie el contenido. (ej., en el lenguaje que el cliente prefiera).
* La Peticion GET tiene un cuerpo opcionar, el cual contiene una cadena de texto.

### Solicitudes HTTP de prueba

Existen varias formas de probar una solicitud en HTTP. Podemos utilizar un programa como _"telnet"_ o _"hyperterm"_, o escribir en algun otro programa de red para enviar un mensaje a cecas a un servidor HTTP para probar las solicitudes.

##### Telnet

_Telnet_ es muy utilizado. Podemos usarlo para establecer una coneccion TCP con un servidor y enviar una solicitud HTTP. Por ejemplo, supongamos que hemos empezado un servidor HTTP en nuestro _localhost_ (dirección IP 127.0.0.1) en el puerto 8000:

	> **telnet**
	telnet> **help**
	... telnet help menu ...
	telnet> **open 127.0.0.1 8000**
	Connecting To 127.0.0.1...
	**GET /index.html HTTP/1.0**
	(Hit enter twice to send the terminating black line ...)
	... HTTP response message ...

Telnet es un protocolo basado en caracteres. Cada caracter que ingresamos en el cliente _telnet_ será enviado al servidor inmediatamente. Por lo tanto, no podemos provocar un error ortográfico ingresando un comando en bruto, como borrar y enviar un espacio en blanco al servidor. Debemos tener activado la opcion de "local echo" para ver los caracteres que ingresamos. Revisa el manual telnel para mas detalles sobre el uso de telnet.

##### Programa de Red

También podemos escribir nuestro propio programa de red para emitir solicitudes HTTP a un servidor HTTP. Nuestro programa de red debe primero establecer una conección TCP/IP con el servidor. Una vez que la conección TCP ha sido establecida, podemos emitir la solicitud en bruto.

Un ejemplo de un programa de red escrito en _Java_ se muestra a continuación (asumiendo que el servidor HTTP esta corriendo en el _localhost_ (dirección IP 127.0.0.1) en el puerto 8000):

	import java.net.*;
	import java.io.*;

	public class HttpClient{
		public static void main(String[] args) throws IOException {
			// The host and port to be connected.
			String host = 8000;
			// Create a TCP socket and connect to the host:port.
			Socket socket = new Socket(host, port);
			// Create the input and output streams for the network socket.
			BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStreams()));
			PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
			// Send request to the HTTP server.
			out.println("**GET /index.html HTTP/1.0**");
			out.println(); // blan line separating header & body
			out.flush(); // Read the response and display on console.
			String line; // ReadLine() returns null if server close the network socket.
			while((line = in.readLine()) != null) {
				System.out.println(line);
			}
			// Close the I/0 streams.
			in.close();
			out.close();
		}
	}

### HTTP/1.0 solicitud GET

El siguiente código muestra la respuesta de una solicitud GET en HTTP/1.0 (via telnet o en nuestro propio programa de red, asumiendo que el servidor HTTP esta funcionando):

	**GET /index.html HTTP/1.0**
	(enter twice to create a blank line)


	**HTTP/1.1 200 OK**
	Date: Sun, 18 Oct 2009 08:56:53 GMT
	Server: Apache/2.2.14 (Win32)
	Last-Modified: Sat, 20 Nov 2004 07:16:26 GMT
	ETag: "10000000565a5-2c-3e94b66c2e680"
	Accept-Ranges: bytes
	Content-Length: 44
	Connection: close
	Content-Type: text/html
	X-Pad: avoid browser bug

	<html><body><h1>It works!</h1></body></html>

	Connection to host lost.

En este ejemplo, el cliente emitio una solicitud GET a un documento llamado "_index.html_" y negocia el protocolo HTTP/1.0. Una linea en blanco despues de la cabecera es necesaria. Esta solicitud no contiene ningun cuerpo de mensaje.

El servido recibe el mensaje de solicitud, lo interpreta y mapea la _solicitud  URI_ a un documento debajo del directorio del documento. Si el documento solicitado esta disponible, el servidor regresa el documento con un mensaje de respuesta "_200 OK_". Las cabeceras de respuesta prveen la descripción necesaria de el documento regresado, como la ultima modificación (_Last-Modified_), el MIME type (Content-Type), y el tamaño del documento (Content-Length). El cuerpo de la resuesta contiene el documento solicitado. El navegador dara formato y mostara el documento de acuerdo al tipo que sea (ej. Texto plano, HTML, JPEG, GIF, etc) y además otra informacion obtenida desde las respuestas de las cabeceras.

Notas:

* El metodo "_GET_", distingue mayúsculas y minúsculas. Debe estar en mayúsculas.
* Si el nombre del metodo de solicitud es deletrado de manera erronea, el servidor regresara un mensaje de error "_501 Method Not Implemented_"
* Si el nombre del metodo no esta permitido, el servidor regresara un mensaje de error "_405 Method Not Allowed_". Ej., DELETE es un nombre valido, pero no puede ser implementado por el servidor.
* Si la solicitud _URI_ no existe, el servidor regresara un mensaje de error "404 Not Found". Debemos proporcionar una _request-URI_ apropiada, desde la raíz del documento "/". De otra manera, el servidor regresara "400 Bad Request".
* Si la versión de HTTP no es correcta, el servidor regresara "400 Bad Request".
* En HTTP/1.0, por default, el servidor cierra la conección TCP despues de entregar la respuesta. Si usamos _telnet_ para conecter al servidor, el mensaje "Connection to host lost" aparece inmediatamente despues de que el cuerpo de la respuesta es recibido. Podemos usar una cabecera opcional "_Connection: Keep-Alive_" para una conección persistente, asi la otra solicitud puede ser enviada a través de la misma conección TCP para mejorar la eficiencia de la red. Por el otro lado, HTTP/1.1 utiliza la conección _keep-alive_ por defecto.

### Código de los mensajes de estado

La primera linea del mensaje de respuesta contiene el código de estado, el cual es generado por el servidor para indicar que esta sucediendo.

El código de estado es un numero de 3 dígitos:

* 1xx (Informacional): Solicitud recibida, el servidor continuara con el proceso.
* 2xx (Éxito): La solicitud fue exitosamente recibida, entendida, aceptada y despachada.
* 3xx (Redirección): Alguna otra accion es necesaria para completar la solicitud.
* 4xx (Error del cliente): La solicitud tenía una sintaxis erronea o no puede ser entendida.
* 5xx (Error del servidor): El servidor fallo en cumplir una solicitud valida.

Algúnos de los códigos de estados más comunes son los siguientes:

* 100 Continue: El servidor recibio la solocitud y en el proceso dió una respuesta.
* 200 OK: La solicitud fue cumplida.
* 301 Move Permanently: El recurso solicitado ha sido permanentemente movido de lugar. La URL de la nueva locacion es proporcionada en la cabecera de respuesta y es llamada _Location_. El cliente debe emitir una nueva solicitud a la nueva locación. La aplicación debe actualizar todas las referencias a esta nueva locación.
* 302 Found & Redirect (or Move Temporarily): Al igual que la el 301, pero la nueva locacion es temporal. El cliente debe emitir una nueva solicitud, pero la aplicación no necesita actualizar las referencias.
* 304 Not Modified: En respuesta a la condicional _If-modified-Since_ del GET, el servidor notifica que el recurso solicitado no ha sido modificado.
* 400 Bad Request: El servidor no pudo interpretar o entender la solicitud, probablemente un error de sintaxis en el mensaje.
* 401 Authentication Required: El recurso solicitado esta protegido y requiere las credenciales del cliente (username/password). El cliente debe re-subir la solicitud con sus credenciales (username/password).
* 403 Forbidden: El servidor se reusa a proporcionar el recurso, independientemente de la identidad del cliente.
* 404 Not Found: El recurso solicitado no puede ser encontrado en el servidor.
* 405 Method Not Allowed: El metodo utilizado, POST, PUT o DELETE, es un metodo invalido. De cualquier manera, el servidor no permite ese metodo para el recurso solicitado.
* 408 Request Timeout.
* 414 Request URI too Large
* 500 Internal Server Error: El servidor esta confundido, muchas veces por un error del lado del programa local respondiendo a la solicitud.
* 501 ethod Not Implemented: El metodo usado es invalido (puede ser causado por escribir un error, ej., escribir "GET" de en minusculas "Get").
* 502 Bad Gateway: El proxy o la puerta indica que recibe una mala respuesta del servidor.
* 503 Service Unavailable: El servidor no puede responde debido a mantenimiento o sobrecarga. El cliente puede intentar despues.
* 504 Gateway Timeout: El proxy o la puerta indican rebicen un "fuera de tiempo" desde el servidor.

### Mas ejemplos de solicitud GET en HTTP/1.0

##### Ejemplo: Metodo mal escrito

En esta solicitud, "GET" fue escrito como "get". El servidor regresara el error "501 Method Not Implemented". La cabecera de respuesta "Allow" le dice al cliente los metodos permitidos.

	**get** /test.html HTTP/1.0
	(enter twice to create a blank line)

	HTTP/1.1 **501 Method Not Implemented**
	Date: Sun, 18 Oct 2009 10:32:05 GMT
	Server: Apache/2.2.14 (Win32)
	**Allow: GET,HEAD,POST,OPTIONS,TRACE**
	Content-Length: 215
	Connection: close
	Content-Type: text/html; charset=iso-8859-1

	<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
	<html><head>
	<title>501 Method Not Implemented</title>
	</head><body>
	<h1>Method Not Implemented</h1>
	<p>get to /index.html not supported.<br />
	</p>
	</body></html>

##### Ejemplo: 404 File Not Found

En esta solicitud GET, la solicitud _URI_ "/t.html" no puede ser encontrada en el el directorio del servidor. El servidor regresa el mensaje "404 Not Found".

	GET **/t.html** HTTP/1.0
	(enter twice to create a blank line)

	HTTP/1.1 404 Not Found
	Date: Sun, 18 Oct 2009 10:36:20 GMT
	Server: Apache/2.2.14 (Win32)
	Content-Length: 204
	Connection: close
	Content-Type: text/html; charset=iso-885-1

	<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
	<html><head>
	<title>404 Not Found</title>
	</head><body>
	<h1>Not Found</h1>
	<p>The requested URL /t.html was not found on this server.</p>
	</body></html>

##### Ejemplo: Numero de versión HTTP erroneo

En esta solicitud GET, la version HTTP está mal escrita, resultado de una mala sintaxis. El servidor regresa el error "404 Bad Request". La version HTTP debe ser HTTP/1.0 o HTTP/1.1.

	GET /index.html **HTTTTTP/1.0**
	(enter twice to create a blank line)

	HTTP/1.1 **400 Bad Request**
	Date: Sun, 08 Feb 2004 01:29:40 GMT
	Server: Apache/1.3.29 (Win32)
	Connection: close
	Content-Type: text/html; charset=iso-8859-1

	<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
	<HTML><HEAD>
	<TITLE>400 Bad Request</TITLE>
	</HEAD><BODY>
	<H1>Bad Request</H1>
	Your browser sent a request that this server could not understand.<P>
	The request line contained invalid characters following the protocol string.<P><P>
	</BODY></HTML>

Nota: La última version de Apache ignora este error y regresa el documento con el código "200 OK"

##### Ejemplo: Solicitud URI erronea

En la siguiente solicitud GET, la solicitud URI no fue comenzada con "/", resultando en un "bad request".

	GET test.html HTTP/1.0
	(blank line)

	HTTP/1.1 400 Bad Request
	Date: Sun, 18 Oct 2009 10:42:27 GMT
	Server: Apache/2.2.14 (Win32)
	Content-Length: 226
	Connection: close
	Content-Type: text/html; charset=iso-8859-1

	<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
	<html><head>
	<title>400 Bad Request</title>
	</head><body>
	<h1>Bad Request</h1>
	<p>Your browser sent a request that this server could not understand.<br />
	</p>
	</body></html>

##### Ejemplo: Conección Keep-Alive

Por default, para una solicitud GET en HTTP/1.0, el servidor cierra la conección TCP una vez que la respuesta ha sido entregada. Podemos solicitar que la conexión TCP se mantenga, por medio de una cabecera del tipo "Connection: Keep/Alive". El servidor incluye una cabecera de mensaje del tipo "Connection: Keep-Alive" para informarle al cliente que puede enviar otra solicitud usando esa conexión, antes de que expire la conexión. Otro tipo de cabecera puede ser "Keep-Alive: timeout=x, max=x", esta le dice al cliente el tiempo máximo y el número máximo de solicitudes que puedes ser enviadas por esa conexión.

	GET /test.html HTTP/1.0
	**Connection: Keep-Alive**
	(blank line

	HTTP/1.1 200 OK
	Date: Sun, 18 Oct 2009 10:47:06 GMT
	Server: Apache/2.2.14 (Win32)
	Last-Modified: Sat, 20 Nov 2004 07:16:26 GMT
	ETag: "10000000565a5-2c-3e94b66c2e680"
	Accept-Ranges: bytes
	Content-Length: 44
	Keep-Alive: timeout=5, max=100
	Connection: Keep-Alive
	Content-Type: text/html

	<html><body><h1>It works!</h1></body></html>

Notas:

* El mensaje "Connection to host lost" (para telnet) aparece despues de "keep-alive timeout".
* Antes de que el mensaje "Connection to host lost" aparezca, podemos enviar otra solicitud mediante la misma conexión TCP.
* La cabecera "Connection: Keep-Alive" no reconoce mayúsculas ni minúsculas. El espacio es opcional.
* Si una cabecera opcional es invalida o está mal escrita, esta sera ignorada por el servidor.


##### Ejemplo: Accesando a un recurso protegido

La siguiente solicitud GET intenta acceder a un recurso protegido. El servidor regresa el error "403 Forbidden". En este ejemplo, el directorio "htdocs\forbidden" esta configurada para denegar todo el acceso en el servidor HTTP de Apache, y esta configurado de la siguiente manera:

	<Directory "C:/apache/htdocs/forbidden>
	Order deny,allow
	deny from all
	</Directory>

	GET **/forbidden/index.html** HTTP/1.0
	(blank line)

	HTTP/1.1 **403 Forbidden**
	Date: Sun, 18 Oct 2009 11:58:41 GMT
	Server: Apache/2.2.14 (Win32)
	Content-Length: 222
	Keep-Alive: timeout=5, max=100
	Connection: Keep-Alive
	Content-Type: text/html; charset=iso-8859-1

	<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
	<html><head>
	<title>403 Forbidden</title>
	</head><body>
	<h1>Forbidden</h1>
	<p>You don't have permission to access /forbidden/index.html
	on this server.</p>
	</body></html>


### HTTP/1.1 GET Request

Un servidor HTTP/1.1 soporta _virtual hosts_. Esto es, el mismo servidor fisico puede albergar varios hosts virtuales con diferentes nombres y sus propios directorios raices. Por lo tanto, en una solicitud GET en HTTP/1.1, es necesario incluir una cabecera llamada "Host" para seleccionar uno de los hosts virtuales.

##### Ejemplo: Solicitud HTTP/1.1

HTTP/1.1 mantiene una conexión  persistente por default para aumentar la eficiencia de a red. Podemos usar la cabecera "Connection: Close" para pedirle al servidor que cierre la conexión TCP cuando la respuesta haya sido entregada.

	GET /index.html HTTP/1.1
	Host: 127.0.0.1
	(blank line)

	HTTP/1.1 200 OK
	Date: Sun, 18 Oct 2009 12:10:12 GMT
	Server: Apache/2.2.14 (Win32)
	Last-Modified: Sat, 20 Nov 2004 07:16:26 GMT
	ETag: "10000000565a5-2c-3e94b66c2e680"
	Accept-Ranges: bytes
	Content-Length: 44
	Content-Type: text/html

	<html><body><h1>It works!</h1></body></html>

##### Ejemplo: Cabecera Host perdida en HTTP/1.1

El siguiente ejemplo muestra que una cabecera "Host" es necesaria en una solicitud HTTP/1.1. Si esta cabecera no esta, el servidor regresara el error "400 Bad Request".

	GET /index.html HTTP/1.1
	(blank line)

	HTTP/1.1 400 Bad Request
	Date: Sun, 18 Oct 2009 12:13:46 GMT
	Server: Apache/2.2.14 (Win32)
	Content-Length: 226
	Connection: close
	Content-Type: text/html; charset=iso-8859-1

	<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
	<html><head>
	<title>400 Bad Request</title>
	</head><body>
	<h1>Bad Request</h1>
	<p>Your browser sent a request that this server could not understand.<br />
	</p>
	</body></html>


### Solicitudes condicionales GET

En todos los ejemplos anteriores, el servidor regresa un documento entero si la solicitud fue cumplida. Debemos usar una cabecera adicionar para emitir una "_Solicitud condicional_". Por ejemplo, para pedir un documento basado en su última fecha de modificación, o para pedir una porción del documento, en vez del documento entero.

La cabecera condicional incluye:

* If-Modified-Since (check for response status code "304 Not Modified").
* If-Unmodified-Since
* If-Match
* If-None-Match
* If-Range

### Cabeceras de solicitud

Esta seccion describe algunas de las cabeceras mas comunes. Refenrenciado a las especificaciones de HTTP. La sintaxis del nombre de la cabecera inicia con una mayúscula unida a un guión. Ej., Content-Length, If-Modified-Since.

**Host: domain-name** - HTTP/1.1. Soporta hosts virtuales. Multiples nombres de DNS pueden estar en el mismo servidor fisico, con sus propios documentos y directorios. El Host en la cabecera es necesario en HTTP/1.1 para elegir uno de los Hosts.

La siguiente cabecera puede ser usada para _negociar contenido_  con el cliente para pedir al servidor entregar el tipo preferido de documento si el servidor maneja multiples versiones para el mismo documento.

**Accept: mime-type-1, mime-type-2, ...** -  El cliente puede usar la cabecera _Accept_ para decirle al servidor los _MIME types_ que puede soportar y que prefiere. Si el servidor tiene múltiples versiones del documento solicitado, puede checar su cabecera para decidir que version sera entregada al cliente. Este proceso es conocido como _content-type negotiaton_.

**Accept-Language: language-1, language-2, ...** - El cliente puede usar la cabecera _Accept-Language_ para decirle al servidor que lenguaje puede soportar y/o prefiere. Si el servidor tiene múltiples versiones del documento solicitado, puede checar la cabecera para decidir que versión regresar. Este proceso es conocido como _language negotiation_.

**Accept-Charset: Charset-1, Charset-2, ...** - Para la negociación de caracteres, el cliente puede usar esta cabecera para decir cuales prefiere. Ejemplos de sets de caracteres son el ISO-8859-1, ISO-8859-2, ISO-8859-5, BIG5, UCS2, UCS4, UTF8.

**Accept-Encoding: encoding-method-1, encoding-method-2, ...** - El cliente puede usar esta cabecera para decirle al servidor el tipo de codificación que soporta. Si el servidor tiene una versión codificada del documento solicitado, puede regresar una version codificada soportada por el cliente. El servior tabien decide codificar el documento antes de regresarlo al cliente para reducir el tiempo de transmición. El servidor debe colocar la cabecera "Content-Encoding" para informar al cliente que el documento regresado está codificado. Los metodos más comúnes de codificación son "x-gzip (.gz, .tgz)" and "x-compress (.Z)".

**Connection: Close|Keep-Alive** - El cliente puede usar esta cabecera para decirle al servidor cuando cerrar la conexión, o mantener la para otra petición. HTTP/1.1 utiliza una conexiónpersistente por default. HTTP/1.0 cierra todas las conexiones por default.

**Referer: referer-URL** - El cliente puede usar esta cabecera para indicar la referencia de esta petición. Si damos click en un enlace de una Web 1 para visitar una Web 2, la Web 1 es la petición ferenciada a la Web 2. La mayoria de los navegadores ponen esta cabecera, la cual puede ser usada para localizar desde donde viene la petición. Sin embargo, esta cabecera no es de confianza y puede ser falsificada facilmente.

**User-Agent: browser-type** -  Identifica el tipo de navegador utilizado para hacer la petición. El servidor puede usar esta información para regresar un documento diferente dependiente el tipo de navegador.

**Content-Length: number-of-bytes** -  Usado por la petición POST para informar al servidor el tamaño del cuerpo de la petición.

**Content-Type: mime-type** -  Usado por la petición POST para informar el tipo de medios del cuerpo de la petición.

**Cache-Control: no-cache|...** - El cliente puede usar esta cabecera para especificar cuantas páginas sera cacheadas por el proxy.

**Authorization:** Usada por el cliente para proporcionar las credenciales necesarias para acceder a recursos protegidos.

**Cookie: cookie-name-1=cookie-value-1, cookie-name-2=cookie-value-2, ...** - El cliente utiliza esta cabecera para regresar una cooki devuelta al servidor, la cual fue enviada anteriormente por el mismo servidor para administrar el estado.

**If-Modified-Since: date** - Le dice al servidor que envie solo la página que fue modificada despues de una fecha especifica.

### Solicitud GET para un Directorio

Supongamos que tenemos un directorio llamado "testdir" en el directorio base "htdocs".

Si el cliente emite una solcitud GET a "/testdir/":
1. El servidor regresara "/testdir/index.html"si el directorio cotiene un archivo "index.html".
2. De otra manera, el servidor regresa la lista del directorio si esta activada.
3. De cualquier otra manera, el servidor regresa "404 Page Not Found".

Es importante tomar nota que si el cliente emite una solicitud GET a "/testdir", el servidor regresara un "301 Move Permanently" con una nueva "locación" de "/testdir/" como se muestra a continuación:

	GET /testdir HTTP/1.1
	Host: 127.0.0.1
	(blank line)

	HTTP/1.1 **301 Moved Permanently**
	Date: Sun, 18 Oct 2009 13:19:15 GMT
	Server: Apache/2.2.14 (Win32)
	**Location: http://127.0.0.1:8000/testdir/**
	Content-Length: 238
	Content-Type: text/html; charset=iso-8859-1

	<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
	<html><head>
	<title>301 Moved Permanently</title>
	</head><body>
	<h1>Moved Permanently</h1>
	<p>The document has moved <a href="http://127.0.0.1:8000/testdir/">here</a>.</p>

	</body></html>

La mayoria de los navegadores seguiran con otra petición a "/testdir/". Por ejemplo, si escribimos _http://127.0.0.1:8000/testdir_ son el "/" de un navegador, nos daremos cuenta que un "/" fue agregado a la dirección en la respuesta dada. La moraleja de la historia es: debemos incluir el "/" para el directorio solicitado para ahorrarnos una peticion GET extra.


### Emitir una solicitud GET a un Servidor Proxy

Para enviar una solicitud GET a través de un servidor proxy, se debe establecer la conexión TCP al servidor y se debe extablecer una solicitud URI para localizar al servidor: _http://hostname:port/path/fileName_.

El siguiente ejemplo fue usado en telnet. Una conexión es establecda con el servidor proxy y se emitio una solicitud GET.

	GET **http://www.amazon.com/index.html** HTTP/1.1
	Host: www.amazon.com
	Connection: Close
	(blank line)


	HTTP/1.1 302 Found
	Transfer-Encoding: chunked
	Date: Fri, 27 Feb 2004 09:27:35 GMT
	Content-Type: text/html; charset=iso-8859-1
	Connection: close
	Server: Stronghold/2.4.2 Apache/1.3.6 C2NetEU/2412 (Unix)
	Set-Cookie: skin=; domain=.amazon.com; path=/; expires=Wed, 01-Aug-01 12:00:00 GMT
	Connection: close
	Location: http://www.amazon.com:80/exec/obidos/subst/home/home.html
	Via: 1.1 xproxy (NetCache NetApp/5.3.1R4D5)

	ed
	<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
	<HTML><HEAD>
	<TITLE>302 Found</TITLE>
	</HEAD><BODY>
	<H1>Found</H1>
	The document has moved
	<A HREF="http://www.amazon.com:80/exec/obidos/subst/home/home.html">
	here</A>.<P>
	</BODY></HTML>

	0

Notese que la respuesta fue regresada en "pedazos".

### Metodo de petición "HEAD"

_HEAD_ es similar a _GET_. Sin embargo, el servidor regresa solamente la cabecera de respuesta sin el cuerpo del mismo, el cual contiene el documento actual. _HEAD_ es muy útil para checar las cabeceras, como _Last-Modified_, _Content-Type_, _COntent-Lenght_, antes de enviar una solicitud GET apropiada.

La sintaxis de _HEAD_ es como se muestra a continuación:

	HEAD request-URI HTTP-version
	(other optional request headers)
	(blank line)
	(optional request body)

##### Ejemplo

	**HEAD** /index.html HTTP/1.0
	(blank line)

	HTTP/1.1 200 OK
	Date: Sun, 18 Oct 2009 14:09:16 GMT
	Server: Apache/2.2.14 (Win32)
	Last-Modified: Sat, 20 Nov 2004 07:16:26 GMT
	ETag: "10000000565a5-2c-3e94b66c2e680"
	Accept-Ranges: bytes
	Content-Length: 44
	Connection: close
	Content-Type: text/html
	X-Pad: avoid browser bug

Notese que la respuesta consiste de una única cabecera sin el cuerpo.


### Método de petición "OPTIONS"

El cliente puede utilizar _OPTIONS_ para solicitar una consulta que sea soportada. La sintaxis para _OPTIONS_ es la siguiente:

	OPTIONS request-URI|* HTTP-version
	(other optional headers)
	(blank line)

El asterisco puede ser usado en lugar de una solicitud URI para indicar que la solicitud no aplica a un recurso en particular.

##### Ejemplo

En este ejemplo, _OPTIONS_ se envia a traves de un servidor proxy:

	OPTIONS http://www.amazon.com/ HTTP/1.1
	Host: www.amazon.com
	Connection: Close
	(blank line)


	HTTP/1.1 200 OK
	Date: Fri, 27 Feb 2004 09:42:46 GMT
	Content-Length: 0
	Connection: close
	Server: Stronghold/2.4.2 Apache/1.3.6 C2NetEU/2412 (Unix)
	Allow: GET, HEAD, POST, OPTIONS, TRACE
	Connection: close
	Via: 1.1 xproxy (NetCache NetApp/5.3.1R4D5)
	(blank line)

Todos los servidores que permitan GET permitiran HEAD. Algunas veces, HEAD no se encuenta listada.


### Método de petición "TRACE"

El cliente puede enviar una petición _TRACE_ para pedir un diagnostico al servidor.
_TRACE_ tiene la siguiente sintaxis:

	TRACE / HTTP-version
	(blank line)

##### Ejemplo

El siguiente ejemplo muestra una petición TRACE usando un servidor proxy.

	TRACE http://www.amazon.com/ HTTP/1.1
	Host: www.amazon.com
	Connection: Close
	(blank line)


	HTTP/1.1 200 OK
	Transfer-Encoding: chunked
	Date: Fri, 27 Feb 2004 09:44:21 GMT
	Content-Type: message/http
	Connection: close
	Server: Stronghold/2.4.2 Apache/1.3.6 C2NetEU/2412 (Unix)
	Connection: close
	Via: 1.1 xproxy (NetCache NetApp/5.3.1R4D5)
	
	9d
	TRACE / HTTP/1.1
	Connection: keep-alive
	Host: www.amazon.com
	Via: 1.1 xproxy (NetCache NetApp/5.3.1R4D5)
	X-Forwarded-For: 155.69.185.59, 155.69.5.234

	0

### Submitting HTML Form Data and Query String

En muchas aplicaciones de Internet, como "_e-commerce_" y "_search engine_", los clientes deben proporcionar información adicional a servidor (ej., nombre, dirección, palabras clave, etc). Basado en la información entregada, el servidor toma una acción apropiada y produce una respuesta personalizada.

Los clientes normalente presentan la información en un formulario. Una vez este es llenado y clickeado el botón de enviar, el navegador empaqueta la información y la envia al servidor, utilizando ya sea GET o POST.

El siguiente ejemlo muestra un formulario HTML, el cual es producido por el script HTML:

	<html>
	<head><title>A Sample HTML Form</title></head>
	<body>
	  <h2 align="left">A Sample HTML Data Entry Form</h2>
	    <form method="get" action="/bin/process">
	        Enter your name: <input type="text" name="username"><br />
		Enter your password: <input type="password" name="password"><br />
		Which year?
		<input type="radio" name="year" value="2" />Yr 1
		<input type="radio" name="year" value="2" />Yr 2
	        <input type="radio" name="year" value="3" />Yr 3<br />
		Subject registered:
		<input type="checkbox" name="subject" value="e101" />E101
		<input type="checkbox" name="subject" value="e102" />E102
		<input type="checkbox" name="subject" value="e103" />E103<br />
		Select Day:
		<select name="day">
			<option value="mon">Monday</option>
			<option value="wed">Wednesday</option>
			 <option value="fri">Friday</option>
		</select><br />
		<textarea rows="3" cols="30">Enter your special request here</textarea><br />
		<input type="submit" value="SEND" />
		<input type="reset" value="CLEAR" />
		<input type="hidden" name="action" value="registration" />
	    </form>
	 </body>
	 </html>


![HTML SAMPLE DATA FORM](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTML_SampleForm.png)

Una forma contiene "_campos_". Estos tipos de "_campos_" incluyen:

* **Text Box**: producido por un <input type="text">.
* **Password Box**: producido por un <input type="password">.
* **Radio Button**: producido por un <input type="radio">.
* **Checkbox**: producido por un <input type="checkbox">.
* **Selection**: producido por <select> y <option>.
* **Text Area**: producido por <textarea>.
* **Submit Button**: producido por <input type="submit">.
* **Reset Button**: producido por <input type="reset">.
* **Hidden Field**: producido por <input type="hidden">.
* **Button**: producido por <input type="button">.

Cada campo tiene un _nombre_ y puede tomar un _valor_ específico. Una vez que el cliente llena los campos y da click al botón de enviar, el navegador toma ambos campos, y los empaqueta en pares "_name=value_", y concatena todos los campos utilizando un "_&_" como separador de campos. Esto es conocido como un "_query string_". Este enviará la cadena al servidor como parte de la petición.
	**name1=value1&name2=value2&name3=value3&...**

Los caracteres especiales no son permitidos dentro de la _query string_. Deben ser reemplazados por un "%" seguido del código **ASCII** en _hexadecimal_. Ej.,  "~" es reemplazado por "%7E", "#" por "%23" , etc. Desde que el espacio en blanco es muy común, puede ser reemplazado yasea por "%20" o "+". Este proceso de reemplazo es llamado "_URL-encoding_", y el resultado es un "_URL-encoded query string_". Por ejemplo, supongamos que tenemos 3 campos dentro de un formulario con _name/value_ de "name=Peter Lee", "address=#123 Happy Ave" y "language=C++", la _URL-encoded query string_ sería:

	name=Peter+Lee&address=%23123+Happy+Ave&Language=C%2B%2B

La _query string_ puede ser enviada al servidor utilizando GET o POST, las cuales estan espeficificadas en el atributo "_method_" de <form>.

	<form method="get|post" action="url">

Si utilizamos GET, la "_URL-encoded query string_" sera agregada antes de la _request-URL_ despues de un "?":

	GET request-URI?query-string HTTP-version
	(other optional request headers)
	(blank line)
	(optional request body)

Usando GET para enviar la _query string_ tiene los siguients inconvenientes:

* La cantidad de datos que podemos adjuntar antes de _request-URL_ es limitado. Si esta cantidad excete la permitida, el servidor regresara un error como  "414 Request URI too Large".

* La _URL-encoded query string_ aparecerá en la caja de direcciones del navegador.

El metodo POST vence estos inconvenientes. Si utilizamos POST, la _query string_ sera enviada en el cuerpo del mensaje, donde la cantidad de información no es limitada. Las cabeceras _Content-Type_ y _Content-Length_ son usadas para notificar al servidor el tipo y longitud de la _query string_. La _query string_ no aparecera en la caja de direcciones del navegador.

##### Ejemplo

El siguiente formulario HTML es usado para reunir el usuario y contraseña en un menú de login:

	<html>
	<head><title>Login</title></head>
	<body>
		<h2>LOGIN</h2>
		<form method="get" action="/bin/login">
			Username: <input type="text" name="user" size="25" /><br />
			Password: <input type="password" name="pw" size="10" /><br /><br />
			<input type="hidden" name="action" value="login" />
			<input type="submit" value="SEND" />
		</form>
	</body>
	</html>

![Ejemplo LOGIN](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTML_LoginForm.png)

El metodo GET es usado para enviar la _querry string_. Supongamos que el usuario ingresa "Peter Lee" como usuario y "123456" como contraseña y clickea el botón de enviar. La solicitud GET sería:

	GET /bin/login?user=Peter+Lee&pw=123456&action=login HTTP/1.1
	Accept: image/gif, image/jpeg, */*
	Referer: http://127.0.0.1:8000/login.html
	Accept-Language: en-us
	Accept-Encoding: gzip, deflate
	User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
	Host: 127.0.0.1:8000
	Connection: Keep-Alive

Nota que la contraseña que ingresamos no aparece en la pantalla, es posible verla en la caja de direcciones del navegador. Nunca debemos enviar una contraseña sin la encriptación apropiada.

	http://127.0.0.1:8000/bin/login?user=Peter+Lee&pw=123456&action=login

### URL y URI

##### URL (Uniform Resource Locator)

Una URL definida en el RFL 2396, es utilizada para identificar un recuero en la web y tiene la siguiente sintaxis:

	protocol://hostname:port/path-and-file-name

Una URL tene 4 partes:

1. Protocolo: el utilizado por el servidor
2. Hostname: el nombre de dominio DNS de el servidor
3. Puerto: El numero del puerto TCP que el servidor esta esperando
4. Path-and-file-name: El nombre y localización del recurso solicitado

Ejemplos de URL son:

	ftp://www.ftp.org/docs/test.txt
	mailto:user@test101.com
	news:soc.culture.Singapore
	telnet://www.nowhere123.com/

##### Encoded URL

La URL no puede contener caracteres especiales. Estos caracteres son codificados en la forma %xx, donde xx es el codigo ASCII Hexadecimal. La URL despues de ser codificada es llamada _encoded URL_.

##### URI (Uniform Resource Identifier)

La URI es mas general que la URL, la cual puede localizar un fragmento sin el recurso completo. La sintaxis que tiene es la siguiente:

	http://host:port/path?request-parameters#nameAnchor

* Los parametros solicitades son separados de la URL por un "?". Los demas valores son separados por un "&".

* El _#nameAnchor_ identifica un fragmento sin necesitar el HTML completo, definido por el tag  <a name="anchorName">...</a>.

### Método de solicitud POST

Este es utlizado para agregar información adicional al servidor. Emitiendo una URL HTML desde el navegador siempre activara una solicitud GET. Para activar una solicitud POST, podemos utilizar un formulario HTML con el atributo method="post" o escribir nuestro propio programa de red. Para enviar un formulario HTML, POST se utiliza  al igual que GET exceptuando la _URL-encoded query string_, esta es enviada en el cuerpo del mensaje.

POST toma la siguiente sintaxis:

	POST request-URI HTTP-version
	Content-Type: mime-type
	Content-Length: number-of-bytes
	(other optional request headers)
	  
	(URL-encoded query string)

Las cabeceras "_Content-Type and Content-Length_" son necesarias en POST para informar al servidor el tipo de archivos y la longuitud del cuerpo del mensaje.


##### Ejemplo: Formulario para enviar información utilizando el metodo POST


	<html>
	<head><title>Login</title></head>
	<body>
		  <h2>LOGIN</h2>
		  <form method="post" action="/bin/login">
		  	Username: <input type="text" name="user" size="25" /><br />
			  Password: <input type="password" name="pw" size="10" /><br /><br />
			  <input type="hidden" name="action" value="login" />
			  <input type="submit" value="SEND" />
		  </form>
	</body>
	</html>


Supongamos que escribimos "Peter Lee" como username y "123456" como contraseña y damos click en el botón de enviar. El navegador generara el siguiente POST:

	POST /bin/login HTTP/1.1
	Host: 127.0.0.1:8000
	Accept: image/gif, image/jpeg, */*
	Referer: http://127.0.0.1:8000/login.html
	Accept-Language: en-us
	Content-Type: application/x-www-form-urlencoded
	Accept-Encoding: gzip, deflate
	User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
	Content-Length: 37
	Connection: Keep-Alive
	Cache-Control: no-cache
	   
	**User=Peter+Lee&pw=123456&action=login** 

Notemos que la cabecera Content-Type le informa al servidor que la información es una URL-encoded y la cabecera Content-Length le dice al servidor cuantos bytes leer del cuerpo del mensaje.

##### Formulario POST vs GET

El método POST tiene las siguientes ventajas comparado contra GET al enviar una _query string_:

* La cantidad de información es ilimitada, siempre y cuando vayan en el cuerpo del mensaje, el cual es enviado comunmente al servidor de forma separada.

* La _query string_ no es mostrada en la caja del navegador

Notemos que aunque la contraseña no es mostrada en el navegador, si es enviada al servidor en texto plano y vulnerable. Por lo tanto, enviar una contraseña enviando el método POST es absolutamente no seguro.

### Carga de archivos usando _multipart/form-data_ POST

La RFC 1867 especifica como un archivo puede ser cargando al servidor utilizando POST desde un formulario HTML. El atributo _type="file"_ es agregado a la etiqueta <input> tag de la etiqueta <form> para soportar la carga de archivos. El método POST para la carga de archivos no es una _URL-encoded_ pero utiliza el nuevl _MIME type_ llamado _multipart/form-data_.

##### Ejemplo

El siguiente formulario HTML puede ser usado para cargar archivos:

	<html>
	<head><title>File Upload</title></head>
	<body>
		<h2>Upload File</h2>
		<form method="post" enctype="multipart/form-data" action="servlet/UploadServlet">
		Who are you: <input type="text" name="username" /><br />
		Choose the file to upload:
		<input type="file" name="fileID" /><br />
		<input type="submit" value="SEND" />
		</form>
	</body>
	</html>
![UPLOAD FILE IMAGE](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTML_FileUploadForm.png)

Cuando el navegador encuentra la etiqueta <input> con el atributo _type="file"_, muestra una caja de texto y un boton para navegar dentro de una carpeta y encontrar el archivo que sera cargado.

Cuando el usuario da click en el boton de enviar, el navegador envia el formulario y el contenido junto con el archivo. La codificación _"application/x-www-form-urlencoded"_ es neficiente para enviar datos binarios e información que no sean caracteres ASCII. Para esto se utiliza _"multipart/form-data"_ en su lugar.

El archivo local original puede ser sustituido como un parametro "filename" o en la cabecera _"Content-Disposition: form-data"_.

Un ejemplo de un mensaje POST para cargar un archivo es el siguiente:

	POST /bin/upload HTTP/1.1
	Host: test101
	Accept: image/gif, image/jpeg, */*
	Accept-Language: en-us
	Content-Type: multipart/form-data; boundary=---------------------------7d41b838504d8
	Accept-Encoding: gzip, deflate
	User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
	Content-Length: 342
	Connection: Keep-Alive
	Cache-Control: no-cache

	-----------------------------7d41b838504d8 Content-Disposition: form-data; name="username" 
	Peter Lee
	-----------------------------7d41b838504d8 Content-Disposition: form-data; name="fileID"; filename="C:\temp.html" Content-Type: text/plain 
	<h1>Home page on main server</h1> 
	-----------------------------7d41b838504d8--

