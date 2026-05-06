# ARCH-FE-02 — Estructura de carpetas

**Estado:** TODO
**Depende de:** ARCH-FE-01

---

## Objetivo

Definir la estructura de carpetas del frontend que se va a mantener durante todo el desarrollo.

---

## Estructura esperada al terminar

```
apps/mobile/
├── src/
│   ├── api/
│   │   ├── client.ts          ← instancia de Axios con interceptores
│   │   ├── queryKeys.ts       ← claves de React Query centralizadas
│   │   └── services/          ← una carpeta por módulo (auth, routines, etc.)
│   │       └── auth.service.ts
│   ├── components/
│   │   └── ui/                ← componentes reutilizables (Button, Card, Input...)
│   ├── hooks/                 ← hooks compartidos
│   ├── navigation/
│   │   ├── AuthNavigator.tsx
│   │   ├── CoachNavigator.tsx
│   │   ├── AthleteNavigator.tsx
│   │   └── RootNavigator.tsx
│   ├── screens/
│   │   ├── auth/
│   │   ├── coach/
│   │   └── athlete/
│   ├── store/
│   │   └── authStore.ts       ← Zustand: token, rol, userId
│   ├── types/
│   │   └── index.ts           ← tipos compartidos (User, Role, etc.)
│   └── utils/
│       └── index.ts           ← helpers, formatters, constantes
├── App.tsx
├── app.json
└── package.json
```

---

## Tareas

- [ ] Crear la estructura de carpetas completa
- [ ] Crear `src/types/index.ts` con tipos base:
  ```typescript
  export type Role = 'COACH' | 'ATHLETE'

  export interface AuthUser {
    id: string
    name: string
    role: Role
  }
  ```
- [ ] Crear `src/utils/index.ts` vacío con comentario de uso
- [ ] Crear componentes UI vacíos como placeholders: `Button.tsx`, `Card.tsx`, `Input.tsx`

---

## Criterios para marcar como DONE

- [ ] Estructura de carpetas creada en el repo
- [ ] Los tipos base están definidos en `src/types/index.ts`
- [ ] La app sigue compilando sin errores después de crear la estructura
