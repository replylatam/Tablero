# Recomendaciones de diseño UI/UX para la sección inicial del Admin

## Objetivo visual (inspirado en tu referencia)
- Llevar la home del admin a un estilo **corporativo, oscuro y minimalista** con alto contraste y jerarquía visual clara.
- Priorizar **lectura rápida de KPIs**, navegación lateral compacta y paneles con métricas accionables.

## 1) Sidebar / Menú lateral (look & feel como referencia)

### Qué mantener
- Sidebar fija con íconos y expansión a labels (ya existe en `.leftSidebar` + `.expanded`).

### Qué mejoraría
1. **Ancho más limpio y consistente**
   - Compacto: 72px.
   - Expandido: 224px.
   - Esto da mejor equilibrio entre “modo íconos” y “modo texto”.

2. **Estados visuales más corporativos**
   - Item activo: fondo sutil + borde izquierdo de 2px en color primario.
   - Hover: solo elevar contraste 8–12%, sin sombras agresivas.
   - Desactivar emojis en iconografía principal y migrar a iconos lineales (Lucide/Heroicons).

3. **Agrupación de navegación**
   - Secciones: “Overview”, “Operación”, “Analítica”, “Configuración”.
   - Cada sección con title de 11–12px, tracking amplio, color secundario.

4. **Orb de calidad al footer como widget discreto**
   - Mantenerlo pero más pequeño y con tooltip “Calidad global”.
   - Debe competir menos con el contenido principal.

## 2) Header principal

1. **Título + subtítulo de contexto**
   - Ejemplo: “Dashboard Overview” + “Última actualización: hh:mm”.

2. **Barra de búsqueda/acción alineada a la derecha**
   - Input compacto (max 320px) + botón de acción primaria (“Nuevo ticket”, “Exportar”).

3. **Espaciado estable**
   - Grid base de 8px; bloques de 16/24px entre cards.

## 3) Tarjetas KPI (fila superior)

1. **Unificar altura y estructura de cards**
   - Título corto, valor principal, delta (%), mini-trend opcional.
   - Evitar mezclar gauges y líneas en cards muy pequeñas.

2. **Jerarquía tipográfica**
   - Label: 12px semibold.
   - Valor: 30–34px bold.
   - Meta secundaria: 12–13px.

3. **Semántica de color estricta**
   - Verde = mejora.
   - Ámbar = alerta.
   - Rojo = deterioro.
   - Azul/cian = neutro/informativo.

## 4) Panel “Training Status” → cambiar a “Cantidad de tickets por analista”

Este cambio es excelente porque conecta mejor con operación real.

### Propuesta de contenido
- Nuevo título: **Cantidad de tickets por analista**.
- Subtítulo opcional: “Últimos 7 días” o rango seleccionado.
- Mostrar **todos los analistas**, ordenados de mayor a menor volumen.

### Visual recomendado
1. **Lista con barras horizontales**
   - Izquierda: nombre del analista.
   - Derecha: total de tickets.
   - Fondo de barra tenue + barra de progreso sólida.

2. **Top performer destacado**
   - Primer analista con badge “Top”.

3. **Scroll interno si hay más de 8–10 analistas**
   - Altura fija para no romper layout del dashboard.

4. **Tooltips o detalle al hover**
   - Tickets resueltos, pendientes y SLA.

### Métricas sugeridas por analista
- Total tickets.
- % resueltos dentro de SLA.
- Tiempo promedio de primera respuesta.

## 5) Gráfico principal (área grande)

1. **Título orientado a decisión**
   - “Evolución de tickets por hora” o “Backlog vs Resueltos”.

2. **Ejes y labels mínimos pero claros**
   - Pocas marcas, grid muy tenue.

3. **Leyenda compacta arriba a la derecha**
   - Máximo 2–3 series.

## 6) Diseño system recomendado (para mantener consistencia)

- Bordes: 10–14px.
- Sombra: muy sutil (evitar glow fuerte en corporativo).
- Stroke: 1px con opacidad baja.
- Motion: transiciones cortas (160–220ms), sin rebotes.
- Densidad: evitar sobrecargar con más de 6 KPIs en primera vista.

## 7) Accesibilidad y claridad ejecutiva

- Contraste mínimo AA en texto y labels.
- Estados de foco visibles para teclado.
- No depender solo de color para comunicar estado (añadir icono/etiqueta).
- Números con formato local (`1.234` o `1,234`) y unidad explícita.

## 8) Microcopy corporativo sugerido

- “Dashboard Overview” → “Resumen operativo”.
- “Training Status” → “Cantidad de tickets por analista”.
- “Model Accuracy” → “Cumplimiento SLA”.
- “Inference Latency” → “Tiempo promedio de respuesta”.

## 9) Orden de implementación recomendado

1. Ajustar sidebar (ancho, estados, iconografía).
2. Normalizar cards KPI (altura, tipografía, colores).
3. Reemplazar panel de Training por “Tickets por analista”.
4. Refinar gráfico principal y leyendas.
5. Cerrar con accesibilidad + QA visual responsive.

---

## Resultado esperado
Con estos cambios, el admin se va a ver más “enterprise”: limpio, serio, con foco en operación y lectura ejecutiva rápida, manteniendo la estética moderna que te gustó de la referencia.
