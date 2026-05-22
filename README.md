# menu.lacrypta.ar

Sitio estático con el menú del evento de **La Crypta**: Barra, Comida y Merch.
Look & feel de LaPOS (fondo oscuro, fuentes IAAB3 + SF). En pantalla es
responsive; al imprimir, cada menú ocupa exactamente una hoja **A4**.

## Estructura

```
data/        barra.json · comida.json · merch.json · categories.json
fonts/       IAAB3.woff2 · SF-Regular.woff2 · SF-Bold.woff2  (embebidas en base64)
assets/      logo.png
scripts/     generate-menu.mjs   (genera public/index.html desde data/)
public/      index.html (generado) · icon.png
```

## Datos del menú

El menú se genera **a partir de estos archivos JSON**, que lee
`scripts/generate-menu.mjs`:

| Archivo | Contenido |
|---|---|
| `data/barra.json` | Items del menú **Barra** (con/sin alcohol) |
| `data/comida.json` | Items del menú **Comida** |
| `data/merch.json` | Items del menú **Merch** |
| `data/categories.json` | Nombres de las categorías (referenciadas por `category_id`) |

Cada item tiene esta forma:

```json
{
  "id": 6,
  "category_id": 9,
  "name": "Fuck KYC (Cuba Libre)",
  "description": "",
  "price": { "value": 7300, "currency": "ARS" }
}
```

`currency` admite `ARS`, `USD` o `SAT`. El texto entre paréntesis del `name` se
muestra como subtítulo (ej.: **Fuck KYC** / _Cuba Libre_).

### Origen (fuente de verdad)

Los archivos de `data/` son una **copia** del menú de la app LaPOS, repo
[`lawalletio/mobile-pos`](https://github.com/lawalletio/mobile-pos):

| Acá (`menu-lacrypta`) | Origen (`mobile-pos`) |
|---|---|
| `data/barra.json` | `src/constants/menus/barra.json` |
| `data/comida.json` | `src/constants/menus/comida.json` |
| `data/merch.json` | `src/constants/menus/merch.json` |
| `data/categories.json` | `src/constants/categories.json` |

Si el menú cambia en `mobile-pos`, volvé a copiar esos archivos a `data/` y
regenerá con `npm run build`.

## Actualizar el menú

1. Editá los precios/items en `data/*.json`.
2. Regenerá la página:

   ```bash
   npm run build      # = node scripts/generate-menu.mjs
   ```

3. Commit + push. Vercel redeploya solo.

## Desarrollo local

```bash
npm run dev          # genera y sirve en http://localhost:3000
```

## Imprimir (A4)

Abrí el sitio → **Cmd/Ctrl + P** → Tamaño **A4**, Márgenes **Ninguno**,
y activá **Gráficos de fondo** para que se imprima el fondo oscuro.

## Deploy

Hosteado en Vercel. El build corre `node scripts/generate-menu.mjs` y publica
`public/`. Dominio: **menu.lacrypta.ar**.
