# Análisis de Producto — Athletica

## Propuesta de Valor Central

Athletica es una plataforma de gestión deportiva B2B2C que conecta a los coaches con sus atletas a través de una única app mobile. Los coaches disponen de una herramienta profesional para planificar entrenamientos, hacer seguimiento del rendimiento, gestionar cobros y animar a su comunidad. Los atletas acceden a una experiencia de entrenamiento estructurada, con accountability, motivación social y comunicación directa con su coach.

La plataforma se monetiza mediante suscripciones escalonadas para coaches, siendo los atletas usuarios gratuitos que se unen a través del código de invitación de su coach.

---

## Problema que Resuelve

Los coaches independientes y las academias deportivas pequeñas gestionan a sus atletas con herramientas dispersas: WhatsApp para comunicarse, planillas para las rutinas, transferencias bancarias rastreadas a mano y sin datos estructurados de rendimiento.

Athletica consolida la planificación del entrenamiento, el seguimiento de pagos, el engagement de la comunidad y el progreso del atleta en una sola plataforma — reduciendo la carga administrativa del coach y mejorando la retención del atleta a través de la accountability social.

---

## Usuarios Objetivo

### Primario (cliente que paga)
**Coach** — entrenador personal independiente, coach deportivo, o dueño de una academia pequeña que gestiona entre 1 y 150+ atletas. Deportes: Running, CrossFit, Funcional/Gym, Triatlón, Entrenamiento Personalizado.

El coach paga una suscripción mensual escalonada según el tamaño de su plantel:
- 0–5 atletas: Gratis
- 6–40 atletas: Tier 1
- 41–100 atletas: Tier 2
- 101–150 atletas: Tier 3
- 150+ atletas: Enterprise (ventas)

### Secundario (usuario final)
**Atleta** — se une a través de la invitación del coach. Accede a rutinas estructuradas, registra sus entrenamientos y participa en la comunidad. El uso es gratuito; el valor está en la experiencia de entrenamiento que le brinda su coach.

---

## Mapa de Features

### Autenticación y Onboarding

| Feature | Requerimiento | MVP |
|---|---|---|
| Selección de rol al registrarse (Coach / Atleta) | RFG-001, RFG-002 | Sí |
| Login con email + contraseña | RFG-008 | Sí |
| Login social (Google, Apple) | RFG-009 | No |
| Recuperación de contraseña | — | Sí |
| Configuración inicial (deporte, objetivo, edad, sexo) | RFG-010, RFG-011 | Sí |
| Perfil del coach (nombre, logo, negocio) | RFC-002 | Sí |
| El atleta se une via QR o código de invitación | RFG-003 | Sí |
| Generación del QR/código del coach | RFG-003 | Sí |
| Flujo de onboarding guiado | HU-04, HU-05 | Sí |

### Entrenamiento

| Feature | Requerimiento | MVP |
|---|---|---|
| Creador de rutinas — individual (1:1) | RFC-021–027, HU-06 | Sí |
| Creador de rutinas — grupal (1:N) | HU-07 | Sí |
| Biblioteca de ejercicios (árbol por tipo) | RFC-021 | Sí |
| Bloques + observaciones por ejercicio | RFC-026, RFC-027 | Sí |
| Adjuntar archivo a la rutina | RFC-024 | Sí |
| Asignar rutina a atleta o grupo | RFC-018 | Sí |
| El atleta ve sus rutinas asignadas | RFA-010, HU-08 | Sí |
| El atleta registra la completitud del entrenamiento | RFA-003 | Sí |
| El atleta envía feedback de RPE post-entrenamiento | HU-09 | Sí |
| El coach ve el rendimiento e historial del atleta | RFC-015, RFC-019 | Sí |
| Detalle del entrenamiento con estadísticas | RFA-003 | Sí |
| Imágenes de ejercicios (paso a paso) | RFC-022 | No |
| Videos explicativos de ejercicios | RFC-023 | No |
| Plantillas de rutinas previas | RFC-020 | No |
| Sugerencias de rutinas con IA | RINT-005, RFC-028 | No |
| Integración con datos de smartwatch | RINT-001 | No |

### Pagos

| Feature | Requerimiento | MVP |
|---|---|---|
| El coach configura planes de suscripción para atletas | RFC-050 | Sí |
| El atleta ve su pago pendiente | RFA-006, RFA-013 | Sí |
| El atleta sube comprobante de transferencia bancaria | RFA-014, HU-01 | Sí |
| El atleta ingresa el monto pagado manualmente | RFA-014 | Sí |
| Compartir comprobante desde otra app (intent/share extension) | RFA-015, RFA-016 | Sí |
| El coach recibe notificación de pago | RFC-008, HU-03 | Sí |
| El coach visualiza el comprobante y aprueba o rechaza | RFC-030, RFC-031, HU-03 | Sí |
| El coach ve el historial de pagos por atleta | RFC-029 | Sí |
| Estado de pago en la card del atleta | RFC-011, RFC-014 | Sí |
| Pasarela de pagos automatizada (MercadoPago, etc.) | RINT-004, RFC-032 | No |
| Extracción automática del monto por OCR | — | No |
| Billetera digital | — | No |

### Comunidad

| Feature | Requerimiento | MVP |
|---|---|---|
| Espacio de comunidad del coach (cerrado, administrado por el coach) | RFC-039, HU-10 | Sí |
| El coach publica contenido (broadcast) | RFC-040, HU-11 | Sí |
| Los atletas ven el feed de la comunidad | RFA-024, HU-14 | Sí |
| Los atletas publican en la comunidad | RFA-025 | Sí |
| Los atletas siguen a otros atletas (dentro de la comunidad) | RFA-026, HU-13 | Sí |
| Compartir entrenamiento en el feed interno | RFA-027, HU-14 | Sí |
| Sistema de badges de logros | RFG-010, HU-16 | Sí |
| Configuración de reglas de la comunidad por el coach | RFC-043, HU-17 | Sí |
| El atleta comparte actividad en redes externas | HU-15 | Sí |
| Reacciones (me gusta) a posts | RFC-041 | Sí |
| Comentarios en posts | RFC-042 | Sí |
| Feed público entre comunidades (estilo Strava global) | — | No |
| El atleta propone posts al feed del coach | RFA-021 | No (ambiguo) |
| Selector de feed público / del coach | RFC-038 | No |

### Calendario

| Feature | Requerimiento | MVP |
|---|---|---|
| Calendario in-app — vista semanal + mensual | RFC-039, RFA-022 | Sí |
| El coach crea eventos/sesiones | RFC-043, RFC-040 | Sí |
| El atleta ve sus rutinas programadas por día | RFA-023 | Sí |
| El atleta ve el historial de entrenamientos completados | RFA-024 | Sí |
| Detalle del evento con lista de asistentes | RFC-046, RFA-027 | Sí |
| Filtro del calendario por tipo/fuente | RFC-042, RFC-047 | Sí |
| Sincronización unidireccional con Google/Apple/Outlook | RINT-003 | Sí |
| Actividades propuestas por la comunidad (aprobadas por el coach) | RFC-040, RFC-041 | Sí |
| Notificación cuando un amigo se suma a una actividad | RFA-028 | Sí |
| Sincronización bidireccional con calendario externo | — | No |
| Integración con Google Maps para ubicación de eventos | RINT-002 | No |

### Configuración

| Feature | Requerimiento | MVP |
|---|---|---|
| Configuración general (idioma, notificaciones, login) | RFC-048 | Sí |
| Configuración de planes de suscripción del coach | RFC-049, RFC-050 | Sí |
| Configuración de la comunidad (permisos, deportes) | RFC-051, RFC-054, RFC-055 | Sí |
| Carga del logo | RFC-002 | Sí |
| Preferencias de notificaciones (coach + atleta) | RFC-048 | Sí |
| Paleta de colores / theming white-label | RFC-001 | No |
| Nombre e ícono de la app white-label | RFG-005, RFG-006 | No |
| Pool de coaches / coaches referidos | RFA-030 | No |

---

## Ambigüedades y Riesgos

### Severidad Alta

**1. Disparador del RPE**
El spec no define cuándo aparece el prompt de RPE. Dos opciones:
- (A) Se dispara cuando el atleta toca "Terminar entrenamiento" en la app — más simple, recomendada para MVP
- (B) Notificación basada en tiempo, después de la duración estimada del entrenamiento — requiere lógica de notificaciones programadas

**Recomendación:** Opción A para MVP. Documentar explícitamente.

**2. Ingreso del monto del pago**
Cuando el atleta sube el comprobante, no está claro si el monto es:
- Ingresado manualmente por el atleta
- Pre-completado a partir del plan configurado por el coach
- Extraído automáticamente del comprobante por OCR

El OCR es una dependencia de IA/ML considerable — demasiado complejo para el MVP.

**Recomendación:** El atleta ingresa el monto manualmente. El monto del plan del coach se muestra como referencia.

**3. Arquitectura del modelo de suscripción doble**
Existen DOS sistemas de suscripción:
- Athletica le cobra al coach (Gratis, Tier 1–3, Enterprise)
- El coach configura lo que les cobra a sus atletas (planes personalizados)

Son relaciones de facturación separadas. El modelo de datos debe distinguir claramente `platformSubscription` (coach→Athletica) de `coachPlan` (atleta→coach). Esto debe resolverse antes de diseñar el schema del backend.

### Severidad Media

**4. Dirección de la sincronización de calendario**
RINT-003 (API de Calendario) es MVP pero no especifica si es unidireccional o bidireccional.
**Recomendación:** Solo exportación desde la app hacia el calendario externo para MVP.

**5. Rutinas grupales — visibilidad entre atletas**
Cuando se asigna una rutina grupal, no está especificado si los atletas pueden ver el progreso de sus compañeros.
**Recomendación:** Visibilidad solo para el coach en MVP.

**6. Contradicción en el alcance del white-label**
RFC-002 (carga de logo) es MVP. RFC-001 (paleta de colores) no lo es. Esto genera una experiencia de white-label incompleta en v1.
**Recomendación:** Solo logo en MVP. Documentarlo explícitamente para gestionar las expectativas del cliente.

**7. Features de IA en el MVP**
RINT-005 (API de IA/GPT) no es MVP, pero RFC-017 menciona IA en el contexto del chat de coaching.
**Recomendación:** Tratar todas las funcionalidades de IA como post-MVP. Consultar con el product owner sobre RFC-017.

### Severidad Baja

**8. Código QR — estático vs dinámico**
Un QR estático por coach es más simple. Los códigos dinámicos con expiración son más seguros.
**Recomendación:** QR estático por coach para MVP.

**9. Matriz de triggers de notificaciones no definida**
El spec marca las notificaciones push como MVP (RS-002) pero no enumera todos los eventos disparadores.
**Recomendación:** Definir la matriz de notificaciones antes de implementar el Stage 11. Ya está documentada en el [EXECUTION_PLAN.md](EXECUTION_PLAN.md).

**10. Infraestructura del backend**
No se especifica proveedor de cloud. No es un bloqueante para el desarrollo, pero debe decidirse antes del entorno de staging.
**Recomendación:** Railway o Render para staging. Documentar en un ADR.
