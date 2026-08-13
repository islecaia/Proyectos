# DESIGN.md — Sprint Dashboard

> Guía de diseño visual para la aplicación de gestión de sprints. Inspirada en la claridad corporativa, el peso visual y la economía gráfica de **Cecabank** (cecabank.es): fondos blancos estructurados, tipografía sólida, acento cian sobre azul profundo, y una voz directa y profesional.

---

## 1. Paleta de colores

### Colores base

| Token               | Hex       | Uso principal                                        |
|---------------------|-----------|------------------------------------------------------|
| `--color-navy`      | `#0D1B35` | Sidebar, header, fondos de sección oscura            |
| `--color-navy-mid`  | `#162346` | Hover en sidebar, tablas con fondo alterno           |
| `--color-white`     | `#FFFFFF` | Fondo de página, tarjetas, modales                   |
| `--color-surface`   | `#F4F6F9` | Fondo de paneles secundarios, inputs                 |
| `--color-border`    | `#DDE2EA` | Bordes de cards, divisores, separadores              |

### Colores de acento

| Token               | Hex       | Uso principal                                        |
|---------------------|-----------|------------------------------------------------------|
| `--color-cyan`      | `#00C2D4` | CTA primario, links activos, badges, highlights      |
| `--color-cyan-dark` | `#009BAA` | Hover de botón primario                              |
| `--color-cyan-light`| `#E0F8FB` | Fondo de estados activos, chips seleccionados        |

### Colores semánticos

| Token                | Hex       | Uso                              |
|----------------------|-----------|----------------------------------|
| `--color-success`    | `#1DB87E` | Sprint completado, tarea done    |
| `--color-warning`    | `#F5A623` | En riesgo, bloqueado, próximo    |
| `--color-danger`     | `#E03F3F` | Overdue, eliminado, error        |
| `--color-info`       | `#3B82F6` | Notas, comentarios, en progreso  |

### Texto

| Token                  | Hex       | Uso                                   |
|------------------------|-----------|---------------------------------------|
| `--text-primary`       | `#0D1B35` | Títulos, datos principales            |
| `--text-secondary`     | `#526180` | Subtítulos, labels, metadatos         |
| `--text-muted`         | `#8B9CB5` | Marcadores de tiempo, placeholders    |
| `--text-on-dark`       | `#FFFFFF` | Texto sobre fondos navy               |
| `--text-on-dark-soft`  | `#A8BECE` | Texto secundario sobre fondos navy    |

---

## 2. Tipografía

### Fuentes

```
Principal: Inter (Google Fonts)
Monoespaciada: JetBrains Mono (para IDs, fechas, contadores)
```

### Escala tipográfica

| Rol             | Tamaño    | Peso      | Tracking  | Uso                                     |
|-----------------|-----------|-----------|-----------|-----------------------------------------|
| Display         | 28px      | 700       | −0.5px    | Título de página, hero de sprint        |
| Heading 1       | 22px      | 700       | −0.3px    | Títulos de sección principal            |
| Heading 2       | 18px      | 600       | −0.2px    | Títulos de card, nombre de sprint       |
| Heading 3       | 15px      | 600       | 0         | Subtítulos de sección, nombres de tarea |
| Body            | 14px      | 400       | 0         | Descripciones, contenido general        |
| Body Small      | 13px      | 400       | 0         | Metadatos, comentarios, detalles        |
| Label           | 12px      | 500       | +0.3px    | Etiquetas de campo, encabezados tabla   |
| Caption         | 11px      | 400       | +0.2px    | Timestamps, versión, notas de pie       |
| Mono            | 13px      | 400       | 0         | IDs de ticket, fechas de sprint, puntos |

### Reglas de uso

- Los títulos de dashboard siempre en `--color-navy`, nunca en gris.
- Labels de tabla en mayúsculas con `letter-spacing: 0.3px`.
- Usar `JetBrains Mono` para contadores de puntos, IDs de issues y fechas absolutas.
- Evitar más de 3 pesos tipográficos en una misma vista.

---

## 3. Botones

### Primario — CTA principal

```css
background: var(--color-cyan);
color: var(--color-navy);
font-weight: 600;
font-size: 14px;
padding: 10px 20px;
border-radius: 6px;
border: none;
transition: background 150ms ease;

&:hover  { background: var(--color-cyan-dark); }
&:active { transform: scale(0.98); }
&:focus  { outline: 2px solid var(--color-cyan); outline-offset: 2px; }
```

### Secundario — Acciones de apoyo

```css
background: transparent;
color: var(--color-navy);
border: 1.5px solid var(--color-border);
font-weight: 500;
font-size: 14px;
padding: 10px 20px;
border-radius: 6px;

&:hover  { border-color: var(--color-navy); background: var(--color-surface); }
```

### Ghost — Acciones discretas

```css
background: transparent;
color: var(--text-secondary);
border: none;
font-weight: 500;
font-size: 13px;
padding: 8px 14px;
border-radius: 6px;

&:hover { background: var(--color-surface); color: var(--text-primary); }
```

### Danger — Eliminar / cancelar

```css
background: transparent;
color: var(--color-danger);
border: 1.5px solid var(--color-danger);
font-weight: 500;
padding: 10px 20px;
border-radius: 6px;

&:hover { background: #FFF0F0; }
```

### Tamaños disponibles

| Variante | Padding        | Font-size |
|----------|----------------|-----------|
| `sm`     | `6px 14px`     | 13px      |
| `md`     | `10px 20px`    | 14px      |
| `lg`     | `12px 28px`    | 15px      |

### Icono + texto: separación de 8px entre icono y label.

---

## 4. Esquinas (Border Radius)

| Token           | Valor  | Uso                                                    |
|-----------------|--------|--------------------------------------------------------|
| `--radius-sm`   | `4px`  | Badges, tags, chips, inputs pequeños                   |
| `--radius-md`   | `6px`  | Botones, campos de formulario, dropdowns               |
| `--radius-lg`   | `10px` | Cards, modales, paneles laterales                      |
| `--radius-xl`   | `16px` | Modales grandes, drawers                               |
| `--radius-full` | `999px`| Avatares, indicadores de estado, progress pills        |

**Regla general:** el sistema evita esquinas muy redondeadas en elementos de datos (tablas, listas de tareas) para mantener lecturabilidad y densidad de información. El `--radius-lg` es el máximo para cards de sprint.

---

## 5. Espaciados

### Escala base: múltiplos de 4px

| Token      | Valor | Uso típico                                              |
|------------|-------|---------------------------------------------------------|
| `--sp-1`   | `4px` | Gaps internos mínimos, entre icono y texto              |
| `--sp-2`   | `8px` | Padding de badges, separación entre chips               |
| `--sp-3`   | `12px`| Padding de inputs, gap entre campos relacionados        |
| `--sp-4`   | `16px`| Padding de cards, separación entre secciones dentro de card |
| `--sp-5`   | `20px`| Padding horizontal de sidebar                           |
| `--sp-6`   | `24px`| Margen entre cards, padding de modales                  |
| `--sp-8`   | `32px`| Separación entre secciones de dashboard                 |
| `--sp-10`  | `40px`| Márgenes de página, padding de header principal         |
| `--sp-16`  | `64px`| Padding vertical en vistas vacías / estado de carga     |

### Estructura de layout

```
┌─ Sidebar 240px ─┬─────────── Contenido principal ────────────┐
│                 │  Padding: 32px 40px                         │
│  Padding: 20px  │                                             │
│                 │  Header de página:  mb-32px                 │
│                 │  Gap entre cards:   24px                    │
│                 │  Gap interno card:  16px                    │
└─────────────────┴─────────────────────────────────────────────┘
```

### Grid de contenido

- Layout de 12 columnas con `gap: 24px`.
- Cards de KPI: 3 columnas (span 4 c/u).
- Tablero de sprint: columna ancha (span 8) + lateral (span 4).
- Vista de backlog: full-width con tabla.

---

## 6. Sombras y elevación

| Token          | Valor CSS                                      | Uso                            |
|----------------|------------------------------------------------|--------------------------------|
| `--shadow-sm`  | `0 1px 3px rgba(13,27,53,0.08)`               | Cards en reposo                |
| `--shadow-md`  | `0 4px 12px rgba(13,27,53,0.10)`              | Cards con hover, dropdowns     |
| `--shadow-lg`  | `0 8px 24px rgba(13,27,53,0.14)`              | Modales, drawers               |
| `--shadow-xl`  | `0 16px 48px rgba(13,27,53,0.18)`             | Tooltips flotantes, popovers   |

---

## 7. Iconografía

- Librería: **Lucide Icons** (stroke, no fill).
- Tamaño estándar: `16px` en listas, `20px` en botones/headers, `24px` en hero.
- Stroke width: `1.5px`.
- Color por defecto: `var(--text-secondary)`. Activo: `var(--color-cyan)`.

---

## 8. Estados de tarea (chips / badges)

| Estado         | Fondo          | Texto          | Borde         |
|----------------|----------------|----------------|---------------|
| To Do          | `#F4F6F9`      | `#526180`      | `#DDE2EA`     |
| In Progress    | `#EBF3FF`      | `#3B82F6`      | `#BFDBFE`     |
| In Review      | `#FFF8E6`      | `#D97706`      | `#FDE68A`     |
| Done           | `#E6FAF3`      | `#1DB87E`      | `#A7F3D0`     |
| Blocked        | `#FFF0F0`      | `#E03F3F`      | `#FECACA`     |

Todos los badges: `border-radius: var(--radius-sm)`, `font-size: 12px`, `font-weight: 500`, `padding: 2px 8px`.

---

## 9. Tono de los textos

### Principios

1. **Directo, no imperativo.** No órdenes, sino orientación. "Ver sprint" en lugar de "Haz clic para ver el sprint".
2. **Concreto sobre vago.** "3 tareas bloqueadas" en lugar de "hay problemas en el sprint".
3. **Institucional pero humano.** Lenguaje técnico cuando el contexto lo exige, sin jerga innecesaria.
4. **Positivo en estados vacíos.** Los estados vacíos deben invitar a la acción, no decir "no hay datos".

### Ejemplos por contexto

| Contexto               | ❌ Evitar                          | ✅ Usar                                    |
|------------------------|-----------------------------------|--------------------------------------------|
| Estado vacío           | "No hay tareas"                   | "Este sprint no tiene tareas aún. Agrega la primera." |
| Error de carga         | "Error al cargar los datos"       | "No pudimos cargar el sprint. Intenta de nuevo." |
| Confirmación de borrado| "¿Estás seguro?"                  | "¿Eliminar esta tarea? Esta acción no se puede deshacer." |
| Éxito                  | "OK. Tarea guardada."             | "Tarea guardada correctamente."            |
| Tiempo restante        | "Faltan días"                     | "Cierre en 4 días · 12 ago"               |
| Carga inicial          | "Cargando..."                     | "Cargando sprint..."                       |

### Capitalización

- Títulos de página y sección: **Title Case** en inglés, **primera letra** en español.
- Labels de campo: minúsculas (`nombre del ticket`, no `Nombre Del Ticket`).
- Botones CTA: primera letra en mayúscula (`Crear sprint`, `Ver backlog`).
- Estados y badges: capitalización solo en primera letra (`In progress`, no `IN PROGRESS`).

### Idioma

- La interfaz puede funcionar en español o inglés; no mezclar idiomas dentro de la misma vista.
- Los términos técnicos de Scrum (`sprint`, `backlog`, `story points`, `velocity`) se mantienen en inglés independientemente del idioma de la UI.

---

## 10. Componentes clave — resumen visual

```
┌─────────────────────────────────────────────────────┐
│  SPRINT CARD                                        │
│  ┌──────────────────────────────────────────────┐  │
│  │ Sprint 14 · 4 ago — 18 ago            [Done] │  │
│  │                                               │  │
│  │ Velocity: 42 pts   ████████████░░  78%       │  │
│  │ Tareas: 18 total · 14 completadas · 2 bloq.  │  │
│  │                                               │  │
│  │              [Ver detalle]  [Cerrar sprint]   │  │
│  └──────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────┘

Cards: radius-lg, shadow-sm, padding 24px
Botones: md, primario + ghost
Progress bar: height 6px, radius-full, color-cyan sobre color-surface
```

---

*Versión 1.0 — Agosto 2026*
