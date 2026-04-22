# Firebase RTDB · Diagnóstico y permisos para Calidad Interna

Este proyecto usa Firebase Realtime Database desde frontend (`firebase-database`) y no integra `firebase-auth` en `index.html`.

## 1) Qué rutas usa Calidad Interna

Para renderizar **Calidad interna** (admin), el código lee estas rutas:

- `users_by_email`
- `tickets`
- `activity_logs`
- `quality_internal_config`
- `quality_internal_feedback`

Además, admin guarda en:

- `quality_internal_config` (write)
- `quality_internal_feedback` (write)

## 2) Regla temporal (rápida) para destrabar el módulo

> Úsala solo como contingencia para validar que el problema era permisos.

```json
{
  "rules": {
    "users_by_email": { ".read": true, ".write": true },
    "tickets": { ".read": true, ".write": true },
    "activity_logs": { ".read": true, ".write": true },
    "quality_internal_config": { ".read": true, ".write": true },
    "quality_internal_feedback": { ".read": true, ".write": true }
  }
}
```

Si con esta regla funciona, el bloqueo original era de Rules.

## 3) Recomendación de seguridad (producción)

Como el frontend no usa Firebase Auth, **no se puede aplicar control por rol real en Rules** con `auth != null` ni claims.

Recomendado:

1. Integrar Firebase Auth (email/password o SSO).
2. Persistir rol en custom claims (o validar contra un nodo administrado por backend).
3. Cambiar Rules a controladas por `auth`.

Ejemplo mínimo cuando ya exista Auth:

```json
{
  "rules": {
    "users_by_email": { ".read": "auth != null", ".write": "auth != null && auth.token.role == 'admin'" },
    "tickets": { ".read": "auth != null", ".write": "auth != null" },
    "activity_logs": { ".read": "auth != null", ".write": "auth != null" },
    "quality_internal_config": { ".read": "auth != null", ".write": "auth != null && auth.token.role == 'admin'" },
    "quality_internal_feedback": { ".read": "auth != null", ".write": "auth != null && auth.token.role == 'admin'" }
  }
}
```

## 4) Verificación operativa

Después de publicar Rules:

1. Entrar al panel admin → Calidad interna.
2. Si falla, usar el botón **Diagnosticar permisos** para ver ruta exacta bloqueada.
3. Revisar consola del navegador para `PERMISSION_DENIED`.
