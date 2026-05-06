# ARCH-BE-05 — Manejo de errores y validación

**Estado:** TODO
**Depende de:** ARCH-BE-03

---

## Objetivo

Tener un sistema consistente de errores y validación de datos que aplique a toda la API.

---

## Tareas

- [ ] Instalar Zod:
  ```bash
  npm install zod
  ```
- [ ] Crear clase `AppError` en `src/types/errors.ts`:
  ```typescript
  export class AppError extends Error {
    constructor(
      public message: string,
      public statusCode: number = 500
    ) {
      super(message)
    }
  }
  ```
- [ ] Crear `src/middleware/error.middleware.ts`:
  - Captura todos los errores que llegan con `next(error)`
  - Si es `AppError` → devuelve `{ error: message }` con el statusCode correspondiente
  - Si es cualquier otro error → devuelve `500 { error: 'Internal server error' }`
  - En desarrollo, loguea el stack trace
- [ ] Crear `src/middleware/validate.middleware.ts`:
  - Recibe un schema de Zod
  - Valida `req.body` contra el schema
  - Si falla → devuelve `400` con los errores de validación
  - Si pasa → llama a `next()`
- [ ] Registrar `error.middleware` al final de todos los middlewares en `index.ts`

---

## Formato de respuesta de error

Todos los errores de la API devuelven este formato:

```json
{
  "error": "Mensaje descriptivo del error"
}
```

Para errores de validación (400):
```json
{
  "error": "Validation error",
  "details": [
    { "field": "email", "message": "Email inválido" }
  ]
}
```

---

## Uso esperado

```typescript
// En un controller
const validate = (schema: ZodSchema) => validateMiddleware(schema)

router.post('/login', validate(loginSchema), authController.login)

// En un service
if (!user) throw new AppError('Usuario no encontrado', 404)
```

---

## Criterios para marcar como DONE

- [ ] Un body inválido devuelve `400` con detalle de los campos erróneos
- [ ] Lanzar `AppError('msg', 404)` en un service devuelve `404` al cliente
- [ ] Cualquier error no controlado devuelve `500` sin exponer el stack
