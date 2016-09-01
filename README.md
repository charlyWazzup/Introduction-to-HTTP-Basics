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


