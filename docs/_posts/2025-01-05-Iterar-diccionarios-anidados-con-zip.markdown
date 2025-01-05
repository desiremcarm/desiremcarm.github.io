---
layout: post
title: "Itera un diccionario de listas con zip()"
date: 2025-01-05 12:17:33 +0100
tags: [python, frontend]
sum: "Iterando un diccionario de listas anidadas con <code>zip()</code>."
---

### 📌 Resumen

En [este artículo](https://desiremcarm.github.io/2024/12/17/Iterar-con-zip-en-Python.html) ya hablamos de la función `zip()` en Python y lo útil que es, en este te traigo un caso de uso bastante común: iterar listas anidadas en un diccionario.

Para seguir el tutorial sin necesidad de crear un nuevo proyecto puedes utilizar
[este compilador Python online](https://www.programiz.com/python-programming/online-compiler/) 😉.

#### Resultado final:

Script:

```python
# Dict
npcs = {
    'npc_name': ['Pike', 'Scanlan', 'Grog'],
    'npc_class': ['Cleric', 'Bard', 'Barbarian'],
    'npc_level': [5, 5, 5]
}

# Zip function
for npc_n, npc_c, npc_l in zip(npcs['npc_name'], npcs['npc_class'], npcs['npc_level']):
    print(f"Name: {npc_n}, class: {npc_c}, level: {npc_l}")
```

Resultado:

```shell
Name: Pike, class: Cleric, level: 5
Name: Scanlan, class: Bard, level: 5
Name: Grog, class: Barbarian, level: 5
```

---

### Caso de uso

Imaginemos que tenemos un diccionario y dentro de cada clave tenemos una lista de valores.

```python
warlock_spells = {
    'name': ['Armor of Agathys', 'Banishment', 'Charm Person',
     'Arcane Gate', 'Cause Fear'],
    'level': [1, 4, 1, 6, 1]
}
```

Y queremos algo simple: **recorrer las listas de ambas claves y mostrar los valores conjuntamente**, quedando en el siguiente formato:

```shell
Spell name: Armor of Agathys; Spell level: 1
```

Hay varias formas de resolver esto, una de mis favoritas es utilizando la función `zip()` con un bucle `for`. Siento que es una forma sencilla, óptima y legible:

```python
for name, level in zip(warlock_spells['name'], warlock_spells['level']):
    print(f"Spell name: {name}; Spell level: {level}")
```

Resultado por consola:

```shell
Spell name: Armor of Agathys; Spell level: 1
Spell name: Banishment; Spell level: 4
Spell name: Charm Person; Spell level: 1
Spell name: Arcane Gate; Spell level: 6
Spell name: Cause Fear; Spell level: 1
```

En este código estamos utilizando un bucle **for** normal para iterar los valores **name** y **level**.

Le estamos indicando que queremos buscar ambos valores **conjuntamente y a la vez** (esto lo indicamos con `zip()`) en **warlock_spells['name']** es decir, el diccionario _warlock_spells_ en la lista contenida en la clave _name_, y también en **warlock_spells['level']**, es decir, en el diccionario _warlock_spells_ en la lista contenida en la clave _level_.

<mark>Es importante saber que esto sólo funciona si ambas listas son de igual longitud.</mark>

### ¿Y si las listas no son de igual longitud?

Pongamos que tenemos el siguiente diccionario de listas:

```python
warlock_spells = {
    'name': ['Armor of Agathys', 'Banishment', 'Charm Person',
     'Arcane Gate', 'Cause Fear'],
    'level': [1, 4, 1]
}
```

Como puedes ver, la clave _name_ contiene un total de 5 valores, pero _level_ sólo contiene 3.

En este caso no podríamos utilizar la función `zip()` en su forma simple, necesitamos su versión evolucionada, esta es: `zip_longest()`, la cual debemos importar para su uso:

```python
from itertools import zip_longest
```

En este caso, `zip_longest()` nos permite indicar qué valor por defecto queremos mostrar **si no encuentra un valor en la lista que está recorriendo** utilizando la instrucción _fillvalue="Valor por defecto"_:

```python
for name, level in zip_longest(warlock_spells['name'],
warlock_spells['level'], fillvalue="Unknown"):
    print(f"Spell name: {name}; Spell level: {level}")
```

Resultado en consola:

```shell
Spell name: Armor of Agathys; Spell level: 1
Spell name: Banishment; Spell level: 4
Spell name: Charm Person; Spell level: 1
Spell name: Arcane Gate; Spell level: Unknown
Spell name: Cause Fear; Spell level: Unknown
```

Si no indicas el parámetro que quieres por defecto en _fillvalue_, `zip_longest()` reemplazará el valor faltante con un `None`.
