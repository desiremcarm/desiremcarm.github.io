---
layout: post
title: "Crea una API con FastAPI y Python"
date: 2024-12-21 18:17:33 +0100
tags: [python, apis, backend]
sum: "Crea una API simple y funcional utilizando FastAPI y Python."
---

### 📌 Resumen

En este artículo te enseño a **crear una API simple utilizando FastAPI y Python**. Forma parte de una serie de artículos en los que también añadiremos validación de modelos y una base de datos con SQLite.

<details>

  <summary>
  
  <h3>🗂️ Pre-requisitos</h3> (Click para abrir la sección)
  
  </summary>

  <hr>

  <div markdown="1">
  
  **Puedes omitir esta parte si ya tienes una carpeta para el proyecto y un entorno virtual creado**.

Para poder desarrollar una pequeña API con FastAPI y Python, te recomiendo seguir las siguientes instrucciones:

1️⃣. Crea una carpeta en tu PC para alojar el proyecto

2️⃣. Instala Python si no lo tenías instalado

3️⃣. Crea un entorno virtual para trabajar cómodamente en el proyecto

Personalmente te recomiendo `virtualenv`. Para crear un ambiente virtual con `virtualenv` primero debes instalar `virtualenv` si no lo tienes:

```shell
pip install virtualenv
```

A continuación, **dentro de la carpeta que alojará el proyecto**, escribiremos la siguiente instrucción para crear nuestro entorno virtual:

```shell
virtualenv env
```

Una vez se haya creado es neceario **activar dicho entorno**. Si utilizas Windows, escribe:

```shell
env\Scripts\activate
```

Si utilizas Mac o Linux, escribe:

```shell
source env/bin/activate
```

Deberías ver en la consola que estás dentro de tu entorno porque la ubicación se precede con un `(env)`:

```shell
(env) C:\Users\...
```

  </div>
</details>

## 🟪 Instalar FastAPI

Una vez dentro de nuestro entorno virtual, instalaremos `FastAPI` utilizando la siguiente instrucción:

```shell
pip install fastapi uvicorn
```

## 🟪 Configurando la API

En la carpeta del proyecto crearemos un nuevo fichero llamado `main.py`.

1️⃣. Dentro de este fichero **importaremos fastAPI**:

```python
from fastapi import FastAPI
```

2️⃣. Creamos una **instancia de la aplicación** para poder definirla y utilizarla:

```python
from fastapi import FastAPI

# FastAPI instance
app = FastAPI()
```

3️⃣. Definir **la ruta home**:

Esta será la primera ruta que aparezca al visitar la API desde nuestro navegador. Es la ruta principal por defecto de `app`:

```python
from fastapi import FastAPI

# FastAPI instance
app = FastAPI()

# Root HOME
@app.get("/")
def root():
    return {"msg": "Hello!"}
```

Más tarde entraremos en explicación de qué está pasando.

Por ahora, le estamos indicando a la aplicación que la principal devuelva un simple mensaje: `Hello!`

4️⃣. Iniciar el servidor:

A continuación **iniciaremos el servidor** para poder ver la API en funcionamiento.

Para iniciar el servidor, escribe la siguiente instrucción en la consola:

```shell
uvicorn main:app --reload
```

Para ver el resultado, visita la dirección en localhost donde la API te informa que ha iniciado el servicio. Te indicará esa dirección en la consola:

```shell
]
INFO:     Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C to quit)
...
```

Ahí deberías ver tu mensaje de esta forma:

```json
{
  "msg": "Hello!"
}
```

## 🟪 Explicación

#### Importar FastAPI

Con esta línea de código:

```python
from fastapi import FastAPI
```

Estamos indicando al programa que vamos a utilizar FastAPI. Importándola tenemos acceso a todas sus funcionalidades.

#### Crear una instancia de FastAPI

Importándola no es suficiente, **para poder utilizar lo que acabamos de importar necesitamos crear un recipiente en nuestro programa** donde guardar una instancia de FastApi y así poder acceder a todas sus funciones y herramientas.

```python
# Creating FastAPI instance
app = FastAPI()
```

En este caso llamamos al recipiente `app` por convención, porque se trata de la propia aplicación.

Quiero que entiendas bien esto.

Lo estamos llamando `app` y a continuación, para arrancar el servicio, estamos utilizando instrucción `uvicorn main:app --reload`.

`Uvicorn` es el servidor, es decir, lo que da vida a nuestra aplicación.
Con la instrucciónn anterior le estamos indicando que **debe buscar la aplicación (o recipiente) `app` dentro del archivo `main`** y debe arrancar con la información que tenga disponible ahí.

Si nuestra `app` en lugar de "app" se llamase "mofa_viciosa":

```python
from fastapi import FastAPI

# FastAPI instance
mofa_viciosa = FastAPI()

# Root HOME
@mofa_viciosa.get("/")
def root():
    return {"msg": "Hello!"}
```

Deberíamos iniciar el servidor con la instrucción:

```shell
uvicorn main:mofa_viciosa --reload
```

#### Definición de rutas

Una API se compone en esencia de endpoints o rutas, por ejemplo: `"/products"`, `"/products/product_id"`, `"/categories/fantasy"`, etc.

Estamos definiendo la primera ruta de nuestra aplicación, la de home, de la siguiente manera:

```python
# Root HOME
@app.get("/")
def root():
    return {"msg": "Hello!"}
```

Desglosemos un poco qué hay aquí.

Lo primero que encontramos es un **decorador**, decorando la función `def root`.

```python
# Root HOME
@app.get("/")
```

No te asustes si los decoradores no te suenan o te suenan poco.

Los cubriremos en profundidad en otro artículo, por ahora te basta con saber que **un decorador en Python no es más que una función que recibe otra función y le añade funcionalidad extra**.

En FastAPI los decoradores **se utilizan principalmente para definir los endpoints o rutas de la aplicación**.

En esa pieza de código estamos utilizando un decorador para definir una ruta, este caso la ruta por defecto `"/"`, con un método concreto, en este caso `get`.

Así, cuando un navegador visite la ruta `"/"` de nuestra aplicación, se ejecutará la función que indique este decorador, en este caso será la función `def root`.

#### La función bajo el decorador

Como hemos comentado anteriormente, el decorador `@app.get("/")` está decorando la función `def root`, por lo tanto, al visitar la ruta `"/"` de nuestro proyecto, se ejecutará el código que exista dentro de la función `def root`:

```python
# Root HOME
@app.get("/")
def root():
    return {"msg": "Hello!"}
```

En este caso, esta función simplemente manda un `Hello!`, pero podría devolver cualquier cosa.

Por ejemplo, una lista de hechizos de bardo:

```python
# Root HOME
@app.get("/")
def root():
    bard_spells = ["Risa fantástica", "Disfrazarse",
    "Invisibilidad", "Voz terriblemente poderosa",]
    return bard_spells
```

El nombre de la función, `root`, también es una convención por buenas prácticas.
Bien podría llamarse `not_another_bard_please()` y funcionaría, pero no es tan legible y claro como `root` 😉

## Reto: crea otra ruta

Intenta crear una o dos rutas más de tipo `get`, una de ellas buscando un ID concreto.

Abajo os dejo una posible solución.

<details>

  <summary>
  
  <h3>🗂️ Solución</h3> (Click para abrir la sección)
  
  </summary>

  <hr>

  <div markdown="1">

```python

from fastapi import FastAPI

# Getting the APP
app = FastAPI()

# Root HOME
@app.get("/")
def root():
    return {"msg": "Hello!"}

# List of bard spells
bard_spells = ["Risa fantástica", "Disfrazarse",
    "Invisibilidad", "Voz terriblemente poderosa",]


@app.get("/spells")
def get_spells():
    """ Function to retrieve all bard spells """
    return bard_spells


@app.get("/spells/{spell_id}")
def get_single_spell(spell_id: int):
    """ This function retrieves a bard spell given an ID.
    Before searching the spell, we check wether the spell_id
    is greater than 0 (not negative) and less than the total
    length of the bard_spells list.
    """
    if 0 <= spell_id < len(bard_spells):
        return bard_spells[spell_id]
    else:
      # If the spell is not found...
        return "Spell not found!"

```

  </div>

</details>

## Conclusión

¡Y sólo hemos rascado un poco la superficie!

FastAPI es rápida (😆), cómoda y sencilla de aprender y utilizar.

Espero que los artículos sobre su funcionamiento te puedan ser de utilidad. Un abrazo.
