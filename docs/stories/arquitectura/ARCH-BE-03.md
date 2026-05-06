# ARCH-BE-03 — Estructura de carpetas y módulos

**Estado:** TODO
**Depende de:** ARCH-BE-01

---

## Objetivo

Definir la estructura de carpetas del backend que se va a mantener durante todo el desarrollo. Cada dominio de negocio tiene su propia carpeta con router, controller y service.

---

## Estructura esperada al terminar

```
apps/api/src/
├── modules/
│   ├── auth/
│   │   ├── auth.router.ts
│   │   ├── auth.controller.ts
│   │   └── auth.service.ts
│   ├── users/
│   ├── coaches/
│   ├── athletes/
│   ├── routines/
│   ├── workouts/
│   ├── payments/
│   ├── community/
│   ├── calendar/
│   └── notifications/
├── middleware/
│   ├── auth.middleware.ts    ← verifica JWT
│   ├── error.middleware.ts   ← manejo global de errores
│   └── validate.middleware.ts ← valida body con Zod
├── prisma/
│   └── client.ts
├── types/
│   └── express.d.ts         ← extiende Request con user
└── index.ts
```

---

## Patrón por módulo

Cada módulo sigue la misma estructura:

```
router    → define las rutas y aplica middlewares
controller → recibe el request, llama al service, devuelve la respuesta
service   → contiene la lógica de negocio y llama a Prisma
```

---

## Tareas

- [ ] Crear la estructura de carpetas completa (pueden ser archivos vacíos)
- [ ] Crear `src/types/express.d.ts` para extender `Request`:
  ```typescript
  declare namespace Express {
    interface Request {
      user?: { id: string; role: 'COACH' | 'ATHLETE' }
    }
  }
  ```
- [ ] Registrar todos los routers en `src/index.ts`:
  ```typescript
  app.use('/auth', authRouter)
  app.use('/users', usersRouter)
  // etc.
  ```
- [ ] Crear un router vacío de ejemplo en `modules/auth/` para verificar el patrón

---

## Criterios para marcar como DONE

- [ ] Estructura de carpetas creada
- [ ] `GET /auth/ping` devuelve `200` (ruta de prueba del módulo auth)
- [ ] El patrón router → controller → service está documentado con un ejemplo funcional
