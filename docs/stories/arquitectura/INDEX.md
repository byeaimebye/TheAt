# Arquitectura — Index

Setup inicial del repositorio, backend y frontend.
Estas historias se completan antes de cualquier funcionalidad de producto.

---

## Monorepo

| ID | Historia | Estado |
|---|---|---|
| ARCH-00 | [Configuración del Monorepo](ARCH-00.md) | TODO |

## Backend (Express + TypeScript)

| ID | Historia | Estado |
|---|---|---|
| ARCH-BE-01 | [Inicializar proyecto Express + TypeScript](ARCH-BE-01.md) | TODO |
| ARCH-BE-02 | [Conectar Prisma con Supabase](ARCH-BE-02.md) | TODO |
| ARCH-BE-03 | [Estructura de carpetas y módulos](ARCH-BE-03.md) | TODO |
| ARCH-BE-04 | [Middleware de autenticación JWT](ARCH-BE-04.md) | TODO |
| ARCH-BE-05 | [Manejo de errores y validación](ARCH-BE-05.md) | TODO |
| ARCH-BE-06 | [Configurar Firebase FCM](ARCH-BE-06.md) | TODO |
| ARCH-BE-07 | [Configurar Supabase Storage](ARCH-BE-07.md) | TODO |

## Frontend (Expo + React Native)

| ID | Historia | Estado |
|---|---|---|
| ARCH-FE-01 | [Inicializar proyecto Expo con development build](ARCH-FE-01.md) | TODO |
| ARCH-FE-02 | [Estructura de carpetas](ARCH-FE-02.md) | TODO |
| ARCH-FE-03 | [Configurar navegación con React Navigation](ARCH-FE-03.md) | TODO |
| ARCH-FE-04 | [Configurar cliente HTTP (Axios + interceptores)](ARCH-FE-04.md) | TODO |
| ARCH-FE-05 | [Configurar estado global (Zustand + React Query)](ARCH-FE-05.md) | TODO |
| ARCH-FE-06 | [Configurar notificaciones push (Expo + Firebase)](ARCH-FE-06.md) | TODO |

---

## Orden de trabajo

```
ARCH-00
  ├── ARCH-BE-01 → ARCH-BE-02 → ARCH-BE-03 → ARCH-BE-04 → ARCH-BE-05
  │                                                       → ARCH-BE-06
  │                                        → ARCH-BE-07
  └── ARCH-FE-01 → ARCH-FE-02 → ARCH-FE-03
                              → ARCH-FE-04 → ARCH-FE-05
                              → ARCH-FE-06
```

Backend y Frontend pueden trabajarse en paralelo después de ARCH-00.
