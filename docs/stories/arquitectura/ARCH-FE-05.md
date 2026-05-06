# ARCH-FE-05 — Configurar estado global (Zustand + React Query)

**Estado:** TODO
**Depende de:** ARCH-FE-04

---

## Objetivo

Tener el estado global de autenticación funcionando con Zustand y React Query configurado para el estado del servidor.

---

## Tareas

- [ ] Crear `src/store/authStore.ts`:
  ```typescript
  interface AuthStore {
    accessToken: string | null
    refreshToken: string | null
    user: AuthUser | null
    isAuthenticated: boolean
    login: (tokens, user) => void
    logout: () => void
    setAccessToken: (token: string) => void
  }
  ```
  - `login()` guarda tokens en Zustand + `expo-secure-store`
  - `logout()` limpia Zustand + `expo-secure-store`
- [ ] Lógica de auto-login en `App.tsx`:
  - Al arrancar, leer refresh token de `expo-secure-store`
  - Si existe → intentar refresh → si funciona, setear estado autenticado
  - Si falla → mostrar login
- [ ] Configurar `QueryClient` con defaults:
  ```typescript
  new QueryClient({
    defaultOptions: {
      queries: {
        retry: 1,
        staleTime: 1000 * 60 * 5,
      },
    },
  })
  ```
- [ ] Crear hook `useAuth()` que expone el estado de `authStore`

---

## Criterios para marcar como DONE

- [ ] Al cerrar y reabrir la app, la sesión activa se restaura automáticamente
- [ ] `useAuth()` devuelve el usuario y el rol correctamente
- [ ] `logout()` limpia todo el estado y redirige a login
