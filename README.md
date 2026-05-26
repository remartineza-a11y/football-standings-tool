# ⚽ Football Standings Tool

## Descripción del Proyecto

Herramienta de consola que consulta en tiempo real la tabla de posiciones de La Liga Española mediante la API oficial de API-Football, entregando datos actualizados de forma instantánea.

---

## 👤 Stakeholder

**Periodista deportivo** de un medio digital que cubre ligas europeas y necesita acceder rápidamente a tablas de posiciones actualizadas para redactar notas antes del cierre de edición.

---

## 🎯 Problema / Solución

| Problema | Solución |
|---|---|
| Consultar standings en múltiples sitios web consume tiempo valioso antes del cierre de edición | Esta herramienta obtiene en segundos la tabla de posiciones completa con partidos, victorias, goles y forma reciente directamente desde la API oficial |
| Los datos pueden estar desactualizados en fuentes secundarias | La consulta es directa a la fuente oficial en cada ejecución |
| Requiere abrir el navegador y navegar entre páginas | Un solo comando en consola entrega toda la información necesaria |

---

## ⚙️ Variables de Entorno requeridas

| Variable | Descripción |
|---|---|
| `API_KEY_PROYECTO` | X-RapidAPI-Key obtenida desde rapidapi.com al suscribirse a API-Football |

### Configurar la variable (Windows PowerShell)
```powershell
$env:API_KEY_PROYECTO="5e716dca76msh370e8b79fe80512p12d0cfjsn5b32150d154c"
```

### Configurar la variable (Linux / Mac)
```bash
export API_KEY_PROYECTO="5e716dca76msh370e8b79fe80512p12d0cfjsn5b32150d154c"
```

---

## 🐳 Ejecución con Docker

### 1. Configurar la variable de entorno
```powershell
$env:API_KEY_PROYECTO="5e716dca76msh370e8b79fe80512p12d0cfjsn5b32150d154c"
```

### 2. Ejecutar el script de automatización
```powershell
bash build.sh
```

### 3. Ver los logs del contenedor
```powershell
docker logs samplerunning
```

---

## 🐍 Ejecución directa con Python (sin Docker)

```powershell
pip install -r requirements.txt
$env:API_KEY_PROYECTO="5e716dca76msh370e8b79fe80512p12d0cfjsn5b32150d154c"
python app.py
```

---

## 📊 Datos que entrega la aplicación

| Campo | Descripción |
|---|---|
| Posición | Lugar en la tabla |
| Equipo | Nombre del club |
| PJ | Partidos jugados |
| G | Victorias |
| E | Empates |
| P | Derrotas |
| GF | Goles a favor |
| GC | Goles en contra |
| Pts | Puntos totales |
| Forma | Resultados de los últimos 5 partidos |

---

## 🏆 Liga configurada

- **La Liga** (ID 140, temporada 2024)
- Para cambiar de liga, modifica `LEAGUE_ID` en `app.py`:
  - `39` → Premier League
  - `135` → Serie A
  - `78` → Bundesliga
  - `61` → Ligue 1

---

## 📁 Estructura del repositorio

```
football-standings-tool/
├── app.py                        # Script principal que consulta la API
├── build.sh                      # Script de automatización Docker
├── requirements.txt              # Dependencias Python
├── .gitignore                    # Archivos excluidos de Git
├── README.md                     # Documentación del proyecto
└── evidencias/
    ├── docker/
    │   ├── output.txt            # docker ps -a + logs con datos reales
    │   └── screenshot.png        # Captura de la salida en consola
    └── jenkins/
        ├── stage_view.png        # Stage View de SamplePipeline en verde
        ├── console_output_build.png  # Console Output de BuildAppJob
        ├── credentials.png       # Credenciales de GitHub en Jenkins
        └── pipeline_script.txt   # Script del pipeline
```

---

## 🔒 Seguridad

- Las credenciales **nunca se escriben en el código**
- Se leen exclusivamente mediante `os.getenv()` desde variables de entorno
- El archivo `.gitignore` protege archivos `.env` y otros archivos sensibles

---

## 🛠️ Errores manejados

| Código / Tipo | Descripción |
|---|---|
| 401 | Clave de API inválida |
| 403 | Acceso denegado / suscripción inactiva |
| 404 | Liga o temporada no encontrada |
| 429 | Límite de peticiones alcanzado |
| ConnectionError | Sin conexión a internet |
| Timeout | La API tardó demasiado en responder |
| KeyError | Campo inesperado en la respuesta JSON |
| Exception | Cualquier error inesperado |
