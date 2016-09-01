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

* Nota de _RFC2616_: `"El Protocolo de transferencia de Hypertexto (HTTP)` es un protocolo para los sistemas de información hypermedia, distrbuída y colaborativa. Es un protocolo genérico sin estado, el cual puede ser usado para varias tareas mas haya de su uso con el hypertexto, como por ejemplo, como nombre de servidores y sistemas distribuidos de manejo de objetos, extensión de metodos de solicitud, codigos de errores y cabeceras."
