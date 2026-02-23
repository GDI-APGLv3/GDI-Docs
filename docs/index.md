---
hide:
  - navigation
  - toc
---

# GDI Docs

**Documentacion unificada** del Sistema de Gestion Documental Inteligente para gobiernos LATAM.

Selecciona la seccion que corresponde a tu perfil:

---

<div class="grid cards" markdown>

-   :material-account:{ .lg .middle } **Usuarios**

    ---

    Manual de usuario: como crear documentos, gestionar expedientes, enviar notas, firmar y usar el asistente AI.

    [:octicons-arrow-right-24: Ir al manual de usuario](usuarios/index.md)

-   :material-shield-account:{ .lg .middle } **Administradores**

    ---

    Panel de administracion (BackOffice): gestion de organizaciones, usuarios, permisos, sectores y configuracion del sistema.

    [:octicons-arrow-right-24: Ir a administracion](administradores/index.md)

-   :material-code-braces:{ .lg .middle } **Desarrollo**

    ---

    Documentacion tecnica por servicio: arquitectura, endpoints, services, database, deploy y guias de desarrollo.

    [:octicons-arrow-right-24: Ir a desarrollo](desarrollo/index.md)

</div>

---

## Stack Tecnologico

| Capa | Tecnologias |
|------|-------------|
| **Frontend** | Next.js 15, React 18, TypeScript, Tailwind CSS, shadcn/ui |
| **Backend** | FastAPI, Python 3.12, Auth0, PostgreSQL 17 |
| **Microservicios** | PDFComposer (Gotenberg), Notary (pyHanko), eMailService, AgenteLANG (LangGraph) |
| **Infraestructura** | Railway, Cloudflare R2, GitHub Actions |

## Servicios y Puertos

| Servicio | Puerto | Stack |
|----------|--------|-------|
| GDI-FRONTEND | `:3003` | Next.js 15, React 18, TypeScript |
| GDI-BackOffice-Front | `:3013` | Next.js 15, React 18, TypeScript |
| GDI-Backend | `:8000` | FastAPI, Python 3.12 |
| GDI-BackOffice-Back | `:8010` | FastAPI, Python 3.12 |
| GDI-Notary | `:8001` | FastAPI, pyHanko, PyMuPDF |
| GDI-PDFComposer | `:8002` | FastAPI, Gotenberg, Jinja2 |
| GDI-eMailService | `:8003` | FastAPI, Jinja2, SMTP |
| GDI-AgenteLANG | `:8004` | FastAPI, LangGraph, OpenRouter |
| GDI-MCP | `:8005` | Integrado en Backend |

---

!!! info "Sobre esta documentacion"
    Esta documentacion esta organizada por audiencia. Cada tab corresponde a un perfil de usuario diferente. Usa el buscador para encontrar cualquier termino en las tres secciones.
