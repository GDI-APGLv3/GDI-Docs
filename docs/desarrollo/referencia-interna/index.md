---
title: Referencia Interna
description: Documentacion interna para el equipo de desarrollo de GDI Latam.
---

# Referencia Interna

!!! note "Seccion interna"
    Esta seccion es referencia interna para el equipo de desarrollo de GDI. Si buscas integrar tu sistema con GDI, ve a [Gateway API](../gateway/index.md).

Esta seccion contiene la documentacion tecnica detallada de cada componente del sistema GDI. Aqui encontraras guias de arquitectura, convenciones de codigo, configuracion de entornos y procedimientos operativos que utiliza el equipo de desarrollo.

---

<div class="grid cards" markdown>

-   **Frontend**

    ---

    Aplicaciones web construidas con Next.js 15, React 18 y TypeScript. Incluye el portal ciudadano y el backoffice administrativo.

    [:octicons-arrow-right-24: Ver documentacion](../frontend/index.md)

-   **Backend Services**

    ---

    APIs REST construidas con FastAPI y Python 3.12. Gestionan toda la logica de negocio, autenticacion y comunicacion con microservicios.

    [:octicons-arrow-right-24: Ver documentacion](../backend/index.md)

-   **Database**

    ---

    PostgreSQL 17 con arquitectura multi-tenant. Cada municipio opera en un schema aislado con pgvector para busqueda semantica.

    [:octicons-arrow-right-24: Ver documentacion](../database/index.md)

-   **Notary**

    ---

    Microservicio de firma digital PAdES. Genera firmas electronicas validas sobre documentos PDF con sellado de tiempo.

    [:octicons-arrow-right-24: Ver documentacion](../notary/index.md)

-   **Deploy**

    ---

    Infraestructura con Docker, almacenamiento en Cloudflare R2 y CI/CD con GitHub Actions. Incluye guias de despliegue y troubleshooting.

    [:octicons-arrow-right-24: Ver documentacion](../deploy/index.md)

</div>
