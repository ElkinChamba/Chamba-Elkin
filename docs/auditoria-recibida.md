# Auditoría a Chamba Maura Elkin Jair (Lista 28)

**Auditor:** Yadaicela Uyaguari Andres Renato (Lista 29)  
**Cadena indicada en clase:** el 28 me envía su repositorio, yo lo evalúo y le devuelvo el informe.  
**Ficha auditada (N.º 28):** Clínica veterinaria | Fecha y hora de reserva | 720 px | Acordeón accesible con details y summary, sin JavaScript

---

## Qué espero encontrar antes de abrir su página

1. header, nav, main, dos o más section o article con encabezado, aside y footer; encabezados de h1 a h2 sin saltos.
2. Formulario con 5 o más campos con label for, fieldset y legend, incluyendo campos de fecha y hora de reserva (type="date", type="time" o datetime-local).
3. Tabla con caption, thead, tbody y th con scope.
4. Grid general, Flexbox interno, breakpoint en 720 px y sin scroll horizontal en 360 px.
5. Acordeón con details y summary que abra y cierre con Enter, sin ninguna etiqueta script en toda la página.
6. Colores en variables --color- con contraste 4.5:1 y foco visible al navegar con Tab.

---

## Hallazgos de la auditoría

| N.º | Requisito | Ubicación | Hallazgo | Norma | Evidencia | Severidad |
|---|---|---|---|---|---|---|
| 1 | Base 1: Estructura semántica | `index.html`, líneas 14-16 | **CUMPLE PARCIALMENTE:** El nav no tiene aria-label para identificar su propósito ante lectores de pantalla. Debería ser `<nav aria-label="Principal">` | WHATWG HTML Living Standard; WCAG 2.2 Criterio 1.3.1 | `docs/evidencias/hallazgo-1-nav.png` | Media |
| 2 | Base 2: Formulario accesible | `index.html`, líneas 98-101 | **CUMPLE PARCIALMENTE:** El campo teléfono tiene pattern="[0-9]{10}" pero no tiene aria-describedby que explique el formato. Falta un párrafo con id="ayuda-telefono" | WCAG 2.2 Criterio 3.3.2 | `docs/evidencias/hallazgo-2-telefono.png` | Media |
| 3 | Base 3: Tabla accesible | `index.html`, líneas 67-89 | **CUMPLE:** La tabla tiene caption, thead, tbody y th con scope="col" correctamente implementado. | WHATWG HTML Living Standard | `docs/evidencias/hallazgo-3-tabla.png` | N/A |
| 4 | Base 4: Layout Grid | `css/estilos.css`, líneas 210-235 | **CUMPLE:** El breakpoint está en 720px correctamente. Usa display: grid en body con grid-template-columns: 2fr 1fr. | Especificación CSS Grid Layout Module Level 1 | `docs/evidencias/hallazgo-4-grid.png` | Baja |
| 5 | Base 5: Flexbox | `css/estilos.css`, línea 58 | **CUMPLE:** El nav ul usa display: flex con justify-content: center y gap: 15px correctamente. | Especificación CSS Flexible Box Layout Module | `docs/evidencias/hallazgo-5-flexbox.png` | N/A |
| 6 | Ficha 28: Acordeón sin JS | `index.html`, líneas 120-130 | **CUMPLE TOTALMENTE:** Usa details y summary. No hay ninguna etiqueta `<script>` en todo el documento. Funciona con teclado. | WHATWG HTML Living Standard | `docs/evidencias/hallazgo-6-acordeon.png` | N/A |
| 7 | Ficha 28: Fecha y hora | `index.html`, línea 104 | **CUMPLE:** Usa `<input type="datetime-local">` correctamente para fecha y hora de reserva. | WHATWG HTML Living Standard | `docs/evidencias/hallazgo-7-datetime.png` | N/A |
| 8 | Accesibilidad: Skip-link | No encontrado | **NO CUMPLE:** No hay enlace "Saltar al contenido" al inicio del body. Es obligatorio para accesibilidad. | WCAG 2.2 Criterio 2.4.1 | `docs/evidencias/hallazgo-8-skip.png` | Alta |
| 9 | Accesibilidad: Contraste | `css/estilos.css`, línea 3 | **CUMPLE APENAS:** El color primario #008392 sobre fondo blanco tiene un contraste de ~4.6:1. Cumple el mínimo de 4.5:1 pero está en el límite. | WCAG 2.2 Criterio 1.4.3 | `docs/evidencias/hallazgo-9-contraste.png` | Baja |
| 10 | Accesibilidad: Foco visible | `css/estilos.css`, líneas 67-71 | **CUMPLE:** Tiene `outline: 3px solid var(--color-foco)` con outline-offset. El foco es claramente visible. | WCAG 2.2 Criterio 2.4.7 | `docs/evidencias/hallazgo-10-foco.png` | N/A |
| 11 | Imágenes: Alt descriptivo | `index.html`, línea 56 | **NO CUMPLE:** El alt dice "Logotipo principal" pero la imagen parece ser una foto del edificio. El alt debe describir el contenido real. | WCAG 2.2 Criterio 1.1.1 | `docs/evidencias/hallazgo-11-alt.png` | Media |

---

**Auditor:** Yadaicela Uyaguari Andres Renato