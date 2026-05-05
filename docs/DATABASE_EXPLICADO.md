# Base de Datos Explicada — Para Humanos

Esto explica cómo están relacionadas las tablas de Athletica en lenguaje simple.
Sin código, sin SQL, sin jerga técnica.

---

## La idea central

La base de datos es como un conjunto de listas que se conectan entre sí.
Cada tabla es una lista. Cada fila es un elemento de esa lista.
Las relaciones son las conexiones entre listas.

---

## Usuarios

```
Un USUARIO puede ser Coach o Atleta.
Eso se define con un campo "rol".

Si es Coach  → tiene un PERFIL DE COACH  (logo, nombre de comunidad, código QR)
Si es Atleta → tiene un PERFIL DE ATLETA (deporte, objetivo, edad, sexo)

Un Atleta pertenece a UN solo Coach.
Un Coach puede tener MUCHOS Atletas.
```

---

## Entrenamiento

```
Un COACH crea RUTINAS.
  Una Rutina tiene un nombre, una fecha objetivo y un deporte.

Dentro de cada Rutina hay BLOQUES.
  Ejemplos de bloques: "Entrada en calor", "Trabajo principal", "Vuelta a la calma"

Dentro de cada Bloque hay EJERCICIOS.
  Cada ejercicio tiene: series, reps, descanso, carga, notas.
  Los ejercicios vienen de la BIBLIOTECA DE EJERCICIOS.

Cuando el Coach termina de armar la Rutina, la ASIGNA a uno o más Atletas.
  Eso crea una ASIGNACIÓN DE RUTINA por cada atleta.
  → Coach asigna a 5 atletas = 5 asignaciones separadas.

Cuando el Atleta abre su Rutina y empieza a entrenar,
  se crea un REGISTRO DE ENTRENAMIENTO (WorkoutLog).
  Ahí se guarda: cuándo empezó, cuándo terminó, qué ejercicios completó.

Al terminar, el Atleta envía su RPE (percepción de esfuerzo del 1 al 10).
  Ese número se guarda dentro del mismo Registro de Entrenamiento.
```

---

## Pagos

```
El COACH define sus PLANES DE SUSCRIPCIÓN.
  Ejemplos: "Plan mensual $5000", "Plan semanal $1500"

A cada Atleta se le asigna UN plan.
  Eso es la SUSCRIPCIÓN DEL ATLETA.
  Dice: "este atleta está en el plan mensual desde tal fecha"

Cuando el Atleta transfiere la plata y sube el comprobante,
  se crea un REGISTRO DE PAGO.
  Guarda: monto, imagen del comprobante, estado.

El estado del pago puede ser:
  → PENDIENTE DE REVISIÓN  (el atleta subió el comprobante, el coach no revisó)
  → APROBADO               (el coach confirmó que recibió el pago)
  → RECHAZADO              (el coach dice que algo está mal)

El Registro de Pago referencia la Suscripción
  para saber a qué plan corresponde ese pago.
```

---

## Comunidad

```
Cada COACH tiene UNA COMUNIDAD.
  Es su espacio cerrado donde solo están sus atletas.

Dentro de la Comunidad, el Coach (y opcionalmente los atletas) publican POSTS.
  Un Post puede tener texto e imágenes.

Los Atletas pueden REACCIONAR a un Post (👍).
  Cada reacción guarda quién reaccionó y a qué post.

Los Atletas pueden COMENTAR un Post.
  Cada comentario guarda quién escribió, qué escribió y cuándo.

Cuando un Atleta cumple un hito de entrenamiento,
  el sistema genera un LOGRO (Achievement).
  Ejemplos de hitos: "Primer entrenamiento", "10 entrenamientos completados"
  
  Si el atleta no optó por privacidad,
  ese Logro genera automáticamente un Post en la Comunidad.
```

---

## Calendario

```
El COACH crea EVENTOS en el calendario.
  Un Evento tiene: título, fecha, hora, descripción, lugar (texto libre).

Los Atletas pueden SUMARSE a un Evento.
  Eso crea un registro de ASISTENTE con su estado:
  → VOY / TALVEZ / NO VOY

Además de los Eventos, en el calendario del Atleta también aparecen
  sus RUTINAS ASIGNADAS organizadas por fecha.
  Así ve en un solo lugar: "el lunes tengo rutina de fuerza y el miércoles hay una clase grupal"
```

---

## Notificaciones

```
Cuando el usuario instala la app, el dispositivo genera un TOKEN PUSH.
  Ese token es como la "dirección" a la que se mandan las notificaciones.
  Se guarda en la tabla DISPOSITIVO DEL USUARIO.

Un usuario puede tener varios dispositivos (celular + tablet).
  Por eso la relación es: un Usuario → muchos Dispositivos.

Cuando pasa algo importante en la app (nuevo pago, nueva rutina, etc.),
  el sistema busca los tokens del destinatario
  y les manda la notificación.
```

---

## Resumen de una línea por tabla

| Tabla | Qué guarda |
|---|---|
| USER | Todos los usuarios (coaches y atletas) |
| COACH_PROFILE | Datos específicos del coach (logo, QR, deportes) |
| ATHLETE_PROFILE | Datos específicos del atleta (deporte, objetivo, a qué coach pertenece) |
| ATHLETE_GROUP | Grupos de atletas creados por el coach |
| EXERCISE | Biblioteca de ejercicios (globales + personalizados) |
| ROUTINE | Rutinas de entrenamiento creadas por el coach |
| ROUTINE_BLOCK | Bloques dentro de una rutina |
| ROUTINE_EXERCISE | Ejercicios dentro de un bloque, con sus parámetros |
| ROUTINE_ASSIGNMENT | Qué atleta recibió qué rutina |
| WORKOUT_LOG | El registro de cuando un atleta hizo un entrenamiento + RPE |
| WORKOUT_EXERCISE_LOG | Qué ejercicios específicos completó en ese entrenamiento |
| COACH_PLAN | Planes de suscripción que el coach ofrece a sus atletas |
| ATHLETE_SUBSCRIPTION | Qué plan tiene cada atleta |
| PAYMENT_RECORD | Cada pago que un atleta registró con su comprobante |
| COMMUNITY | La comunidad de cada coach (configuración y modo) |
| POST | Posts publicados en la comunidad |
| REACTION | Reacciones (👍) a los posts |
| COMMENT | Comentarios en los posts |
| ACHIEVEMENT | Logros ganados por atletas |
| CALENDAR_EVENT | Eventos del calendario creados por el coach |
| EVENT_ATTENDEE | Quién se anotó a cada evento |
| USER_DEVICE | Tokens push de cada dispositivo del usuario |
| ATHLETE_FOLLOW | Qué atletas siguen a otros atletas |
