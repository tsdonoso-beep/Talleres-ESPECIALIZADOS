# GRAMA Design System — Referencia técnica para Claude

> Este archivo es la fuente de verdad del design system para la vista de taller.
> Claude Code debe leerlo completo antes de generar cualquier componente de UI.

---

## 1. Tokens CSS — pegar en `:root` de cada archivo

```css
:root {
  /* ── BRAND ── */
  --g:          #00C16A;   /* verde primario: CTAs, nav activo, progreso, badges */
  --g-dark:     #00A359;   /* hover del verde */
  --g-deep:     #007A42;   /* gradientes oscuros, inicio de degradado */
  --g-light:    #E8F7F0;   /* fondos muy claros con tinte verde */
  --g-pale:     #F0FBF5;   /* fondo de botón ghost */

  /* ── TEMA OSCURO — sidebar y hero banners ── */
  --dk-base:    #0C1D15;   /* fondo del sidebar y hero */
  --dk-surface: #112219;   /* superficie secundaria oscura */
  --dk-card:    #162D1E;   /* cards en contexto oscuro */
  --dk-border:  #1F3828;   /* bordes en contexto oscuro */
  --dk-text:    #D8EFE2;   /* texto principal en oscuro */
  --dk-muted:   #6B9A7A;   /* texto secundario en oscuro */

  /* ── TEMA CLARO — contenido, cards, formularios ── */
  --lt-bg:      #F5F5F0;   /* fondo de la zona de contenido */
  --lt-surface: #FFFFFF;   /* cards, inputs, modales */
  --lt-border:  #E4E8E3;   /* bordes por defecto */
  --lt-border2: #D0D8CC;   /* bordes de inputs y elementos interactivos */
  --lt-text:    #1A2B20;   /* texto principal en claro */
  --lt-muted:   #6B7E6F;   /* texto secundario, placeholders */
  --lt-subtle:  #F0F4F1;   /* fondo de hover, separadores */

  /* ── TAGS DE TIPO DE CONTENIDO ── */
  --tag-pdf-bg:   #FEF3F2;
  --tag-pdf-text: #DC2626;
  --tag-vid-bg:   #FFF7ED;
  --tag-vid-text: #D97706;
  --tag-3d-bg:    #F5F3FF;
  --tag-3d-text:  #7C3AED;

  /* ── TIPOGRAFÍA ── */
  --font-ui:   'Plus Jakarta Sans', sans-serif;
  --font-mono: 'DM Mono', monospace;

  /* ── ESCALA TIPOGRÁFICA ── */
  --tx-xs:   0.72rem;    /* captions, badge labels, section headers */
  --tx-sm:   0.85rem;    /* labels, nav items, tags, botones */
  --tx-base: 1rem;       /* cuerpo por defecto */
  --tx-lg:   1.125rem;   /* cuerpo grande, descripciones */
  --tx-xl:   1.3rem;     /* subtítulos */
  --tx-2xl:  1.6rem;     /* títulos de card, encabezados de panel */
  --tx-3xl:  2.1rem;     /* títulos de sección */
  --tx-hero: 3.8rem;     /* hero de bienvenida */

  /* ── ESPACIADO (base 4px) ── */
  --s1:  4px;
  --s2:  8px;
  --s3:  12px;
  --s4:  16px;
  --s5:  20px;
  --s6:  24px;
  --s8:  32px;
  --s10: 40px;
  --s12: 48px;
  --s16: 64px;

  /* ── RADIOS ── */
  --r-xs:   4px;      /* badges, chips pequeños */
  --r-sm:   8px;      /* inputs, nav items, botones pequeños */
  --r-md:   12px;     /* botones estándar, material cards */
  --r-lg:   16px;     /* workshop cards, paneles */
  --r-xl:   24px;     /* hero banners, login */
  --r-full: 9999px;   /* pills, barras de progreso, dots */

  /* ── SOMBRAS (solo en contexto claro) ── */
  --sh-xs:       0 1px 3px rgba(0,0,0,.06), 0 1px 2px rgba(0,0,0,.04);
  --sh-sm:       0 2px 8px rgba(0,0,0,.08), 0 1px 3px rgba(0,0,0,.05);
  --sh-md:       0 4px 16px rgba(0,0,0,.10), 0 2px 6px rgba(0,0,0,.06);
  --sh-lg:       0 8px 32px rgba(0,0,0,.12), 0 4px 12px rgba(0,0,0,.07);
  --sh-glow:     0 0 0 3px rgba(0,193,106,.20);   /* focus ring de inputs */
  --sh-glow-btn: 0 4px 20px rgba(0,193,106,.35);  /* hover de botón primario */

  /* ── TRANSICIONES ── */
  --tf: 140ms ease;   /* micro-interacciones: hover, focus */
  --tn: 220ms ease;   /* transiciones normales: cards, modales */
}
```

---

## 2. Importar tipografía

```html
<link
  href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&family=DM+Mono:wght@400;500&display=swap"
  rel="stylesheet"
>
```

Reglas de uso:
- `font-family: var(--font-ui)` → TODO el texto de la interfaz
- `font-family: var(--font-mono)` → SOLO código, tokens, valores hex, metadatos técnicos
- Pesos: 800 para hero/display, 700 para h2–h3 y botones, 600 para labels, 400–500 para cuerpo

---

## 3. Layout general de la vista de taller

```
┌─────────────────────────────────────────────────────┐
│  SIDEBAR (250px fijo, tema oscuro)                  │
│  ┌───────────────────────────────────────────────┐  │
│  │  Logo GRAMA                                   │  │
│  │  ── NAVEGACIÓN ──                             │  │
│  │  Inicio                                       │  │
│  │  ── TALLERES ──                               │  │
│  │  Ebanistería          T1                      │  │
│  │  ● Mecánica Automotriz T2  ← activo (verde)   │  │
│  │  Computación          T3                      │  │
│  │  ...                                          │  │
│  │                                               │  │
│  │  [✨ Asistente IA]   ← chip inferior          │  │
│  │  Mi perfil                                    │  │
│  │  Salir                                        │  │
│  └───────────────────────────────────────────────┘  │
│                                                     │
│  CONTENIDO PRINCIPAL (flex: 1, tema claro)          │
│  ┌───────────────────────────────────────────────┐  │
│  │  ‹ Volver a todos los talleres                │  │
│  │  ┌─────────────────────────────────────────┐  │  │
│  │  │  HERO BANNER OSCURO                     │  │  │
│  │  │  TALLER 2 DE 9                          │  │  │
│  │  │  Mecánica Automotriz                    │  │  │
│  │  │  Descripción...                         │  │  │
│  │  │  ⏱ 16h   📦 6 módulos   📂 5 archivos  │  │  │
│  │  └─────────────────────────────────────────┘  │  │
│  │                                               │  │
│  │  MATERIALES DEL TALLER                        │  │
│  │  ┌──────┐  ┌──────┐  ┌──────┐               │  │
│  │  │ PDF  │  │ PDF  │  │  3D  │               │  │
│  │  └──────┘  └──────┘  └──────┘               │  │
│  │                                               │  │
│  │  VIDEOS                                       │  │
│  │  ┌──────────────┐  ┌──────────────┐          │  │
│  │  │   Video 1    │  │   Video 2    │          │  │
│  │  └──────────────┘  └──────────────┘          │  │
│  └───────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────┘
```

---

## 4. Componente: Sidebar

```css
.sidebar {
  width: 200px;
  min-width: 200px;
  background: var(--dk-base);
  border-right: 1px solid var(--dk-border);
  padding: var(--s8) var(--s5);
  height: 100vh;
  position: sticky;
  top: 0;
  display: flex;
  flex-direction: column;
  gap: var(--s8);
  overflow-y: auto;
}

/* Logo */
.sidebar-logo {
  display: flex;
  align-items: center;
  gap: var(--s3);
  padding-bottom: var(--s6);
  border-bottom: 1px solid var(--dk-border);
}
.logo-icon {
  width: 36px; height: 36px;
  background: linear-gradient(135deg, #00A359, #00E07A);
  border-radius: 9px;
  display: flex; align-items: center; justify-content: center;
  font-size: 16px; font-weight: 800; color: #000;
  box-shadow: 0 2px 8px rgba(0,193,106,.35);
}
.logo-brand {
  font-size: 0.95rem; font-weight: 800;
  color: #fff; letter-spacing: .06em;
}
.logo-sub {
  font-size: 0.62rem; color: var(--dk-muted);
  text-transform: uppercase; letter-spacing: .12em;
}

/* Nav section label */
.nav-section-label {
  font-size: 0.62rem; font-weight: 700;
  color: var(--dk-muted);
  text-transform: uppercase; letter-spacing: .12em;
  padding: var(--s2) var(--s3) var(--s1);
}

/* Nav item — inactivo */
.nav-item {
  display: flex; align-items: center; justify-content: space-between;
  padding: 7px var(--s3);
  border-radius: var(--r-sm);
  color: var(--dk-muted);
  font-size: var(--tx-sm); font-weight: 500;
  cursor: pointer; border: none; background: none;
  width: 100%; text-align: left;
  transition: all var(--tf);
}
.nav-item:hover {
  background: var(--dk-border);
  color: var(--dk-text);
}
/* Nav item — ACTIVO (taller seleccionado) */
.nav-item.active {
  background: var(--g);
  color: #000;
  font-weight: 700;
}

/* Badge T1–T9 sobre ítem inactivo */
.nav-badge {
  display: inline-flex; align-items: center; justify-content: center;
  width: 18px; height: 18px; border-radius: var(--r-full);
  font-size: 9px; font-weight: 800;
  background: rgba(0,193,106,.18);
  color: var(--g);
}
/* Badge T1–T9 sobre ítem ACTIVO (fondo verde) */
.nav-item.active .nav-badge {
  background: rgba(0,0,0,.18);
  color: rgba(0,0,0,.75);
}

/* Chip Asistente IA en el pie del sidebar */
.ai-chip {
  display: flex; align-items: center; gap: var(--s3);
  background: rgba(0,193,106,.08);
  border: 1px solid rgba(0,193,106,.18);
  border-radius: var(--r-sm);
  padding: var(--s3) var(--s4);
  cursor: pointer;
  transition: all var(--tf);
}
.ai-chip:hover { background: rgba(0,193,106,.14); }
.ai-dot {
  width: 8px; height: 8px; background: var(--g);
  border-radius: 50%;
  animation: ai-pulse 2s infinite;
}
@keyframes ai-pulse { 0%,100%{opacity:1} 50%{opacity:.35} }
.ai-label { font-size: var(--tx-sm); font-weight: 700; color: var(--dk-text); }
.ai-sub   { font-size: var(--tx-xs); color: var(--dk-muted); }
```

---

## 5. Componente: Hero Banner del Taller

```css
.taller-hero {
  background: linear-gradient(135deg, #0C1D15 0%, #112219 50%, #1A3825 100%);
  border-radius: var(--r-xl);
  padding: var(--s8) var(--s10);
  margin-bottom: var(--s6);
  position: relative;
  overflow: hidden;
}
/* Glow decorativo */
.taller-hero::after {
  content: '';
  position: absolute; top: 0; right: 0; bottom: 0; width: 260px;
  background: radial-gradient(ellipse at right center, rgba(0,193,106,.08) 0%, transparent 65%);
  pointer-events: none;
}

.taller-badge {
  display: inline-block;
  font-size: var(--tx-xs); font-weight: 800;
  color: var(--g); text-transform: uppercase; letter-spacing: .1em;
  background: rgba(0,193,106,.10);
  border: 1px solid rgba(0,193,106,.18);
  padding: 3px 10px; border-radius: var(--r-full);
  margin-bottom: var(--s3);
}
.taller-title {
  font-size: var(--tx-3xl); font-weight: 800;
  color: #fff; letter-spacing: -.02em;
  margin-bottom: var(--s2);
}
.taller-desc {
  font-size: var(--tx-sm); color: var(--dk-muted);
  margin-bottom: var(--s6); max-width: 460px; line-height: 1.6;
}
.taller-stats {
  display: flex; gap: var(--s8); flex-wrap: wrap;
}
.taller-stat {
  display: flex; align-items: center; gap: var(--s2);
}
.taller-stat-icon { font-size: 15px; opacity: .65; }
.taller-stat-label { font-size: var(--tx-xs); color: var(--dk-muted); }
.taller-stat-value { font-size: var(--tx-sm); font-weight: 700; color: #fff; }
```

---

## 6. Componente: Section Header (área de contenido)

```css
.section-header {
  font-size: var(--tx-xs); font-weight: 800;
  color: var(--lt-muted);
  text-transform: uppercase; letter-spacing: .1em;
  margin-bottom: var(--s4);
  padding-bottom: var(--s2);
  border-bottom: 1px solid var(--lt-border);
}
```

---

## 7. Componente: Material Card (PDF / Video / 3D)

```css
.material-card {
  background: var(--lt-surface);
  border: 1px solid var(--lt-border);
  border-radius: var(--r-md);
  padding: var(--s5);
  box-shadow: var(--sh-xs);
  transition: all var(--tn);
  display: flex; flex-direction: column; gap: var(--s3);
}
.material-card:hover {
  box-shadow: var(--sh-md);
  border-color: var(--lt-border2);
  transform: translateY(-1px);
}

/* Tag de tipo — siempre va primero */
.type-tag {
  display: inline-flex; align-items: center; gap: 5px;
  font-size: var(--tx-xs); font-weight: 700;
  padding: 3px 9px; border-radius: var(--r-full);
  width: fit-content;
}
.type-tag.pdf { background: var(--tag-pdf-bg); color: var(--tag-pdf-text); }
.type-tag.vid { background: var(--tag-vid-bg); color: var(--tag-vid-text); }
.type-tag.td3 { background: var(--tag-3d-bg);  color: var(--tag-3d-text);  }

.material-title {
  font-size: var(--tx-base); font-weight: 700;
  color: var(--lt-text); line-height: 1.3;
}
.material-desc {
  font-size: var(--tx-sm); color: var(--lt-muted); line-height: 1.5;
  flex: 1;
}
.material-meta {
  font-size: var(--tx-xs); color: var(--lt-muted);
  display: flex; align-items: center; gap: var(--s1);
}
.material-footer {
  display: flex; align-items: center; justify-content: space-between;
  margin-top: auto;
}

/* Botón descarga (ícono) */
.btn-download {
  background: none; border: none; cursor: pointer;
  color: var(--lt-muted); font-size: 16px;
  padding: var(--s1); border-radius: var(--r-xs);
  transition: color var(--tf);
}
.btn-download:hover { color: var(--lt-text); }
```

---

## 8. Componente: Botón Primario

```css
.btn-primary {
  display: inline-flex; align-items: center; gap: 6px;
  background: var(--g); color: #000;
  font-family: var(--font-ui); font-weight: 700; font-size: var(--tx-sm);
  padding: 9px 18px; border-radius: var(--r-md);
  border: none; cursor: pointer;
  transition: all var(--tf);
  white-space: nowrap;
}
.btn-primary:hover {
  background: var(--g-dark);
  transform: translateY(-1px);
  box-shadow: var(--sh-glow-btn);
}
.btn-primary:active  { transform: translateY(0); }
.btn-primary:disabled { opacity: .42; cursor: not-allowed; transform: none; box-shadow: none; }

/* Variante pequeña */
.btn-primary.sm { padding: 6px 13px; font-size: var(--tx-xs); border-radius: var(--r-sm); }
```

---

## 9. Componente: Botón Ghost

```css
.btn-ghost {
  display: inline-flex; align-items: center; gap: 6px;
  background: var(--g-pale); color: var(--g-dark);
  border: 1.5px solid rgba(0,193,106,.22);
  font-family: var(--font-ui); font-weight: 700; font-size: var(--tx-sm);
  padding: 9px 18px; border-radius: var(--r-md);
  cursor: pointer; transition: all var(--tf);
}
.btn-ghost:hover { background: var(--g-light); }
.btn-ghost.sm { padding: 6px 13px; font-size: var(--tx-xs); border-radius: var(--r-sm); }
```

---

## 10. Componente: Breadcrumb

```css
.breadcrumb {
  display: flex; align-items: center; gap: var(--s2);
  font-size: var(--tx-sm); color: var(--lt-muted);
  margin-bottom: var(--s5); cursor: pointer;
  width: fit-content;
  transition: color var(--tf);
}
.breadcrumb:hover { color: var(--lt-text); }
.breadcrumb-link { color: var(--g); font-weight: 600; }
.breadcrumb-link:hover { color: var(--g-dark); }
```

---

## 11. Componente: Chat Widget

```css
/* Contenedor flotante */
.chat-widget {
  position: fixed; bottom: 24px; right: 24px;
  width: 300px;
  background: var(--lt-surface);
  border: 1px solid var(--lt-border);
  border-radius: var(--r-lg);
  box-shadow: var(--sh-lg);
  overflow: hidden;
  z-index: 100;
  display: flex; flex-direction: column;
}

/* Header */
.chat-header {
  display: flex; align-items: center; justify-content: space-between;
  padding: var(--s4) var(--s5);
  background: var(--lt-surface);
  border-bottom: 1px solid var(--lt-border);
}
.chat-avatar {
  width: 34px; height: 34px; background: var(--g);
  border-radius: var(--r-sm);
  display: flex; align-items: center; justify-content: center;
  font-size: 15px;
}
.chat-name   { font-size: var(--tx-sm); font-weight: 700; color: var(--lt-text); }
.chat-status { display: flex; align-items: center; gap: 5px; font-size: var(--tx-xs); color: var(--lt-muted); }
.chat-status-dot {
  width: 7px; height: 7px; background: var(--g);
  border-radius: 50%; animation: ai-pulse 2s infinite;
}
.chat-close {
  background: none; border: none; cursor: pointer;
  color: var(--lt-muted); font-size: 18px; line-height: 1;
  transition: color var(--tf);
}
.chat-close:hover { color: var(--lt-text); }

/* Cuerpo */
.chat-body {
  background: var(--lt-bg);
  padding: var(--s4) var(--s5);
  flex: 1; overflow-y: auto;
  display: flex; flex-direction: column; gap: var(--s3);
}

/* Burbuja del asistente */
.chat-bubble {
  background: var(--lt-surface);
  border: 1px solid var(--lt-border);
  border-radius: 0 var(--r-md) var(--r-md) var(--r-md);
  padding: var(--s3) var(--s4);
  font-size: var(--tx-sm); color: var(--lt-text); line-height: 1.55;
  box-shadow: var(--sh-xs); max-width: 92%;
}

/* Sugerencias predefinidas */
.chat-suggestions { display: flex; flex-direction: column; gap: 6px; }
.chat-suggestion {
  background: var(--lt-surface);
  border: 1px solid var(--lt-border);
  border-radius: var(--r-sm);
  padding: 6px 12px;
  font-size: var(--tx-xs); color: var(--lt-muted);
  cursor: pointer; transition: all var(--tf); text-align: left;
  font-family: var(--font-ui);
}
.chat-suggestion:hover { border-color: var(--g); color: var(--g-dark); }

/* Input row */
.chat-input-row {
  display: flex; gap: var(--s2); align-items: flex-end;
  padding: var(--s3) var(--s5);
  border-top: 1px solid var(--lt-border);
  background: var(--lt-surface);
}
.chat-input {
  flex: 1; border: none; outline: none;
  background: var(--lt-bg); border-radius: var(--r-sm);
  padding: 8px 12px; resize: none;
  font-family: var(--font-ui); font-size: var(--tx-sm);
  color: var(--lt-text); line-height: 1.4;
}
.chat-input::placeholder { color: var(--lt-muted); }
.chat-send {
  width: 34px; height: 34px; background: var(--g); color: #000;
  border: none; border-radius: var(--r-sm); cursor: pointer;
  display: flex; align-items: center; justify-content: center;
  font-size: 14px; flex-shrink: 0;
  transition: all var(--tf);
}
.chat-send:hover { background: var(--g-dark); }
```

---

## 12. Componente: Filtros de contenido

```css
.filter-tabs { display: flex; gap: var(--s2); flex-wrap: wrap; }

.filter-tab {
  padding: 6px 18px; border-radius: var(--r-full);
  font-family: var(--font-ui); font-size: var(--tx-sm); font-weight: 600;
  cursor: pointer; border: 1.5px solid transparent;
  transition: all var(--tf);
}
/* Activo — fondo oscuro (texto del taller) */
.filter-tab.active {
  background: var(--lt-text); color: var(--lt-surface);
  border-color: var(--lt-text);
}
/* Inactivo */
.filter-tab.inactive {
  background: transparent; color: var(--lt-muted);
  border-color: var(--lt-border2);
}
.filter-tab.inactive:hover {
  border-color: var(--g);
  color: var(--g-dark);
}
```

---

## 13. Componente: Barra de progreso

```css
/* Usada en cards del listado de talleres */
.progress-wrap { display: flex; flex-direction: column; gap: 3px; flex: 1; }
.progress-meta {
  display: flex; justify-content: space-between;
  font-size: var(--tx-xs); color: var(--lt-muted);
}
.progress-meta .pct-active { color: var(--g); font-weight: 700; }
.progress-bar {
  height: 5px; background: var(--lt-border);
  border-radius: var(--r-full); overflow: hidden;
}
.progress-fill {
  height: 100%; background: var(--g);
  border-radius: var(--r-full);
  transition: width var(--ts);
}
```

---

## 14. Estados de progreso (chips)

```css
.status-chip {
  display: inline-flex; align-items: center; gap: 6px;
  border-radius: var(--r-sm); padding: 4px 10px;
  font-size: var(--tx-xs); font-weight: 700;
  width: fit-content;
}
.status-dot { width: 6px; height: 6px; border-radius: 50%; background: currentColor; }

/* Variantes */
.status-chip.done    { background: var(--g-pale);  color: var(--g-dark); }
.status-chip.active  { background: #FFF7ED;        color: #B45309; }
.status-chip.pending { background: var(--lt-subtle); color: var(--lt-muted); }
```

---

## 15. Grids de contenido

```css
/* Grid de material cards — 3 columnas */
.materials-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: var(--s4);
  margin-bottom: var(--s8);
}

/* Grid de videos — 2 columnas */
.videos-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: var(--s4);
}

/* Responsive */
@media (max-width: 900px) {
  .materials-grid { grid-template-columns: repeat(2, 1fr); }
  .videos-grid    { grid-template-columns: 1fr; }
}
@media (max-width: 600px) {
  .materials-grid { grid-template-columns: 1fr; }
}
```

---

## 16. Página completa — estructura HTML base

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mecánica Automotriz — GRAMA</title>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
  <style>
    /* 1. Pegar aquí todos los tokens de la sección 1 */
    /* 2. Pegar aquí los estilos de los componentes usados */

    * { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; }
    body {
      font-family: var(--font-ui);
      font-size: var(--tx-base);
      line-height: 1.6;
      background: var(--lt-bg);
      color: var(--lt-text);
      display: flex;
      min-height: 100vh;
    }
  </style>
</head>
<body>

  <!-- SIDEBAR (tema oscuro) -->
  <aside class="sidebar">
    <!-- logo, nav items, ai-chip, mi perfil, salir -->
  </aside>

  <!-- CONTENIDO PRINCIPAL (tema claro) -->
  <main style="flex:1; padding: var(--s10) var(--s12); overflow-y: auto;">

    <!-- Breadcrumb -->
    <div class="breadcrumb">‹ <span class="breadcrumb-link">Volver a todos los talleres</span></div>

    <!-- Hero banner (tema oscuro dentro de tema claro) -->
    <div class="taller-hero">
      <div class="taller-badge">TALLER 2 DE 9</div>
      <h1 class="taller-title">Mecánica Automotriz</h1>
      <p class="taller-desc">Aprende los fundamentos de la mecánica automotriz, diagnóstico y mantenimiento de vehículos.</p>
      <div class="taller-stats">
        <div class="taller-stat">
          <span class="taller-stat-icon">⏱</span>
          <div>
            <div class="taller-stat-label">Duración</div>
            <div class="taller-stat-value">16 horas</div>
          </div>
        </div>
        <div class="taller-stat">
          <span class="taller-stat-icon">📦</span>
          <div>
            <div class="taller-stat-label">Módulos</div>
            <div class="taller-stat-value">6 módulos</div>
          </div>
        </div>
        <div class="taller-stat">
          <span class="taller-stat-icon">📂</span>
          <div>
            <div class="taller-stat-label">Materiales</div>
            <div class="taller-stat-value">5 archivos</div>
          </div>
        </div>
      </div>
    </div>

    <!-- Filtros -->
    <div class="filter-tabs" style="margin-bottom: var(--s6);">
      <button class="filter-tab active">Todos</button>
      <button class="filter-tab inactive">Videos</button>
      <button class="filter-tab inactive">PDFs</button>
      <button class="filter-tab inactive">Fichas</button>
      <button class="filter-tab inactive">3D</button>
    </div>

    <!-- Sección: Materiales -->
    <div class="section-header">Materiales del taller</div>
    <div class="materials-grid">
      <!-- .material-card × N -->
    </div>

    <!-- Sección: Videos -->
    <div class="section-header">Videos</div>
    <div class="videos-grid">
      <!-- .material-card.vid × N -->
    </div>

  </main>

  <!-- Chat widget flotante -->
  <div class="chat-widget">
    <!-- header, body, input-row -->
  </div>

</body>
</html>
```

---

## 17. Reglas DO / DON'T

| ✓ HACER | ✗ EVITAR |
|---------|----------|
| Sidebar y heroes siempre en tema oscuro | Formularios o cards en fondo oscuro |
| Verde `#00C16A` solo para: CTA primario, nav activo, progreso, badge activo | Verde en texto corrido o etiquetas decorativas |
| Tags coloreados por tipo: PDF rojo / Video amber / 3D violeta | Un solo color para todos los tipos de contenido |
| Inputs con `background: #FFFFFF` + `box-shadow` sutil | Inputs con fondo gris oscuro o sin sombra |
| `Plus Jakarta Sans` weight 800 para títulos de hero | Inter, Roboto, Arial o system-ui |
| `font-family: var(--font-mono)` solo para código/tokens | DM Mono en etiquetas o botones |
| Active nav = `background: var(--g); color: #000` sólido | Active nav = solo subrayado o borde lateral |
| Botón de acción principal siempre verde sólido | Botón de guardar en gris o neutro |
| Badge T1–T9 adapta colores según contexto (claro en oscuro / oscuro en verde) | Badge con color fijo independiente del fondo |
| Hero banner con `border-radius: var(--r-xl)` (24px) | Hero a full-bleed sin radio |

---

## 18. Checklist antes de entregar código

- [ ] ¿Los tokens CSS de la sección 1 están en `:root`?
- [ ] ¿La tipografía importa `Plus Jakarta Sans` desde Google Fonts?
- [ ] ¿El sidebar usa `var(--dk-base)` como fondo?
- [ ] ¿El área de contenido usa `var(--lt-bg)` como fondo?
- [ ] ¿El hero banner del taller usa gradiente oscuro + `border-radius: var(--r-xl)`?
- [ ] ¿Las material cards tienen `background: var(--lt-surface)` + `box-shadow: var(--sh-xs)`?
- [ ] ¿Los tags de tipo usan los colores correctos (PDF rojo / Video amber / 3D violeta)?
- [ ] ¿El botón primario es verde `var(--g)` con texto negro `#000`?
- [ ] ¿El chat widget está en tema claro?
- [ ] ¿Ningún valor de color está hardcodeado (todo usa variables CSS)?
