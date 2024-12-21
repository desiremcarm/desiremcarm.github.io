---
layout: post
title: "Uso de extend, append e insert en listas"
date: 2024-12-17 18:17:33 +0100
tags: [python, frontend]
sum: "Domina los métodos <code>append</code>, <code>extend</code> e <code>insert</code> para manipular listas en Python."
---

### 📌 Resumen

En este artículo te enseño cómo utilizar y cuándo es mejor utilizar los métodos `append`,`insert` y `extend` en Python.

Para seguir el tutorial sin necesidad de crear un nuevo proyecto puedes utilizar
[este compilador Python online](https://www.programiz.com/python-programming/online-compiler/) 😉.

---

#### Contenidos

\*️⃣ [Append](#append)

\*️⃣ [Extend](#extend)

\*️⃣ [Insert](#insert)

#### Resultado final

Uso de `append()`:

```python
vox_machina = ['Grog', 'Keyleth', 'Scanlan', 'Vax\'ildan', 'Vex\'ahlia', 'Percival']

vox_machina.append('Pike')
```

Uso de `extend()`:

```python
vox_machina = ['Grog', 'Keyleth', 'Scanlan', 'Vax\'ildan', 'Vex\'ahlia', 'Percival']

vox_machina.extend(['Pike', 'Trinket'])
```

Uso de `insert()`:

```python
vox_machina = ['Grog', 'Keyleth', 'Scanlan', 'Vax\'ildan', 'Vex\'ahlia', 'Percival']

vox_machina.insert(0, 'Pike')
```

---

### 0️⃣ <a name="append">Agregando datos con `append`</a>

El método `append()` será el favorito si **tienes que añadir valores individuales a una lista** en Python.

Sin embargo, estudiemos un poco más a fondo su comportamiento.

Primero, veamos un ejemplo de lo más sencillo. Tenemos la siguiente lista:

```python
vox_machina = ['Grog', 'Keyleth', 'Scanlan', 'Vax\'ildan', 'Vex\'ahlia', 'Percival']
```

Y queremos añadir un nuevo valor, en este caso: `'Pike'`. Para esto, utilizaremos el método `append`
de la siguiente forma:

```python
vox_machina = ['Grog', 'Keyleth', 'Scanlan', 'Vax\'ildan', 'Vex\'ahlia', 'Percival']

vox_machina.append('Pike') # Añadimos el valor 'Pike' a nuestra lista 'vox_machina'

print(vox_machina)
```

El resultado por consola será:

```shell
['Grog', 'Keyleth', 'Scanlan', "Vax'ildan", "Vex'ahlia", 'Percival', 'Pike']
```

¡Genial! A priori parece sencillo, pero debes tener en cuenta las siguientes características de `append`:

- 🟣 Siempre agrega el valor **al final** de la lista.
- 🟣 Es un método que **modifica el objeto original**.
- 🟣 Si añades múltiples valores, **los añade como un único valor**, por ejemplo:

Si quisieramos añadir una lista a la lista que ya teníamos, se verá de la siguiente forma:

```python

vox_machina = ['Grog', 'Keyleth', 'Scanlan', 'Vax\'ildan', 'Vex\'ahlia', 'Percival']

vox_machina.append(['Pike', 'Trinket'])

print(vox_machina)
```

El resultado por consola será:

```shell
['Grog', 'Keyleth', 'Scanlan', "Vax'ildan", "Vex'ahlia", 'Percival', ['Pike', 'Trinket']]
```

Es decir, **se convertirá en una lista que guarda en su última posición otra lista**.

Para printar los valores por pantalla, deberías hacer algo como:

```python
print(vox_machina[6][0]) # Mostrará "Pike"
```

Resultado:

```shell
'Pike'
```

### 1️⃣ <a name="extend">Agregando datos con `extend`</a>

El método `extend`, a diferencia de `append`, recibe un conjunto de valores, **los desempaqueta** y los **añade uno por uno** a la lista.

Este método también **añade los valores indicados al final de la lista original que le indiques**.

Repitamos el último ejemplo anterior, esta vez con `extend`:

```python
vox_machina = ['Grog', 'Keyleth', 'Scanlan', 'Vax\'ildan', 'Vex\'ahlia', 'Percival']

vox_machina.extend(['Pike', 'Trinket'])

print(vox_machina)
```

El resultado por consola será:

```shell
['Grog', 'Keyleth', 'Scanlan', "Vax'ildan", "Vex'ahlia", 'Percival', 'Pike', 'Trinket']
```

Puedes utilizar `extend` **para añadir elementos de una lista, tupla o cualquier tipo de iterable a la lista que quieras**.

⚠️ Una notación importante es recordarte que **las Strings son listas de caracteres**, por lo tanto, un código como el que ves a continuación:

```python
vox_machina = ['Grog', 'Keyleth', 'Scanlan', 'Vax\'ildan', 'Vex\'ahlia', 'Percival']

vox_machina.extend('Pike')

print(vox_machina)
```

Resultará en:

```shell
['Grog', 'Keyleth', 'Scanlan', "Vax'ildan", "Vex'ahlia", 'Percival', 'P', 'i', 'k', 'e']
```

### 2️⃣ <a name="insert">Agregando datos con `insert`</a>

Finalmente topamos con el método `insert`.

Este método nos permite **agregar un elemento en una posición específica dentro de una lista**, por lo tanto, requiere de unos argumentos que le indiquen:

- 🟣 En qué **posición** debe añadir el elemento dentro de la lista.
- 🟣 Qué **elemento/s** debe añadir.

A continuación te dejo un ejemplo de uso:

```python
vox_machina = ['Grog', 'Keyleth', 'Scanlan', 'Vax\'ildan', 'Vex\'ahlia', 'Percival']

vox_machina.insert(0, 'Pike') # Insertando el valor 'Pike' en la posición 0

print(vox_machina)
```

Resultado:

```shell
['Pike', 'Grog', 'Keyleth', 'Scanlan', "Vax'ildan", "Vex'ahlia", 'Percival']
```

Como ves, el valor `'Pike'` ha sido añadido en la posición `0` de la lista. (_Recuerda que en programación, los conjuntos como listas, arrays, etc., empiezan en el índice 0, no el 1_).

Veamos su comportamiento al intentar añadir una lista a la lista original:

```python
vox_machina = ['Grog', 'Keyleth', 'Scanlan', 'Vax\'ildan', 'Vex\'ahlia', 'Percival']

vox_machina.insert(0, ['Pike', 'Trinket'])

print(vox_machina)
```

El resultado por consola será:

```shell
[['Pike', 'Trinket'], 'Grog', 'Keyleth', 'Scanlan', "Vax'ildan", "Vex'ahlia", 'Percival']
```

#### Conclusión

| **Método** | **Descripción**                                                                       | **Uso**                                                                                     |
| ---------- | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| `append`   | Añade un elemento o conjunto de elementos (entero) en la posición final de una lista. | **Ideal cuando el orden de los elementos en un conjunto no importa.**                       |
| `extend`   | Añade un elemento o más de un elemento, uno por uno, al final de una lista.           | **Ideal si quieres insertar varios valores a una lista**.                                   |
| `insert`   | Añade un elemento o conjunto de elemento en una posición específica de una lista.     | **Ideal cuando, por el motivo que sea, el orden de los elementos en la lista es relevante** |

⚠️ **Importante**, estos métodos son **exclusivos para listas**, no pueden ser utilizados con otro tipo de conjuntos de valores, como diccionarios.
