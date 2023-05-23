Rust no se entera automáticamente ni pretende inferir una estructura de módulos. Se lo tienes que indicar manualmente.

Cuando importas un módulo escribiendo:

``` 
mod mafs;
```

Rust busca  ```mafs.rs```  o  ```mafs/mod.rs``` . Vas a ver que en internet comentan que lo de mod.rs ya se dejó de hacer en el Rust del 2018, sin embargo, si quieres importar un fichero de una carpeta que se llama distinta de él:

mafs
	__ euclidean.rs
	__ non.rs

Tendrás que crear el  ```mafs/mod.rs``` , donde declararás la visibilidad de tus multiples módulos. Ejemplo:

```
pub mod euclidean;
mod non;
```

En  ```main.rs``` , o en el fichero en el que estés trabajando, lo importarás así:

```
mod mafs;

fn main() {
	mafs::euclidean::<struct, enum, func...>;
}
```

Para usar una supuesta función "sumar", definida **públicamente** en  ```euclidean.rs``` , sin tener que escribir cada vez:

```
mafs::euclidean::sumar()
```

Se puede dejar el main.rs así:

```
mod mafs;
use crate::mafs::euclidean::sumar;

fn main() {
	sumar(2, 3);
}
```