# Stock Pokémon TCG (últimas colecciones)

Web privada por enlace: lista las colecciones de los últimos 2 años; dentro de cada una ves los productos
y, por producto, las tiendas con precio y stock. Un robot la actualiza cada 30 minutos.

## Instalar (unos 10 minutos, sin programar)

1. Crea cuenta gratis en github.com.
2. **New repository** con un nombre difícil de adivinar (ej. `stock-k7x92`), en **Public**
   (las páginas gratis de GitHub exigen repositorio público).
3. **Add file → Upload files**: sube `index.html`, `stores.json`, `extras.json` y la carpeta `scripts`. Commit.
4. **Add file → Create new file**, nombre `.github/workflows/update.yml` (las barras crean las carpetas),
   pega el contenido de `update.yml` y Commit.
5. **Settings → Pages → Source: GitHub Actions**.
6. Pestaña **Actions → Actualizar stock → Run workflow**. Tarda 1-3 minutos.
7. Tu enlace: `https://TU-USUARIO.github.io/NOMBRE-DEL-REPO/`. Guárdalo en la pantalla de inicio y compártelo.

## Qué lee y qué no

- Tiendas Shopify y WooCommerce (la mayoría de las especializadas): descubre solo todos sus productos Pokémon.
- Carrefour, El Corte Inglés y Cardmarket: no tienen datos públicos legibles ni dejan entrar a robots.
  La web pone un enlace "Mirar a mano en" que abre su buscador con el producto ya escrito.
- Fnac y MediaMarkt: solo enlace de búsqueda (los formatos de sus URLs no están verificados; si alguno no abre bien, edita `stores.json`).
- Dynos y las tiendas añadidas en `auto` (Alfriki, Darizard9, Don Dino, El Rincón del Gachapon, ElBazarTCG, Grillecards, RyuCards, The Card Station, Toy Planet, Pokezilla, Collectorage, Solo Hits, Friki de Nacimiento, Geekkaos, Mana Vortex, Unsobremás): el robot prueba si es Shopify o WooCommerce. Si no lo es, sale en rojo en "Tiendas vigiladas" y la web enseña un enlace a su listado para mirarlo a mano.
- Amazon: solo cuenta como stock si la página tiene el botón "Añadir a la cesta" y NO pone "Solicitar invitación" ni "Pendiente de invitación".
  Amazon suele bloquear a los robots con captcha; si pasa, sale "fallo" en el pie y se usa el enlace de búsqueda a mano.
  Para vigilar un producto concreto, añade a `extras.json`:
  `{"producto": "Caja de Entrenador Élite", "coleccion": "30 aniversario", "idioma": "ES", "tienda": "Amazon", "tipo": "amazon", "url": "https://www.amazon.es/dp/XXXXXXXXXX"}`
- Un producto antiguo o una carta suelta se descartan solos. Lo dudoso va a "Otros productos (sin clasificar)".
- Si una tienda falla, se muestra su último dato bueno marcado como antiguo.

## Añadir tiendas

- Shopify: en `stores.json`, `{"name": "Mi tienda", "type": "shopify", "url": "https://mitienda.com"}`
  (prueba que `https://mitienda.com/products.json` abre en el navegador).
- WooCommerce: igual con `"type": "woo"` (prueba `https://mitienda.com/wp-json/wc/store/v1/products`).
- Otras: una línea en `extras.json` con el enlace directo del producto.
- Solo enlace de búsqueda: `"type": "search"` y `"url"` con `{q}` donde va la palabra buscada.

## Añadir colecciones nuevas

Al salir una expansión, añade una línea a la lista `COLLECTIONS` de `scripts/classify.mjs`
(copia una existente y cambia nombre y palabras clave). Hasta entonces sus productos salen en "Otros".

## Privacidad

La web lleva `noindex` y solo entra quien tenga el enlace, pero no es una contraseña y el repositorio es público.
No guardes nada personal. Para contraseña real: Cloudflare Pages + Access (gratis hasta 50 personas).

## Si algo falla

GitHub pausa el robot tras 60 días sin actividad en el repositorio: reactívalo con **Run workflow**.
Si la web avisa de datos antiguos, mira la pestaña **Actions**.


## Novedades
- Colección nueva: Megaevolución: Dominio Delta (Delta Reign), 6 nov 2026.
- Productos clasificados por tipo (ETB, bundle, display, minilata, blíster, mazo, carpeta, figura…) con secciones dentro de cada colección y nombres canónicos.
- Variantes por Pokémon (p. ej. ex Box Sylveon vs Greninja) como productos separados.
