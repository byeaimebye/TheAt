# Stack Tecnológico — Athletica

Decisiones técnicas definidas para el desarrollo del MVP.

---

## Stack Completo

| Capa | Tecnología | Motivo |
|---|---|---|
| **Frontend** | React Native + Expo (development builds) | Multiplataforma iOS/Android, módulos nativos sin configuración manual, no se usa Expo Go |
| **Backend** | Express + TypeScript | Simple, flexible, sin boilerplate innecesario |
| **ORM** | Prisma | TypeScript nativo, migraciones limpias, excelente DX |
| **Base de datos** | Supabase (PostgreSQL) | Free tier generoso, gestionado, sin configuración de servidor |
| **Storage** | Supabase Storage | Incluido en Supabase, suficiente para PDFs e imágenes del MVP |
| **Push notifications** | Firebase FCM | Gratuito sin límite práctico, compatible con Expo |
| **Navegación** | React Navigation v6 | Estándar de la industria para React Native |
| **Estado global** | Zustand | Liviano, simple, sin boilerplate |
| **Estado servidor** | React Query (TanStack Query v5) | Maneja caché, loading y errores automáticamente |
| **Formularios** | React Hook Form + Zod | Validación con tipado fuerte |
| **HTTP client** | Axios | Interceptores para auth y refresh token |

---

## Costos

| Servicio | Plan | Costo |
|---|---|---|
| Supabase (DB + Storage) | Free tier | $0 hasta 500MB DB / 1GB Storage |
| Firebase FCM | Free tier | $0 sin límite de notificaciones |
| Expo EAS Build | Free tier | $0 hasta 30 builds/mes |
| Google Play | One-time | $25 |
| Apple Developer | Anual | $99/año |

**Total infraestructura MVP: $0/mes**

---

## Lo que NO se usa y por qué

| Tecnología | Por qué no |
|---|---|
| Expo Go | No soporta módulos nativos necesarios (push, cámara, share intent) |
| NestJS | Más boilerplate del necesario para este scope |
| TypeORM | Más propenso a errores en TypeScript estricto que Prisma |
| Redux | Overhead innecesario — Zustand + React Query cubren todo |
| Cloudinary | Supabase Storage cubre el caso de uso sin agregar un servicio extra |
