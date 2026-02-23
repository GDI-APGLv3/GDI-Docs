# Previsualizar Documento

La pantalla de previsualizacion permite revisar el documento en formato PDF antes de iniciar el proceso de firma. Muestra como quedara el documento final con el membrete oficial, la referencia y el contenido, junto con una marca de agua diagonal que indica que aun no es un documento oficial.

![Vista previa del documento](../capturas/previsualizacion-documento.png)

---

## Como llegar a esta pantalla

Desde el editor de documento (ya sea HTML o importado), hacer click en el boton **"Previsualizar"** en la parte inferior del panel lateral. El sistema guarda automaticamente los cambios antes de navegar a la previsualizacion.

!!! note "Requisitos previos"
    Para previsualizar se necesita: una referencia no vacia, contenido en el editor (o un PDF cargado para documentos importados) y al menos un firmante asignado.

---

## Encabezado

En la parte superior se muestra:

- **Flecha de retorno** (`<`): al hacer click, aparece el texto **"Vista Previa"** como titulo de la pantalla
- No se muestra el tipo de documento en el encabezado (ese dato esta en el panel lateral)

---

## Visor PDF

El area principal muestra el documento renderizado en formato PDF dentro de un visor integrado.

### Barra de herramientas del visor

| Herramienta | Funcion |
|-------------|---------|
| **Menu** (hamburguesa) | Opciones adicionales del visor |
| **Titulo** | Muestra "PREVISUALIZACION - GDILatam.c..." |
| **Paginador** | Navegar entre paginas (ej: "1/1", "2/5") |
| **Zoom** | Ajustar nivel de zoom (ej: "100%") |
| **Vista de pagina** | Cambiar modo de visualizacion (una pagina, dos paginas) |
| **Rotacion** | Rotar el documento 90 grados |
| **Busqueda** | Buscar texto dentro del documento |
| **Descarga** | Descargar el PDF de previsualizacion |
| **Impresion** | Imprimir el documento |

### Contenido del PDF

El PDF generado incluye:

- **Logo de la organizacion** en el encabezado (ej: "Municipalidad del Futuro")
- **Tipo de documento**: sigla y nombre (ej: "IF - Informe")
- **Placeholders**: "[ciudad y fecha a asignar]", "[numero a asignar]" (se completan al firmar)
- **Referencia**: el titulo descriptivo ingresado por el usuario
- **Cuerpo**: el contenido redactado en el editor o el PDF importado

---

## Marca de agua "PREVISUALIZACION"

| Propiedad | Valor |
|-----------|-------|
| **Texto** | PREVISUALIZACION |
| **Orientacion** | Diagonal (esquina inferior izquierda a esquina superior derecha) |
| **Visible en** | Todas las paginas del documento |
| **Proposito** | Indica que el documento aun no es oficial y no tiene validez legal |

!!! warning "No es un documento oficial"
    Mientras se muestre la marca de agua "PREVISUALIZACION", el documento no tiene numero oficial ni firmas. No debe utilizarse como documento valido. La marca de agua desaparece una vez que se completa el proceso de firma.

---

## Panel lateral derecho

El panel lateral en la previsualizacion es de **solo lectura** y muestra un resumen de la configuracion del documento.

### Secciones del panel

| Seccion | Contenido | Editable |
|---------|-----------|:--------:|
| **Tipo de documento** | Nombre del tipo seleccionado (ej: "Informe") | No |
| **Firmantes** | Lista de firmantes con indicador de numerador | No |
| **Propuesto para vincular a** | Expedientes propuestos para vinculacion | No |

### Firmantes en la previsualizacion

Cada firmante se muestra con su nombre completo. El firmante designado como **numerador** se identifica con un **check azul** (circulo con tilde) junto a su nombre.

| Indicador | Significado |
|-----------|-------------|
| Check azul (circulo con tilde) | Este firmante es el **numerador** (asigna el numero oficial) |
| Sin indicador | Firmante regular |

### Expedientes propuestos

Si se propuso vincular el documento a uno o mas expedientes, se muestran con su numero y referencia. Ejemplo:

```
EE-2026-000019-TXST-INTE / Designacion Director Sistemas - Innovacion
```

---

## Acciones

En la parte inferior del panel lateral se encuentran dos botones.

### Boton: Volver

| Propiedad | Valor |
|-----------|-------|
| **Estilo** | Boton blanco con borde (secundario) |
| **Accion** | Regresa al editor de documento para seguir editando |

### Boton: Comenzar proceso de firma

| Propiedad | Valor |
|-----------|-------|
| **Estilo** | Boton azul (primario) |
| **Accion** | Inicia el circuito de firmas. El documento pasa al estado "En proceso de firma" |
| **Habilitado cuando** | El numerador tiene el rango adecuado para el tipo de documento |

!!! warning "Validacion del numerador"
    Si el firmante designado como numerador no tiene el rango necesario para firmar el tipo de documento seleccionado (por ejemplo, un Decreto requiere rango de Intendente), se muestra una **advertencia en color amarillo** y el boton "Comenzar proceso de firma" queda inhabilitado. Se debe volver al editor y cambiar el numerador por uno con el rango adecuado.

---

## Preguntas frecuentes

??? question "Puedo descargar el PDF de previsualizacion?"
    Si. La barra de herramientas del visor incluye un boton de descarga. Sin embargo, el PDF descargado tendra la marca de agua "PREVISUALIZACION" y no es un documento oficial.

??? question "Si vuelvo al editor y hago cambios, tengo que previsualizar de nuevo?"
    Si. Cada vez que se hacen cambios en el editor es recomendable previsualizar nuevamente para verificar que el PDF refleje los cambios correctamente antes de iniciar el proceso de firma.

??? question "Que pasa si inicio el proceso de firma y el documento tiene errores?"
    Se puede cancelar la firma desde la pantalla de proceso de firma. El documento vuelve a estado editable para corregir los errores. Ver [Rechazar y Subsanar](rechazar-y-subsanar.md) para mas detalles.
