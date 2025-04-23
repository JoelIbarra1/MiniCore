# MiniCore Task Filter - FastAPI App

MiniCore es una aplicación web construida con **FastAPI** que permite filtrar tareas que se encuentran "In Progress" y que han excedido su tiempo estimado, dentro de un rango de fechas definido por el usuario. La visualización se hace mediante un archivo HTML usando el motor de plantillas **Jinja2**.

---

## Funcionalidades

- Visualización de tareas en progreso cuyo estimado ya pasó.
- Filtro de tareas por rango de fechas.
- Base de datos SQLite precargada desde un archivo `.sql`.
- Redirección automática desde `/` hacia `/filter-inprogress-tasks`.
- Despliegue en la nube mediante **Render**.

---

## Estructura del Proyecto

```
MINICORE-MAIN/
│
├── db/
│   ├── data.sql                 # Script SQL que inicializa la base de datos
│   ├── db_connection.py         # Conexión a SQLite con SQLAlchemy
│   └── db.py                    # Modelos de SQLAlchemy (Empleado, Proyecto, Tarea)
│
├── templates/
│   └── filter_inprogress_tasks.html # Template Jinja2 que renderiza los resultados
│
├── main.py                      # Punto de entrada principal de la aplicación
├── requirements.txt             # Lista de dependencias del proyecto
├── .gitignore                   # Archivos a ignorar por git
└── README.md                    # Documentación del proyecto
```

---

## Instalación y ejecución local

1. Clona el repositorio:
   ```bash
   git clone https://github.com/tu_usuario/tu_repositorio.git
   cd MINICORE-MAIN
   ```

2. Crea un entorno virtual e instala dependencias:
   ```bash
   python -m venv venv
   source venv/bin/activate  # En Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```

3. Ejecuta la aplicación:
   ```bash
   uvicorn main:app --reload
   ```

4. Accede a `http://localhost:8000` y serás redirigido a `/filter-inprogress-tasks`.

---

## ☁️ Despliegue en Render

Para desplegar esta app en [Render](https://render.com):

1. Asegúrate de tener un repositorio en GitHub con esta estructura.
2. Crea un archivo `render.yaml` como este:

   ```yaml
   services:
     - type: web
       name: minicore-task-app
       env: python
       plan: free
       buildCommand: "pip install -r requirements.txt"
       startCommand: "uvicorn main:app --host 0.0.0.0 --port 10000"
       autoDeploy: true
   ```

3. En Render:
   - Ve a "New Web Service"
   - Conecta tu cuenta de GitHub y selecciona el repositorio.
   - Deja el **Root Directory** como `.` (vacío).
   - Render detectará automáticamente el archivo `render.yaml` y desplegará tu app.

---

## Cómo usar la app

1. Entra al sitio desplegado (por ejemplo: `https://minicore-task-app.onrender.com`)
2. Selecciona una **fecha de inicio** y **fecha final**
3. Pulsa el botón para ver tareas que:
   - Están en estado **In Progress**
   - Y su fecha estimada ya ha vencido


