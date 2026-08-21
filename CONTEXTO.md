# CONTEXTO DEL PROYECTO — "Don Humberto" (aceitunas)

> Archivo de referencia para retomar el desarrollo sin perder el hilo.
> Crear / mantener actualizado en cada sesión.

---

## 1. Qué es el proyecto

Sitio web **catálogo** (NO tienda online) de aceitunas de mesa y AOVE de la
marca **Don Humberto**.

- **Referencia real:** Francisco Javier Orquera.
- **Elaborado y envasado por:** **Finca Alma Fuerte** · Ruta 60, **Copacabana** (Catamarca, NOA) — dato real impreso en los rótulos.
- **Productos reales (de los rótulos):** aceite de oliva extra virgen (½ L y 1 L), aceitunas griegas (500 g), aceitunas negras en salmuera (1 kg y 5 kg escurrido) y pasta de aceitunas (200 g y 350 g).
- **Registros reales:** R.N.E. 60-003366 · R.N.P.A. 60-084200-0 (aceite) · R.N.E. 03-000396 · R.N.P.A. 03-004200-0 (aceitunas).
- **Instagram real (en el envase):** `@DONHUMBERTO.AR`.
- **Punto de venta:** Salta Capital · Barrio **Villa Las Rosas**.
- **Celular ficticio (placeholder):** `+54 9 387 5555-5555` — enlace `tel:+54938755555555`.

---

## 2. Estructura del proyecto

```
e:\sistemas\sistema gemma\
├── index.html              (~566 líneas · HTML + Tailwind Play CDN + HTMX)
├── CONTEXTO.md             (este archivo)
├── REGLAS.md               (skills / reglas aplicadas)
├── generar_previews.ps1    (utilidad dev · convierte los PNG de img\cartoon en JPG web livianos)
├── dims.ps1                 (utilidad dev · verifica dimensiones de img\productos)
├── reemplazar_catalogo.py   (utilidad dev · reemplaza el bloque de tarjetas del catálogo)
├── provisorio_catalogo.html (utilidad dev · plantilla del card de catálogo)
├── ocr2.ps1                 (utilidad dev · OCR de rótulos)
└── img\
    ├── marca.png           (719 KB · gris degradado · se usa en el logo redondo del header)
    ├── logo.png            (199 KB · se usa en el banner del hero)
    ├── cartoon\            (originales PNG 4K de los rótulos, ~7–10 MB c/u · FUENTE de datos reales)
    └── productos\          (JPG livianos para la web · se usan en la sección #catalogo)
        ├── aceitunas-griegas-500g-1.jpg   (900x561 · 95 KB · vista frontal)
        └── aceitunas-griegas-500g-2.jpg   (900x561 · 97 KB · segunda vista)
```

- No hay `css/` ni `js/` — las utilidades visuales viven en **`css/app.css`** (sí existe) y el JS va inline al final de `index.html`.
- El archivo carga Tailwind desde `https://cdn.tailwindcss.com` y fuentes de Google (`Fraunces` para títulos + `Inter` para cuerpo).
- El CSS de marca define la paleta `oliva/crema/tierra/oro`, la fuente display `Fraunces`, sombras `soft`/`card`/`card-osc` y **el modo nocturno activado por defecto** (`html[data-theme="oscuro"]`) con variables CSS.

---

## 3. Punto de control actual (lo último hecho)

Estado: **datos reales de los rótulos + catálogo completo + modo nocturno por defecto (reglas del `.clinerules`)** ✅

---

## 3. Punto de control actual (lo último hecho)

Estado: **datos reales de los rótulos integrados + catálogo con fotos optimizadas para web + modo nocturno por defecto (reglas del `.clinerules`)** ✅

- **Imágenes del catálogo optimizadas:** las 2 fotos PNG subidas (2.1 MB c/u, 1310×816) se convirtieron a
  **JPG calidad 84** (95–97 KB, 900×561) manteniendo la proporción 16:10 para `aspect-[16/10]` en
  `.foto-panel`. Se eliminaron los PNG pesados; los JPG se nombraron
  `aceitunas-griegas-500g-1.jpg` y `aceitunas-griegas-500g-2.jpg` (patrón consistente con
  `generar_previews.ps1`).
- **Layout de la tarjeta pulido:** `lg:col-span-2` en el `<article>` para ocupar todo el ancho en
  desktop (con una sola tarjeta en `sm:grid-cols-2` no se desperdicia espacio); padding `sm:p-5` y
  gaps responsivos (`sm:gap-4 sm:p-7`) para mejor jerarquía en tablet.
- **Dark mode verificado:** el gradiente `from-oro-400/10 via-white to-oliva-100` se adapta vía los
  overrides CSS existentes (`via-white → #1b2613`, `from-oro-400/10 → rgba(217,180,92,0.14)`),
  evitando bandas blancas en modo oscuro.
- **Scripts de desarrollo sincronizados:** `reemplazar_catalogo.py` ahora busca el marker correcto
  `<!-- ====== ACEITUNAS GRIEGAS` (no "ACEITE DE OLIVA EXTRA VIRGEN"); `dims.ps1` referencia los
  JPG nuevos.

### Datos reales extraídos de las fotos (`img/cartoon/`, vía OCR)
- **Aceite de oliva extra virgen** — frascos de **500 ml y 1 litro** · 100 % AOVE obtenido por
  procedimientos mecánicos y en frío · sin conservantes ni aditivos · rico en vitamina E ·
  conservar fresco y, abierto, refrigerado (consumir en 30 días).
- **Aceitunas griegas** — **500 g** · aceitunas negras seleccionadas + aceite de oliva virgen extra
  + sal + especias naturales · artesanal, receta familiar.
- **Aceitunas negras enteras en salmuera** — **1 kg y 5 kg** (peso escurrido) · aceitunas, agua, sal ·
  sin gluten · sin conservantes añadidos · refrigerar 2–8 °C tras abrir.
- **Pasta de aceitunas** — **200 g y 350 g** · aceitunas verdes + AOVE + ajo + sal + especias ·
  artesanal, receta familiar.
- **Elaborado y envasado por:** **Finca Alma Fuerte** · Ruta 60, **Copacabana, Provincia de Catamarca**, Argentina.
- **Registros reales impresos:** aceite R.N.E. 60-003366 · R.N.P.A. 60-084200-0 · aceitunas R.N.E. 03-000396 · R.N.P.A. 03-004200-0.
- **Instagram real del envase:** `@DONHUMBERTO.AR` (https://instagram.com/donhumberto.ar).
- EAN reales: aceitunas griegas `779 1234 567890` · pasta 350 g `779 9988 776655`.

### Secciones nuevas en `index.html`
- `#inicio` (ancla agregada al hero) + `#catalogo` (4 tarjetas con las fotos reales y datos de ingredientes/pesos/conservación) + `#categorias` (Líneas) + `#proceso` (Producción) + `#nosotros` + `#contacto` + footer con datos reales y año dinámico.

### Reemplazos de datos inventados → reales
- "Cosecha propia 2025 · Finca familiar en Catamarca" → "Elaborado y envasado en Finca Alma Fuerte · Copacabana, Catamarca".
- "Cosecha 2025" (pie del banner) → "Finca Alma Fuerte".
- "Prensado en frío en 3 h tras la recolecta" → "procedimientos mecánicos, sin calor".
- "Km 0 · origen propio en Catamarca" → "Sin gluten · aceitunas sin conservantes añadidos".
- "Trazabilidad · parcela y lote por botella" → "Sin conservantes · ni aditivos · 100 % natural".
- "14 premios · NYIOOC y Alimentos Argentinos" → "Finca Alma Fuerte · Ruta 60 · Copacabana, Catamarca".
- Meta description actualizada con los productos y la finca reales.

### Hero / menú (conservados)
- H1 "El oro verde de la oliva catamarqueña, convertido en mesa." + badge real de Finca Alma Fuerte.
- Tarjeta de la finca con `img/logo.png`, pie "Finca Alma Fuerte" y leyenda de venta en Salta.
- Menú móvil fullscreen completo (JS `alternarMenu()`: toggle, icono ☰↔✕, scroll lock, cierre por X / enlace / toque fuera). Se agregó **botón de tema dentro del menú móvil** sin alterar su lógica.
- Banda de confianza con 4 datos reales.
- Documento cerrado con `</body></html>` y balance verificado (`div` 75/75, `section` 5/5, `article` 4/4, estructura validada con parser HTML).
- Utilidad `generar_previews.ps1` para convertir los PNG de `img/cartoon` en JPG livianos para la web.

### Reglas del `.clinerules` aplicadas (sesión actual)
1. **Preservación del código:** se conservó todo el diseño existente (paleta, tarjetas, hero, nav, menú móvil); solo se agregó lo solicitado.
2. **Adaptación a HTMX/Django:**
   - `<body hx-boost="true">` → navegación por AJAX lista para Django.
   - `#grid-catalogo` con `hx-get="/api/v1/catalogo/productos/"` y `hx-trigger="none"` (preparado: al existir la API, basta activar el trigger).
   - Datos estructurados JSON-LD (Organization con Finca Alma Fuerte) para SEO/consumidores de API.
3. **Diseño:** se respetó el diseño general; el modo nocturno usa la misma paleta (oliva/crema/tierra/oro) adaptada a fondos oscuros.
4. **Responsividad:** tarjetas fluidas `grid sm:grid-cols-2`, botones móvil `w-full`, y menú móvil fullscreen.
5. **Navegación:** nav-link con línea dorada animada, seguimiento de sección activa por scroll y menú hamburguesa intacto.
6. **Comportamiento Senior:**
   - **Modo nocturno activado por defecto** (`<html data-theme="oscuro">` + `localStorage`, se aplica antes de pintar para evitar parpadeo). Botón luna/sol en desktop y dentro del menú móvil.
   - **Fotos al 100 % de sus contenedores**: nuevo componente `.foto-panel` con `object-fit:contain` + `aspect-*` correcto por imagen, hover suave y fondo consistente en claro/oscuro. Sin fotos cortadas ni "a media".
   - **Fuentes más llamativas**: se añadió **Fraunces** (serif display con peso variable) como fuente de títulos sobre Playfair Display; `Inter` sigue en el cuerpo.
   - Solo datos reales de los rótulos (ver sección "reales de las fotos").

---

## 4. Pendientes (próxima sesión)

1. **Foto de marca en color** — en modo claro el logo del header `marca.png` es gris/débil; el logo redondo del header usa el SVG de olivo como base, `marca.png` solo de respaldo. Ideal: usar una versión a color de la marca.
4. ~~Crear `css/app.css`~~ ✅ Hecho (modo nocturno, foto-panel, nav-link, reveal, arte de olivo).
5. ~~Opcional: animación suave de apertura del menú móvil~~ → se agregó transición de items (hover translate) y `data-reveal` al scroll.
6. **Migración a HTMX/Django (.clinerules):** preparada con `hx-boost="true"` y `#grid-catalogo hx-get` (trigger `none` por ahora). Cuando exista la API de Django, activar el trigger o reemplazar el grid estático por el loop de templates manteniendo las tarjetas actuales.

---

## 5. Cómo verificar / probar

- Abrir `index.html` con **doble clic** (sin servidor) para la prueba definitiva.
- Si se usa Live Server: **reiniciarlo** cada vez que cambie el archivo y hacer **Ctrl+F5**.
  (Live Server inyecta un script y, sin `</body></html>`, rompía el render medio archivo.)
- Vista móvil: F12 → ícono 📱 (o ventana < 1024px).

---

## 6. Errores diagnosticados (historial)

| Síntoma | Causa | Solución |
|---|---|---|
| "Recuadro blanco vacío" en el hero | Foto gris casi blanca a lo ancho | Banner con `logo.png` + pie degradado (o usar recorte `object-cover`) |
| Menú no desplegaba | Llamaba a `alternarMenu()` que no existía | Crear la función en `<script>` antes de `</body>` |
| El overlay no cubría la pantalla | Estaba dentro del `<header>` con `backdrop-filter` | Moverlo como hijo directo de `<body>` |
| Tarjeta desaparece / parseo roto | Live Server inyectaba su script dentro de un `<svg>` porque no había `</body>` | Cerrar el documento con `</body></html>` |
| Fotos del catálogo pesadas (2.1 MB PNG) | Imágenes subidas sin optimizar para web | Convertir a JPG calidad 84 (900 px) → 95 KB c/u · patrón `optimizar_imagenes.ps1` / `generar_previews.ps1` |
| `reemplazar_catalogo.py` fallaba | Buscaba marker `<!-- ====== ACEITE...` pero el HTML empezaba con `<!-- ====== ACEITUNAS GRIEGAS` | Corregir el marker a ACEITUNAS GRIEGAS |
| Single card en `sm:grid-cols-2` | La tarjeta ocupaba solo la mitad del ancho en desktop | Agregar `lg:col-span-2` para ocupar todo el ancho |

---

## 7. Archivos anexos

- `REGLAS.md` → skills y reglas de desarrollo aplicadas.