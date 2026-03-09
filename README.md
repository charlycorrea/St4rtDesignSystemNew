# ST4RT Design System v1 (No destructivo)

Este paquete agrega una base de Design System **opt-in** para Shopify sin modificar componentes existentes.

## Archivos

- `assets/st4rt-global.css`
- `assets/st4rt-typography.css`
- `assets/st4rt-buttons.css`
- `assets/st4rt-utils.css`

## Objetivo

- Tokens globales (color, spacing, motion, typography).
- Tipografía reutilizable por clases.
- Contrato unificado de botones.
- Utilidades de layout/alineación/a11y.
- **Sin overrides globales de tags** (`h1`, `p`, etc.).

---

## Integración en un theme Shopify

### Opción A (recomendada): snippet de head

1. Crear un snippet, por ejemplo: `snippets/st4rt-design-system-head.liquid`.
2. Incluir los assets en este orden:

```liquid
{{ 'st4rt-global.css' | asset_url | stylesheet_tag }}
{{ 'st4rt-typography.css' | asset_url | stylesheet_tag }}
{{ 'st4rt-buttons.css' | asset_url | stylesheet_tag }}
{{ 'st4rt-utils.css' | asset_url | stylesheet_tag }}
```

3. Renderizar snippet en `<head>` del layout principal:

```liquid
{% render 'st4rt-design-system-head' %}
```

> Ventaja: orden explícito y fácil rollback.

---

### Opción B (alternativa): importar desde `base.css`

Si prefieres una única entrada CSS:

```css
@import url('{{ "st4rt-global.css" | asset_url }}');
@import url('{{ "st4rt-typography.css" | asset_url }}');
@import url('{{ "st4rt-buttons.css" | asset_url }}');
@import url('{{ "st4rt-utils.css" | asset_url }}');
```

> Recomendación: mantener el orden de importación para que tokens/base estén disponibles antes de componentes/utilidades.

---

## Orden de carga recomendado

1. `st4rt-global.css`
2. `st4rt-typography.css`
3. `st4rt-buttons.css`
4. `st4rt-utils.css`

Este orden garantiza que:
- Los tokens estén disponibles primero.
- Tipografía y botones tomen esos tokens.
- Las utilidades se apliquen al final como capa de composición.

---

## Uso rápido

```html
<div class="st4rt-container">
  <p class="st4rt-type-kicker">Nuevo</p>
  <h2 class="st4rt-type-display-m">Podium Series</h2>
  <p class="st4rt-type-body-m">Texto descriptivo del componente.</p>

  <a class="st4rt-btn st4rt-btn--primary st4rt-btn--md" href="#">
    Comprar ahora
  </a>
</div>
```

## Nota

Este DS v1 está diseñado para convivir con los componentes actuales sin romperlos.
La migración puede hacerse progresivamente componente por componente aplicando clases/tokens de forma explícita.
