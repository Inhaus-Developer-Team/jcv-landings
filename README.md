# Landing Pages para GHL — Campaña Juan Carlos Vega 2027

Dos landing pages simples, independientes y autocontenidas, para captar datos desde **GoHighLevel (GHL)**. Viven en `landing-pages/` y **no tocan** la plataforma ni el plan de trabajo.

## Páginas

| Página | Archivo | Para qué |
|---|---|---|
| **Únete al equipo (voluntarios)** | [`voluntarios.html`](./voluntarios.html) | Capta datos de voluntarios: nombre completo, celular, email, barrio (+ área opcional). |
| **Necesito ayuda** | [`pedir-ayuda.html`](./pedir-ayuda.html) | Capta datos de personas que piden ayuda: nombre, celular, email, barrio, tipo de ayuda y breve detalle. |

## Publicación (GitHub Pages)

Se sirven desde este mismo repositorio mediante el workflow
[`.github/workflows/deploy-lp.yml`](.github/workflows/deploy-lp.yml), que publica la raíz del repo. URLs resultantes (tras el primer deploy):

```
https://<org>.github.io/<repo>/voluntarios.html
https://<org>.github.io/<repo>/pedir-ayuda.html
```

> Importante: en **Settings → Pages → Build and deployment**, la fuente debe ser **"GitHub Actions"** (no una rama). El workflow ya está preparado; solo hay que activarlo en los ajustes del repo si aún no está activo.

## Conectar con GHL

Cada página tiene un bloque de configuración arriba del `<script>` con la constante:

```js
var GHL_ENDPOINT = ""; // <-- PEGA AQUÍ TU URL DE GHL
```

Dos opciones:

- **Opción A (recomendada):** pega la URL de webhook/formulario nativo de GHL. El formulario hace `POST` en JSON con los campos del lead.
- **Opción B (API):** pega un endpoint de contactos/campaña de GHL.

Si `GHL_ENDPOINT` queda vacío, el formulario cae a `mailto:` para probar el flujo en local sin servidor. Al enviar, el nombre del campo `fuente` distingue cada landing (`landing-voluntarios` / `landing-pedir-ayuda`) para etiquetar el origen del lead en GHL.

### Payload que envía `voluntarios.html`
```json
{ "fullName": "…", "phone": "…", "email": "…", "barrio": "…", "tipo": "…", "fuente": "landing-voluntarios" }
```

### Payload que envía `pedir-ayuda.html`
```json
{ "fullName": "…", "phone": "…", "email": "…", "barrio": "…", "tipo_ayuda": "…", "detalle": "…", "fuente": "landing-pedir-ayuda" }
```

## Diseño

Siguen el **manual de marca VEGA** (morado `#682AA6` · Pantone 267 C, amarillo `#E2D02A` · Pantone 604 C, Bebas Neue / Jost), sin fotos de campaña. Móvil-first: la mayoría llenará el form desde el celular.
