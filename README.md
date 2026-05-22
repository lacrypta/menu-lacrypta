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
