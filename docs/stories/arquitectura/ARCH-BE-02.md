# ARCH-BE-02 — Conectar Prisma con Supabase

**Estado:** TODO
**Depende de:** ARCH-BE-01

---

## Objetivo

Tener Prisma conectado a la base de datos de Supabase con el schema inicial y la primera migración aplicada.

---

## Estructura esperada al terminar

```
apps/api/
├── src/
│   └── prisma/
│       └── client.ts    ← instancia singleton de PrismaClient
├── prisma/
│   ├── schema.prisma
│   └── migrations/
```

---

## Tareas

- [ ] Crear proyecto en Supabase y copiar la `DATABASE_URL` al `.env`
- [ ] Instalar Prisma:
  ```bash
  npm install prisma @prisma/client
  npx prisma init
  ```
- [ ] Configurar `provider = "postgresql"` en `schema.prisma`
- [ ] Crear modelo inicial `User` en el schema:
  ```prisma
  model User {
    id                     String    @id @default(uuid())
    name                   String
    email                  String    @unique
    passwordHash           String
    role                   Role
    hasCompletedOnboarding Boolean   @default(false)
    createdAt              DateTime  @default(now())
    deletedAt              DateTime?

    @@map("users")
  }

  enum Role {
    COACH
    ATHLETE
  }
  ```
- [ ] Correr primera migración:
  ```bash
  npx prisma migrate dev --name init
  ```
- [ ] Crear `src/prisma/client.ts` con singleton de PrismaClient
- [ ] Verificar conexión con `npx prisma studio`

---

## src/prisma/client.ts

```typescript
import { PrismaClient } from '@prisma/client'

const globalForPrisma = globalThis as unknown as { prisma: PrismaClient }

export const prisma =
  globalForPrisma.prisma ?? new PrismaClient({ log: ['query'] })

if (process.env.NODE_ENV !== 'production') globalForPrisma.prisma = prisma
```

---

## Criterios para marcar como DONE

- [ ] `npx prisma migrate dev` corre sin errores
- [ ] `npx prisma studio` muestra la tabla `users`
- [ ] La conexión a Supabase funciona desde el código
