# CLAUDE.md — Instrucciones para Claude Code

## Proyecto
Plataforma educativa **GRAMA** — vista de detalle de un **taller individual**.
Siempre aplica el design system definido en `design-system.md` antes de escribir cualquier código de UI.

## Reglas globales

- Fuente principal: **Plus Jakarta Sans** (importar desde Google Fonts)
- Fuente mono: **DM Mono** (solo para código, tokens, valores hex)
- Nunca usar: Inter, Roboto, Arial, system-ui como fuente principal
- Idioma de la UI: **español**
- Framework: HTML/CSS/JS puro salvo que se indique React
- No usar Tailwind — usar CSS custom properties del design system
- Siempre usar las variables CSS definidas en `design-system.md`, nunca valores hardcoded

## Arquitectura de temas — CRÍTICO

GRAMA usa un sistema **dual de temas en la misma vista**:

| Zona | Tema | Fondo |
|------|------|-------|
| Sidebar de navegación | OSCURO | `#0C1D15` |
| Hero banner del taller | OSCURO | `linear-gradient(135deg, #0C1D15, #1A3825)` |
| Área de contenido (materiales, videos) | CLARO | `#F5F5F0` |
| Cards de materiales | CLARO | `#FFFFFF` |
| Formularios y perfiles | CLARO | `#F5F5F0` → `#FFFFFF` |
| Chat widget | CLARO | `#FFFFFF` |

**Nunca** poner formularios o cards de contenido sobre fondo oscuro.
**Nunca** poner el sidebar sobre fondo claro.

## Vista del taller — estructura esperada

La vista de un taller tiene exactamente estas secciones en orden:

1. Breadcrumb `‹ Volver a todos los talleres`
2. Hero banner oscuro con: badge "TALLER N DE 9", título, descripción, stats (duración / módulos / materiales)
3. Sección "MATERIALES DEL TALLER" — grid de material cards (claro)
4. Sección "VIDEOS" — grid de video cards (claro)
5. Módulos del programa (opcional)

## Referencia completa
Ver `design-system.md` para todos los tokens, componentes y patrones CSS.
