# Roles y Sellos

Gestiona los rangos jerarquicos y sellos de firma del municipio. Los rangos determinan que tipos de documentos puede firmar cada funcionario. Los sellos definen la firma visual que aparece en los PDFs.

![Roles y Sellos](capturas/roles-y-sellos.png)

---

## Sellos del Municipio

Cada sello define un tipo de firma visual que se estampa en los documentos firmados.

| Campo | Descripcion |
|-------|-------------|
| **Nombre** | Nombre del sello (ej: *Director*, *Intendente Municipal*, *Secretario*) |
| **Descripcion** | Texto descriptivo del sello |
| **Estado** | <span class="campo-tag campo-tag--obligatorio">vinculado</span> indica que el sello esta asignado a al menos un usuario |

### Acciones por sello

| Accion | Descripcion |
|--------|-------------|
| :material-pencil: **Editar** | Modificar nombre y descripcion del sello |
| :material-delete: **Eliminar** | Eliminar el sello (solo si no esta vinculado a ningun usuario) |
| **+ Agregar sello** | Crear un nuevo sello para el municipio |

---

## Rangos Jerarquicos

Los rangos definen la jerarquia del municipio y determinan que tipo de documentos puede numerar cada funcionario.

| Campo | Descripcion |
|-------|-------------|
| **Nivel** | Posicion en la jerarquia (1 = mas alto) |
| **Nombre** | Nombre del rango (ej: *Intendente*, *Secretario*, *Director*) |
| **Firma** | Nombre del sello de firma asociado a este rango |

!!! info "Relacion Rango - Tipo de Documento"
    Algunos tipos de documento requieren un rango minimo para poder ser numerados. Por ejemplo, un **Decreto** solo puede ser numerado por un funcionario con rango de **Intendente** (Nivel 1).

### Acciones por rango

| Accion | Descripcion |
|--------|-------------|
| :material-pencil: **Editar** | Modificar nombre y firma del rango |
| :material-delete: **Eliminar** | Eliminar el rango |
| **+ Agregar rango** | Crear un nuevo nivel jerarquico |
