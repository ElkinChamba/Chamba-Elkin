# Respuesta a la Auditoría (Parte 3)

**Estudiante:** Chamba Maura Elkin Jair (Lista 28)  
**Auditor:** Yadaicela Uyaguari Andres Renato (Lista 29)  
**Ficha 28:** Clínica veterinaria | Fecha y hora de reserva | 720 px | Un acordeón accesible con details y summary, sin JavaScript

## 1. Respuesta hallazgo por hallazgo

| N.º de hallazgo | Decisión (acepta o refuta) | Justificación con la norma | Evidencia antes y después | Commit |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Refuto (pero agrego la mejora) | Según la especificación HTML de WHATWG para el elemento `<nav>` y WCAG 2.2 (Criterio 1.3.1), cuando hay un solo bloque de navegación en toda la página, el navegador ya lo identifica en el árbol de accesibilidad con el rol `navigation`. El atributo `aria-label` solo es obligatorio cuando existen dos o más `<nav>` para diferenciarlos. De igual forma le agregué `aria-label="Principal"` para dejar más claro su nombre accesible. | Antes: `docs/evidencias/hallazgo-1-nav.png` / Después: `docs/evidencias/despues-hallazgo-1-nav.png` | `89bdbfe` |
| 2 | Acepto | Tiene razón según WCAG 2.2 Criterio 3.3.2 (Etiquetas o instrucciones): como mi input de teléfono exige un formato de 10 números con `pattern="[0-9]{10}"`, hacía falta indicarle ese formato al usuario. Agregué el párrafo `<p id="ayuda-telefono">` debajo del campo y lo asocié al input con `aria-describedby="ayuda-telefono"`. | Antes: `docs/evidencias/hallazgo-2-telefono.png` / Después: `docs/evidencias/despues-hallazgo-2-telefono.png` | `89bdbfe` |
| 3 | Cumple (N/A) | En el mismo informe el compañero indica que cumple con WHATWG porque la tabla ya tiene `<caption>`, `<thead>`, `<tbody>` y los `<th scope="col">`. | `docs/evidencias/hallazgo-3-tabla.png` | N/A |
| 4 | Refuto la severidad Baja | En el hallazgo mi compañero puso que sí cumplo con el breakpoint de 720px y con `display: grid` (`grid-template-columns: 2fr 1fr`), pero en la columna de severidad le puso "Baja" en vez de N/A. Según el módulo CSS Grid Layout del W3C y mi Ficha 28, este punto está completo y no tiene errores. | `docs/evidencias/hallazgo-4-grid.png` | N/A |
| 5 | Cumple (N/A) | El menú de navegación usa `display: flex`, `justify-content: center` y `gap: 15px` cumpliendo con la especificación CSS Flexible Box Layout del W3C. | `docs/evidencias/hallazgo-5-flexbox.png` | N/A |
| 6 | Cumple (N/A) | Las preguntas frecuentes usan `<details>` y `<summary>` nativos de HTML (WHATWG) sin nada de JavaScript, como pide la Ficha 28. | `docs/evidencias/hallazgo-6-acordeon.png` | N/A |
| 7 | Cumple (N/A) | El formulario usa `<input type="datetime-local">` con su respectivo `<label for="fecha_cita">` como pide la Ficha 28 y el estándar HTML de WHATWG. | `docs/evidencias/hallazgo-7-datetime.png` | N/A |
| 8 | Acepto | De acuerdo con WCAG 2.2 Criterio 2.4.1 (Evitar bloques), faltaba el enlace para saltar la navegación con el teclado. Agregué al inicio del `<body>` el enlace `<a href="#contenido-principal" class="skip-link">Saltar al contenido principal</a>` conectado al `<main id="contenido-principal">`, que se muestra arriba cuando recibe `:focus` con la tecla Tab. | Antes: `docs/evidencias/hallazgo-8-skip.png` / Después: `docs/evidencias/despues-hallazgo-8-skip.png` | `89bdbfe` |
| 9 | Refuto en fondo blanco (pero corrijo por el menú) | Refuto que `#008392` sobre fondo blanco (`#ffffff`) sea un error, porque en el inspector da un contraste de 4.59:1 y sí pasa el mínimo de 4.5:1 del Criterio 1.4.3 de WCAG 2.2. Sin embargo, revisando mi página vi que en los botones del menú (`nav a`) ese mismo color estaba sobre fondo gris claro (`#f1f5f9`) y ahí bajaba a 4.15:1. Por eso cambié `--color-primario` a `#006672`, subiendo el contraste a 6.68:1 en blanco y 6.09:1 en el menú. | Antes: `docs/evidencias/hallazgo-9-contraste.png` / Después: `docs/evidencias/despues-hallazgo-9-contraste.png` | `89bdbfe` |
| 10 | Cumple (N/A) | Todos los enlaces, inputs, `summary` y el botón tienen foco visible con `outline: 3px solid var(--color-foco)`, cumpliendo el Criterio 2.4.7 de WCAG 2.2. | `docs/evidencias/hallazgo-10-foco.png` | N/A |
| 11 | Acepto | Según el Criterio 1.1.1 de WCAG 2.2 y la especificación HTML de WHATWG, el atributo `alt` debe describir lo que realmente muestra la imagen. Antes decía "Logotipo principal", así que lo cambié en `index.html` para que describa la ilustración de la fachada de la clínica veterinaria. | Antes: `docs/evidencias/hallazgo-11-alt.png` / Después: `docs/evidencias/despues-hallazgo-11-alt.png` | `89bdbfe` |

## 2. Problemas adicionales que encontré y corregí

| N.º | Ubicación | Problema que el auditor no vio | Norma que incumplía | Corrección y evidencia | Commit |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Adicional 1 | `css/estilos.css`, regla `nav a` | El auditor solo probó el color primario `#008392` sobre el fondo blanco de las tarjetas (donde daba 4.59:1 y sí cumplía), pero no revisó los enlaces del menú `nav a`, que tienen de fondo `--color-fondo` (`#f1f5f9`). Ahí el contraste bajaba a 4.15:1. | WCAG 2.2 Criterio 1.4.3 (Contraste mínimo de 4.5:1) | Oscurecí la variable `--color-primario` a `#006672`, con lo que el contraste en los botones del menú subió a 6.09:1 en DevTools (`docs/evidencias/adicional-1-contraste-nav.png`). | `89bdbfe` |
| Adicional 2 | `css/estilos.css`, reglas `:root`, `th, td` y `nav ul` | En pantalla móvil de 360px la tabla quedaba muy apretada por el padding de `12px 15px` en las celdas, y además me habían quedado algunos colores en hexadecimal directo en el CSS en lugar de estar todos como variables `--color-...` en `:root`. | Requisitos Base 4 y 5; WCAG 2.2 Criterio 1.4.10 (Reflow) | Pasé todos los colores restantes a variables en `:root`, agregué `flex-wrap: wrap` al menú y bajé el padding de `th, td` a `10px 8px` en móvil dejando `12px 15px` dentro del `@media (min-width: 720px)` (`docs/evidencias/adicional-2-tabla-360px.png`). | `cee82b0` |

## 3. Validación W3C (Requisito Base 7)

- Validador HTML del W3C: 0 errores (`docs/evidencias/validador-html.png`)
- Validador CSS del W3C: 0 errores (`docs/evidencias/validador-css.png`)