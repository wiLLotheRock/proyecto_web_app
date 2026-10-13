# StudyLock UNJBG 📚⏱️

Aplicación móvil de estudio adaptativo, microaprendizaje e interrupción positiva, diseñada para los estudiantes de la Universidad Nacional Jorge Basadre Grohmann (UNJBG).

## 🚀 Stack Tecnológico

* **Frontend:** Flutter (Dart) - Interfaz de usuario dinámica y monitoreo en segundo plano (usando Method Channels para Android).
* **Backend:** Python (FastAPI) - API REST ultrarrápida y asíncrona para orquestar la lógica del sistema.
* **Base de Datos:** MySQL - Motor relacional robusto para el almacenamiento central.
* **ORM:** SQLAlchemy - Gestión y modelado de datos en el servidor.
* **Integraciones Externas:** Scraper web para el Aula Virtual UNJBG y consumo de API de Inteligencia Artificial (OpenAI/Gemini).

## 📂 Arquitectura y Estructura de Carpetas

El proyecto está dividido en un ecosistema Cliente-Servidor. Para garantizar la escalabilidad y mantenibilidad, el backend está organizado siguiendo los principios de la **Arquitectura Hexagonal (Puertos y Adaptadores)** y **Domain-Driven Design (DDD)**. Esto aísla la lógica central de negocio de las tecnologías externas (como MySQL o el scraper).

```text
studylock-unjbg/
├── frontend/                   # Aplicación móvil (Flutter)
│   ├── lib/
│   │   ├── main.dart           # Punto de entrada de la app
│   │   ├── core/               # Utilidades, constantes y temas globales
│   │   ├── ui/                 # Pantallas y widgets (Dashboard, Overlay de Retos)
│   │   └── services/           # Clientes HTTP para consumir la API de FastAPI
│   └── android/                # Código nativo (Kotlin/Java) para permisos (SYSTEM_ALERT_WINDOW)
│
├── backend/                    # Servidor central (FastAPI)
│   ├── app/
│   │   ├── domain/             # Entidades core y reglas de negocio (Estudiante, Curso, Reto)
│   │   ├── application/        # Casos de uso e interfaces / Puertos (SincronizarMaterial, EvaluarReto)
│   │   ├── infrastructure/     # Implementaciones / Adaptadores
│   │   │   ├── web/            # Controladores, rutas de FastAPI y schemas Pydantic
│   │   │   ├── database/       # Modelos SQLAlchemy, repositorios y conexión MySQL
│   │   │   └── external/       # Conectores externos: Scraper UNJBG y cliente de IA
│   │   └── main.py             # Instancia principal de FastAPI
│   ├── requirements.txt        # Dependencias de Python
│   └── .env.example            # Plantilla de variables de entorno (credenciales BD, API Keys)
│
├── database/                   # Gestión de la base de datos
│   └── init.sql                # Script SQL inicial para levantar esquemas en MySQL
│
└── docs/                       # Documentación técnica
    ├── uml/                    # Diagramas de Casos de Uso y Secuencia
    └── bpmn/                   # Diagramas de Modelado de Negocio (AS-IS / TO-BE)
```

## ⚙️ Configuración Inicial para Desarrollo

### 1. Clonar el repositorio
```bash
git clone https://github.com/wiLLotheRock/proyecto_web_app.git
cd studylock-unjbg
```

### 2. Configurar y levantar el Backend (FastAPI)
```bash
cd backend
# Crear y activar entorno virtual
python -m venv venv
source venv/bin/activate  # En Windows: venv\Scripts\activate

# Instalar dependencias
pip install -r requirements.txt

# Levantar el servidor de desarrollo
uvicorn app.main:app --reload
```

### 3. Configurar y levantar el Frontend (Flutter)
```bash
cd frontend
flutter pub get
flutter run
```