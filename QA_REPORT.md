# QA Report - NOVA

Fecha: 2026-04-19

## Alcance de QA ejecutado

Se realizó QA funcional y técnico sobre flujos críticos visibles en `index.html`, con foco en:

- Roles de usuario: `admin`, `analista`, `consultor`.
- Sección social **Encuentro**: carga de feed, reacciones, comentarios y felicitaciones.
- Seguridad de renderizado en handlers inline (`onclick`) para entradas dinámicas.

## Hallazgos

### 1) Falla por caracteres especiales en parámetros de `onclick`

**Severidad:** Alta  
**Módulo:** Encuentro (reacciones, comentarios y felicitaciones)

**Descripción:**
Los valores dinámicos (id de publicación, emoji/email) se escapaban con `htmlEscape` y luego se insertaban en literales JavaScript dentro de atributos `onclick`.

Con caracteres como comilla simple (`'`) el HTML decodea `&#39;` a `'` antes de ejecutar el handler, rompiendo la cadena JS y disparando error de sintaxis.

**Impacto:**
- Botones de reacción pueden fallar en casos edge.
- Comentar publicación puede fallar para ids con caracteres especiales.
- Felicitar usuario puede fallar para emails no estándar con apóstrofe.

**Corrección aplicada:**
- Se agregó helper `jsStringEscape` para contexto JavaScript string literal.
- Se reemplazó `htmlEscape` por `jsStringEscape` en parámetros `onclick` de esas acciones.

## Resultado post-fix

- Se mitiga el error de sintaxis en handlers inline ante caracteres especiales.
- Se conserva `htmlEscape` en contexto HTML (texto/atributos), y `jsStringEscape` en contexto JS.

## Recomendaciones adicionales

1. Migrar eventos inline a `addEventListener` para evitar interpolación de JS en HTML.
2. Crear suite smoke E2E por rol (`admin`, `analista`, `consultor`) con casos edge de caracteres especiales.
3. Agregar validadores centralizados por contexto de escape (HTML vs JS vs URL).
