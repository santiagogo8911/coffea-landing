# Coffea – Landing page (HTML + CSS)

TP4 · Diseño UX-UI 2026 · Licenciatura en Sistemas de Información (FCyT). Landing estática de una página, solo HTML5 + CSS3 (sin JavaScript, frameworks ni preprocesadores), según el PRD.

## Estructura

```
coffea-landing/
├── index.html
├── 404.html
├── netlify.toml
├── css/
│   ├── main.css          # @import de las capas en orden
│   ├── tokens.css        # @layer + custom properties (único lugar con colores/fuentes/radios)
│   ├── base.css          # reset, tipografía base, :focus-visible, skip-link
│   ├── layout.css        # .container, franjas
│   ├── utilities.css     # .visually-hidden / .sr-only
│   └── components/       # header, hero, categories, product-card, carousel,
│                         # promo, testimonial-card, newsletter, footer, notfound
└── assets/
    ├── img/              # imágenes (placeholders SVG, ver "Pendientes")
    └── icons/            # íconos SVG
```

## Convenciones

- BEM (`.product-card__title`, `.testimonial-card--featured`).
- Sin valores sueltos: color, fuente, radio y espaciado salen de `tokens.css`.
- Mobile-first: base 360 px, `min-width` en 768 / 1024 / 1440 px.
- `@layer tokens, base, layout, components, utilities`.
- Interacciones solo con CSS: carrusel con `scroll-snap`, flechas como anclas, menú `<details>`, favorito con `checkbox`, validación nativa del email.

## Levantar en local

Servir la carpeta por HTTP (los íconos usan `mask-image`, que Chrome bloquea desde `file://`):

```bash
python3 -m http.server 8000
```

## Despliegue en Netlify

1. Subir el repo a GitHub/GitLab.
2. En Netlify: *Add new site → Import from Git*, rama `main`.
3. Build command: vacío. Publish directory: `.` (ya declarado en `netlify.toml`).
4. Cada Pull Request genera un Deploy Preview.
5. Medir Lighthouse sobre la URL de producción.

Como `/css/*` y `/assets/*` son `immutable`, si cambiás un archivo renombralo con versión (p. ej. `main.v2.css`).

## Pendientes / decisiones abiertas

- **Imágenes:** son placeholders SVG. Exportar desde Figma los 15 rasters (hero, 4 café, 4 postre, mano, granos, newsletter, 3 avatares) a 2x, comprimir a AVIF/WebP + JPG y usar `<picture>`, `srcset`/`sizes`. Confirmar licencia (hay una foto de iStock).
- **Copy:** corregidos los typos del Figma; textos de cards y testimonios siguen siendo placeholders. Idioma `lang="en"`, confirmar.
- **Moneda:** "Rs." como en el diseño; confirmar.
- **Dessert:** usa las mismas fotos placeholder; pedir fotos de postres.
- **Tablet/mobile:** propuesta de la sección 7 del PRD, validar con diseño.
- **Flechas del carrusel:** se muestran desde 1440 px como anclas a la primera/última card.
- **Fuentes:** Google Fonts con `display=swap`; evaluar autohospedar en woff2.
