
![[kerckhoff_principle.png]]

Existen diferentes tipos de ataque en el tipico esquema de comunicación Alice-Bob con Eve haciendo eavesdropping en su comunicación. Para demostrar que un mensaje ha sido encriptado por una cierta llave se usa un sistema (o código) MAC. Básicamente, son 3 cosas:

1. Un algoritmo de genración de llave
2. Un algoritmo de cálculo del código de **autenticación**, es decir un algoritmo para **firmar** (toma el mensaje y la llave) y produce el código de autenticación (si la lla)
3. Un algoritmo de verificación (toma la llave y el código, o tag) 

Esto otorga dos propiedades:
1. **Integridad a los datos**: Si el mensaje fuera modificado, su firma sería diferente
2. **Autenticidad**: Solo la llave conocida por Alice podrá generar un resultado positivo en el algoritmo de verificación, si el mensaje no ha sido alterado.

Son dos propiedades derivadas de que la firma es exclusiva al mensaje (integridad) y a la llave (autenticidad). La autenticidad del mensaje, de todas formas, será garantizada mientras se pueda afirmar que NADIE más conoce la llave usada para firmar el mensaje (se presupone que Bob la ha recibido a través de un canal seguro).

Para conseguir más garantías como:

1. Eve reenvíe a Bob antiguos mensajes, junto con su firma, porque está escuchando en el canal, aunque no tenga la llave generada por Alice
2. Saber si Eve ha eliminado algún mensaje de camino a Bob

Se implementa una numbering scheme para los mensajes, es decir, se cuentan los mensajes enviados y se incluye esa información en el propio mensaje.

Nota final:

![[eve_will_change_ciphertext.png]]


