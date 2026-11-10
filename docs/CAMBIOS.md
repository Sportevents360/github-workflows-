# Registro de cambios

## 2026-11-10 (2)
- **Qué:** workflow desactivado; queda como único robot el de `Sportevents360/supabase-pinger`.
- **Por qué:** los dos despertaban el mismo proyecto de Supabase.
- **Archivos:** `docs/`.
- **Comprobación:** el robot de supabase-pinger se lanzó a mano con éxito (200 en las dos tablas) antes de desactivar este.
- **Pendiente:** nada.

## 2026-11-10
- **Qué:** reactivado el workflow (GitHub lo había desactivado por 60 días sin cambios). Añadido un paso que lo vuelve a marcar como activo en cada ejecución, y el ping ahora llama a `/rest/v1/` y falla si Supabase no responde. Creada la documentación.
- **Por qué:** evitar que el despertador se desactive solo y enterarse si deja de funcionar.
- **Archivos:** `.github/workflows/keep_alive.yml`, `docs/`.
- **Comprobación:** ejecución manual desde Actions tras el cambio.
- **Pendiente:** nada.
