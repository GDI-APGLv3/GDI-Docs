---
hide:
  - toc
---

# Administradores - BackOffice

**Panel de administracion** del Sistema de Gestion Documental Inteligente para gobiernos LATAM.

Esta seccion documenta el uso del BackOffice, la herramienta de administracion para gestionar municipios, usuarios, permisos, sectores y configuracion del sistema.

---

<div class="grid cards" markdown>

-   :material-information:{ .lg .middle } **Informacion General**

    ---

    Datos institucionales del municipio: nombre, acronimo, ciudad de firma, logo y color institucional.

    [:octicons-arrow-right-24: Ver seccion](informacion-general.md)

-   :material-stamp:{ .lg .middle } **Roles y Sellos**

    ---

    Rangos jerarquicos y sellos de firma. Define quien puede numerar cada tipo de documento.

    [:octicons-arrow-right-24: Ver seccion](roles-y-sellos.md)

-   :material-sitemap:{ .lg .middle } **Organigrama**

    ---

    Estructura organizativa: reparticiones, sectores, usuarios asignados y responsables.

    [:octicons-arrow-right-24: Ver seccion](organigrama.md)

-   :material-file-cog:{ .lg .middle } **Tipos de Documentos**

    ---

    Configurar tipos de documento habilitados, restricciones por sector y por rango. Catalogo global.

    [:octicons-arrow-right-24: Ver seccion](tipos-de-documentos.md)

-   :material-folder-cog:{ .lg .middle } **Tipos de Expedientes**

    ---

    Configurar tipos de expediente habilitados, departamentos permitidos y catalogo global.

    [:octicons-arrow-right-24: Ver seccion](tipos-de-expedientes.md)

-   :material-account-group:{ .lg .middle } **Usuarios**

    ---

    Administrar usuarios: crear, editar, asignar sectores, roles, sellos y permisos de busqueda.

    [:octicons-arrow-right-24: Ver seccion](usuarios.md)

-   :material-shield-account:{ .lg .middle } **Administracion**

    ---

    Gestionar que usuarios tienen permisos de administrador en el BackOffice.

    [:octicons-arrow-right-24: Ver seccion](administracion.md)

-   :material-certificate:{ .lg .middle } **Certificados**

    ---

    Gestionar certificados digitales para firma electronica de documentos.

    [:octicons-arrow-right-24: Ver seccion](certificados.md)

-   :material-backup-restore:{ .lg .middle } **Backups**

    ---

    Copias de seguridad de los datos del municipio.

    [:octicons-arrow-right-24: Ver seccion](backups.md)

</div>

---

## Menu del BackOffice

El sidebar izquierdo del BackOffice contiene las siguientes secciones:

| Seccion | Descripcion | Estado |
|---------|-------------|--------|
| **Informacion general** | Datos y branding del municipio | Documentado |
| **Roles y Sellos** | Jerarquias y sellos de firma | Documentado |
| **Organigrama** | Estructura organizativa | Documentado |
| **Tipos de Documentos** | Catalogo de tipos de documento | Documentado |
| **Tipos de Expedientes** | Catalogo de tipos de expediente | Documentado |
| **Usuarios** | Gestion de usuarios | Documentado |
| **Administracion** | Permisos de admin | Documentado |
| **Certificados** | Certificados digitales | Proximamente |
| **Backups** | Copias de seguridad | Proximamente |
| **Integraciones** | Integraciones externas | No disponible |
| **API Key** | Claves de API | No disponible |
| **Auditorias** | Registros de auditoria | No disponible |

## Acceso al BackOffice

El BackOffice es accesible en un puerto separado (`:3013`) y requiere credenciales de administrador. Solo usuarios con permisos de administracion pueden acceder a estas funcionalidades.

| Componente | Puerto | URL |
|-----------|--------|-----|
| BackOffice Frontend | `:3013` | `https://backoffice.gdi.app` |
| BackOffice Backend | `:8010` | API interna |
