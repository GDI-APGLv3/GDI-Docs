---
hide:
  - toc
---

# Documentacion Tecnica

**Documentacion tecnica por servicio** del Sistema de Gestion Documental Inteligente para gobiernos LATAM.

---

<div class="grid cards" markdown>

-   :material-sitemap:{ .lg .middle } **Arquitectura**

    ---

    Vision general, diagramas de servicios, comunicacion inter-servicio, multi-tenant y flujos principales.

    [:octicons-arrow-right-24: Ver arquitectura](arquitectura/index.md)

-   :material-react:{ .lg .middle } **Frontend**

    ---

    Next.js 15, React 18, TypeScript, Tailwind CSS, shadcn/ui. Paginas, componentes, hooks y auth.

    [:octicons-arrow-right-24: Ver frontend](frontend/index.md)

-   :material-api:{ .lg .middle } **Backend**

    ---

    FastAPI, Python 3.12. Endpoints REST, services, models, middleware, auth y API Gateway MCP.

    [:octicons-arrow-right-24: Ver backend](backend/index.md)

-   :material-file-pdf-box:{ .lg .middle } **PDFComposer**

    ---

    FastAPI + Gotenberg. Generacion de PDFs con templates Jinja2 para documentos oficiales.

    [:octicons-arrow-right-24: Ver PDFComposer](pdfcomposer/index.md)

-   :material-certificate:{ .lg .middle } **Notary**

    ---

    Firma digital PAdES, firma visual, estampado, certificados. pyHanko + PyMuPDF + ReportLab.

    [:octicons-arrow-right-24: Ver Notary](notary/index.md)

-   :material-database:{ .lg .middle } **Database**

    ---

    PostgreSQL 17 + pgvector. Schemas multi-tenant, tablas, enums, scripts de deploy y numeracion.

    [:octicons-arrow-right-24: Ver database](database/index.md)

-   :material-rocket-launch:{ .lg .middle } **Deploy**

    ---

    Railway, Cloudflare R2, GitHub Actions. Infraestructura y CI/CD.

    [:octicons-arrow-right-24: Ver deploy](deploy/index.md)

-   :material-book-open-variant:{ .lg .middle } **Guias**

    ---

    Desarrollo local, crear endpoints, nuevos tipos de documento, nuevos municipios y troubleshooting.

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
| GDI-Notary | <span class="port-badge">:8001</span> | FastAPI, pyHanko, PyMuPDF |
| GDI-PDFComposer | <span class="port-badge">:8002</span> | FastAPI, Gotenberg, Jinja2 |
| GDI-eMailService | <span class="port-badge">:8003</span> | FastAPI, Jinja2, SMTP |
| GDI-AgenteLANG | <span class="port-badge">:8004</span> | FastAPI, LangGraph, OpenRouter |
| GDI-MCP | <span class="port-badge">:8005</span> | Integrado en Backend |
