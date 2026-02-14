# 🌐 colomr.dev

¡Hola! Este es el repositorio de mi landing page personal. Está construida con HUGO Framework y desplegada en Firebase. La uso como punto central para compartir mis redes sociales y mi trayectoria profesional. 👋

## 🛠️ Tecnologías

- [HUGO](https://gohugo.io/) - Framework para sitios web estáticos
- [Firebase](https://firebase.google.com/) - Plataforma de hosting
- [Google Cloud Platform](https://cloud.google.com/) - Para pruebas y experimentos

## 🚀 Despliegue en Firebase

Para desplegar el sitio en Firebase, sigue estos pasos:

1. Instala la CLI de Firebase:
```bash
npm install -g firebase-tools
```

2. Inicia sesión en Firebase:
```bash
firebase login
```

3. Inicializa Firebase en el directorio raíz de Hugo:
```bash
firebase init
```

4. Durante la inicialización:
   - ✅ Selecciona la funcionalidad **Hosting**
   - ✅ Elige tu proyecto de Firebase
   - ✅ Acepta el valor predeterminado para reglas de base de datos
   - ✅ Usa `public` como directorio de publicación
   - ❌ Responde "No" a la aplicación de una sola página

5. Despliega el sitio:
```bash
firebase deploy --only hosting
```

## 🎓 Sistema de Badges de Certificaciones

Este sitio incluye un sistema completo para mostrar certificaciones y skill badges de Google Cloud. Aquí está todo lo que necesitas saber para mantenerlo actualizado.

### 📁 Estructura de Archivos

```
colomr.pm/
├── data/
│   ├── badges.json          # Lista de todas las certificaciones
│   └── categorias.json      # Categorías de badges (colores, iconos)
├── layouts/
│   ├── badges/
│   │   └── single.html      # Template de la página /badges
│   └── partials/
│       ├── badges.html      # Vista completa con filtros (página /badges)
│       └── badges-preview.html  # Preview del home (últimos 6 badges)
├── assets/scss/
│   ├── _badges.scss         # Estilos modo claro
│   ├── _badges_dark.scss    # Estilos modo oscuro
│   └── custom.scss          # Imports y estilos globales
└── content/badges/
    └── _index.md            # Contenido de la página /badges
```

### ➕ Cómo Añadir un Nuevo Badge

#### 1. Agregar el badge en `data/badges.json`

Añade un nuevo objeto JSON al **inicio** del array (para que aparezca primero):

```json
{
  "titulo": "Nombre del Curso",
  "img": "https://cdn.qwiklabs.com/HASH_DE_LA_IMAGEN",
  "fecha": "2026-02-13",
  "desc": "Descripción detallada del curso y lo que aprendiste",
  "url": "https://www.skills.google/public_profiles/TU_PERFIL/badges/ID_BADGE",
  "categoria": "ai-infrastructure"
}
```

**Campos explicados:**
- `titulo`: Nombre exacto del curso/certificación
- `img`: URL de la imagen del badge (cópiala desde tu perfil público de Google Skills)
- `fecha`: Fecha de completado en formato `YYYY-MM-DD`
- `desc`: Descripción de 1-2 frases sobre qué aprendiste
- `url`: Link directo al badge en tu perfil público
- `categoria`: ID de categoría (debe existir en `categorias.json`)

#### 2. (Opcional) Agregar nueva categoría

Si el badge es de una categoría nueva, añádela en `data/categorias.json`:

```json
{
  "id": "nombre-categoria",
  "nombre": "Nombre Visible",
  "icono": "fa-icon-name",
  "color": "#HEX_COLOR"
}
```

**Categorías disponibles:**
- `ai-infrastructure` - AI Infrastructure (azul #4285F4)
- `ai-ml` - AI / Machine Learning (verde #34A853)
- `bases-datos` - Bases de Datos (rojo #EA4335)
- `data-engineering` - Data Engineering (amarillo #FBBC05)
- `presales` - Ventas Técnicas (morado #9C27B0)
- `cloud-fundamentals` - Cloud Fundamentals (cyan #00BCD4)

**Iconos disponibles:** Cualquier icono de [Font Awesome 6](https://fontawesome.com/icons) (usar clase `fa-nombre-icono`)

#### 3. Reconstruir el sitio

```bash
hugo --cleanDestinationDir
```

#### 4. Verificar localmente

```bash
hugo server -D --bind 0.0.0.0 --port 1313
```

Visita:
- Home: `http://localhost:1313/` (últimos 6 badges)
- Página completa: `http://localhost:1313/badges/` (todos los badges con filtros)

#### 5. Desplegar

```bash
firebase deploy --only hosting
```

### 🎨 Personalización de Estilos

Si necesitas ajustar los estilos visuales:

- **Modo claro**: `assets/scss/_badges.scss`
- **Modo oscuro**: `assets/scss/_badges_dark.scss`
- **Estilos globales**: `assets/scss/custom.scss`

### 📋 Checklist para Añadir un Badge

- [ ] Copiar URL de la imagen del badge desde Google Skills
- [ ] Copiar URL directa al badge en tu perfil público
- [ ] Agregar entrada al inicio de `data/badges.json`
- [ ] Verificar que la categoría existe en `data/categorias.json`
- [ ] Reconstruir con `hugo --cleanDestinationDir`
- [ ] Probar localmente con `hugo server`
- [ ] Verificar que aparece en el home (últimos 6)
- [ ] Verificar que aparece en /badges con la categoría correcta
- [ ] Desplegar con `firebase deploy --only hosting`

### 🔧 Solución de Problemas

**El badge no aparece:**
- Verifica que el JSON sea válido (sin comas finales)
- Comprueba que la categoría existe en `categorias.json`
- Asegúrate de reconstruir el sitio con `hugo --cleanDestinationDir`

**La imagen no carga:**
- Verifica que la URL de la imagen sea correcta
- Comprueba que la URL comience con `https://cdn.qwiklabs.com/`

**Error de categoría:**
- El `id` de categoría en `badges.json` debe coincidir exactamente con el `id` en `categorias.json`
- Los IDs usan minúsculas y guiones (ej: `ai-infrastructure`)

## 🔍 Más Información

Para conocer más sobre mi trayectoria profesional y contactar conmigo, ¡visita [colomr.pm](https://colomr.pm)! 🌟
