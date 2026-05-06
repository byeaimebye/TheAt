# ARCH-BE-06 — Configurar Firebase FCM

**Estado:** TODO
**Depende de:** ARCH-BE-01

---

## Objetivo

Tener un servicio de notificaciones push listo para usar desde cualquier módulo del backend.

---

## Tareas

- [ ] Crear proyecto en Firebase Console y habilitar Cloud Messaging
- [ ] Agregar credenciales al `.env`:
  ```env
  FIREBASE_PROJECT_ID=tu-proyecto
  FIREBASE_CLIENT_EMAIL=firebase-adminsdk@...
  FIREBASE_PRIVATE_KEY="-----BEGIN PRIVATE KEY-----\n...\n-----END PRIVATE KEY-----\n"
  ```
- [ ] Instalar Firebase Admin SDK:
  ```bash
  npm install firebase-admin
  ```
- [ ] Crear `src/modules/notifications/firebase.ts`:
  - Inicializa Firebase Admin con las credenciales del `.env`
  - Exporta la instancia de messaging
- [ ] Crear `src/modules/notifications/notifications.service.ts`:
  ```typescript
  sendToUser(userId: string, title: string, body: string, data?: object)
  sendToMultiple(userIds: string[], title: string, body: string)
  ```
  - Busca los tokens del usuario en `UserDevice`
  - Envía la notificación vía FCM
  - Si un token falla, lo elimina de la DB

---

## Modelo en Prisma a agregar

```prisma
model UserDevice {
  id        String   @id @default(uuid())
  userId    String
  pushToken String
  platform  String
  createdAt DateTime @default(now())
  user      User     @relation(fields: [userId], references: [id])

  @@map("user_devices")
}
```

---

## Criterios para marcar como DONE

- [ ] Firebase Admin inicializa sin errores al arrancar el servidor
- [ ] `notifications.service.sendToUser()` puede llamarse desde cualquier módulo
- [ ] Una notificación de prueba llega al emulador con Google Play
