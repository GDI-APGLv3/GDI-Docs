# Docker

## Vision General

Cada servicio de GDI se empaqueta como imagen Docker. Las organizaciones despliegan el ecosistema completo usando Docker Compose, que orquesta todos los contenedores, redes y volumenes necesarios.

---

## Servicios

### GDI-Backend (API Principal)

| Campo | Valor |
|-------|-------|
| **Stack** | Python 3.12, FastAPI, Gunicorn + Uvicorn |
| **Puerto** | 8000 |
| **Tipo** | Publico (expuesto al exterior) |
| **Dockerfile** | Si |
| **Start Command** | `gunicorn main:app --workers 8 --worker-class uvicorn.workers.UvicornWorker --bind 0.0.0.0:$PORT --timeout 120 --keep-alive 5 --max-requests 1000 --max-requests-jitter 50 --preload` |

**Variables de entorno:**

| Variable | Descripcion | Ejemplo |
|----------|-------------|---------|
| `DATABASE_URL` | Connection string PostgreSQL | `postgresql://user:pass@postgres:5432/railway` |
| `TESTING_MODE` | Modo testing (header X-User-ID) | `true` / `false` |
| `AUTH0_DOMAIN` | Dominio Auth0 | `tu-tenant.us.auth0.com` |
| `AUTH0_AUDIENCE` | Audience JWT | `https://api.tu-dominio.com` |
| `PDFCOMPOSER_URL` | URL PDFComposer (internal) | `http://pdfcomposer:8002` |
| `PDFCOMPOSER_API_KEY` | API Key PDFComposer | `(secreto)` |
| `NOTARY_URL` | URL Notary (internal) | `http://notary:8001` |
| `NOTARY_API_KEY` | API Key Notary | `(secreto)` |
| `CF_R2_ENDPOINT` | Endpoint Cloudflare R2 | `https://ACCOUNT_ID.r2.cloudflarestorage.com` |
| `CF_R2_ACCESS_KEY_ID` | R2 Access Key | `(secreto)` |
| `CF_R2_SECRET_ACCESS_KEY` | R2 Secret Key | `(secreto)` |
| `CF_R2_SIGN_EXPIRATION` | Expiracion URLs firmadas (seg) | `600` |
| `FRONTEND_URL` | URL del frontend (CORS) | `https://tu-frontend.tu-dominio.com` |

**Health check:**

```bash
curl http://localhost:8000/health
# {"status": "healthy", "database": "connected"}
```

---

### GDI-FRONTEND (Portal Principal)

| Campo | Valor |
|-------|-------|
| **Stack** | Next.js 15, React 18, TypeScript 5, Tailwind |
| **Puerto** | 3003 |
| **Tipo** | Publico (expuesto al exterior) |

**Variables de entorno:**

| Variable | Descripcion |
|----------|-------------|
| `AUTH0_SECRET` | Secret para sesiones |
| `AUTH0_BASE_URL` | URL base de la app |
| `AUTH0_ISSUER_BASE_URL` | URL Auth0 |
| `AUTH0_CLIENT_ID` | Client ID Auth0 |
| `AUTH0_CLIENT_SECRET` | Client Secret Auth0 |
| `NEXT_PUBLIC_API_URL` | URL del Backend API |

---

### GDI-BackOffice-Front (Panel Admin)

| Campo | Valor |
|-------|-------|
| **Stack** | Next.js 15, React 18, TypeScript 5, Tailwind |
| **Puerto** | 3013 |
| **Tipo** | Publico (expuesto al exterior) |

**Variables de entorno:** Identicas a GDI-FRONTEND pero apuntando al BackOffice-Back.

---

### GDI-BackOffice-Back (API Admin)

| Campo | Valor |
|-------|-------|
| **Stack** | Python 3.12, FastAPI, psycopg2 |
| **Puerto** | 8010 |
| **Tipo** | Publico (expuesto al exterior) |

**Variables de entorno:**

| Variable | Descripcion |
|----------|-------------|
| `DB_HOST` | Host PostgreSQL |
| `DB_PORT` | Puerto PostgreSQL |
| `DB_USER` | Usuario BD |
| `DB_PASSWORD` | Password BD |
| `DB_NAME` | Nombre de la base de datos |
| `AUTH0_DOMAIN` | Dominio Auth0 |
| `AUTH0_AUDIENCE` | Audience JWT |
| `FRONTEND_URL` | URL del BackOffice-Front (CORS) |
| `TESTING_MODE` | Modo testing |

---

### GDI-PDFComposer (Generador de PDFs)

| Campo | Valor |
|-------|-------|
| **Stack** | Python 3.11, FastAPI, Jinja2, WeasyPrint, PyMuPDF |
| **Puerto** | 8002 |
| **Tipo** | Interno (solo accesible dentro de la red Docker) |
| **Dockerfile** | Si |
| **Start Command** | `gunicorn main:app -c gunicorn_conf.py` |

**Variables de entorno:**

| Variable | Descripcion |
|----------|-------------|
| `API_KEY` | API Key para autenticacion |
| `GUNICORN_WORKERS` | Numero de workers (default 4) |

**Health check:**

```bash
# Solo desde dentro de la red Docker
curl http://pdfcomposer:8002/health
```

---

### GDI-Notary (Firma Digital)

| Campo | Valor |
|-------|-------|
| **Stack** | Python 3.11, FastAPI, pyHanko, PyMuPDF, ReportLab |
| **Puerto** | 8001 |
| **Tipo** | Interno (solo accesible dentro de la red Docker) |
| **Dockerfile** | Si |
| **Start Command** | `gunicorn app.main:app -c gunicorn_conf.py` |

**Variables de entorno:**

| Variable | Descripcion |
|----------|-------------|
| `API_KEY` | API Key para autenticacion |
| `ENVIRONMENT` | `test` o `prd` |
| `CERTS_DIR` | Directorio de certificados (default `./certs`) |
| `TSA_URL` | Servidor de timestamp (default `http://timestamp.digicert.com`) |
| `FALLBACK_TO_VISUAL` | Fallback a firma visual si no hay certificado |
| `GUNICORN_WORKERS` | Numero de workers (default 3) |
| `GUNICORN_TIMEOUT` | Timeout en segundos (default 90) |

**Health check:**

```bash
curl http://notary:8001/health
# {"status": "healthy", "signature_system": "pades", ...}
```

---

### GDI-AgenteLANG (Agente IA)

| Campo | Valor |
|-------|-------|
| **Stack** | Python 3.11, FastAPI, LangGraph, pgvector |
| **Puerto** | 8004 |
| **Tipo** | Interno (solo accesible dentro de la red Docker) |
| **Dockerfile** | Si |
| **Start Command** | `uvicorn app.main:app --host 0.0.0.0 --port ${PORT:-8004}` |

**Variables de entorno:**

| Variable | Descripcion |
|----------|-------------|
| `OPENROUTER_API_KEY` | API Key OpenRouter |
| `OPENROUTER_MODEL` | Modelo principal (Gemini Flash 2.0) |
| `OPENROUTER_FAST_MODEL` | Modelo router (Llama 3.3 free) |
| `EMBEDDINGS_MODEL` | Modelo embeddings |
| `GDI_BACKEND_URL` | URL Backend (para tools) |
| `INTERNAL_API_KEY` | API Key interna |
| `DATABASE_URL` | PostgreSQL connection string |
| `AUTH0_DOMAIN` | Dominio Auth0 |
| `AUTH0_AUDIENCE` | Audience JWT |
| `AI_WORKER_INTERVAL` | Intervalo polling worker (seg) |
| `AI_WORKER_BATCH_SIZE` | Docs por batch |
| `ENABLED_SCHEMAS` | Schemas a procesar (JSON array) |

---

### PostgreSQL

| Campo | Valor |
|-------|-------|
| **Version** | 17+ con pgvector |
| **Tipo** | Interno (solo accesible dentro de la red Docker) |
| **Puerto** | 5432 |
| **Imagen** | `pgvector/pgvector:pg17` |

---

## Networking (Comunicacion Interna)

Docker Compose crea una red interna donde los servicios se comunican por nombre de servicio. Esto es mas rapido y seguro que exponer puertos al exterior.

```mermaid
graph LR
    subgraph Internet
        Client["Cliente externo"]
    end

    subgraph Docker["Docker Compose"]
        BE["GDI-Backend"]
        PDF["PDFComposer"]
        NOT["Notary"]
    end

    Client -->|"https://tu-backend.tu-dominio.com"| BE
    BE -->|"http://pdfcomposer:8002"| PDF
    BE -->|"http://notary:8001"| NOT
```

### URLs Internas (Docker Networking)

```
http://<nombre-servicio>:<puerto>
```

| Servicio | URL Interna |
|----------|-------------|
| GDI-Backend | `http://backend:8000` |
| GDI-PDFComposer | `http://pdfcomposer:8002` |
| GDI-Notary | `http://notary:8001` |
| GDI-AgenteLANG | `http://agentelang:8004` |
| PostgreSQL | `postgres:5432` |

!!! tip "Ventajas de Docker Networking"
    - Sin exposicion a internet (comunicacion directa dentro de la red Docker)
    - Sin costo de egress
    - No exponen servicios internos a internet
    - Nombres DNS estables (el nombre del servicio en Docker Compose)

!!! warning "Limitaciones"
    - Solo funcionan entre servicios de la misma red Docker Compose
    - No accesibles desde maquinas fuera del host (usar URLs publicas para acceso externo)
    - Protocolo `http://` (no https) porque el trafico es interno

---

## Docker Compose

### Archivo de ejemplo

```yaml
# docker-compose.yml
version: "3.8"

services:
  postgres:
    image: pgvector/pgvector:pg17
    restart: always
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: ${DB_PASSWORD}
      POSTGRES_DB: railway
    volumes:
      - pgdata:/var/lib/postgresql/data
    ports:
      - "5432:5432"
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U postgres"]
      interval: 10s
      timeout: 5s
      retries: 5

  backend:
    build:
      context: ./GDI-Backend
      dockerfile: Dockerfile
    restart: always
    ports:
      - "8000:8000"
    env_file: ./env/backend.env
    depends_on:
      postgres:
        condition: service_healthy
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8000/health"]
      interval: 30s
      timeout: 10s
      retries: 3

  backoffice-back:
    build:
      context: ./GDI-BackOffice-Back
      dockerfile: Dockerfile
    restart: always
    ports:
      - "8010:8010"
    env_file: ./env/backoffice-back.env
    depends_on:
      postgres:
        condition: service_healthy

  pdfcomposer:
    build:
      context: ./GDI-PDFComposer
      dockerfile: Dockerfile
    restart: always
    expose:
      - "8002"
    env_file: ./env/pdfcomposer.env
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8002/health"]
      interval: 30s
      timeout: 10s
      retries: 3

  notary:
    build:
      context: ./GDI-Notary
      dockerfile: Dockerfile
    restart: always
    expose:
      - "8001"
    env_file: ./env/notary.env
    volumes:
      - certs:/app/certs
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8001/health"]
      interval: 30s
      timeout: 10s
      retries: 3

  agentelang:
    build:
      context: ./GDI-AgenteLANG
      dockerfile: Dockerfile
    restart: always
    expose:
      - "8004"
    env_file: ./env/agentelang.env
    depends_on:
      postgres:
        condition: service_healthy

  frontend:
    build:
      context: ./GDI-FRONTEND
      dockerfile: Dockerfile
    restart: always
    ports:
      - "3003:3003"
    env_file: ./env/frontend.env
    depends_on:
      - backend

  backoffice-front:
    build:
      context: ./GDI-BackOffice-Front
      dockerfile: Dockerfile
    restart: always
    ports:
      - "3013:3013"
    env_file: ./env/backoffice-front.env
    depends_on:
      - backoffice-back

volumes:
  pgdata:
  certs:
```

### Archivos de entorno

Crear un directorio `env/` con un archivo `.env` por servicio:

```
env/
├── backend.env
├── backoffice-back.env
├── pdfcomposer.env
├── notary.env
├── agentelang.env
├── frontend.env
└── backoffice-front.env
```

!!! danger "Seguridad"
    Nunca commitear los archivos `.env` al repositorio. Agregarlos a `.gitignore`.

---

## Health Check Endpoints

Cada servicio expone un endpoint `/health` que no requiere autenticacion:

| Servicio | Endpoint | Respuesta esperada |
|----------|----------|--------------------|
| GDI-Backend | `GET /health` | `{"status": "healthy", "database": "connected"}` |
| GDI-BackOffice-Back | `GET /health` | `{"status": "ok"}` |
| GDI-PDFComposer | `GET /health` | `{"status": "ok"}` |
| GDI-Notary | `GET /health` | `{"status": "healthy", "signature_system": "pades"}` |
| GDI-AgenteLANG | `GET /health` | `{"status": "ok", "database": "ok", "ai_worker": "running"}` |
| GDI-AgenteLANG | `GET /health/detailed` | Health detallado con stats del worker |

---

## Comandos Utiles

### Levantar todo el ecosistema

```bash
docker compose up -d
```

### Ver logs

```bash
# Todos los servicios
docker compose logs -f

# Un servicio especifico
docker compose logs -f backend

# Ultimas 100 lineas
docker compose logs --tail 100 backend
```

### Reiniciar un servicio

```bash
docker compose restart backend
```

### Reconstruir un servicio (despues de cambios de codigo)

```bash
docker compose up -d --build backend
```

### Detener todo

```bash
docker compose down
```

### Ver estado de los servicios

```bash
docker compose ps
```

### Ejecutar comando dentro de un contenedor

```bash
docker compose exec backend python -c "import main; print('OK')"
```

---

## Actualizacion

Para actualizar los servicios con nuevas versiones:

```bash
# Si usas imagenes de un registry
docker compose pull
docker compose up -d

# Si construyes localmente
git pull  # en cada repositorio
docker compose up -d --build
```

---

## Rollback

Si una actualizacion causa problemas, volver a la version anterior:

```bash
# Reconstruir con el codigo anterior
git checkout <commit-anterior>  # en el repo del servicio
docker compose up -d --build <servicio>
```

Si usas imagenes con tags de un registry, simplemente cambiar el tag en `docker-compose.yml` y re-levantar.

---

## Troubleshooting

### Build Failed

```bash
# Ver logs de build
docker compose build --no-cache <servicio>

# Verificar que exista Dockerfile
# Verificar requirements.txt (Python) o package.json (Node)
```

### Service Crashed

```bash
# Ver logs detallados
docker compose logs --tail 100 <servicio>

# Ver variables de entorno
docker compose exec <servicio> env

# Reiniciar
docker compose restart <servicio>
```

### Cannot Connect to Database

```bash
# Verificar que PostgreSQL este corriendo
docker compose ps postgres

# Verificar conectividad
docker compose exec backend python -c "import psycopg2; print('OK')"

# Verificar variables de entorno
docker compose exec backend env | grep DB_
```

### Servicio Interno No Responde

```bash
# Verificar que el servicio este corriendo
docker compose ps

# Verificar conectividad desde otro contenedor
docker compose exec backend curl http://pdfcomposer:8002/health
docker compose exec backend curl http://notary:8001/health
```
