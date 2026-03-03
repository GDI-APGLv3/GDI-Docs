---
hide:
  - toc
---

# Documentacion Tecnica

**Documentacion tecnica por servicio** del Sistema de Gestion Documental Inteligente para gobiernos LATAM.

---

<div class="grid cards" markdown>

-   :material-api:{ .lg .middle } **Gateway API**

    ---

    Interfaz publica de integracion: MCP Server para agentes IA (Claude, ChatGPT) y REST API para sistemas externos. 45 endpoints documentados.

    [:octicons-arrow-right-24: Ver Gateway API](gateway/index.md)

-   :material-sitemap:{ .lg .middle } **Arquitectura**

    ---

    Vision general, diagramas de servicios, comunicacion inter-servicio, multi-tenant y flujos principales.

    [:octicons-arrow-right-24: Ver arquitectura](arquitectura/index.md)

-   :material-book-open-page-variant:{ .lg .middle } **Referencia Interna**

    ---

    Documentacion tecnica interna: Frontend, Backend, Database, Notary y Deploy. Para el equipo de desarrollo GDI.

    [:octicons-arrow-right-24: Ver referencia interna](referencia-interna/index.md)

-   :material-book-open-variant:{ .lg .middle } **Guias**

    ---

    Desarrollo local, crear endpoints, nuevos tipos de documento, nuevas organizaciones y troubleshooting.

    [:octicons-arrow-right-24: Ver guias](guias/desarrollo-local.md)

</div>

---

## Servicios y Puertos

| Servicio | Puerto | Stack |
|----------|--------|-------|
| GDI-FRONTEND | <span class="port-badge">:3003</span> | Next.js 15, React 18, TypeScript |
| GDI-BackOffice-Front | <span class="port-badge">:3013</span> | Next.js 15, React 18, TypeScript |
| GDI-Backend | <span class="port-badge">:8000</span> | FastAPI, Python 3.12 |
| GDI-BackOffice-Back | <span class="port-badge">:8010</span> | FastAPI, Python 3.12 |
| GDI-Gateway | <span class="port-badge">:8005</span> | MCP Server + REST API |
| GDI-Notary | <span class="port-badge">:8001</span> | FastAPI, pyHanko, PyMuPDF |
| GDI-AgenteLANG | <span class="port-badge">:8004</span> | FastAPI, LangGraph, OpenRouter |
