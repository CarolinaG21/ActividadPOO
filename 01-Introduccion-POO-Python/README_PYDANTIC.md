# README_PYDANTIC.md

# Pydantic Documentation

## Introducción a Pydantic
Pydantic es una biblioteca de validación de datos y configuración en Python que permite definir modelos de datos utilizando clases. Su propósito principal es facilitar la validación y el manejo de datos, asegurando que los datos de entrada cumplan con las expectativas definidas en los modelos.

## Instalación
Para instalar Pydantic, puedes utilizar pip. Ejecuta el siguiente comando en tu terminal:

```
pip install pydantic
```

## Modelos de datos
En Pydantic, los modelos de datos se definen utilizando clases que heredan de `BaseModel`. Cada atributo de la clase representa un campo en el modelo, y puedes especificar tipos de datos para cada uno. Aquí tienes un ejemplo:

```python
from pydantic import BaseModel

class User(BaseModel):
    id: int
    name: str
    email: str
```

## Validación de datos
Pydantic valida automáticamente los datos de entrada al crear instancias de los modelos. Si los datos no cumplen con los tipos especificados, se generará un error de validación. Por ejemplo:

```python
user = User(id=1, name='John Doe', email='john.doe@example.com')  # Correcto
user = User(id='not_a_number', name='John Doe', email='john.doe@example.com')  # Error de validación
```

## Configuración de modelos
Puedes personalizar el comportamiento de los modelos utilizando configuraciones especiales. Por ejemplo, puedes establecer que los campos sean opcionales o definir valores predeterminados:

```python
from pydantic import BaseModel, Field

class User(BaseModel):
    id: int
    name: str
    email: str = Field(default='no-reply@example.com')
```

## Uso de Pydantic con FastAPI
Pydantic se integra perfectamente con FastAPI, una moderna biblioteca para construir APIs en Python. Puedes utilizar modelos de Pydantic para definir los datos de entrada y salida de tus endpoints. Aquí tienes un ejemplo:

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class User(BaseModel):
    id: int
    name: str
    email: str

@app.post("/users/")
async def create_user(user: User):
    return user
```

## Ejemplos prácticos
Pydantic es útil en una variedad de casos de uso, como la validación de datos de formularios, la configuración de aplicaciones y la creación de APIs. Aquí hay un ejemplo de cómo usar Pydantic para validar datos de configuración:

```python
from pydantic import BaseSettings

class Settings(BaseSettings):
    app_name: str
    admin_email: str

settings = Settings(app_name='My App', admin_email='admin@example.com')
```
