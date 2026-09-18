# AIFindOps — Plataforma de Observabilidad, Gobernanza y FindOps de IA

## Índice

0. [Ficha del proyecto](#0-ficha-del-proyecto)
1. [Descripción general del producto](#1-descripción-general-del-producto)
2. [Arquitectura del sistema](#2-arquitectura-del-sistema)
3. [Modelo de datos](#3-modelo-de-datos)
4. [Especificación de la API](#4-especificación-de-la-api)
5. [Historias de usuario](#5-historias-de-usuario)
6. [Tickets de trabajo](#6-tickets-de-trabajo)
7. [Pull requests](#7-pull-requests)

---

## 0. Ficha del proyecto

### **0.1. Tu nombre completo:**
Marcos Luna

### **0.2. Nombre del proyecto:**
AIFindOps

### **0.3. Descripción breve del proyecto:**
AIFindOps es una plataforma integral de observabilidad, gobernanza y FindOps de Inteligencia Artificial diseñada para monitorizar, auditar y optimizar el consumo de modelos y agentes de IA (OpenAI, Google Gemini, Anthropic, etc.) a nivel de organizaciones, departamentos y usuarios, ofreciendo visibilidad multidimensional filtrable por entornos (DEV, PRE y PRO).

### **0.4. URL del proyecto:**
*Pendiente de despliegue en Entrega 3

### **0.5. URL o archivo comprimido del repositorio:**
Repositorio Git del proyecto: `https://github.com/marcoslunadev/AI4Devs-finalproject-aifindops`

---

## 1. Descripción general del producto

### **1.1. Objetivo:**
En la actualidad, las empresas se enfrentan a un crecimiento exponencial y descontrolado en el uso de modelos fundacionales y agentes autónomos de Inteligencia Artificial (OpenAI, Google Gemini, Claude, etc.). Esta situación genera problemas críticos como el *Shadow AI*, facturas impredecibles de proveedores, falta de atribución de costes por centros de responsabilidad y ausencia de métricas de rendimiento y adopción.

**Propósito y Valor:**
AIFindOps centraliza la telemetría, auditoría y control financiero del consumo de IA en la empresa, transformando datos crudos de ejecución en información estratégica.

**¿Qué soluciona?**
* **Falta de visibilidad:** Desconocimiento de qué agentes, departamentos o usuarios generan el gasto.
* **Control presupuestario (FindOps):** Permite calcular el coste unitario por ejecución, token y departamento.
* **Gobierno y Auditoría:** Supervisión de latencias, tasas de error y cumplimiento de entornos (DEV, PRE, PRO).
* **Toma de decisiones:** Proporciona a los roles directivos información en tiempo casi real para justificar el ROI y planificar inversiones en IA.

**Público Objetivo:**
* **C-Level & Directivos (CIO, CTO, CFO):** Visualización de KPIs ejecutivos globales, tendencias a 90 días y distribución presupuestaria.
* **Gestores de Innovación & Heads of AI:** Monitorización del catálogo de agentes, adopción por departamentos y rendimiento técnico.
* **Líderes de Departamento (Managers):** Control del consumo y ejecuciones de los usuarios bajo su responsabilidad.

---

### **1.2. Características y funcionalidades principales:**

1. **Ingesta y Normalización de Logs de IA (Data Ingestion Engine):**
   * Procesamiento de ficheros de telemetría (JSON, JSONL, CSV) provenientes de gateways, proxies o SDKs de proveedores de IA (OpenAI, Google Gemini, Anthropic).
   * Normalización de tokens (Prompt/Input, Completion/Output), costes monetarios estandarizados, latencias, timestamps y modelos utilizados.

2. **Dashboard Ejecutivo con KPIs Globales (Ventana de 90 días / Rango dinámico):**
   * Panel superior con métricas agregadas:
     * **Total de Agentes de IA Activos** (nuevos vs acumulados).
     * **Volumen Total de Tokens** (desglose Input / Output).
     * **Coste Total Acumulado ($/€)** con comparativa de tendencia.
     * **Coste Medio por Ejecución** (Unit Economics de IA).
     * **Mix de Proveedores / Modelos** (distribución de cuota de uso).
     * **Tasa de Éxito / SLA** (% de ejecuciones exitosas vs fallidas).

3. **Matriz Jerárquica Drill-Down (Organización ➔ Departamento ➔ Usuario):**
   * Tabla interactiva con sumatorios en cascada: la suma de usuarios conforma el total del departamento, y la suma de departamentos conforma el total de la organización.
   * Filtros dinámicos multidimensionales: rango de fechas y entorno (**DEV**, **PRE**, **PRO**).
   * Despliegue en acordeón:
     * Fila Organización ➔ Despliega Departamentos.
     * Fila Departamento ➔ Despliega Usuarios.

4. **Explorador de Auditoría y Trazabilidad Granular (Detail Views):**
   * **Vista Detalle de Organización:** Inventario de agentes de IA asociados a la organización, versiones y actividad global.
   * **Vista Detalle de Departamento:** Análisis de consumo departamental y agentes asignados.
   * **Vista Detalle de Usuario:** Trazabilidad individual con el log completo de ejecuciones (timestamp, agente, modelo, tokens, coste, latencia y entorno).

5. **Control de Acceso Basado en Roles (RBAC) y Seguridad:**
   * Autenticación segura con JWT.
   * Perfiles de acceso segmentados: `SUPER_ADMIN` (visión multi-organización), `ORG_MANAGER` (acceso a su organización), `DEPT_MANAGER` (acceso a su departamento) y `AUDITOR`.

---

### **1.3. Diseño y experiencia de usuario:**

La experiencia de usuario está optimizada para ofrecer una navegación fluida, profesional y orientada al análisis de datos sin sobrecarga cognitiva:

```
+---------------------------------------------------------------------------------------+
|  [Logo AIFindOps]   Organización: [Acme Corp v]   Entorno: [TODOS | DEV | PRE | PRO]   |
+---------------------------------------------------------------------------------------+
|  KPIs GLOBALES (Últimos 90 días):                                                     |
|  +----------------+ +----------------+ +----------------+ +------------------------+  |
|  | Agentes Activos| | Tokens Totales | | Coste Total    | | Coste Medio/Ejecución  |  |
|  |     24 (+3)    | |  145.8M tokens | |   $ 1,420.50   | |       $ 0.0042         |  |
|  +----------------+ +----------------+ +----------------+ +------------------------+  |
+---------------------------------------------------------------------------------------+
|  TABLA JERÁRQUICA DE CONSUMO (Drill-Down Matrix)             [Rango: Últimos 30 días v]
|                                                                                       |
|  Entidad / Jerarquía             | Agentes Nuevos | Ejecuciones | Tokens       | Coste |
|  --------------------------------+----------------+-------------+--------------+-------|
|  [-] Acme Corp (Organización)    |       8        |   345,210   | 145,800,000  | $1,420|
|     [-] Ingeniería (Dept)        |       5        |   280,000   | 112,000,000  | $1,100|
|        - Juan Pérez (User - PRO) |       2        |   150,000   |  65,000,000  | $ 620 |
|        - Ana Gómez (User - DEV)  |       3        |   130,000   |  47,000,000  | $ 480 |
|     [+] Marketing (Dept)         |       3        |    65,210   |  33,800,000  | $ 320 |
+---------------------------------------------------------------------------------------+
```

**Flujo de Navegación del Usuario:**
1. **Acceso:** Login con credenciales seguras y redirección según rol.
2. **Dashboard Central:** Vista ejecutiva de KPIs y tabla jerárquica con filtros de entorno aplicables en tiempo real.
3. **Exploración Jerárquica:** El usuario despliega la fila de su organización o departamento para identificar picos de consumo o anomalías.
4. **Inspección Profunda:** Al hacer clic en un agente, departamento o usuario, el sistema abre una vista de detalle con gráficos de series temporales y el histórico de ejecuciones.
5. **Módulo de Ingesta:** Modal drag-and-drop para subir nuevos ficheros de logs con validación y previsualización de datos.

---

### **1.4. Instrucciones de instalación:**

El proyecto está diseñado para levantarse localmente de forma rápida y reproducible utilizando **Docker Compose** para la base de datos y scripts de desarrollo para frontend y backend.

#### **Requisitos previos:**
* Node.js v18+ y npm v9+
* Docker Desktop o Docker Engine con Docker Compose v2+
* Git

#### **Paso 1: Clonar el repositorio**
```bash
git clone https://github.com/marcoslunadev/AI4Devs-finalproject-aifindops.git
cd AI4Devs-finalproject-aifindops
```

#### **Paso 2: Configurar las variables de entorno**
Copiar el archivo de ejemplo para backend y frontend:
```bash
# En la raíz o carpeta backend
cp .env.example .env
```
Contenido básico de `.env`:
```env
PORT=3000
NODE_ENV=development
DATABASE_URL="postgresql://aifindops_user:aifindops_pass@localhost:5432/aifindops_db?schema=public"
JWT_SECRET="super_secret_jwt_key_aifindops_2026"
CORS_ORIGIN="http://localhost:5173"
```

#### **Paso 3: Levantar la base de datos PostgreSQL con Docker Compose**
```bash
docker compose up -d
```
> Esto levantará un contenedor de **PostgreSQL 16** en el puerto `5432` con volumen persistente (`postgres_data`) y opcionalmente un panel Adminer/pgAdmin en el puerto `8080`.

#### **Paso 4: Instalar dependencias y ejecutar migraciones de BBDD**
```bash
# Instalación de dependencias
npm install

# Generar cliente de Prisma y aplicar migraciones
npx prisma migrate dev --name init

# Poblar la base de datos con datos semilla (organizaciones, usuarios, agentes y logs de ejemplo)
npx prisma db seed
```

#### **Paso 5: Iniciar los servidores de desarrollo**
```bash
# En terminal 1 (Backend - Express API):
npm run dev:backend
# Servidor disponible en: http://localhost:3000

# En terminal 2 (Frontend - React + Vite):
npm run dev:frontend
# Aplicación web disponible en: http://localhost:5173
```

---

## 2. Arquitectura del Sistema

### **2.1. Diagrama de arquitectura:**

```mermaid
flowchart TB
    subgraph ClientLayer ["Capa de Presentación (Frontend SPA)"]
        UI["React 18 + Vite + TypeScript"]
        Router["React Router DOM"]
        State["Zustand / React Query"]
        Tailwind["TailwindCSS + Lucide + Recharts"]
    end

    subgraph Security ["Seguridad y Middleware"]
        CORS["CORS & Helmet"]
        AuthMid["JWT Auth & RBAC Middleware"]
        RateLimit["Express Rate Limiter"]
    end

    subgraph APILayer ["Capa de Backend (Node.js + Express API)"]
        RouterAPI["Express REST Router"]
        
        subgraph Controllers ["Controladores"]
        AuthController["Auth Controller"]
        MetricsController["Metrics & Dashboard Controller"]
        AgentController["Agent & Traceability Controller"]
        IngestionController["Log Ingestion Controller"]
        end

        subgraph Services ["Capa de Negocio / Dominio"]
        AuthService["Auth Service (Bcrypt + JWT)"]
        AggregationService["Aggregation Engine (Hierarchical Rollup)"]
        AgentService["Agent Catalog Service"]
        IngestionParser["Log Parser & Normalizer (Zod Schema)"]
        end

        subgraph Repositories ["Capa de Acceso a Datos"]
        PrismaClient["Prisma ORM Client"]
        end
    end

    subgraph DataLayer ["Capa de Persistencia & Infraestructura"]
        subgraph DockerCompose ["Docker Container: PostgreSQL 16"]
            PGMaster[("PostgreSQL DB
(Relacional + JSONB + BRIN Indexes)")]
            Volume[("Persistent Docker Volume
(postgres_data)")]
        end
    end

    subgraph ExternalSources ["Fuentes Externas de Telemetría"]
        LogsJSON["Ficheros Logs JSON / JSONL / CSV"]
        OpenAI["OpenAI Telemetry Events"]
        Gemini["Google Gemini Events"]
    end

    %% Conexiones
    UI --> Router --> State --> Tailwind
    State -->|HTTP / JSON Requests| Security
    Security --> CORS --> AuthMid --> RateLimit --> RouterAPI
    
    RouterAPI --> AuthController --> AuthService --> PrismaClient
    RouterAPI --> MetricsController --> AggregationService --> PrismaClient
    RouterAPI --> AgentController --> AgentService --> PrismaClient
    RouterAPI --> IngestionController --> IngestionParser --> PrismaClient

    ExternalSources -->|Upload / Batch| IngestionController
    PrismaClient -->|SQL Connection Pool| PGMaster
    PGMaster --- Volume
```

#### **Justificación Arquitectónica:**
* **Patrón de Arquitectura Limpia por Capas (Clean Architecture):** Se desacoplan la capa de presentación (controladores HTTP), la lógica de negocio (servicios y motores de agregación) y la persistencia (Prisma Repositories). Esto permite testear la lógica de cálculo financiero de forma aislada.
* **Separación Frontend/Backend:** La SPA en React garantiza una experiencia de usuario interactiva y fluida para el drill-down colapsable sin recargas de página, consumiendo una API REST tipada de alto rendimiento.
* **PostgreSQL contenerizado con Docker Compose:** Proporciona un entorno de desarrollo aislado, determinista y listo para replicar en entornos de testing e integración continua (CI).

#### **Beneficios y Trade-offs:**
* **Beneficios:**
  * **Consistencia e integridad:** Estricta integridad referencial para la jerarquía *Organización ➔ Departamento ➔ Usuario*.
  * **Potencia analítica en SQL:** Agregaciones complejas con `GROUP BY`, `SUM` y filtros de series temporales directamente en el motor de base de datos.
  * **Flexibilidad con JSONB:** Permite almacenar metadatos heterogéneos de diferentes proveedores de LLM sin alterar el esquema.
* **Sacrificios / Déficits identificados:**
  * Para volúmenes extremos (cientos de millones de ejecuciones diarias), una base de datos relacional pura requeriría una estrategia de particionado temporal o la delegación de métricas de telemetría a un almacén columnar como ClickHouse/TimescaleDB. Para el alcance del proyecto y MVP, PostgreSQL con índices adecuados cubre sobradamente el rendimiento requerido.

---

### **2.2. Descripción de componentes principales:**

1. **Frontend Client (React + Vite + TypeScript):**
   * Gestiona el estado de la aplicación, el renderizado de gráficos analíticos (Recharts) y la interacción de la tabla jerárquica con acordeón multinivel.
2. **API Gateway & Router (Express + TypeScript):**
   * Punto de entrada de las peticiones HTTP, validación de esquemas de entrada con Zod, control de cabeceras de seguridad con Helmet y gestión de CORS.
3. **Ingestion Engine & Parser:**
   * Módulo encargado de recibir ficheros de logs en formato batch, validar la estructura de eventos de IA, normalizar costes/tokens según la tabla de precios del modelo y persistirlos transaccionalmente.
4. **Aggregation & Metrics Engine:**
   * Motor de cálculo que ejecuta consultas optimizadas de agregación en cascada para calcular KPIs globales y desgloses por Organización, Departamento, Usuario y Entorno (DEV, PRE, PRO).
5. **Prisma ORM & PostgreSQL Database:**
   * Capa de persistencia tipada que maneja modelos, migraciones y ejecución de consultas sobre el contenedor PostgreSQL.

---

### **2.3. Descripción de alto nivel del proyecto y estructura de ficheros:**

El proyecto sigue una estructura limpia y modular organizada como monorepo:

```
AI4Devs-finalproject-aifindops/
├── docker/
│   └── docker-compose.yml        # Definición del contenedor PostgreSQL y volúmenes
├── backend/
│   ├── src/
│   │   ├── config/               # Variables de entorno y configuración
│   │   ├── controllers/          # Manejadores de rutas HTTP (Auth, Metrics, Ingestion, Agents)
│   │   ├── services/             # Lógica de negocio (Agregación, Ingesta, Auditoría)
│   │   ├── repositories/         # Consultas de acceso a datos y agregaciones Prisma
│   │   ├── middlewares/          # Auth JWT, RBAC, validación Zod, Error Handler
│   │   ├── schemas/              # Esquemas de validación Zod (DTOs)
│   │   ├── types/                # Tipos e interfaces TypeScript
│   │   └── app.ts                # Inicialización de Express y middlewares
│   ├── prisma/
│   │   ├── schema.prisma         # Esquema de base de datos relacional
│   │   ├── migrations/           # Historial de migraciones SQL
│   │   └── seed.ts               # Semilla con datos de prueba
│   ├── tests/                    # Tests unitarios y de integración (Vitest + Supertest)
│   ├── package.json
│   └── tsconfig.json
├── frontend/
│   ├── src/
│   │   ├── assets/               # Recursos estáticos e iconos
│   │   ├── components/           # Componentes UI reutilizables (KPI Cards, Tables, Charts, Modals)
│   │   ├── pages/                # Vistas principales (Dashboard, AgentDetail, Traceability, Login)
│   │   ├── hooks/                # Custom React Hooks para fetching y filtros
│   │   ├── services/             # Cliente API (Axios / Fetch)
│   │   ├── types/                # Definiciones de tipos para frontend
│   │   ├── App.tsx               # Enrutamiento principal
│   │   └── main.tsx
│   ├── package.json
│   ├── vite.config.ts
│   └── tailwind.config.js
├── prompts.md                    # Registro de interacción y prompts de IA
├── readme.md                     # Documentación técnica del proyecto
└── .env.example                  # Plantilla de variables de entorno
```

---

### **2.4. Infraestructura y despliegue:**

```mermaid
flowchart LR
    subgraph LocalDev ["Entorno de Desarrollo Local"]
        DevFE["Vite Dev Server (Port 5173)"]
        DevBE["Express Server (Port 3000)"]
        DevDB["Docker Compose: Postgres 16 (Port 5432)"]
        DevFE --> DevBE --> DevDB
    end

    subgraph CloudProd ["Entorno de Producción (Entrega 3)"]
        ProdFE["Frontend: Vercel / Netlify (CDN Edge)"]
        ProdBE["Backend: Render / Railway (Node.js Container)"]
        ProdDB[("Cloud PostgreSQL: Neon / Supabase / Railway")]
        ProdFE -->|HTTPS API Requests| ProdBE -->|SSL Connection Pool| ProdDB
    end
```

* **Local:** Contenedor Docker para PostgreSQL con persistencia en volumen `postgres_data`. Hot-reloading en Frontend (Vite) y Backend (tsx/nodemon).
* **Producción (Entrega 3):**
  * Frontend: Despliegue estático continuo en Vercel con integración a GitHub.
  * Backend: Contenedor en Railway / Render con pipelines automáticos de CI/CD.
  * Base de Datos: PostgreSQL gestionado en la nube (Neon / Supabase / Railway) con backups automáticos y pooling de conexiones.

---

### **2.5. Seguridad:**

1. **Autenticación y Autorización:**
   * Tokens **JWT (JSON Web Tokens)** firmados con algoritmo HMAC-SHA256 y tiempo de expiración configurable.
   * Middleware **RBAC** que valida el rol (`SUPER_ADMIN`, `ORG_MANAGER`, `DEPT_MANAGER`, `AUDITOR`) y comprueba que el usuario solo acceda a los recursos de su jerarquía asignada.
2. **Protección de Datos y Contraseñas:**
   * Hashing seguro de contraseñas con **bcrypt** (cost factor 10+).
   * Variables de entorno para secretos (`.env`) excluidas estrictamente de git (`.gitignore`).
3. **Seguridad en la Capa HTTP y API:**
   * **Helmet:** Configuración de cabeceras HTTP seguras (CSP, HSTS, X-Content-Type-Options).
   * **CORS:** Restricción estricta de orígenes permitidos.
   * **Express Rate Limiting:** Protección contra ataques de fuerza bruta y saturación de peticiones en endpoints de autenticación e ingesta.
   * **Validación e Inmunización:** Validación de payloads con **Zod** para prevenir inyecciones y datos corruptos.

---

### **2.6. Tests:**

* **Tests Unitarios (Vitest):** Cobertura de la lógica de cálculo del motor de agregación jerárquica (sumatorios en cascada, cálculo de costes medios y normalización de tokens de proveedores).
* **Tests de Integración (Supertest + Vitest):** Verificación de los endpoints principales de la API (`/api/v1/ingestion/logs`, `/api/v1/metrics/dashboard`), validando códigos de estado HTTP, autenticación JWT y persistencia en una BBDD PostgreSQL de test.
* **Tests End-to-End (Playwright):** Prueba automatizada del flujo crítico: Login ➔ Carga del Dashboard con KPIs ➔ Despliegue del acordeón jerárquico (*Org ➔ Dept ➔ User*) ➔ Filtrado por entorno DEV/PRO.

---

## 3. Modelo de Datos

### **3.1. Diagrama del modelo de datos:**

```mermaid
erDiagram
    ORGANIZATION ||--o{ DEPARTMENT : "contiene"
    ORGANIZATION ||--o{ AI_AGENT : "posee"
    DEPARTMENT ||--o{ USER : "emplea"
    USER ||--o{ EXECUTION_LOG : "ejecuta"
    AI_AGENT ||--o{ EXECUTION_LOG : "es_ejecutado"
    INGESTION_BATCH ||--o{ EXECUTION_LOG : "registra"
    USER }|--|| ROLE : "tiene_rol"

    ORGANIZATION {
        string id PK "cuid/uuid"
        string name "unique, not null"
        string tax_id "cif/nif opcional"
        timestamp created_at
        timestamp updated_at
    }

    DEPARTMENT {
        string id PK "cuid/uuid"
        string organization_id FK "not null"
        string name "not null"
        string code "identificador interno"
        timestamp created_at
    }

    ROLE {
        string id PK
        string code "SUPER_ADMIN, ORG_MANAGER, DEPT_MANAGER, AUDITOR"
        string description
    }

    USER {
        string id PK "cuid/uuid"
        string department_id FK "not null"
        string role_id FK "not null"
        string email "unique, not null"
        string password_hash "not null"
        string full_name "not null"
        boolean is_active "default true"
        timestamp created_at
    }

    AI_AGENT {
        string id PK "cuid/uuid"
        string organization_id FK "not null"
        string name "not null"
        string provider "OPENAI, GOOGLE_GEMINI, ANTHROPIC"
        string model_default "gpt-4o, gemini-1.5-pro, etc."
        string version "1.0.0"
        string description
        boolean is_active "default true"
        timestamp created_at
    }

    INGESTION_BATCH {
        string id PK "cuid/uuid"
        string filename "not null"
        string source "API_GATEWAY, FILE_UPLOAD, AGENT_PROXY"
        int total_records "default 0"
        string status "PENDING, PROCESSED, FAILED"
        timestamp processed_at
    }

    EXECUTION_LOG {
        string id PK "cuid/uuid"
        string agent_id FK "not null"
        string user_id FK "not null"
        string batch_id FK "nullable"
        string environment "DEV, PRE, PRO (not null)"
        string provider "OPENAI, GOOGLE_GEMINI, etc."
        string model "gpt-4o, gemini-1.5-pro, etc."
        int prompt_tokens "not null, default 0"
        int completion_tokens "not null, default 0"
        int total_tokens "not null, default 0"
        decimal cost_usd "numeric(10,6), not null"
        int latency_ms "not null"
        string status "SUCCESS, ERROR, TIMEOUT"
        jsonb metadata "detalles del proveedor y payload"
        timestamp executed_at "not null, indexed"
        timestamp created_at "default now"
    }
```

---

### **3.2. Descripción de entidades principales:**

#### **1. `ORGANIZATION` (Organizaciones)**
* Representa la entidad raíz corporativa.
* **Campos:**
  * `id` (String, PK, CUID/UUID): Identificador único.
  * `name` (String, Not Null, Unique): Nombre comercial de la organización.
  * `tax_id` (String, Nullable): CIF/NIF o identificador fiscal.
  * `created_at` / `updated_at` (Timestamp): Marcas de tiempo de auditoría.

#### **2. `DEPARTMENT` (Departamentos)**
* Unidad organizativa dentro de una organización (ej. *Ingeniería, Marketing, Finanzas, Producto*).
* **Campos:**
  * `id` (String, PK): Identificador único.
  * `organization_id` (String, FK, Not Null): Referencia a `ORGANIZATION.id` (Restricción `ON DELETE CASCADE`).
  * `name` (String, Not Null): Nombre del departamento.
  * `code` (String, Nullable): Código departamental interno (ej. `ENG-01`).

#### **3. `USER` (Usuarios del Sistema)**
* Usuarios que ejecutan agentes o acceden a la plataforma de gestión. Cada usuario pertenece estrictamente a una organización y a un departamento.
* **Campos:**
  * `id` (String, PK): Identificador único.
  * `department_id` (String, FK, Not Null): Referencia a `DEPARTMENT.id`.
  * `role_id` (String, FK, Not Null): Referencia a `ROLE.id`.
  * `email` (String, Not Null, Unique): Correo electrónico para autenticación.
  * `password_hash` (String, Not Null): Contraseña cifrada con bcrypt.
  * `full_name` (String, Not Null): Nombre completo del usuario.
  * `is_active` (Boolean, Default True): Estado de la cuenta.

#### **4. `AI_AGENT` (Catálogo de Agentes de IA)**
* Definición de agentes y modelos autónomos dados de alta dentro de la organización.
* **Campos:**
  * `id` (String, PK): Identificador único.
  * `organization_id` (String, FK, Not Null): Organización propietaria del agente.
  * `name` (String, Not Null): Nombre identificativo del agente (ej. *DataAnalyzer-Agent*, *SupportBot-v2*).
  * `provider` (String, Not Null): Proveedor de IA (`OPENAI`, `GOOGLE_GEMINI`, `ANTHROPIC`, `MISTRAL`).
  * `model_default` (String, Not Null): Modelo base (ej. `gpt-4o`, `gemini-1.5-pro`).
  * `version` (String, Default '1.0.0'): Versión del agente.
  * `is_active` (Boolean, Default True): Disponibilidad operativa.

#### **5. `EXECUTION_LOG` (Telemetría de Ejecuciones y Consumo)**
* Registro inmutable de cada invocación o inferencia realizada por un agente. Es la tabla de mayor volumen y base de las consultas analíticas.
* **Campos:**
  * `id` (String, PK): Identificador único de ejecución.
  * `agent_id` (String, FK, Not Null): Agente invocado (`AI_AGENT.id`).
  * `user_id` (String, FK, Not Null): Usuario que originó la petición (`USER.id`).
  * `batch_id` (String, FK, Nullable): Identificador del lote de ingesta origen.
  * `environment` (Enum String, Not Null): Entorno de ejecución (`DEV`, `PRE`, `PRO`).
  * `provider` (String, Not Null): Proveedor utilizado en la llamada.
  * `model` (String, Not Null): Modelo concreto utilizado (ej. `gpt-4o-2024-08-06`).
  * `prompt_tokens` (Int, Not Null): Tokens de entrada/contexto.
  * `completion_tokens` (Int, Not Null): Tokens de salida/generación.
  * `total_tokens` (Int, Not Null): Suma calculada de tokens.
  * `cost_usd` (Decimal 10,6, Not Null): Coste monetario de la ejecución en dólares/euros.
  * `latency_ms` (Int, Not Null): Tiempo de respuesta en milisegundos.
  * `status` (String, Not Null): Estado (`SUCCESS`, `ERROR`, `RATE_LIMIT_EXCEEDED`).
  * `metadata` (JSONB, Nullable): Datos adicionales (parámetros de temperatura, IDs externos, error codes).
  * `executed_at` (Timestamp, Not Null, Index): Fecha/hora exacta de la ejecución.

#### **6. `INGESTION_BATCH` (Lotes de Ingesta)**
* Registro de auditoría de los ficheros de logs procesados por el sistema.

---

## 4. Especificación de la API

A continuación se describen los 3 endpoints principales en formato **OpenAPI 3.0 (Swagger)**:

```yaml
openapi: 3.0.3
info:
  title: AIFindOps API
  description: API de Observabilidad, Gobernanza y FindOps para consumo de Agentes de IA.
  version: 1.0.0
servers:
  - url: http://localhost:3000/api/v1
    description: Servidor de desarrollo local

paths:
  /ingestion/logs:
    post:
      summary: Ingesta de fichero o lote de logs de ejecución de IA
      description: Procesa y normaliza un lote de eventos de ejecución provenientes de logs de OpenAI, Gemini u otros agentes.
      security:
        - BearerAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              required:
                - source
                - events
              properties:
                source:
                  type: string
                  example: "FILE_UPLOAD"
                filename:
                  type: string
                  example: "openai_logs_2026_09_dev.json"
                events:
                  type: array
                  items:
                    $ref: '#/components/schemas/ExecutionEventInput'
      responses:
        '201':
          description: Lote de logs procesado e insertado correctamente
          content:
            application/json:
              schema:
                type: object
                properties:
                  success:
                    type: boolean
                    example: true
                  batchId:
                    type: string
                    example: "batch_clw98127391283"
                  recordsProcessed:
                    type: integer
                    example: 1500
                  totalCostCalculated:
                    type: number
                    format: float
                    example: 24.8512
        '400':
          description: Error de validación en los esquemas de los eventos

  /metrics/dashboard:
    get:
      summary: Obtención de KPIs globales y agregaciones jerárquicas (Drill-Down)
      description: Devuelve las métricas consolidadas (últimos 90 días o rango seleccionado) y la matriz jerárquica con sumatorios (Organización -> Departamento -> Usuario).
      security:
        - BearerAuth: []
      parameters:
        - name: organizationId
          in: query
          required: false
          schema:
            type: string
          description: Filtrar por organización concreta
        - name: environment
          in: query
          required: false
          schema:
            type: string
            enum: [ALL, DEV, PRE, PRO]
            default: ALL
          description: Entorno de ejecución a filtrar
        - name: startDate
          in: query
          required: false
          schema:
            type: string
            format: date
          example: "2026-06-01"
        - name: endDate
          in: query
          required: false
          schema:
            type: string
            format: date
          example: "2026-09-01"
      responses:
        '200':
          description: KPIs globales y árbol jerárquico de consumo
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/DashboardMetricsResponse'

  /agents/{agentId}/executions:
    get:
      summary: Trazabilidad y detalle de ejecuciones de un agente de IA
      description: Obtiene el histórico granular de ejecuciones de un agente específico con métricas de tokens, costes y latencias.
      security:
        - BearerAuth: []
      parameters:
        - name: agentId
          in: path
          required: true
          schema:
            type: string
        - name: environment
          in: query
          required: false
          schema:
            type: string
            enum: [DEV, PRE, PRO]
        - name: limit
          in: query
          required: false
          schema:
            type: integer
            default: 50
        - name: offset
          in: query
          required: false
          schema:
            type: integer
            default: 0
      responses:
        '200':
          description: Lista paginada de ejecuciones del agente
          content:
            application/json:
              schema:
                type: object
                properties:
                  agentId:
                    type: string
                    example: "agent_cm4918239"
                  agentName:
                    type: string
                    example: "DataAnalyzer-Agent"
                  totalExecutions:
                    type: integer
                    example: 3420
                  items:
                    type: array
                    items:
                      $ref: '#/components/schemas/ExecutionDetailItem'

components:
  securitySchemes:
    BearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT

  schemas:
    ExecutionEventInput:
      type: object
      required:
        - agentId
        - userId
        - environment
        - provider
        - model
        - promptTokens
        - completionTokens
        - latencyMs
        - executedAt
      properties:
        agentId:
          type: string
          example: "agent_cm4918239"
        userId:
          type: string
          example: "usr_823941"
        environment:
          type: string
          enum: [DEV, PRE, PRO]
          example: "PRO"
        provider:
          type: string
          example: "OPENAI"
        model:
          type: string
          example: "gpt-4o"
        promptTokens:
          type: integer
          example: 1250
        completionTokens:
          type: integer
          example: 430
        latencyMs:
          type: integer
          example: 850
        status:
          type: string
          example: "SUCCESS"
        executedAt:
          type: string
          format: date-time
          example: "2026-09-18T10:15:30Z"

    DashboardMetricsResponse:
      type: object
      properties:
        kpis:
          type: object
          properties:
            activeAgents:
              type: integer
              example: 24
            newAgentsInRange:
              type: integer
              example: 5
            totalTokens:
              type: integer
              example: 145800000
            promptTokens:
              type: integer
              example: 98200000
            completionTokens:
              type: integer
              example: 47600000
            totalCostUsd:
              type: number
              format: float
              example: 1420.50
            averageCostPerExecution:
              type: number
              format: float
              example: 0.004115
            successRatePercentage:
              type: number
              example: 99.4
        hierarchy:
          type: array
          items:
            $ref: '#/components/schemas/OrganizationAggregation'

    OrganizationAggregation:
      type: object
      properties:
        organizationId:
          type: string
          example: "org_1"
        organizationName:
          type: string
          example: "Acme Corp"
        newAgentsCount:
          type: integer
          example: 8
        totalExecutions:
          type: integer
          example: 345210
        totalTokens:
          type: integer
          example: 145800000
        totalCostUsd:
          type: number
          example: 1420.50
        departments:
          type: array
          items:
            $ref: '#/components/schemas/DepartmentAggregation'

    DepartmentAggregation:
      type: object
      properties:
        departmentId:
          type: string
          example: "dept_eng"
        departmentName:
          type: string
          example: "Ingeniería"
        newAgentsCount:
          type: integer
          example: 5
        totalExecutions:
          type: integer
          example: 280000
        totalCostUsd:
          type: number
          example: 1100.00
        users:
          type: array
          items:
            $ref: '#/components/schemas/UserAggregation'

    UserAggregation:
      type: object
      properties:
        userId:
          type: string
          example: "usr_10"
        userName:
          type: string
          example: "Juan Pérez"
        environment:
          type: string
          example: "PRO"
        totalExecutions:
          type: integer
          example: 150000
        totalTokens:
          type: integer
          example: 65000000
        totalCostUsd:
          type: number
          example: 620.00

    ExecutionDetailItem:
      type: object
      properties:
        id:
          type: string
          example: "exec_9812401"
        userName:
          type: string
          example: "Ana Gómez"
        departmentName:
          type: string
          example: "Ingeniería"
        environment:
          type: string
          example: "DEV"
        model:
          type: string
          example: "gpt-4o"
        promptTokens:
          type: integer
          example: 2100
        completionTokens:
          type: integer
          example: 650
        costUsd:
          type: number
          example: 0.0084
        latencyMs:
          type: integer
          example: 920
        status:
          type: string
          example: "SUCCESS"
        executedAt:
          type: string
          format: date-time
          example: "2026-09-18T09:40:12Z"
```

---

## 5. Historias de Usuario

### **Historia de Usuario 1**
* **Identificador:** `HU-01`
* **Título:** Visualización del Dashboard Ejecutivo y Matriz Jerárquica Drill-Down
* **Como:** CIO / Gestor de Innovación de la empresa,
* **Quiero:** Visualizar los KPIs globales de consumo de IA a 90 días y desplegar una tabla en cascada por Organización, Departamento y Usuario con filtros de entorno (DEV, PRE, PRO),
* **Para:** Analizar la distribución del gasto de IA por centros de coste, detectar anomalías presupuestarias y tomar decisiones informadas sobre la adopción tecnológica.

**Criterios de Aceptación (Gherkin):**
* **Escenario 1: Carga exitosa de KPIs globales**
  * **Dado que** un usuario autenticado con rol `SUPER_ADMIN` o `ORG_MANAGER` accede al Dashboard,
  * **Cuando** la página principal se carga,
  * **Entonces** debe visualizar en el panel superior: Total de agentes activos, Tokens totales (Input/Output), Coste total acumulado, Coste medio por ejecución y Mix de modelos del periodo seleccionado.
* **Escenario 2: Despliegue jerárquico de la tabla (Drill-Down)**
  * **Dado que** el usuario visualiza la fila de su organización con los sumatorios totales,
  * **Cuando** hace clic en el botón de descolapsar (+),
  * **Entonces** se muestran las filas de cada departamento asociado, y la suma de las métricas de los departamentos debe coincidir exactamente con el total de la organización.
  * **Y cuando** hace clic en un departamento, se despliegan sus usuarios individuales con su desglose de consumo por entorno.
* **Escenario 3: Filtro por entorno**
  * **Dado que** el usuario selecciona el filtro de entorno "PRO",
  * **Cuando** se aplica el filtro,
  * **Entonces** todos los KPIs y sumatorios de la tabla jerárquica se recalculan en tiempo real para mostrar únicamente las ejecuciones realizadas en entorno productivo.

---

### **Historia de Usuario 2**
* **Identificador:** `HU-02`
* **Título:** Ingesta y normalización de archivos de logs de telemetría de IA
* **Como:** Administrador del Sistema / Ingeniero de Plataforma,
* **Quiero:** Subir ficheros de logs (JSON/JSONL/CSV) con eventos de ejecución de OpenAI, Google Gemini o proxies de IA,
* **Para:** Centralizar y estandarizar automáticamente los registros de consumo, cálculo de tokens y costes monetarios en la base de datos de AIFindOps.

**Criterios de Aceptación (Gherkin):**
* **Escenario 1: Ingesta de fichero válido**
  * **Dado que** el administrador selecciona un archivo JSON con eventos de telemetría válidos,
  * **Cuando** envía la solicitud al endpoint `POST /api/v1/ingestion/logs`,
  * **Entonces** el sistema valida los esquemas con Zod, calcula el coste monetario de cada ejecución según el modelo, inserta los registros en PostgreSQL y retorna un estado `201 Created` con el ID de lote y el número de filas procesadas.
* **Escenario 2: Manejo de errores de formato**
  * **Dado que** el archivo contiene registros con campos obligatorios ausentes (ej. falta `promptTokens` o `model`),
  * **Cuando** se procesa la ingesta,
  * **Entonces** el sistema rechaza los registros corruptos, devuelve un `400 Bad Request` indicando las líneas erróneas y no corrompe los datos previamente existentes.

---

### **Historia de Usuario 3**
* **Identificador:** `HU-03`
* **Título:** Auditoría y trazabilidad granular de ejecuciones por Agente y Usuario
* **Como:** Responsable de Departamento / Auditor de Seguridad,
* **Quiero:** Navegar al detalle de un agente de IA o de un usuario específico y revisar su historial cronológico de ejecuciones,
* **Para:** Auditar el uso adecuado de los modelos, verificar latencias, identificar ejecuciones fallidas y supervisar qué usuario realiza cada llamada.

**Criterios de Aceptación (Gherkin):**
* **Escenario 1: Acceso a la vista de detalle de agente**
  * **Dado que** el usuario hace clic sobre el nombre o contador de ejecuciones de un agente en la tabla,
  * **Cuando** se carga la vista de detalle del agente,
  * **Entonces** se muestra la ficha técnica (proveedor, modelo por defecto, versión) y una tabla paginada con cada una de sus ejecuciones individuales (timestamp, usuario, entorno, tokens, coste y latencia).
* **Escenario 2: Filtrado por estado de ejecución**
  * **Dado que** el auditor desea revisar incidencias,
  * **Cuando** filtra la tabla de ejecuciones por estado "ERROR" o "RATE_LIMIT_EXCEEDED",
  * **Entonces** la tabla muestra únicamente las llamadas fallidas con el código de error y latencia asociada.

---

## 6. Tickets de Trabajo

### **Ticket 1: Infraestructura de BBDD, Esquema Prisma y Docker Compose**
* **ID:** `TCK-001`
* **Componente:** Base de Datos / Infraestructura
* **Tipo:** Tarea Técnica / Setup
* **Estimación:** 5 Story Points
* **Descripción:**
  Configurar el entorno contenerizado de PostgreSQL 16 utilizando Docker Compose, definir el esquema completo de entidades en `schema.prisma`, crear las migraciones iniciales y desarrollar un script de semillas (`seed.ts`) con datos de prueba realistas para organizaciones, departamentos, usuarios, roles, agentes de IA y logs de ejecución.
* **Dependencias:** Ninguna (Tarea inicial).
* **Tareas a realizar:**
  1. Crear archivo `docker/docker-compose.yml` con el servicio `postgres:16-alpine`, volumen persistente `postgres_data` y variables de entorno.
  2. Inicializar Prisma en el backend (`npx prisma init`).
  3. Definir los modelos en `schema.prisma`: `Organization`, `Department`, `Role`, `User`, `AiAgent`, `ExecutionLog`, `IngestionBatch`.
  4. Configurar índices en `ExecutionLog` (`executed_at`, `agent_id`, `user_id`, `environment`) y campo `metadata` tipo `Json`.
  5. Ejecutar migración inicial (`npx prisma migrate dev --name init_schema`).
  6. Escribir script `prisma/seed.ts` con al menos 2 organizaciones, 4 departamentos, 8 usuarios, 6 agentes y más de 1,000 registros de logs distribuidos en entornos DEV, PRE y PRO.
* **Criterios de Aceptación (Definition of Done):**
  * El comando `docker compose up -d` levanta la base de datos sin errores en el puerto 5432.
  * El comando `npx prisma db seed` puebla la base de datos con relaciones coherentes e íntegras.

---

### **Ticket 2: Motor de Ingesta, Autenticación y API de Agregación Jerárquica**
* **ID:** `TCK-002`
* **Componente:** Backend (Node.js + Express + TypeScript)
* **Tipo:** Feature Backend
* **Estimación:** 8 Story Points
* **Descripción:**
  Implementar la arquitectura limpia en el backend, incluyendo la autenticación JWT con roles RBAC, el motor de ingesta de ficheros de logs con validación Zod, y los endpoints analíticos que calculan los KPIs globales y la matriz jerárquica agregada (*Org ➔ Dept ➔ User*) con filtros por entorno y fechas.
* **Dependencias:** `TCK-001`.
* **Tareas a realizar:**
  1. Configurar servidor Express con middlewares de seguridad (`cors`, `helmet`, `express-rate-limit`).
  2. Implementar servicio de autenticación con `bcrypt` y firma de tokens `jsonwebtoken`.
  3. Crear middleware `authenticateJWT` y `authorizeRoles`.
  4. Desarrollar `IngestionService` con parser de logs, validación Zod y cálculo automático de costes según precios por millón de tokens para OpenAI y Gemini.
  5. Desarrollar `MetricsService` con consultas SQL / Prisma optimizadas que agreguen tokens, costes y ejecuciones agrupadas jerárquicamente.
  6. Exponer y testear los endpoints:
     * `POST /api/v1/auth/login`
     * `POST /api/v1/ingestion/logs`
     * `GET /api/v1/metrics/dashboard`
     * `GET /api/v1/agents/:agentId/executions`
  7. Escribir tests unitarios y de integración con Vitest y Supertest.
* **Criterios de Aceptación (Definition of Done):**
  * Cobertura de tests en la capa de servicios > 80%.
  * Endpoints documentados y conformes a la especificación OpenAPI 3.0.

---

### **Ticket 3: Dashboard Ejecutivo con KPIs y Tabla Interactiva Drill-Down**
* **ID:** `TCK-003`
* **Componente:** Frontend (React + Vite + TypeScript)
* **Tipo:** Feature Frontend
* **Estimación:** 8 Story Points
* **Descripción:**
  Construir la interfaz de usuario en React con TailwindCSS, creando el panel superior de KPIs globales interactivos, la tabla colapsable multinivel (*Organización ➔ Departamento ➔ Usuario*) con sumatorios en cascada, la barra de filtros por entorno (DEV/PRE/PRO) y fechas, y el modal de ingesta de logs.
* **Dependencias:** `TCK-002`.
* **Tareas a realizar:**
  1. Inicializar proyecto React con Vite, TypeScript, TailwindCSS y Lucide Icons.
  2. Implementar cliente API con Axios y gestión de estado con React Query / Zustand.
  3. Crear componente `KpiCard` y gráficos de distribución de modelos con Recharts.
  4. Desarrollar el componente `DrillDownTable` con soporte para expandir/colapsar filas jerárquicas y cálculo reactivo de sumatorios.
  5. Implementar selector de entorno (`DEV`, `PRE`, `PRO`, `TODOS`) y selector de rango temporal con actualización reactiva.
  6. Construir vistas de detalle (`AgentDetailView` y `UserTraceabilityView`).
  7. Crear componente `LogUploadModal` con soporte drag-and-drop para subir ficheros de telemetría.
* **Criterios de Aceptación (Definition of Done):**
  * La interfaz es 100% responsiva y accesible.
  * El despliegue de acordeón es instantáneo y los sumatorios coinciden matemáticamente en todos los niveles.

---

## 7. Pull Requests

### **Pull Request 1**
* **Título:** `feat(infra): setup docker-compose, prisma schema, migrations and realistic seeders`
* **Rama Origen:** `feature/db-docker-prisma-setup` ➔ **Rama Destino:** `develop`
* **Descripción de cambios:**
  * Añadida configuración de `docker/docker-compose.yml` para servicio PostgreSQL 16 persistente.
  * Definido el esquema `schema.prisma` con modelos: `Organization`, `Department`, `Role`, `User`, `AiAgent`, `ExecutionLog`, `IngestionBatch`.
  * Índices de alto rendimiento creados para consultas de series temporales en `ExecutionLog`.
  * Implementado script `seed.ts` con datos de prueba estructurados para demostración.
* **Validación realizada:**
  * `docker compose up -d` verificado en macOS / Linux.
  * `npx prisma migrate dev` ejecutado limpiamente.
  * Seed verificado mediante consultas SQL de comprobación.

---

### **Pull Request 2**
* **Título:** `feat(backend): implement clean architecture, ingestion pipeline, JWT/RBAC auth & aggregation API`
* **Rama Origen:** `feature/backend-core-api` ➔ **Rama Destino:** `develop`
* **Descripción de cambios:**
  * Estructurada la arquitectura en capas: controladores, servicios, repositorios y middlewares.
  * Implementado sistema de autenticación JWT y control de acceso basado en roles (RBAC).
  * Añadido pipeline de ingesta (`POST /api/v1/ingestion/logs`) con validación Zod y cálculo dinámico de costes de tokens.
  * Desarrollado motor analítico (`GET /api/v1/metrics/dashboard`) con agregaciones en cascada por Organización, Departamento, Usuario y Entorno.
  * Suite de tests unitarios y de integración con Vitest y Supertest.
* **Validación realizada:**
  * 100% de tests unitarios y de integración pasando en verde.
  * Validación de contratos OpenAPI 3.0 con Swagger.

---

### **Pull Request 3**
* **Título:** `feat(frontend): build executive dashboard, dynamic drill-down table, environment filters & detail views`
* **Rama Origen:** `feature/frontend-dashboard-drilldown` ➔ **Rama Destino:** `main`
* **Descripción de cambios:**
  * Creado el panel superior de KPIs ejecutivos con métricas de 90 días (tokens, costes, agentes, mix de modelos).
  * Construida la tabla jerárquica interactiva colapsable (*Org ➔ Dept ➔ User*) con sumatorios en cascada.
  * Añadida barra de navegación con filtros en tiempo real por entorno (**DEV**, **PRE**, **PRO**) y rango de fechas.
  * Implementadas vistas de detalle para auditoría de agentes y trazabilidad de ejecuciones por usuario.
  * Añadido modal drag-and-drop para ingesta de archivos de logs.
* **Validación realizada:**
  * Tests E2E con Playwright simulando login, despliegue del árbol jerárquico y filtrado de entornos.
  * Verificación de diseño responsive y rendimiento en Lighthouse (> 90).
