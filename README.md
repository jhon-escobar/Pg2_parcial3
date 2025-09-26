# Pg2_parcial3

# 📚 Medider - Librería de Validación de Datos

Medider es una librería Python especializada en validación de datos, diseñada con una arquitectura de clases base y especializadas para facilitar la validación de información personal y de contacto.

## 🚀 Instalación

### Opción 1: Instalación directa desde los archivos

bash
`
Clona o descarga el proyecto

`cd Pg2_parcial3`

Instala en modo desarrollo

`pip install -e .`

### Opción 2: Uso directo (sin instalación)

```python
import sys
sys.path.append('src') # Agrega la carpeta src al path

from medider import ValidadorDatosPersonales, ValidadorDatosContacto
```

### Opción 3: Instalación desde un paquete (futura versión)

bash
`pip install medider`

## 📁 Estructura del Proyecto

text
Pg2_parcial3/
├── src/
│ └── medider/
│ ├── **init**.py
│ └── validador.py
├── test/
│ └── test.py
├── README.md
└── requirements.txt

## 🏗️ Arquitectura de Clases

### `ValidadorBase` - Clase Base

Clase fundamental que contiene métodos genéricos de validación.

##### Métodos:

`validar_solo_numeros(texto: str) -> bool`: Valida que el texto contenga solo números

`validar_solo_letras(texto: str) -> bool`: Valida que el texto contenga solo letras y espacios

`validar_alfanumerico(texto: str) -> bool`: Valida que el texto sea alfanumérico

### `ValidadorDatosPersonales` - Validación de Datos Personales

Clase especializada que hereda de ValidadorBase y utiliza sus métodos internamente.

##### Métodos:

`validar_edad(edad: str) -> bool`: Valida que la edad sea un número entre 0-120

`validar_nombre(nombre: str) -> bool`: Valida nombres con solo letras y espacios

`validar_documento_identidad(documento: str) -> bool`: Valida formato de documento

### `ValidadorDatosContacto` - Validación de Datos de Contacto

Clase especializada que hereda de ValidadorBase para validación de contacto.

##### Métodos:

`validar_email(email: str) -> bool`: Valida formato de email

`validar_celular(celular: str) -> bool`: Valida números de celular (8-15 dígitos)

`validar_direccion(direccion: str) -> bool`: Valida direcciones con números y letras

## 💻 Uso Básico

##### Ejemplo 1: Validación de Datos Personales

python

```python
from medider import ValidadorDatosPersonales

validador = ValidadorDatosPersonales()

# Validar edad

print(validador.validar_edad("25")) # True
print(validador.validar_edad("150")) # False

# Validar nombre

print(validador.validar_nombre("Juan Pérez")) # True
print(validador.validar_nombre("Juan123")) # False

# Validar documento

print(validador.validar_documento_identidad("12345678A")) # True
print(validador.validar_documento_identidad("123")) # False
```

### Ejemplo 2: Validación de Datos de Contacto

python

```python
from medider import ValidadorDatosContacto

validador = ValidadorDatosContacto()

# Validar email

print(validador.validar_email("usuario@example.com")) # True
print(validador.validar_email("email.invalido")) # False

# Validar celular

print(validador.validar_celular("612345678")) # True
print(validador.validar_celular("123")) # False

# Validar dirección

print(validador.validar_direccion("Calle Principal 123")) # True
print(validador.validar_direccion("Calle Sin Número")) # False
```

### Ejemplo 3: Uso Combinado

python

```python
from medider import ValidadorDatosPersonales, ValidadorDatosContacto

def validar_usuario_completo(nombre, edad, email, celular):
validador_personal = ValidadorDatosPersonales()
validador_contacto = ValidadorDatosContacto()

    resultados = {
        'nombre': validador_personal.validar_nombre(nombre),
        'edad': validador_personal.validar_edad(edad),
        'email': validador_contacto.validar_email(email),
        'celular': validador_contacto.validar_celular(celular)
    }

    return all(resultados.values()), resultados

# Uso

valido, detalles = validar_usuario_completo(
"María García",
"30",
"maria@example.com",
"612345678"
)

print(f"Válido: {valido}")
print(f"Detalles: {detalles}")
```

## 🧪 Ejecución de Tests

##### Pruebas Unitarias

bash

Ejecutar todos los tests

`python test/test.py`

O usando unittest

`python -m unittest discover test/`

Con verbosidad

`python -m unittest discover test/ -v`

##### Verificación de Instalación

bash

Verificar que la librería funciona

`python -c "import sys; sys.path.append('src'); from medider import ValidadorDatosPersonales; v = ValidadorDatosPersonales(); print(f'Librería funcionando: {v.validar_nombre(\\\"Test\\\")}')"`

## 📋 Casos de Validación

##### Datos Personales Válidos

Campo Ejemplo Válido Ejemplo Inválido
Edad `"25"`, `"0"`, `"120" "150"`, `"abc"`, `"-5"`
Nombre `"Juan Pérez"`, `"María José"` `"Juan123"`, `"J"`
Documento `"12345678A"`, `"AB123456" "123"`, `"12@45"`

#### Datos de Contacto Válidos

Campo Ejemplo Válido Ejemplo Inválido
Email "usuario@example.com" "usuario@", "@example.com"
Celular "612345678", "+34612345678" "123", "abc"
Dirección "Calle 123" (mínimo 10 chars) "Calle", "123"

## 🔧 Desarrollo

#### Requisitos del Sistema

Python 3.7 o superior

Módulo `re` (incluido en la librería estándar de Python)

#### Estructura de Archivos

text
src/medider/
├── **init**.py # Exportación de clases
└── validador.py # Implementación principal

#### Extender la Librería

python

```python
from medider import ValidadorBase

class ValidadorPersonalizado(ValidadorBase):
def validar_codigo_postal(self, codigo: str) -> bool:
"""Valida formato de código postal"""
if not self.validar_solo_numeros(codigo):
return False
return len(codigo) == 5 # Ejemplo para España
```

## 🐛 Solución de Problemas

#### Error: `NameError`: `name 're' is not defined`

Solución: Asegúrate de que `import re` esté al inicio de `validador.py`

### Error: `ModuleNotFoundError`: `No module named 'medider'`

Solución: Agrega la carpeta `src` al path de Python:

python

```python
import sys
sys.path.append('src')
```

### Error en Tests

Solución: Verifica la estructura de archivos y que todos los imports estén correctos.

#### 📄 Licencia

Este proyecto está bajo la Licencia MIT. Ver archivo LICENSE para más detalles.

#### 🤝 Contribuciones

Las contribuciones son bienvenidas. Por favor:

Fork el proyecto

Crea una rama para tu feature

Commit tus cambios

Push a la rama

Abre un Pull Request

##### 📞 Soporte

Si encuentras problemas o tienes preguntas:

Revisa la documentación

Verifica los tests de ejemplo

Revisa los issues existentes
