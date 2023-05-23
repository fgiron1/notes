**WEB DE CHAT**

ARQUITECTURA


**FRONT**

Se tratará de una aplicación React con la que el usuario interactuará para enviar mensajes, unirse y crear salas de chat, al igual que registar un usuario en el servicio. Se conectará con el servidor turn. Enviará los mensajes de cada peer al servidor de señalización

Existirá un backend escrito en Java Spring Boot (3 o 2.7.6)

**SERVIDOR DE SEÑALES**

Se tratará de un servidor de websockets escrito en Java.

Se encarga de comunicar los mensajes entre los peers, tan sencillo como eso. El caso de uso lo hará más y más complejo. Lo más simple sería broadcastear todos los mensajes a todos los peers. Para el chat, los peers solo podrán hablar con otros peers integrantes en las mismas salas de chat.

Se creará un módulo de generación de ruido. Consistirá en crear salas y enviar mensajes en ellas de forma masiva y multihilos, para así tener una fuente de datos con un alto tráfico. Usará la API web del backend para interactuar con él.

En este link se puede encontrar un ejemplo de servidor de señalización escrito en javascript.
https://github.com/mdn/samples-server/tree/master/s/webrtc-from-chat. El servidor nuestro estará escrito en Java

**Servidor TURN**

Se encargará de usar NAT para dar una IP pública a cada peer. Será usado como gateway para los peers. (NAT traversal server). Se usará https://github.com/coturn/coturn/blob/master/docker/coturn/README.md para la implementación, de forma dockerizada.
