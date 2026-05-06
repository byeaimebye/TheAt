# ARCH-FE-01 — Inicializar proyecto Expo con development build

**Estado:** TODO
**Depende de:** ARCH-00

---

## Objetivo

Tener la app Expo corriendo en el emulador Android como development build (sin Expo Go).

---

## Tareas

- [ ] Crear el proyecto Expo dentro de `apps/mobile/`:
  ```bash
  npx create-expo-app mobile --template blank-typescript
  ```
- [ ] Verificar que `app.json` tiene `name`, `slug` y `bundleIdentifier` / `package` configurados
- [ ] Instalar dependencias base:
  ```bash
  npm install axios zustand @tanstack/react-query react-hook-form zod
  ```
- [ ] Crear `.env.example`:
  ```env
  EXPO_PUBLIC_API_URL=http://10.0.2.2:3000
  ```
  > `10.0.2.2` es la IP que usa el emulador Android para acceder al localhost de la máquina
- [ ] Correr en emulador Android sin Expo Go:
  ```bash
  npx expo run:android
  ```
- [ ] Verificar que la app abre y muestra la pantalla por defecto

---

## Importante

- El primer build tarda 5–10 minutos
- Después del primer build, hot reload funciona normalmente
- Solo necesitás re-correr `npx expo run:android` si cambiás `app.json` o plugins nativos
- **Nunca usar** `npx expo start` para abrir en Expo Go

---

## Criterios para marcar como DONE

- [ ] `npx expo run:android` compila y abre la app en el emulador
- [ ] La pantalla por defecto se ve sin errores
- [ ] Hot reload funciona (cambiar texto → guardar → ver cambio sin recompilar)
