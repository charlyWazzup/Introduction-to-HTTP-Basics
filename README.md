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


