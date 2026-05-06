# ARCH-FE-04 — Configurar cliente HTTP (Axios + interceptores)

**Estado:** TODO
**Depende de:** ARCH-FE-02

---

## Objetivo

Tener un cliente HTTP configurado que maneje automáticamente los tokens de autenticación y el refresh silencioso cuando el access token expira.

---

## Tareas

- [ ] Crear `src/api/client.ts`:
  - Instancia de Axios con `baseURL` desde `EXPO_PUBLIC_API_URL`
  - Interceptor de request: agrega `Authorization: Bearer <token>` en cada llamada
  - Interceptor de response: si recibe `401`, intenta refresh silencioso y reintenta la request original
  - Si el refresh falla, limpia el store y redirige a login
- [ ] Crear `src/api/queryKeys.ts` con las claves base:
  ```typescript
  export const queryKeys = {
    auth: {
      me: ['auth', 'me'],
    },
    athletes: {
      list: ['athletes'],
      detail: (id: string) => ['athletes', id],
    },
    routines: {
      list: ['routines'],
      detail: (id: string) => ['routines', id],
    },
    payments: {
      list: ['payments'],
    },
  }
  ```
- [ ] Crear `src/api/services/auth.service.ts` con funciones base:
  ```typescript
  login(email, password) → { accessToken, refreshToken, user }
  refresh(refreshToken) → { accessToken }
  logout()
  ```
- [ ] Instalar y configurar `expo-secure-store` para guardar tokens:
  ```bash
  npx expo install expo-secure-store
  ```

---

## Criterios para marcar como DONE

- [ ] Una llamada a la API incluye el token en el header automáticamente
- [ ] Si el token expira, el interceptor hace refresh y reintenta sin que el usuario lo note
- [ ] Si el refresh falla, el usuario es redirigido a login
- [ ] Los tokens se guardan y leen de `expo-secure-store`
