# Stories — Index General

Cada funcionalidad tiene su propia carpeta. Dentro de cada carpeta hay un índice con el estado de sus historias.

**Estados:** `TODO` | `IN PROGRESS` | `DONE` | `BLOCKED`

---

## Funcionalidades

| Carpeta | Descripción | Estado general |
|---|---|---|
| [arquitectura/](arquitectura/) | Setup del repo, backend, frontend y servicios externos | TODO |
| `login/` | Registro, login y sesión | — |
| `onboarding/` | Wizard de configuración inicial coach y atleta | — |
| `rutinas/` | Creador de rutinas, asignación, vista del atleta | — |
| `pagos/` | Planes, comprobantes, aprobación | — |
| `comunidad/` | Feed, posts, reacciones, logros | — |
| `calendario/` | Vistas, eventos, sync externo | — |
| `notificaciones/` | Push notifications | — |
| `configuracion/` | Perfil, privacidad, ajustes | — |

> Las carpetas sin link todavía no tienen historias. Se crean cuando el cliente aprueba el producto y arranca el desarrollo de esa funcionalidad.

---

## Orden de trabajo

```
arquitectura/   ← siempre primero
    └── login/
            └── onboarding/
                    ├── rutinas/
                    ├── pagos/
                    └── comunidad/
                            └── calendario/
                                    └── notificaciones/
                                            └── configuracion/
```
