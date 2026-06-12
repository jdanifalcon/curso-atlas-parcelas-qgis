# Atlas Dinámicos y Simbología Basada en Reglas en QGIS

Repositorio del material del curso **Atlas Dinámicos y Simbología Basada en Reglas en QGIS**.

Este curso está orientado a usuarios de SIG que desean automatizar la generación de mapas mediante el sistema de **Atlas de QGIS**, utilizando expresiones, simbología basada en reglas y estructuras de datos espaciales eficientes.

---

# 📚 Contenido del Curso

## Sesión 01 — Fundamentos de Atlas

* Variables de Atlas
* Plantillas de impresión
* Generación automática de mapas
* Configuración inicial del Layout

---

## Sesión 02 — Simbología Basada en Reglas

* Reglas dinámicas para polígonos
* Visualización automática de vértices
* Puntos de ubicación
* Uso de `@atlas_feature`
* Reglas `ELSE`

---

## Sesión 03 — Automatización Avanzada

* Parcelas asociadas
* Expresiones avanzadas
* `array_intersect`
* Exportación masiva a PDF
* Optimización de proyectos Atlas

---

# 🗂️ Estructura del Proyecto

```bash
├── data/
│   ├── geopackage/
│   └── ejemplos/
│
├── manual/
│   └── manual_simbologia_reglas_qgis.pdf
│
├── proyectos_qgis/
│   └── atlas_parcelas.qgz
│
├── scripts/
│   └── expresiones_qgis.txt
│
├── recursos/
│   └── flyer_curso_atlas_qgis.jpg
│
└── README.md
```

---

# 🧩 Caso de Estudio

El curso utiliza un caso práctico enfocado en:

* Parcelas agrícolas
* Parcelas asociadas o colindantes
* Vértices
* Puntos de ubicación
* Automatización cartográfica

---

# 📖 Formato 01 — Visualización Básica

Este formato muestra únicamente la parcela principal junto con sus vértices y puntos de ubicación correspondientes.

---

## 1. Parcela Principal

### Regla principal

```sql
$id = @atlas_featureid
```

### Regla ELSE

Oculta cualquier otro elemento que no corresponda a la parcela activa del Atlas.

---

## 2. Vértices

### Primera regla

```sql
"id_parcela" = attribute(@atlas_feature, 'id_parcela')
```

### Regla ELSE

Oculta los vértices que no pertenecen a la parcela activa.

---

## 3. Puntos de Ubicación

### Primera regla

```sql
"id_parcela" = attribute(@atlas_feature, 'id_parcela')
```

### Regla ELSE

Oculta los puntos que no pertenecen a la parcela activa.

---

# 📖 Formato 02 — Parcelas Asociadas

Este formato permite visualizar parcelas colindantes o relacionadas automáticamente dentro del Atlas.

---

## 1. Parcela Principal

### Primera regla obligatoria

```sql
$id = @atlas_featureid
```

---

## 2. Parcelas Asociadas o Colindantes

### Segunda regla

```sql
"id_parcela" = attribute(@atlas_feature, 'id_parcela')
```

---

### Tercera regla

```sql
array_intersect(
 array(
 id_parcela
 ),
 string_to_array(
 replace(
 attribute(
 @atlas_feature,
 'parcelas_asociadas'
 ),
 ' ',
 ''
 )
 )
)
```

---

### Regla ELSE

Oculta cualquier elemento no relacionado con la parcela activa.

---

## 3. Vértices

### Primera regla

```sql
"id_parcela" = attribute(@atlas_feature, 'id_parcela')
```

---

### Segunda regla

```sql
array_intersect(
 array(
 id_parcela
 ),
 string_to_array(
 replace(
 attribute(
 @atlas_feature,
 'parcelas_asociadas'
 ),
 ' ',
 ''
 )
 )
)
```

---

### Regla ELSE

Oculta cualquier vértice no relacionado con la parcela principal ni con las asociadas.

---

## 4. Puntos de Ubicación

### Primera regla

```sql
"id_parcela" = attribute(@atlas_feature, 'id_parcela')
```

---

### Segunda regla

```sql
array_intersect(
 array(
 id_parcela
 ),
 string_to_array(
 replace(
 attribute(
 @atlas_feature,
 'parcelas_asociadas'
 ),
 ' ',
 ''
 )
 )
)
```

---

### Regla ELSE

Oculta cualquier punto no relacionado con la parcela activa.

---

# ⚙️ Requisitos

* QGIS 3.44 o versiones actualizadas
* Conocimientos básicos de SIG
* Manejo básico de capas vectoriales

---

# 📦 Incluye

* Manual digital
* Proyecto QGIS preconfigurado
* GeoPackage de práctica
* Expresiones listas para usar
* Plantilla Atlas

---

# 🛠️ Recomendaciones Generales

* Mantener el orden correcto de las reglas.
* Verificar que `id_parcela` y `parcelas_asociadas` estén correctamente llenados.
* Utilizar reglas `ELSE` para evitar errores visuales.
* Revisar el orden de capas dentro del panel de QGIS.
* Mantener consistencia en el formato de `parcelas_asociadas`.

---

# ⭐ Objetivo del Curso

Aprender a automatizar la generación de mapas en QGIS utilizando Atlas y simbología basada en reglas, reduciendo tiempos de producción cartográfica y mejorando la organización de proyectos SIG.

---

# 👩‍💻 Autoría

**Jessica Daniela Ocaña Falcón**

Especialista en Geomática y automatización cartográfica con QGIS.

---

# 📬 Contacto

📧 [hellojfalcon@gmail.com](mailto:hellojfalcon@gmail.com)

---
