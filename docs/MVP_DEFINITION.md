# Definición del MVP — Athletica

## Qué debe demostrar el MVP

1. Un coach puede registrarse, configurar su perfil y generar un código de invitación
2. Un coach puede crear rutinas estructuradas y asignarlas a sus atletas
3. Un atleta puede ver sus rutinas, registrar entrenamientos y enviar feedback de RPE
4. El flujo de pago manual (carga del comprobante + aprobación del coach) funciona de punta a punta
5. Un feed de comunidad básico mantiene a los atletas comprometidos
6. Un calendario compartido ayuda a planificar y hacer seguimiento de las sesiones
7. Las notificaciones push fomentan la re-apertura de la app

---

## Priorización de Features del MVP

### ALTA PRIORIDAD — Debe estar en v1

Estos features forman el ciclo central: el coach gestiona → el atleta entrena → el feedback vuelve al coach.

| Feature | Justificación |
|---|---|
| Login con email/contraseña y selección de rol | Puerta de entrada — nada funciona sin identidad |
| Onboarding del coach (perfil, logo, generación de QR) | El coach debe estar configurado antes de que los atletas puedan unirse |
| Onboarding del atleta mediante QR o código de invitación | Mecanismo principal de adquisición de usuarios |
| Configuración inicial (deporte, objetivo, edad, sexo) | Personaliza la experiencia; necesario para el contexto del RPE |
| Creador de rutinas (individual) | Valor central del coach — crear entrenamientos estructurados |
| Biblioteca de ejercicios (agrupada por tipo de deporte) | Necesaria para el creador de rutinas |
| Asignación de rutina a atleta | Conecta el trabajo del coach con la ejecución del atleta |
| Vista de rutina para el atleta | El atleta debe saber qué tiene que hacer |
| Registro de completitud del entrenamiento | Mide la adherencia |
| Feedback de RPE al terminar el entrenamiento | Ciclo de datos clave — el coach ve el esfuerzo y ajusta el plan |
| El coach ve el rendimiento e historial del atleta | Cierra el ciclo de feedback del entrenamiento |
| El coach configura los planes de suscripción del atleta | Necesario para el seguimiento de facturación |
| El atleta sube el comprobante bancario + monto manual | Único método de pago en el MVP |
| Compartir comprobante desde otra app (intent de Android / Share Extension iOS) | UX clave — el atleta comparte el comprobante desde la app del banco |
| El coach revisa y aprueba/rechaza el pago | Lado del coach en el flujo de pagos |
| Historial de pagos por atleta | Vista administrativa del coach |
| Estado del pago en la card del atleta | Visibilidad rápida |
| Notificaciones push (nueva rutina, pago, eventos) | Motor principal de engagement |
| Barra de navegación inferior (específica por rol) | Base para toda la navegación |

### PRIORIDAD MEDIA — Debería estar en v1 pero se puede recortar

Estos features completan la experiencia del MVP, pero el ciclo central funciona sin ellos.

| Feature | Justificación |
|---|---|
| Wizard de onboarding guiado (coach) | Mejora la activación; se puede simplificar la UI inicialmente |
| Creador de rutinas — grupal (1:N) | Necesario para coaches con equipos; puede ir en v1.1 si hay restricciones de tiempo |
| Bloques de entrenamiento + observaciones por bloque | Mejora la calidad de la rutina, pero las rutinas funcionan sin bloques |
| Adjuntar archivo a la rutina | Útil pero no bloquea el flujo de entrenamiento |
| Feed de comunidad del coach (broadcast) | Feature clave de retención; puede lanzarse con funcionalidad limitada |
| Posts del coach (texto + imagen) | La comunidad necesita al menos un tipo de contenido |
| Reacciones y comentarios de atletas | Engagement básico; solo comentarios es suficiente para MVP |
| Generación de badges de logros | Feature motivacional; se puede lanzar sin él si es necesario |
| Calendario in-app (vista semanal + mensual) | Importante para la planificación; la vista mensual puede diferirse |
| El coach crea eventos de calendario | Necesario para sesiones grupales |
| Sincronización con calendario externo (Google/Apple/Outlook) | Se puede diferir a v1.1 si es un bloqueante |
| Detalle de evento con lista de asistentes | Útil; mínimo: título del evento + fecha |
| Configuración general (idioma, notificaciones) | UX importante; config de notificaciones es la más prioritaria |
| Configuración de suscripciones del coach (planes + precios) | Necesaria para validar pagos |
| Privacidad de la comunidad (atleta puede optar por no ser destacado) | Requerido en el spec, relevante para privacidad |

### BAJA PRIORIDAD — Post-MVP / v2

Son valiosos pero no necesarios para validar la propuesta central.

| Feature | Justificación |
|---|---|
| Login social (Google/Apple) | Agradable de tener; email/contraseña cubre el auth del MVP |
| Rutinas grupales — visibilidad del progreso entre atletas | Agrega complejidad; visibilidad solo para el coach es suficiente |
| Imágenes de ejercicios paso a paso | Complejidad de gestión de contenido |
| Videos explicativos de ejercicios | Costo de storage y bandwidth |
| Plantillas de rutinas previas | Mejora de productividad; no es core |
| Filtros de calendario por tipo/fuente | Mejora de UI |
| Propuesta de actividades por miembros de la comunidad | Flujo de moderación complejo |
| Grupos/clústers del coach con sub-feed | Complejidad; un feed de comunidad único cubre el MVP |
| Feed público entre comunidades | Nueva superficie de producto; completamente post-MVP |
| Compartir actividades en redes externas (Instagram/TikTok) | Feature de marketing; no es core del producto |
| Asistente de IA en el chat | Explícitamente post-MVP (RINT-005) |
| Generación de rutinas con IA | Explícitamente post-MVP |
| Lectura OCR del monto del comprobante | Dependencia de IA/ML; post-MVP |
| Pasarela de pagos automatizada | Complejidad de arquitectura + legal; post-MVP |
| Billetera digital | Producto financiero; requiere consideraciones regulatorias |
| Paleta de colores personalizable (white-label) | Trabajo de sistema de diseño; solo logo en MVP |
| Nombre e ícono de app personalizado (white-label) | Requiere builds por coach; distribución compleja |
| Integración con Google Maps | Post-MVP (RINT-002) |
| Conectividad con smartwatches | Post-MVP (RINT-001) |
| Sincronización bidireccional de calendario | Complejidad de ingeniería; post-MVP |
| Módulos de nutrición y seguimiento médico | Superficie de producto completamente separada |
| Dashboard de analíticas avanzadas | Post-MVP |
| Pool de coaches / coaches referidos | Feature de crecimiento; no es MVP |

---

## Resumen del Alcance del MVP

**Dos usuarios. Una plataforma. Tres flujos críticos.**

### Flujo Crítico 1: Ciclo de Entrenamiento
```
El coach crea una rutina → La asigna al atleta → El atleta la ve y la registra →
El atleta envía el RPE → El coach ve los datos de rendimiento
```

### Flujo Crítico 2: Ciclo de Pago
```
El coach configura el plan → El atleta debe pagar → El atleta transfiere y sube el comprobante →
El coach recibe la notificación → El coach aprueba o rechaza
```

### Flujo Crítico 3: Ciclo de Comunidad
```
El coach publica en el feed → Los atletas reciben la notificación →
Los atletas reaccionan/comentan → El sistema genera un badge de logro → El coach lo destaca
```

---

## Lo que el MVP NO incluye

Para ser explícitos y estar alineados con los stakeholders:

- Ninguna funcionalidad de IA
- Ningún procesamiento de pagos automatizado
- Sin Google Maps
- Sin integración con smartwatches
- Sin personalización de la app (colores/nombre/ícono) — solo carga de logo
- Sin sincronización bidireccional de calendario
- Sin feed público entre comunidades
- Sin seguimiento de nutrición o datos médicos
- Sin lectura automática de comprobantes
- Sin login social
- Sin biblioteca de videos de ejercicios

---

## Definición de "Listo" para el MVP

El MVP está listo para lanzar cuando:
- [ ] Un coach puede completar el onboarding completo sin ayuda externa
- [ ] Un atleta puede unirse a su coach via QR/código sin ayuda externa
- [ ] Un coach puede crear y asignar una rutina a un atleta específico
- [ ] Un atleta puede ver la rutina, marcarla como completada y enviar el RPE
- [ ] Un atleta puede subir un comprobante bancario y registrar un pago
- [ ] Un coach puede recibir la notificación de pago y aprobarlo
- [ ] Un coach puede publicar en el feed de la comunidad y los atletas lo ven con reacciones
- [ ] Todas las notificaciones push clave se disparan correctamente
- [ ] La app corre en Android (emulador + dispositivo físico) e iOS Simulator sin crashes
- [ ] Todos los criterios de aceptación de las historias de ALTA prioridad están aprobados
