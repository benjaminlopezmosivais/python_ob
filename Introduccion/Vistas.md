## 🛠️ Paso 1: Vista para registrar ventas

python

```
# ventas/views.py
from django.shortcuts import render, redirect
from .models import Producto, Venta
from django.db.models import Sum

def registrar_venta(request):
    if request.method == "POST":
        producto_id = request.POST["producto"]
        cantidad = int(request.POST["cantidad"])
        producto = Producto.objects.get(id=producto_id)
        total = cantidad * producto.precio_unitario

        Venta.objects.create(
            producto=producto,
            cantidad=cantidad,
            total=total,
            estado_pago="efectivo"
        )
        return redirect("resumen")

    productos = Producto.objects.all()
    return render(request, "ventas/registrar.html", {"productos": productos})


def resumen(request):
    ventas = Venta.objects.all()
    total_general = ventas.aggregate(total=Sum("total"))["total"]
    return render(request, "ventas/resumen.html", {"ventas": ventas, "total_general": total_general})
```

## 📑 Paso 2: Configurar URLs

python

```
# punto_venta/urls.py
from django.contrib import admin
from django.urls import path
from ventas import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('registrar/', views.registrar_venta, name="registrar"),
    path('resumen/', views.resumen, name="resumen"),
]
```

## 🖥️ Paso 3: Templates

### `ventas/templates/ventas/registrar.html`

html

```
<h2>Registrar Venta</h2>
<form method="post">
  {% csrf_token %}
  <label>Producto:</label>
  <select name="producto">
    {% for p in productos %}
      <option value="{{ p.id }}">{{ p.nombre }} - ${{ p.precio_unitario }}</option>
    {% endfor %}
  </select><br><br>

  <label>Cantidad:</label>
  <input type="number" name="cantidad" min="1" required><br><br>

  <button type="submit">Guardar Venta</button>
</form>
```

### `ventas/templates/ventas/resumen.html`

html

```
<h2>Resumen de Ventas</h2>
<ul>
  {% for v in ventas %}
    <li>{{ v.producto.nombre }} - {{ v.cantidad }} piezas - ${{ v.total }}</li>
  {% endfor %}
</ul>
<p><strong>Total General: ${{ total_general }}</strong></p>
```

## 🚀 Paso 4: Probar

1. Corre el servidor:
    
    bash
    
    ```
    python manage.py runserver
    ```
    
2. Ve a `http://127.0.0.1:8000/registrar/` para registrar una venta.
    
3. Luego a `http://127.0.0.1:8000/resumen/` para ver el listado y el total.