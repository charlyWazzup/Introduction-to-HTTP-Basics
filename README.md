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




