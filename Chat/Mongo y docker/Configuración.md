
Se van a usar 3 contenedores de docker, cada uno siendo parte de un **replica set** de mongodb, en el que hay un primary y dos secundaries. El primary será el único que reciba las órdenes de lectura/escritura. Y los otros 2 secundarios replicarán las operaciones que se hagan en el primario.

Para incluir todo esto en un docker-compose, además de incluir la definición de los 3 servicios con su puerto, imagen, volúmenes, red virtual privada, incluiremos este entrypoint en cada uno de ellos:

```
/usr/bin/mongod --bind-ip-all --replSet dbrs
```

El entrypoint será el comando que la instancia ejecutará nada más se construya

>*Los contenedore de Docker, una vez construidos, solo corren un comando y cuando acaban, el contenedor se destruye, pero este comportamiento es normal ,porque con este comando se quedará corriendo de forma indefinida el servicio de base de datos o cualquier otro servicio de servidor*.

Ese comando informa a cada nodo que forma parte de un replica set llamado "dbrs". La opción ``` --bind-ip-all ``` deberá ser cambiada con el tiempo, ya que permite conexiones desde cualquier IP (Aunque es cierto que hemos creado una red virtual entre la cual solo se ven a sí mismos).

La primera vez que los contenedores se crean y se inician, se ejecutan los scripts .js o .sh que existan en la carpeta ``` /docker-entrypoint-initdb.d ```, donde hemos mapeado nuestro script de inicialización. Este, además de proveer metadata (a no se donde/para qué) de nuestro replica set, deberá incluir la creación de usuarios y asignación de roles. Por defecto, se ejecuta sin autenticación.

Para llamar al siguiente script:

```
#!/bin/bash

  

mongo <<EOF

var config = {

"_id": "dbrs",

"version": 1,

"members": [

{

"_id": 1,

"host": "primary:27017",

"priority": 3

},

{

"_id": 2,

"host": "secondary1:27017",

"priority": 2

},

{

"_id": 3,

"host": "secondary2:27017",

"priority": 1

}

]

};

rs.initiate(config, { force: true });

rs.status();

EOF
```

Se le pueden añadir múltiples opciones para la inicialización (creación de usuarios con roles asignados y contraseñas...)

