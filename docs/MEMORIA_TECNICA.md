# Memoria técnica: Despertador de Supabase

## Qué es
**Desactivado desde el 2026-11-10.** El proyecto lo despierta ahora solo el robot diario de `Sportevents360/supabase-pinger`, que consulta tablas reales; ver su `docs/MEMORIA_TECNICA.md`. Este workflow se conserva por si hiciera falta reactivarlo (Actions → Enable workflow).

Repositorio de Sportevents360 con una única tarea programada de GitHub Actions que hace una llamada a un proyecto de Supabase cada 3 días, para que Supabase no lo pause por inactividad (el plan gratuito pausa proyectos sin actividad).

## Dónde vive
- Repositorio: `Sportevents360/github-workflows-` (público; no poner aquí datos del proyecto).
- Workflow: `.github/workflows/keep_alive.yml`, nombre «Despertador de Supabase».
- Ejecuciones: pestaña Actions del repositorio.

## Cómo funciona
1. **Ping:** llama a `SUPABASE_URL/rest/v1/` con la clave anónima. Falla si no hay respuesta o si Supabase devuelve un error 5xx; entonces GitHub envía un correo de ejecución fallida.
2. **Mantener activo:** vuelve a marcar el propio workflow como activo mediante la API de GitHub (`PUT .../actions/workflows/keep_alive.yml/enable`), con el token automático de la ejecución y el permiso `actions: write`. Sirve para que GitHub no lo desactive tras 60 días sin cambios en el repositorio.

Se puede lanzar a mano desde Actions → Despertador de Supabase → Run workflow.

## Variables (secretos del repositorio)
- `SUPABASE_URL`: dirección del proyecto de Supabase que se mantiene despierto.
- `SUPABASE_ANON_KEY`: clave anónima de ese proyecto.

Los valores están solo en los secretos del repositorio en GitHub.

## Decisiones
- 2026-11-10: GitHub lo desactivó por 60 días sin cambios. Se descartó hacer commits periódicos automáticos (ensucian el historial) y acciones de terceros; se usa la API de GitHub directamente.
- Antes el ping llamaba a la raíz de `SUPABASE_URL` y siempre salía «correcto». Ahora llama a la API de datos y falla si no hay respuesta.

## Límites y pendientes
- No está documentado aquí qué proyecto de Supabase es (la URL está en el secreto). Si se cambia de proyecto, actualizar los dos secretos.
- Si el paso de mantener activo dejara de funcionar, el síntoma será otro correo de GitHub avisando de que se ha desactivado; se reactiva en Actions → Enable workflow.
