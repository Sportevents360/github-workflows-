# Registro de cambios

## 2026-11-10
- **Qué:** reactivado el workflow (GitHub lo había desactivado por 60 días sin cambios). Añadido un paso que lo vuelve a marcar como activo en cada ejecución, y el ping ahora llama a `/rest/v1/` y falla si Supabase no responde. Creada la documentación.
- **Por qué:** evitar que el despertador se desactive solo y enterarse si deja de funcionar.
- **Archivos:** `.github/workflows/keep_alive.yml`, `docs/`.
- **Comprobación:** ejecución manual desde Actions tras el cambio.
- **Pendiente:** nada.
