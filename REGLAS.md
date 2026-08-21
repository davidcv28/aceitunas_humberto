# REGLAS DE DESARROLLO — "Don Humberto"

> Skills y reglas que se siguieron (y se deben seguir) al tocar este proyecto.

---

## 1. Tecnología

- **HTML semántico** + **Tailwind CSS Play CDN** (`cdn.tailwindcss.com`).
- **Paleta de marca** registrada en `tailwind.config`:
  `oliva-*` (verdes), `crema-*`, `tierra-*`, `oro-*`.
- **Tipografías:** `Playfair Display` (títulos, clase `font-display`) e `Inter` (`font-sans`).
- **HTMX** cargado pero sin uso funcional todavía.
- No usar frameworks de build; mantener archivo único + carpeta `img/`.

## 2. Negocio: es un CATÁLOGO, no una tienda

- ❌ NO agregar: carrito, "comprar ahora", envíos, códigos de descuento, precios promocionales.
- ✅ Sí: descripciones, origen, cosecha, contacto, teléfono, punto de venta.
- Toda la **información de marca es real**:
  - Referencia: **Francisco Javier Orquera**.
  - Elaborado y envasado por: **Finca Alma Fuerte** (Ruta 60 · Copacabana, Catamarca) — dato impreso en los rótulos.
  - Productos reales: AOVE (½ L y 1 L), aceitunas griegas (500 g), aceitunas negras en salmuera (1 y 5 kg) y pasta de aceitunas (200 y 350 g).
  - Registros: R.N.E. 60-003366 · R.N.P.A. 60-084200-0 (aceite) · R.N.E. 03-000396 · R.N.P.A. 03-004200-0 (aceitunas).
  - Instagram: **@DONHUMBERTO.AR**.
  - Venta: **Salta Capital · Villa Las Rosas**.
  - Celular ficticio (placeholder): **+54 9 387 5555-5555** (`tel:+54938755555555`).
- NO inventar premios/años/valoraciones sin confirmar con el cliente.
- La fuente de datos reales son los **rótulos** en `img/cartoon/` (extractos con OCR de Windows).

## 3. Imágenes

- Header: `img/marca.png` (logo redondo; el SVG de oliva es el respaldo visual).
- Hero banner: `img/logo.png`.
- Catálogo: `img/productos/*.jpg` (previews web livianos generados desde `img/cartoon/*.png` con `generar_previews.ps1`).
- Originales 4K (`img/cartoon/`) pesan 7–10 MB → NO usarlos directo en la web.
- SIEMPRE con `alt` descriptivo y `onerror` que quite la imagen (evita iconos rotos).
- **Fotos al 100 % de su contenedor**: usar el componente `.foto-panel` (CSS en `css/app.css`)
  con `object-fit: contain` + `aspect-*` acorde a cada imagen. Nunca dejar fotos "a media"
  (recortadas o con padding blanco roto).
- En modo nocturno los fondos de foto usan `--img-panel` (oliva oscuro), respetando la paleta.

## 3b. Modo nocturno (regla Senior del `.clinerules`)

- Activado por defecto: `<html data-theme="oscuro">` + `localStorage` `tema-donhumberto` (script en `<head>` antes de pintar, sin parpadeo).
- Botón luna/sol: `#boton-tema` (desktop) y `#boton-tema-movil` (dentro del menú móvil) con `alternarTema()`.
- Las variables CSS del tema viven en `css/app.css`; el `body.bg-crema-100` se fuerza oscuro con `html[data-theme="oscuro"] body.bg-crema-100`.
- El menú hamburguesa móvil usa fondo `bg-oliva-950/80` (compatible con ambos temas).

## 4. Móvil primero (mobile-first)

- Breakpoints: `sm` (640) · `md` (768) · `lg` (1024).
- Botones del hero: `flex-col items-stretch w-full` en móvil → `sm:flex-row sm:w-auto`.
- Área táctil mínima ≈ **44–50 px** (botón hamburguesa: `p-3`).
- **Menú móvil = overlay fullscreen**:
  `fixed inset-0 z-[60] flex flex-col bg-oliva-950/80 backdrop-blur-md`.
  - Debe ser **hijo directo de `<body>`** (nunca dentro del `<header>` que tiene `backdrop-filter`).
  - Opciones con `flex-1` para repartir el alto de la pantalla.
  - Iconos al extremo derecho con `justify-between`.

## 5. Accesibilidad

- `aria-label`, `aria-expanded`, `aria-modal="true"`, `role="dialog"` en el menú móvil.
- `aria-hidden="true"` en SVGs decorativos.
- Alt-text en todas las imágenes.

## 6. Robustez del documento

- ✅ SIEMPRE cerrar el HTML con `</body></html>` →
  evita que Live Server inyecte su script dentro de un `<svg>` y rompa el render.
- Verificar restos con búsquedas (grep) antes de terminar una tarea.
- Al editar bloques (tarjetas, menús): mantener indentación y etiquetas balanceadas.

## 7. Estilo de código

- Textos en **español** (rioplatense neutro).
- Clases Tailwind completas por elemento (una utilidad por responsividad: nombre base + `sm:`/`lg:`).
- SVGs inline con `viewBox="0 0 24 24"`, `stroke="currentColor"` y paths **siempre dentro del viewBox** (nunca coordenadas fuera de 0–24).
- Flechas válidas:
  - Derecha: `M4 12 h15 m-5 -5 l5 5 -5 5`
  - Abajo: `M12 4 v13 m-5 -5 l5 5 5 -5`

## 8. Workflow / validación

1. Leer el archivo completo o la sección a editar antes de tocar.
2. Hacer ediciones pequeñas y verificables.
3. Al terminar: buscar restos (`Select-String`) de viejos textos/clases.
4. Avisar al usuario si debe **reiniciar Live Server** o hacer **Ctrl+F5**.
5. Mantener `CONTEXTO.md` actualizado al cierre de cada tarea.