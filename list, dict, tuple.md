## Lista
* Entre corchetes
* Parte del lenguaje estandar
* Se pueden modificar
* Pueden haber valores duplicados
``` python
l = [1, 2, "a"]
```

## Tuplas
* Entre paréntesis
* Parte del lenguaje estandar
* Más rápidas que las listas, porque son inmutables
* Pueden haber valores duplicados
``` python
l = (1, 2, 3)
```

## Dicts
* Secuencia de pares clave-valor
* Parte del lenguaje estandar
* Pueden haber valores duplicados, no claves duplicadas
``` python
d = {'first':'string value', 'second':[1,2]}
```

### Convertir dos listas a un diccionario
``` python
keys = ['a', 'b', 'c']
values = [1, 2, 3]
dictionary = dict(zip(keys, values))
print(dictionary) # {'a': 1, 'b': 2, 'c': 3}
```
