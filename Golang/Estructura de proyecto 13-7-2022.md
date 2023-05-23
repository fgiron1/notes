En Go, todas las carpetas son consideradas módulos, y todos los ficheros deben declarar el paquete al que pertenecen con la keyword  `package` . El paquete `main` es especial, e indica a Go que los contenidos de ese fichero deben de compilarse a un binario ejecutable.

Dentro de cada módulo puedes tener tu fichero main.go que sirva como punto de entrada hacia el módulo.

El layout que voy a seguir es:

/api

Expone la API (si tiene) de tu aplicación