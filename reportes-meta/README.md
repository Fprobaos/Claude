# Reportes Semanales Meta Ads

Documentación operativa del sistema de reportes automáticos para las 16 cuentas publicitarias de clientes inmobiliarios.

> Plan completo: `C:\Users\proba\.claude\plans\keen-imagining-boole.md`

---

## Credenciales (NO subir a git / NO compartir)

Guarda estos valores a medida que los vayas obteniendo en Fase 1. **Nunca** pegues los tokens reales en este archivo si el repo va a GitHub — usa un gestor de contraseñas o un archivo `.env` en `.gitignore`.

| Dato | Dónde se obtiene | Valor |
|------|------------------|-------|
| App ID (Meta for Developers) | developers.facebook.com → Mi App → Configuración básica | `1300877508661974` |
| App Secret | Igual que arriba | `pendiente` |
| Business Manager ID | business.facebook.com → Configuración del negocio | `pendiente` |
| System User ID | Business Manager → Usuarios del sistema | `pendiente` |
| Token System User (ads_read) | Generado desde el System User | `pendiente` |
| WhatsApp Phone Number ID | App → WhatsApp → Configuración API | `275114492355236` |
| WhatsApp Access Token | Igual que arriba | `pendiente` |
| Número personal de Felipe (destino notificación) | — | `pendiente` |
| Google Sheet `Clientes Meta Ads` (ID) | sheets.google.com | `1JnL3r7P6VY9B1jgR9aLEM37cyqCUxH9gQj_KvjaGb28` |

---

## Cuentas publicitarias

Ver `clientes.csv` para la lista completa de los 16 clientes con sus `ad_account_id`.

---

## Cómo regenerar el token si se revoca

1. Entrar a https://business.facebook.com → Configuración del negocio → Usuarios del sistema.
2. Seleccionar el usuario del sistema `Reportes Automáticos`.
3. Click en **Generar nuevo token** → seleccionar la App `Reportes Inmobiliarias` → marcar permisos `ads_read` y `business_management` → click **Generar**.
4. Copiar el nuevo token y actualizarlo en:
   - Este README (campo "Token System User")
   - Make.com → escenario `Reportes Semanales Meta` → módulo HTTP → variable `META_TOKEN`

---

## Cómo correr el escenario manualmente (testing)

1. Entrar a make.com → Scenarios → `Reportes Semanales Meta → PDF → Drive`.
2. Click en **Run once** (abajo a la izquierda).
3. Revisar que cada módulo marca verde.
4. Verificar que los PDFs aparecen en `Google Drive → ReportesSemanales → [cliente]`.

---

## Troubleshooting rápido

- **"Error 190: Invalid OAuth access token"** → token expirado o revocado. Ver sección *Cómo regenerar el token*.
- **"Error 100: Unsupported get request"** → el `ad_account_id` es incorrecto o el System User perdió acceso a esa cuenta. Revisar en Business Manager → Cuentas publicitarias → permisos.
- **PDF vacío / métricas en cero** → la campaña del cliente está pausada esa semana. El escenario debería generar un PDF con leyenda "Sin actividad esta semana".
