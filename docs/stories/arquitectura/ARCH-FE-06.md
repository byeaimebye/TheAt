# ARCH-FE-06 — Configurar notificaciones push (Expo + Firebase)

**Estado:** TODO
**Depende de:** ARCH-FE-01, ARCH-BE-06

---

## Objetivo

Tener el sistema de notificaciones push funcionando end-to-end: la app registra el token del dispositivo y el backend puede enviar notificaciones.

---

## Tareas

- [ ] Instalar dependencias:
  ```bash
  npx expo install expo-notifications expo-device
  ```
- [ ] Configurar `app.json` para notificaciones:
  ```json
  {
    "expo": {
      "plugins": [
        [
          "expo-notifications",
          {
            "icon": "./assets/notification-icon.png",
            "color": "#ffffff"
          }
        ]
      ]
    }
  }
  ```
- [ ] Crear `src/hooks/usePushNotifications.ts`:
  - Solicita permiso de notificaciones al usuario
  - Si el usuario acepta, obtiene el token del dispositivo
  - Envía el token al backend (`POST /notifications/register-token`)
  - Configura el listener para notificaciones recibidas en primer plano
- [ ] Llamar `usePushNotifications()` desde `App.tsx` cuando el usuario está autenticado
- [ ] Configurar deep linking básico: tocar una notificación navega a la pantalla correspondiente
- [ ] Reconstruir el development build después de agregar el plugin:
  ```bash
  npx expo run:android
  ```

---

## Importante

- Las notificaciones push **no funcionan en Expo Go** — requieren el development build
- En el emulador Android, el AVD debe tener **Google Play Services** (usar imagen "Google Play" en Android Studio)
- En iOS Simulator funcionan desde Xcode 14+

---

## Criterios para marcar como DONE

- [ ] La app solicita permiso de notificaciones al primer arranque
- [ ] El token se guarda en la base de datos (tabla `user_devices`)
- [ ] Una notificación enviada desde el backend llega al dispositivo
- [ ] Tocar la notificación abre la app (deep link básico)
