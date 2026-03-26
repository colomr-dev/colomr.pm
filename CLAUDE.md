# CLAUDE.md — Contexto del proyecto colomr.pm

## Qué es este proyecto
Sitio web personal generado con **Hugo** y desplegado en **Firebase Hosting**.
Muestra badges/certificaciones de Google Cloud Skills Boost, con descripción y categoría generadas por Gemini AI.

## Estructura clave
- `hugo.toml` — configuración Hugo (convención moderna, antes `config.toml`)
- `data/badges.json` — lista de badges (fuente de datos principal)
- `data/categorias.json` — categorías de badges con icono y color
- `scripts/sync_badges.py` — script de sincronización automática
- `scripts/requirements.txt` — dependencias Python
- `.github/workflows/sync-badges.yml` — workflow de GitHub Actions
- `layouts/` — plantillas Hugo personalizadas
- `assets/scss/` — estilos SCSS (requiere Hugo Extended)
- `themes/colomr-v1/` — tema propio (Material Design 3)

## Workflow de sincronización automática (Sync Badges)
El workflow se ejecuta cada 2 días (cron `0 8 */2 * *`) o manualmente:
1. Scrapa el perfil público de Google Skills: `https://www.skills.google/public_profiles/36fdb0e1-891c-4dc5-aef1-d89aecc3dd45`
2. Detecta badges nuevos por fecha comparando con `data/badges.json`
3. Genera descripción en español y categoría via Gemini API
4. Si hay cambios: build Hugo + deploy Firebase + commit al repo

### Gemini API — modelos y cuota
La API key se pasa como `GOOGLE_API_KEY` (secret `GEMINI_API_KEY` en GitHub Actions).
Usa fallback entre modelos por si la cuota está agotada:
```python
models_to_try = ["gemini-2.0-flash", "gemini-2.0-flash-lite", "gemini-2.5-flash-lite"]
```
- `gemini-2.0-flash` tiene cuota free tier a 0 en este proyecto (error 429)
- `gemini-1.5-flash` está deprecado en API v1beta (error 404)
- `gemini-2.0-flash-lite` es el que funciona actualmente como fallback

## Comandos útiles
```bash
hugo server          # desarrollo local
hugo --cleanDestinationDir  # build para producción
python scripts/sync_badges.py  # sync manual (requiere GOOGLE_API_KEY en entorno)
```

## Preferencias de workflow con Claude
- Puede hacer commit y push directamente, pero avisar antes con una frase breve explicando qué se va a subir
