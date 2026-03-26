# colomr-v1

Tema Hugo diseñado desde cero para [colomr.pm](https://colomr.pm). Basado en Material Design 3, con soporte nativo de modo claro/oscuro y un sistema de páginas configurables desde `config.toml` sin tocar código.

---

## Requisitos

- Hugo Extended `>= 0.120.0`
- Las fuentes se cargan desde Google Fonts (Plus Jakarta Sans + Inter + Material Symbols)

---

## Estructura del tema

```
themes/colomr-v1/
├── assets/
│   ├── scss/
│   │   ├── main.scss          # Entry point — importa el resto
│   │   ├── _tokens.scss       # Design tokens MD3 (colores, tipografía, spacing)
│   │   ├── _components.scss   # Header, footer, nav, botones, chips...
│   │   ├── _home.scss         # Estilos exclusivos del Home
│   │   └── _page.scss         # Estilos del template de páginas interiores
│   └── js/
│       └── main.js            # Toggle dark/light + drawer móvil
├── layouts/
│   ├── index.html             # Home page
│   ├── _default/
│   │   ├── baseof.html        # Plantilla base (head, header, main, footer)
│   │   ├── page.html          # Template para páginas interiores (Quién, Qué, Dónde)
│   │   └── single.html        # Fallback genérico
│   ├── badges/
│   │   └── single.html        # Página de badges/formación
│   └── partials/
│       ├── header.html        # Nav + drawer móvil + bottom nav
│       ├── footer.html        # Footer con créditos
│       ├── scripts.html       # JS compilado
│       └── head/
│           ├── meta.html      # SEO, favicons
│           ├── fonts.html     # Google Fonts
│           ├── styles.html    # SCSS compilado con fingerprint
│           └── analytics.html # GA4 (solo en producción)
└── theme.toml
```

---

## Diseño y tokens

Los tokens de diseño están en `assets/scss/_tokens.scss` como custom properties CSS. Están disponibles en ambos modos (claro y oscuro) y siguen la nomenclatura Material Design 3:

```scss
var(--color-primary)                // #0058bd
var(--color-surface-container-low)  // fondo de secciones
var(--color-on-surface)             // texto principal
var(--font-display)                 // Plus Jakarta Sans
var(--font-body)                    // Inter
var(--space-6)                      // 1.5rem
var(--radius-xl)                    // 1.5rem
```

El modo oscuro se activa automáticamente por preferencia del sistema (`prefers-color-scheme`) o manualmente mediante `data-theme="dark"/"light"` en `<html>`. El toggle en el header llama a `window.__toggleTheme()`.

---

## Páginas interiores — sistema de bloques

Las páginas interiores (Quién, Qué, Dónde) usan el layout `page` y su contenido se define **íntegramente en `config.toml`**, sin tocar código HTML.

### Crear una página nueva

**1. Crear el fichero de contenido** en `content/`:

```markdown
---
title: "Mi Página"
description: "Descripción para SEO"
url: "/mi-pagina/"
layout: "page"
---
```

**2. Añadir su sección en `config.toml`** bajo `[params.pages.<slug>]`, donde `<slug>` es el nombre del fichero sin extensión:

```toml
[params.pages.mi-pagina]
  cover    = "/images/covers/mi-pagina.jpg"  # imagen de cabecera (opcional)
  icon     = "🚀"                             # emoji Notion-style
  title    = "Mi Página"
  subtitle = "Una línea descriptiva"

  [[params.pages.mi-pagina.tags]]
    label = "Tag 1"
  [[params.pages.mi-pagina.tags]]
    label = "Tag 2"

  # Bloques de contenido (ver tipos más abajo)
  [[params.pages.mi-pagina.blocks]]
    type = "text"
    ...
```

---

### Tipos de bloque disponibles

#### `text` — Párrafo de texto

```toml
[[params.pages.quien.blocks]]
  type    = "text"
  heading = "Sobre mí"          # opcional
  body    = "Texto del párrafo"
```

#### `cards` — Tarjetas en grid (1–3 columnas según pantalla)

```toml
[[params.pages.quien.blocks]]
  type    = "cards"
  heading = "En qué destaco"    # opcional
  [[params.pages.quien.blocks.items]]
    icon  = "architecture"      # nombre de Material Symbol
    title = "Título"
    body  = "Descripción breve"
```

#### `timeline` — Línea de tiempo (experiencia, hitos...)

```toml
[[params.pages.quien.blocks]]
  type    = "timeline"
  heading = "Trayectoria"
  [[params.pages.quien.blocks.items]]
    role    = "Cargo o título"
    company = "Empresa u organización"
    period  = "2021 – presente"
```

#### `contact` — Links de contacto en formato píldora

```toml
[[params.pages.quien.blocks]]
  type    = "contact"
  heading = "Encuéntrame en"
  [[params.pages.quien.blocks.items]]
    label = "LinkedIn"
    url   = "https://linkedin.com/in/..."
    icon  = "fa fa-linkedin"
```

---

### Próximamente

- Activar/desactivar bloques con `enabled = false` sin eliminarlos del TOML
- Layouts predefinidos (perfil, landing, listado) seleccionables desde el frontmatter
- Nuevos tipos de bloque: `badges`, `gallery`, `stats`

---

## Navegación

El menú de cada página se controla desde `config.toml` (para el nav desktop) y desde `layouts/partials/header.html` (para el drawer móvil y el bottom nav). Los links del nav apuntan a las rutas definidas en los ficheros `.md`.

---

## Iconos

El tema usa dos sistemas de iconos:

| Sistema | Uso | Sintaxis |
|---------|-----|----------|
| **Material Symbols Outlined** | UI (nav, bloques) | `<span class="material-symbols-outlined">home</span>` |
| **Font Awesome 4** | Social links, contacto | `<i class="fa fa-github"></i>` |

> Font Awesome 4 se hereda del tema anterior. En una próxima iteración se migrará a Material Symbols o SVG.

---

## Añadir un nuevo tipo de bloque

1. Añadir el bloque `{{ else if eq .type "nuevo" }}` en `themes/colomr-v1/layouts/_default/page.html`
2. Añadir los estilos correspondientes en `themes/colomr-v1/assets/scss/_page.scss`
3. Documentar el schema TOML en este README

---

*Tema diseñado con [Stitch](https://stitch.withgoogle.com) e implementado con Claude.*
