
Perfecto — te doy un procedimiento completo, paso a paso y listo para ejecutar en VS Code para crear el proyecto **UIII_Parisina_0559** con Django, el app `app_Parisina` y el CRUD de **Cliente** (sin `forms.py`). Incluyo comandos, estructura de carpetas, código para `models.py` (usaste el tuyo), `views.py`, `urls.py`, `admin.py`, y los templates con diseño sencillo y colores suaves. Todo en español y listo para pegar en VS Code.

---

# Resumen rápido de estructura (crear al inicio)

```
UIII_Parisina_0559/
├─ .venv/                  <- entorno virtual
├─ backend_Parisina/       <- proyecto Django (manage.py dentro aquí)
│  ├─ backend_Parisina/
│  │  ├─ settings.py
│  │  ├─ urls.py
│  │  └─ ...
│  ├─ app_Parisina/
│  │  ├─ migrations/
│  │  ├─ templates/
│  │  │  ├─ base.html
│  │  │  ├─ header.html
│  │  │  ├─ navbar.html
│  │  │  ├─ footer.html
│  │  │  ├─ inicio.html
│  │  │  └─ Cliente/
│  │  │     ├─ agregar_Cliente.html
│  │  │     ├─ ver_Cliente.html
│  │  │     ├─ actualizar_Cliente.html
│  │  │     └─ borrar_Cliente.html
│  │  ├─ views.py
│  │  ├─ urls.py
│  │  ├─ models.py
│  │  └─ admin.py
│  └─ manage.py
└─ README.md
```

---

# 1. Procedimiento para crear carpeta del Proyecto: `UIII_Parisina_0559`

En tu sistema (PowerShell / CMD / bash):

Windows Powershell / CMD o WSL:

```bash
# desde la carpeta donde quieras crear el proyecto
mkdir UIII_Parisina_0559
cd UIII_Parisina_0559
```

---

# 2. Procedimiento para abrir VS Code sobre la carpeta `UIII_Parisina_0559`

En la misma carpeta ejecuta:

```bash
code .
```

(esto abre VS Code en la carpeta actual).

---

# 3. Procedimiento para abrir terminal en VS Code

* En VS Code: `Ctrl + ` (la tecla de tilde invertida) o `Terminal` → `Nuevo Terminal`.

---

# 4. Procedimiento para crear carpeta entorno virtual “.venv” desde terminal de VS Code

(usa Python ya instalado)

Windows PowerShell:

```powershell
python -m venv .venv
```

Linux / macOS / WSL:

```bash
python3 -m venv .venv
```

---

# 5. Procedimiento para activar el entorno virtual

PowerShell (Windows):

```powershell
.venv\Scripts\Activate.ps1
# si te sale restricción de ejecución: en PowerShell como administrador:
# Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

CMD (Windows):

```cmd
.venv\Scripts\activate.bat
```

Bash (macOS / Linux / WSL):

```bash
source .venv/bin/activate
```

Verificar: el prompt mostrará `(.venv)`.

---

# 6. Procedimiento para activar intérprete de Python en VS Code

1. `Ctrl+Shift+P`
2. Escribe `Python: Select Interpreter`
3. Selecciona la ruta que apunte a `UIII_Parisina_0559/.venv/...` (ej. `.venv\Scripts\python.exe` o similar).

---

# 7. Procedimiento para instalar Django

Con entorno activado:

```bash
pip install --upgrade pip
pip install django
```

(Opcional: `pip freeze > requirements.txt` para guardar dependencias.)

---

# 8. Procedimiento para crear proyecto `backend_Parisina` sin duplicar carpeta

En la carpeta `UIII_Parisina_0559` crea el proyecto dentro de una subcarpeta `backend_Parisina`. Asegúrate de usar el punto `.` al ejecutar startproject desde adentro de la carpeta objetivo si quieres evitar doble anidamiento:

```bash
# crear carpeta del backend y moverse
mkdir backend_Parisina
cd backend_Parisina

# crear proyecto Django dentro de esta carpeta sin crear otra carpeta extra
django-admin startproject backend_Parisina .
```

(Nota: el último `.` crea el proyecto en la carpeta actual y evita `backend_Parisina/backend_Parisina` extra.)

---

# 9. Procedimiento para ejecutar servidor en el puerto 0559

Los puertos no llevan ceros a la izquierda en la ejecución; usaré el puerto **559** (equivalente lógico al 0559). Ejecuta desde `backend_Parisina` (donde está `manage.py`):

```bash
python manage.py runserver 559
```

O si quieres aceptar conexiones externas en la red local:

```bash
python manage.py runserver 0.0.0.0:559
```

---

# 10. Procedimiento para copiar y pegar el link en el navegador

* Cuando el servidor corre con `python manage.py runserver 559`, abre en tu navegador:

```
http://127.0.0.1:559/
```

o si usaste `0.0.0.0:559` en la máquina local:

```
http://<tu-ip-local>:559/
```

Copia y pega la URL en la barra del navegador.

---

# 11. Procedimiento para crear aplicación `app_Parisina`

Desde la carpeta con `manage.py`:

```bash
python manage.py startapp app_Parisina
```

Luego agrega la app a `INSTALLED_APPS` en `backend_Parisina/settings.py` (paso 25 abajo).

---

# 12. Aquí tu `models.py`

Usa el `models.py` que ya diste (lo pego tal cual para que no pierdas nada). Guarda en `backend_Parisina/app_Parisina/models.py`:

```python
from django.db import models

# ==========================================
# MODELO: CLIENTE
# ==========================================
class Cliente(models.Model):
    nombre = models.CharField(max_length=100)
    apellido = models.CharField(max_length=100)
    correo_electronico = models.EmailField(unique=True)
    telefono = models.CharField(max_length=15)
    direccion = models.CharField(max_length=200)
    ciudad = models.CharField(max_length=100)
    fecha_registro = models.DateField(auto_now_add=True)

    def __str__(self):
        return f"{self.nombre} {self.apellido}"

# ==========================================
# MODELO: PROVEEDOR
# ==========================================
class Proveedor(models.Model):
    nombre_empresa = models.CharField(max_length=150)
    contacto = models.CharField(max_length=100)
    correo = models.EmailField()
    telefono = models.CharField(max_length=15)
    direccion = models.CharField(max_length=200)
    pais = models.CharField(max_length=100)
    fecha_registro = models.DateField(auto_now_add=True)

    def __str__(self):
        return self.nombre_empresa

# ==========================================
# MODELO: PRODUCTO
# ==========================================
class Producto(models.Model):
    nombre = models.CharField(max_length=150)
    descripcion = models.TextField()
    categoria = models.CharField(max_length=100)
    precio = models.DecimalField(max_digits=10, decimal_places=2)
    stock = models.PositiveIntegerField()
    cliente = models.ForeignKey(Cliente, on_delete=models.CASCADE, related_name='productos')
    proveedores = models.ManyToManyField(Proveedor, related_name='productos')

    def __str__(self):
        return self.nombre
```

> Como indicaste, por ahora trabajaremos sólo con `Cliente`; deja `Proveedor` y `Producto` sin usar por ahora.

---

# 12.5 Procedimiento para realizar las migraciones (`makemigrations` y `migrate`)

Desde donde está `manage.py`:

```bash
# Crear migraciones para tu app
python manage.py makemigrations app_Parisina

# Aplicar migraciones
python manage.py migrate
```

---

# 13. Primero trabajamos con el MODELO: CLIENTE

Entendido — todo lo siguiente implementa el CRUD de Cliente.

---

# 14. En `views.py` de `app_Parisina` crear funciones:

Crea/edita `backend_Parisina/app_Parisina/views.py` con este código:

```python
from django.shortcuts import render, redirect, get_object_or_404
from .models import Cliente

# Página inicio del sistema
def inicio_parisina(request):
    return render(request, "inicio.html")

# Agregar cliente (muestra formulario y procesa POST)
def agregar_cliente(request):
    if request.method == "POST":
        nombre = request.POST.get("nombre", "").strip()
        apellido = request.POST.get("apellido", "").strip()
        correo = request.POST.get("correo_electronico", "").strip()
        telefono = request.POST.get("telefono", "").strip()
        direccion = request.POST.get("direccion", "").strip()
        ciudad = request.POST.get("ciudad", "").strip()

        Cliente.objects.create(
            nombre=nombre,
            apellido=apellido,
            correo_electronico=correo,
            telefono=telefono,
            direccion=direccion,
            ciudad=ciudad
        )
        return redirect("ver_cliente")
    return render(request, "Cliente/agregar_Cliente.html")

# Ver clientes (lista en tabla)
def ver_cliente(request):
    clientes = Cliente.objects.all().order_by("-fecha_registro")
    return render(request, "Cliente/ver_Cliente.html", {"clientes": clientes})

# Mostrar formulario para actualizar cliente
def actualizar_cliente(request, pk):
    cliente = get_object_or_404(Cliente, pk=pk)
    return render(request, "Cliente/actualizar_Cliente.html", {"cliente": cliente})

# Procesar la actualización (acción POST)
def realizar_actualizacion_cliente(request, pk):
    cliente = get_object_or_404(Cliente, pk=pk)
    if request.method == "POST":
        cliente.nombre = request.POST.get("nombre", cliente.nombre)
        cliente.apellido = request.POST.get("apellido", cliente.apellido)
        cliente.correo_electronico = request.POST.get("correo_electronico", cliente.correo_electronico)
        cliente.telefono = request.POST.get("telefono", cliente.telefono)
        cliente.direccion = request.POST.get("direccion", cliente.direccion)
        cliente.ciudad = request.POST.get("ciudad", cliente.ciudad)
        cliente.save()
        return redirect("ver_cliente")
    # si no es POST, redirigir a formulario
    return redirect("actualizar_cliente", pk=pk)

# Borrar cliente (confirmación GET y eliminación POST)
def borrar_cliente(request, pk):
    cliente = get_object_or_404(Cliente, pk=pk)
    if request.method == "POST":
        cliente.delete()
        return redirect("ver_cliente")
    return render(request, "Cliente/borrar_Cliente.html", {"cliente": cliente})
```

---

# 15. Crear la carpeta `templates` dentro de `app_Parisina`

En `backend_Parisina/app_Parisina/` crea carpeta `templates` y luego los archivos indicados.

---

# 16. En `templates` crear archivos HTML (`base.html`, `header.html`, `navbar.html`, `footer.html`, `inicio.html`)

Coloca estos ficheros en `app_Parisina/templates/`. (A continuación el código.)

## `base.html`

Guarda en `app_Parisina/templates/base.html`:

```html
<!doctype html>
<html lang="es">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Parisina - Sistema</title>

    <!-- Bootstrap CSS (CDN) -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>
      /* Colores suaves y modernos */
      :root{
        --primario: #E8F6EF; /* verde muy suave */
        --secundario: #F9F7FF; /* lila claro */
        --acento: #CDE7F0; /* celeste ligero */
        --texto: #2b2b2b;
      }
      body { background: var(--secundario); color: var(--texto); }
      .navbar-brand { font-weight: 700; color: #2b2b2b !important; }
      .card { border-radius: 12px; box-shadow: 0 6px 18px rgba(0,0,0,0.06); }
      footer { background: white; padding: 12px 0; position: fixed; bottom:0; width:100%; border-top: 1px solid #eee; }
      main { padding-bottom: 80px; } /* espacio para footer fijo */
    </style>
  </head>
  <body>
    {% include "navbar.html" %}
    <main class="container py-4">
      {% block content %}{% endblock %}
    </main>

    {% include "footer.html" %}

    <!-- Bootstrap JS (CDN) -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
  </body>
</html>
```

## `navbar.html`

Guarda en `app_Parisina/templates/navbar.html`:

```html
<nav class="navbar navbar-expand-lg" style="background: var(--primario);">
  <div class="container">
    <a class="navbar-brand" href="{% url 'inicio_parisina' %}">Sistema de Administración Parisina</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navmenu">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navmenu">
      <ul class="navbar-nav ms-auto">
        <li class="nav-item"><a class="nav-link" href="{% url 'inicio_parisina' %}">Inicio</a></li>

        <!-- Cliente -->
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown">Cliente</a>
          <ul class="dropdown-menu">
            <li><a class="dropdown-item" href="{% url 'agregar_cliente' %}">Agregar Cliente</a></li>
            <li><a class="dropdown-item" href="{% url 'ver_cliente' %}">Ver Cliente</a></li>
            <li><a class="dropdown-item" href="#">Actualizar Cliente</a></li>
            <li><a class="dropdown-item" href="#">Borrar Cliente</a></li>
          </ul>
        </li>

        <!-- Proveedor -->
        <li class="nav-item dropdown ms-2">
          <a class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown">Proveedor</a>
          <ul class="dropdown-menu">
            <li><a class="dropdown-item" href="#">Agregar Proveedor</a></li>
            <li><a class="dropdown-item" href="#">Ver Proveedor</a></li>
            <li><a class="dropdown-item" href="#">Actualizar Proveedor</a></li>
            <li><a class="dropdown-item" href="#">Borrar Proveedor</a></li>
          </ul>
        </li>

        <!-- Producto -->
        <li class="nav-item dropdown ms-2">
          <a class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown">Producto</a>
          <ul class="dropdown-menu">
            <li><a class="dropdown-item" href="#">Agregar Producto</a></li>
            <li><a class="dropdown-item" href="#">Ver Producto</a></li>
            <li><a class="dropdown-item" href="#">Actualizar Producto</a></li>
            <li><a class="dropdown-item" href="#">Borrar Producto</a></li>
          </ul>
        </li>

      </ul>
    </div>
  </div>
</nav>
```

## `footer.html`

Guarda en `app_Parisina/templates/footer.html`:

```html
<footer class="text-center">
  <div class="container">
    <small>© {{ now.year }} Parisina. Creado por De La Rosa Abril, Cbtis 128. Todos los derechos reservados.</small>
  </div>
</footer>
```

> `now` lo puedes proporcionar en cada vista con `from django.utils import timezone` si quieres, o también usar el template tag `now`:
> En el `base.html` antes del cierre `</body>` podrías pasar `{% now "Y" as year %}` y en footer usar `{{ year }}`. Pero el ejemplo anterior usa `{{ now.year }}` — si no aparece, Django mostrará vacío; alternativa simple: reemplaza `{{ now.year }}` por un año fijo o usa el tag `{% now "Y" %}`. Para simplicidad, reemplaza por `{% now "Y" %}`:

```html
<small>© {% now "Y" %} Parisina. Creado por De La Rosa Abril, Cbtis 128. Todos los derechos reservados.</small>
```

## `inicio.html`

Guarda en `app_Parisina/templates/inicio.html`:

```html
{% extends "base.html" %}
{% block content %}
<div class="row">
  <div class="col-md-7">
    <div class="card p-4">
      <h3>Bienvenido al Sistema Parisina</h3>
      <p>Este es el panel de administración básico para gestionar clientes, proveedores y productos.</p>
      <p>Usa el menú para navegar entre las opciones del sistema.</p>
    </div>
  </div>
  <div class="col-md-5">
    <div class="card p-2">
      <img src="https://images.pexels.com/photos/373965/pexels-photo-373965.jpeg" alt="Parisina" class="img-fluid rounded">
      <small class="d-block mt-2 text-muted">Imagen de Parisina (tomada de la web para uso ilustrativo).</small>
    </div>
  </div>
</div>
{% endblock %}
```

(La URL de imagen es pública en Pexels; puedes cambiarla por otra si prefieres.)

---

# 21 y 22. Crear subcarpeta `Cliente` y archivos HTML para CRUD

Crea carpeta `app_Parisina/templates/Cliente/` y agrega:

## `agregar_Cliente.html`

```html
{% extends "base.html" %}
{% block content %}
<div class="card p-4">
  <h4>Agregar Cliente</h4>
  <form method="post">
    {% csrf_token %}
    <div class="mb-3"><label class="form-label">Nombre</label><input name="nombre" class="form-control"></div>
    <div class="mb-3"><label class="form-label">Apellido</label><input name="apellido" class="form-control"></div>
    <div class="mb-3"><label class="form-label">Correo electrónico</label><input name="correo_electronico" type="email" class="form-control"></div>
    <div class="mb-3"><label class="form-label">Teléfono</label><input name="telefono" class="form-control"></div>
    <div class="mb-3"><label class="form-label">Dirección</label><input name="direccion" class="form-control"></div>
    <div class="mb-3"><label class="form-label">Ciudad</label><input name="ciudad" class="form-control"></div>
    <button class="btn btn-primary">Guardar</button>
    <a href="{% url 'ver_cliente' %}" class="btn btn-outline-secondary">Cancelar</a>
  </form>
</div>
{% endblock %}
```

## `ver_Cliente.html`

```html
{% extends "base.html" %}
{% block content %}
<div class="card p-3">
  <h4>Lista de Clientes</h4>
  <a href="{% url 'agregar_cliente' %}" class="btn btn-success mb-3">+ Agregar Cliente</a>
  <div class="table-responsive">
    <table class="table table-striped">
      <thead>
        <tr>
          <th>Nombre</th><th>Apellido</th><th>Correo</th><th>Tel</th><th>Ciudad</th><th>Registrado</th><th>Acciones</th>
        </tr>
      </thead>
      <tbody>
        {% for c in clientes %}
        <tr>
          <td>{{ c.nombre }}</td>
          <td>{{ c.apellido }}</td>
          <td>{{ c.correo_electronico }}</td>
          <td>{{ c.telefono }}</td>
          <td>{{ c.ciudad }}</td>
          <td>{{ c.fecha_registro }}</td>
          <td>
            <a class="btn btn-sm btn-info" href="{% url 'actualizar_cliente' c.pk %}">Editar</a>
            <a class="btn btn-sm btn-danger" href="{% url 'borrar_cliente' c.pk %}">Borrar</a>
          </td>
        </tr>
        {% empty %}
        <tr><td colspan="7" class="text-center">No hay clientes</td></tr>
        {% endfor %}
      </tbody>
    </table>
  </div>
</div>
{% endblock %}
```

## `actualizar_Cliente.html`

```html
{% extends "base.html" %}
{% block content %}
<div class="card p-4">
  <h4>Actualizar Cliente</h4>
  <form method="post" action="{% url 'realizar_actualizacion_cliente' cliente.pk %}">
    {% csrf_token %}
    <div class="mb-3"><label class="form-label">Nombre</label><input name="nombre" value="{{ cliente.nombre }}" class="form-control"></div>
    <div class="mb-3"><label class="form-label">Apellido</label><input name="apellido" value="{{ cliente.apellido }}" class="form-control"></div>
    <div class="mb-3"><label class="form-label">Correo electrónico</label><input name="correo_electronico" value="{{ cliente.correo_electronico }}" type="email" class="form-control"></div>
    <div class="mb-3"><label class="form-label">Teléfono</label><input name="telefono" value="{{ cliente.telefono }}" class="form-control"></div>
    <div class="mb-3"><label class="form-label">Dirección</label><input name="direccion" value="{{ cliente.direccion }}" class="form-control"></div>
    <div class="mb-3"><label class="form-label">Ciudad</label><input name="ciudad" value="{{ cliente.ciudad }}" class="form-control"></div>
    <button class="btn btn-primary">Guardar cambios</button>
    <a href="{% url 'ver_cliente' %}" class="btn btn-outline-secondary">Cancelar</a>
  </form>
</div>
{% endblock %}
```

## `borrar_Cliente.html`

```html
{% extends "base.html" %}
{% block content %}
<div class="card p-4">
  <h4>Eliminar Cliente</h4>
  <p>¿Deseas eliminar a <strong>{{ cliente.nombre }} {{ cliente.apellido }}</strong>?</p>
  <form method="post">
    {% csrf_token %}
    <button type="submit" class="btn btn-danger">Sí, eliminar</button>
    <a href="{% url 'ver_cliente' %}" class="btn btn-outline-secondary">Cancelar</a>
  </form>
</div>
{% endblock %}
```

---

# 23. No utilizar `forms.py`

OK — usamos `request.POST` directamente en las vistas (sin validaciones).

---

# 24. Procedimiento para crear el archivo `urls.py` en `app_Parisina`

Crea `backend_Parisina/app_Parisina/urls.py` con:

```python
from django.urls import path
from . import views

urlpatterns = [
    path("", views.inicio_parisina, name="inicio_parisina"),
    path("cliente/agregar/", views.agregar_cliente, name="agregar_cliente"),
    path("cliente/ver/", views.ver_cliente, name="ver_cliente"),
    path("cliente/actualizar/<int:pk>/", views.actualizar_cliente, name="actualizar_cliente"),
    path("cliente/realizar_actualizacion/<int:pk>/", views.realizar_actualizacion_cliente, name="realizar_actualizacion_cliente"),
    path("cliente/borrar/<int:pk>/", views.borrar_cliente, name="borrar_cliente"),
]
```

---

# 25. Procedimiento para agregar `app_Parisina` en `settings.py` de `backend_Parisina`

Editar `backend_Parisina/settings.py` y en `INSTALLED_APPS` añade la app:

```python
INSTALLED_APPS = [
    # apps por defecto...
    'app_Parisina',
]
```

Además, para que Django encuentre tus templates, en `TEMPLATES` dentro de settings.py asegúrate de que `APP_DIRS` esté en `True` (por defecto lo está). Si quieres agregar una carpeta global `templates` usa `TEMPLATES[0]['DIRS'] = [BASE_DIR / 'templates']`, pero con `APP_DIRS=True` y la estructura `app_Parisina/templates/...` Django los encontrará.

---

# 26. Configurar `urls.py` de `backend_Parisina` para enlazar con `app_Parisina`

Edita `backend_Parisina/urls.py` (el del proyecto) así:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('app_Parisina.urls')),  # enruta la app principal
]
```

---

# 27. Procedimiento para registrar los modelos en `admin.py` y volver a realizar las migraciones

Editar `backend_Parisina/app_Parisina/admin.py`:

```python
from django.contrib import admin
from .models import Cliente, Proveedor, Producto

@admin.register(Cliente)
class ClienteAdmin(admin.ModelAdmin):
    list_display = ('nombre', 'apellido', 'correo_electronico', 'telefono', 'ciudad', 'fecha_registro')
    search_fields = ('nombre', 'apellido', 'correo_electronico')

@admin.register(Proveedor)
class ProveedorAdmin(admin.ModelAdmin):
    list_display = ('nombre_empresa', 'contacto', 'correo', 'telefono', 'pais', 'fecha_registro')

@admin.register(Producto)
class ProductoAdmin(admin.ModelAdmin):
    list_display = ('nombre', 'categoria', 'precio', 'stock')
    filter_horizontal = ('proveedores',)
```

Luego recrear migraciones si cambiaste models (si no cambiaste: los pasos ya hechos):

```bash
python manage.py makemigrations
python manage.py migrate
```

---

# 27 (nota) — por lo pronto solo trabajar con `Cliente`

Deja las vistas y templates de `Proveedor` y `Producto` pendientes; el admin ya los registra pero no los usarás aún.

---

# 28. Estilo: colores suaves, sencillo

Los templates usan paleta suave en `base.html`; el HTML es simple con Bootstrap.

---

# 29. Al inicio crear la estructura completa de carpetas y archivos

Puedes crear estructura con comandos (ejemplo en bash):

```bash
cd UIII_Parisina_0559/backend_Parisina
mkdir -p app_Parisina/templates/Cliente
touch app_Parisina/views.py app_Parisina/urls.py app_Parisina/admin.py app_Parisina/models.py
# luego pega el contenido correspondiente en VS Code
```

---

# 30. Proyecto totalmente funcional

Siguiendo los pasos anteriores (crear entorno, instalar Django, crear proyecto, crear app, pegar modelos, vistas, urls, templates, registrar admin, migraciones) tendrás un proyecto funcional que permite crear, listar, actualizar y borrar clientes.

---

# 31. Finalmente ejecutar servidor en el puerto 0559

Ejecuta (desde la carpeta con `manage.py`):

```bash
python manage.py runserver 559
```

y visita `http://127.0.0.1:559/`.

---

## Comandos resumen (rápido, copiar/pegar)

```bash
# 1 crear carpeta y abrir VS Code
mkdir UIII_Parisina_0559
cd UIII_Parisina_0559
code .

# 2 crear virtualenv
python -m venv .venv
# activar (PowerShell)
.venv\Scripts\Activate.ps1

# 3 instalar Django
pip install --upgrade pip
pip install django

# 4 crear proyecto dentro de folder backend_Parisina
mkdir backend_Parisina
cd backend_Parisina
django-admin startproject backend_Parisina .

# 5 crear app
python manage.py startapp app_Parisina

# (pegar los archivos models.py, views.py, templates, urls.py, admin.py, editar settings.py)
# luego:
python manage.py makemigrations
python manage.py migrate

# crear superusuario si quieres administrar con admin
python manage.py createsuperuser

# ejecutar servidor en puerto 559
python manage.py runserver 559
```

---

## Notas finales y recomendaciones

* He respetado que **no uses `forms.py`**: los formularios se procesan con `request.POST`.
* No añadí validaciones (tal como pediste).
* Para la imagen de `inicio.html` utilicé una imagen pública de ejemplo; si quieres otra, dime la URL y la cambio.
* Si quieres que la footer use el año dinámico con `{% now "Y" %}` debes asegurarte de tener `{% load tz %}` si necesario; la forma que di con `{% now "Y" %}` funciona en plantillas normales.
* Si tu sistema Windows bloquea `runserver` en puerto 559, intenta otro puerto (ej. 8000), pero pediste 0559, así que usé 559.

---

Si quieres, pego ahora el contenido completo y listo para pegar de cada archivo (`settings.py` cambios cortos, `views.py`, `urls.py` del app y del proyecto, `admin.py` y los templates) en el chat para que copies uno por uno. ¿Quieres que te entregue los archivos listos (cada archivo en un bloque separado) o prefieres seguir y yo te doy los snippets restantes (por ejemplo `settings.py` mínimos a modificar)?
