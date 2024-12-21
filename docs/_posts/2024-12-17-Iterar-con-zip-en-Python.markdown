---
layout: post
title: "Iterar dos o más iterables con zip()"
date: 2024-12-17 18:17:33 +0100
tags: [python, frontend]
sum: "Une dos iterables o itera sobre ellos conjuntamente con <code>zip()</code>."
---

### 📌 Resumen

En este artículo te enseño a iterar dos o más iterables con la función `zip()` de Python.

#### Resultado final:

Script:

```python
spells = ["alzar a los muertos", "crear muerto viviente",
"hablar con los muertos", "falsa vida"]
levels = [5, 6, 3, 1]

spells_n_levels = list(zip(spells, levels))
print(spells_n_levels)

for spell, level in zip(spells, levels):
	print(spell, level)
```

Resultado:

```shell
[('alzar a los muertos', 5), ('crear muerto viviente', 6),
 ('hablar con los muertos', 3), ('falsa vida', 1)]

alzar a los muertos 5
crear muerto viviente 6
hablar con los muertos 3
falsa vida 1
```

---

### 0️⃣ Situación

Imaginemos que tenemos dos iterables, `spells` y `levels`, que deberían estar relacionados pero están separados.

(Vamos a utilizar datos de la escuela de nigromancia, porque es la mejor 💀):

```python
spells = ["alzar a los muertos", "crear muerto viviente",
"hablar con los muertos", "falsa vida"]
levels = [5, 6, 3, 1]
```

Lo que queremos es combinar los datos, **no simplemente añadir una lista a la otra**. Queremos que `"alzar a los muertos"` esté relacionado con el valor de nivel `5` de `levels`.

Podríamos hacer toda una funcionalidad para conseguir este resultado... Pero `zip()` nos lo hace mucho más fácil.

### 1️⃣ La función `zip()`

La función `zip()` de Python **devuelve un objeto iterable de tuplas**.
Cada tupla **contiene una combinación de los elementos de cada objeto recibido**.

Veámoslo en acción:

```python
spells = ["alzar a los muertos", "crear muerto viviente",
"hablar con los muertos", "falsa vida"]
levels = [5, 6, 3, 1]

spells_n_levels = zip(spells, levels)
print(spells_n_levels)
```

Si ejecutamos el código anterior, la consola nos devolverá lo siguiente:

```shell
<zip object at 0x000001E0E7BFE780>
```

Para que nos devuelva un resultado que podamos entender, es necesario que encapsulemos la función `zip()` dentro de la función `list()`:

```python
spells_n_levels = list(zip(spells, levels))
```

Esto nos devolverá:

```shell
[('alzar a los muertos', 5), ('crear muerto viviente', 6),
 ('hablar con los muertos', 3), ('falsa vida', 1)]
```

Es importante saber que la función `zip()` crea una iterador de tuplas considerando el objeto con **menor** cantidad de elementos.

Es decir, si en lugar de 4 valores dentro de la lista `levels` hubiera sólo 3, `zip()` ignoraría el nombre del último hechizo. Cuando se acabasen los valores de `levels`, dejaría de leer datos.

### 2️⃣ Iterando con zip

También podemos utilizar `zip()` para iterar dos iterables (o más) de forma más cómoda.

Siguiendo el ejemplo anterior, queremos recorrer los datos de `spells` y `levels` y mostrar por consola cada conjunto de valores relacionados.

El script quedaría así:

```python
spells = ["alzar a los muertos", "crear muerto viviente",
 "hablar con los muertos", "falsa vida"]
levels = [5, 6, 3, 1]

for spell, level in zip(spells, levels):
	print(spell, level)
```

Al ejecutar el código anterior, la consola nos mostraría lo siguiente:

```shell
alzar a los muertos 5
crear muerto viviente 6
hablar con los muertos 3
falsa vida 1
```

#### Conclusión

Python ofrece muchas funcionalidades _built-in_ para problemas habituales que encontramos en el día a día.

En especial `zip()` es una función que me parece de lo más útil si necesitamos combinar elementos de dos o más iterables.

¡Espero que te haya sido de utilidad! 😉
