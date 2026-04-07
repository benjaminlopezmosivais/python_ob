## 📂 Paso 1: Crear entorno virtual

Es recomendable trabajar en un **virtualenv** para aislar dependencias.

usar este comando en caso de tener mas de una version de python para crear diferentes entornos virtuales:

py -3.10 -m venv venv15

py -3.13-m venv venv18
## Nota

python C:\Python313\odoo\comunity\odoo\odoo-bin -c C:\Python313\odoo\community.conf -d odoo_community -u l10n_mx_sat_descarga

python ./../odoo-bin -c ./odoo.conf  -d odoo_15

---------------

python -m venv venv
usara el por defecto antes no pasaba nada por que solo se tenia una version

------------------------
 Entrar a psql
 & "C:\Program Files\PostgreSQL\18\bin\psql.exe" -U odoo -d postgres

```
# Crear carpeta del proyecto
mkdir mi_pos
cd mi_pos

# Crear entorno virtual
python -m venv env

# Activar entorno
# En Linux/Mac
source env/bin/activate
# En Windows
env\Scripts\activate
```

## 🛠️ Paso 2: Instalar Django

Con el entorno activado:

bash

```
pip install django
```

Verifica la instalación:

bash

```
django-admin --version
```

## 📑 Paso 3: Crear proyecto Django

bash

```
django-admin startproject punto_venta
cd punto_venta
```

Estructura inicial:

Código

```
punto_venta/
    manage.py
    punto_venta/
        settings.py
        urls.py
        wsgi.py
```

## 🖥️ Paso 4: Ejecutar servidor

bash

```
python manage.py runserver
```

Abre en navegador: 👉 `http://127.0.0.1:8000/`

## 📦 Paso 5: Crear aplicación para ventas

bash

```
python manage.py startapp ventas
```

Agrega `'ventas'` en `INSTALLED_APPS` dentro de `settings.py`.

## 🚀 Paso 6: Primer modelo

Ejemplo de modelo para productos:

python

```
# ventas/models.py
from django.db import models

class Producto(models.Model):
    nombre = models.CharField(max_length=100)
    precio_unitario = models.DecimalField(max_digits=10, decimal_places=2)
    stock = models.PositiveIntegerField(default=0)

    def __str__(self):
        return self.nombre
```

Aplica migraciones:

bash

```
python manage.py makemigrations
python manage.py migrate
```

## ✅ Resultado

Ya tienes:

- Django instalado en un entorno virtual.
    
- Proyecto base (`punto_venta`).
    
- App inicial (`ventas`).
    
- Primer modelo (`Producto`).


cambiesinis