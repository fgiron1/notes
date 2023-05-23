Cuando en una función veas parámetros declarados sin el asterisko, no es que sean pass-by-value, sino que Go hace una COPIA de los valores para que la función pueda manejarlos de forma privada.

Si quieres que la función maneje el mismo valor que se le pasa, debes usar una REFERENCIA con el `*` (asterisco).