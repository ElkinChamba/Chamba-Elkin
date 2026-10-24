# Informe de Auditoría – Laboratorio Cruzado 

- **Auditor:** Elkin Jair Chamba Maura (Ficha 28)
- **Estudiante auditado:** Jonnathan Javier Saavedra Villegas (Ficha 27)
- **Repositorio auditado:** `saavedra-jonnathan-artesanias`

---

## 1. Plan de verificación (Qué se espera encontrar vs. Verificación en navegador)

1. **Base 1 – Estructura semántica y encabezados:**
   - *Qué espero encontrar:* Elementos `<header>`, `<nav>`, `<main>`, mínimo dos `<section>` o `<article>` con encabezado propio, `<aside>` y `<footer>`, manteniendo jerarquía secuencial sin saltos.
   - *Verificación:* Cumple en la organización general de etiquetas semánticas y jerarquía de títulos.
2. **Base 2 – Formulario accesible y validación nativa:**
   - *Qué espero encontrar:* Mínimo 5 controles con `<label for="...">`, agrupados con `<fieldset>` y `<legend>`, tipos de `input` correctos y validación nativa combinada (`required`, `pattern`, `min`/`max`).
   - *Verificación:* Cumple parcialmente. Tiene 5 campos con `<label>`, `<fieldset>` y `<legend>`, pero solo utiliza el atributo `required`, omitiendo `pattern` (por ejemplo, en el campo de celular permite ingresar letras). Además, el selector del CSS excluye al `<textarea>`, dejándolo sin diseño.
3. **Base 3 – Tabla de datos accesible:**
   - *Qué espero encontrar:* Tabla con `<caption>`, `<thead>`, `<tbody>` y celdas de encabezado `<th scope="col">`.
   - *Verificación:* Cumple completamente en la sección `#descripcion-productos`.
4. **Base 4 – Layout responsive (Grid, Flexbox y 360 px sin scroll):**
   - *Qué espero encontrar:* CSS Grid en el layout general, Flexbox en componentes internos y adaptación a 360 px de ancho sin desbordamiento horizontal.
   - *Verificación:* No cumple en 360 px. La sección `.contacto` mantiene dos columnas (`grid-template-columns: minmax(0, 1fr) minmax(0, 1fr)`) en pantallas móviles y el botón de envío exige `min-width: 200px`, provocando desbordamiento horizontal en 360 px.
5. **Base 5 – Variables CSS y contraste mínimo 4.5:1:**
   - *Qué espero encontrar:* Paleta declarada en `:root` con variables `--color-...` y relación de contraste mayor o igual a 4.5:1 en texto normal.
   - *Verificación:* Cumple completamente. El texto principal sobre el fondo supera el contraste mínimo exigido.
6. **Base 6 – Navegación con teclado y foco visible:**
   - *Qué espero encontrar:* Todos los controles e hipervínculos accesibles con `Tab`, mostrando un indicador visual claro (`:focus` / `:focus-visible`).
   - *Verificación:* No cumple. Solo `#saltar-contenido:focus` tiene regla de `outline` en el CSS, y dicho enlace está ubicado después del `<nav>`, obligando a recorrer el menú antes de poder saltar al contenido.
7. **Base 7 – Sintaxis CSS:**
   - *Qué espero encontrar:* Reglas de estilo redactadas conforme a las especificaciones oficiales del W3C.
   - *Verificación:* Presenta un error de orden en la declaración de tipografías.
8. **Base 8 – Imágenes con `alt` adecuado:**
   - *Qué espero encontrar:* Todas las imágenes con atributo `alt` descriptivo acorde a su función.
   - *Verificación:* Cumple completamente en todas las etiquetas `<img>`.
9. **Ficha 27 – Tienda de artesanías, `datalist`, Breakpoint 900 px y `grid-template-areas` con cambio de orden en móvil:**
   - *Qué espero encontrar:* Temática de artesanías, `<input>` asociado a `<datalist>`, media query en `900px` y reordenamiento de las áreas del `grid-template-areas` al pasar a vista móvil.
   - *Verificación:* Cumple temática, `datalist` y breakpoint de `900px`, pero **incumple el cambio de orden en móvil**: el `grid-template-areas` mantiene exactamente la misma secuencia (`header`, `hero`, `busqueda`, `aside`, `main`, `footer`) tanto en escritorio como en móvil.

---

## 2. Tabla de Hallazgos

| N.º | Requisito | Ubicación (archivo y línea o selector) | Hallazgo | Norma que incumple | Evidencia | Severidad (alta, media, baja) |
|---|---|---|---|---|---|---|
| 1 | Ficha 27: `grid-template-areas` cambia de orden en móvil | `css/style.css`, líneas 26-32 y 347-354 (`body`) | En `@media (max-width: 900px)` las áreas pasan a una columna pero conservan exactamente el mismo orden secuencial del DOM (`header`, `hero`, `busqueda`, `aside`, `main`, `footer`) sin cambiar el orden en móvil. | W3C CSS Grid Layout Module Level 1 (Sección 7.3 `grid-template-areas`) y Requisito de Ficha 27 | `evidencias/hallazgo1-grid-orden.png` | Alta |
| 2 | Base 4: Layout sin scroll horizontal en 360 px | `css/style.css`, líneas 274-280 (`.contacto`) y línea 324 (`.formulario-contacto button`) | `.contacto` mantiene 2 columnas en móvil porque no se redefine en los media queries, y el botón tiene `min-width: 200px`, causando desbordamiento horizontal a 360 px de ancho. | WCAG 2.2 Criterio 1.4.10 Reflow (Nivel AA) | `evidencias/hallazgo2-overflow-360px.png` | Alta |
| 3 | Base 6: Navegación con teclado y foco visible | `index.html`, línea 26 (`#saltar-contenido`) y `css/style.css`, líneas 65-91, 312-337 | No se definieron estilos `:focus` visibles para enlaces de navegación, botones ni campos del formulario. Además, el enlace `#saltar-contenido` está dentro de `#hero` (después del `<nav>`), por lo que no es el primer elemento al tabular. | WCAG 2.2 Criterio 2.4.7 Foco visible (Nivel AA) y Criterio 2.4.1 Evitar bloques (Nivel A) | `evidencias/hallazgo4-foco-teclado.png` | Alta |
| 4 | Base 2: Formulario y validación nativa | `index.html`, líneas 191-224 (`#celular` y controles) y `css/style.css`, línea 312 | El formulario solo usa `required` y omite validaciones nativas como `pattern` (ej. en `input type="tel" id="celular"` permite ingresar letras) o `min`/`max`. Además, el selector `.formulario-contacto input` excluye al `<textarea>`, dejándolo sin diseño. | Especificación HTML WHATWG (Sección 4.10.5.3 `pattern` attribute) y WCAG 2.2 Criterio 3.3.2 (Nivel A) | `evidencias/hallazgo5-formulario-validacion.png` | Media |
| 5 | Base 7: Orden de la familia de fuentes en CSS | `css/style.css`, línea 19 (`--fuente-texto`) | En `style.css` (línea 19) se declaró la familia genérica `sans-serif` al inicio de la lista (`--fuente-texto: sans-serif, Arial, Helvetica;`), lo que anula la lectura de las fuentes siguientes ya que el navegador aplica la genérica por defecto inmediatamente. | W3C CSS Fonts Module Level 4 (Sección 4.1 `font-family`) | *(Revisión directa en código fuente CSS)* | Baja |