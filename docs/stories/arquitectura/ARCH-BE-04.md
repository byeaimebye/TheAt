# ARCH-BE-04 — Middleware de autenticación JWT

**Estado:** TODO
**Depende de:** ARCH-BE-02, ARCH-BE-03

---

## Objetivo

Implementar el sistema de autenticación con JWT (access token + refresh token) y el middleware que protege rutas.

---

## Tareas

- [ ] Instalar dependencias:
  ```bash
  npm install jsonwebtoken bcrypt
  npm install -D @types/jsonwebtoken @types/bcrypt
  ```
- [ ] Crear `src/middleware/auth.middleware.ts`:
  - Lee el header `Authorization: Bearer <token>`
  - Verifica el token con `JWT_SECRET`
  - Si es válido, agrega `req.user = { id, role }` y llama a `next()`
  - Si es inválido o no existe, devuelve `401`
- [ ] Crear helpers de JWT en `src/modules/auth/auth.service.ts`:
  - `generateAccessToken(userId, role)` → expira en `JWT_EXPIRES_IN`
  - `generateRefreshToken(userId)` → expira en `JWT_REFRESH_EXPIRES_IN`
  - `verifyAccessToken(token)`
  - `verifyRefreshToken(token)`
  - `hashPassword(password)`
  - `comparePassword(password, hash)`
- [ ] Crear middleware de rol `requireRole('COACH' | 'ATHLETE')`:
  - Verifica que `req.user.role` coincide con el rol requerido
  - Si no coincide, devuelve `403`

---

## Uso esperado en rutas

```typescript
// Ruta pública
router.post('/login', authController.login)

// Ruta autenticada
router.get('/me', authMiddleware, usersController.getMe)

// Ruta solo para coaches
router.post('/routines', authMiddleware, requireRole('COACH'), routinesController.create)
```

---

## Criterios para marcar como DONE

- [ ] Una ruta protegida devuelve `401` sin token
- [ ] La misma ruta devuelve `200` con token válido
- [ ] Una ruta con `requireRole('COACH')` devuelve `403` si el usuario es atleta
- [ ] `hashPassword` y `comparePassword` funcionan correctamente
