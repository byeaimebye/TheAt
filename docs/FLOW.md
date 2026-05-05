# Flujo de la Aplicación — Athletica

Diagramas de flujo completos por área. Usá estos como base para validar pantallas antes de arrancar el desarrollo.

---

## 1. Entrada y Autenticación

```mermaid
flowchart TD
    START([Abrir App]) --> SESSION{¿Tiene sesión activa?}

    SESSION -->|Sí| ROLE{Rol guardado}
    SESSION -->|No| WELCOME[Pantalla de Bienvenida\nIniciar sesión / Registrarse]

    %% Login
    WELCOME --> LOGIN[Iniciar Sesión\nemail + contraseña]
    WELCOME --> REGISTER[Registrarse]
    WELCOME --> FORGOT[¿Olvidaste tu contraseña?]

    FORGOT --> RESET[Ingresar email\nRecibir link de reset]

    LOGIN --> LOGIN_OK{¿Credenciales válidas?}
    LOGIN_OK -->|No| LOGIN_ERR[Error: email o contraseña incorrectos]
    LOGIN_ERR --> LOGIN
    LOGIN_OK -->|Sí| ONBOARDED{¿Completó onboarding?}
    ONBOARDED -->|Sí| ROLE
    ONBOARDED -->|No| ROLE_OB{Rol}
    ROLE_OB -->|Coach| WIZ_COACH
    ROLE_OB -->|Atleta| WIZ_ATH

    %% Registro
    REGISTER --> ROLE_SEL[Seleccionar Rol]
    ROLE_SEL -->|Soy Entrenador/a| REG_COACH[Formulario Coach\nnombre · email · contraseña]
    ROLE_SEL -->|Soy Atleta| REG_ATH[Formulario Atleta\nnombre · email · contraseña]

    REG_COACH --> WIZ_COACH
    REG_ATH --> QR[Ingresar código del coach\no escanear QR]
    QR --> QR_OK{¿Código válido?}
    QR_OK -->|No| QR_ERR[Error: código no encontrado]
    QR_ERR --> QR
    QR_OK -->|Sí| QR_CONFIRM[✓ Te uniste al equipo de Coach X]
    QR_CONFIRM --> WIZ_ATH

    %% Wizards de onboarding
    WIZ_COACH[Wizard Coach\n① Logo opcional\n② Deportes que ofrece\n③ Nombre de comunidad]
    WIZ_ATH[Wizard Atleta\n① Deporte principal + objetivo\n② Edad y sexo]

    WIZ_COACH --> ROLE
    WIZ_ATH --> ROLE

    ROLE -->|Coach| COACH_HOME([🏠 Coach Home])
    ROLE -->|Atleta| ATH_HOME([🏠 Atleta Home])
```

---

## 2. Flujo Coach — Navegación Principal

```mermaid
flowchart TD
    COACH_HOME([Coach Home]) --> NAV{Pestañas}

    NAV --> T1[🏠 Home]
    NAV --> T2[👥 Atletas]
    NAV --> T3[💬 Comunidad]
    NAV --> T4[📅 Calendario]
    NAV --> T5[⚙️ Configuración]

    %% HOME
    T1 --> H1[Estadísticas del negocio\natletas activos · facturación]
    T1 --> H2[Próximos entrenamientos]
    T1 --> H3[⚠️ Atletas que necesitan ayuda]
    T1 --> H4[💳 Pagos pendientes de revisión]

    %% ATLETAS
    T2 --> A1[Lista de cards de atletas]
    A1 --> A2[Card: nombre · deporte · RPE promedio\nestado de actividad · estado de pago]
    A2 -->|Toca la card| DETAIL[Perfil del atleta]

    DETAIL --> D1[📊 Actividad]
    DETAIL --> D2[💬 Chat]
    DETAIL --> D3[📋 Rutinas]
    DETAIL --> D4[💳 Pagos]

    D1 --> D1A[Últimos entrenamientos\ncompletitud + RPE + timestamp]
    D1 --> D1B[Stats: entrenamientos semana\nRPE promedio · tasa completitud]

    D2 --> D2A[Chat directo con el atleta]

    D3 --> D3A[Historial de rutinas asignadas]
    D3 --> D3B[➕ Crear nueva rutina]
    D3B --> BUILDER[Routine Builder]
    BUILDER --> B1[Nombre · fecha · deporte]
    B1 --> B2[Agregar bloques]
    B2 --> B3[Agregar ejercicios por bloque\nseries · reps · descanso · carga · notas]
    B3 --> B4[Adjuntar archivo opcional]
    B4 --> B5[Asignar a atleta/s o grupo]
    B5 --> B6[✓ Notificación push al atleta]

    D4 --> D4A[Historial de pagos del atleta]
    D4A --> D4B{¿Hay pago pendiente?}
    D4B -->|Sí| D4C[Ver comprobante a pantalla completa]
    D4C --> D4D{Aprobar o Rechazar}
    D4D -->|Aprobar| D4E[✓ Pago aprobado\nNotificación al atleta]
    D4D -->|Rechazar| D4F[Ingresar nota de rechazo\nNotificación al atleta]

    %% COMUNIDAD
    T3 --> C1[Feed de la comunidad]
    C1 --> C2[Posts del coach\nreacciones · comentarios]
    C1 --> C3[➕ Crear nuevo post\ntexto + hasta 3 imágenes]
    C1 --> C4[Logros sugeridos de atletas\npara destacar]

    %% CALENDARIO
    T4 --> CAL1[Vista mensual / semanal]
    CAL1 -->|Toca un día| CAL2[Lista de ítems del día\nrutinas · eventos]
    CAL1 --> CAL3[➕ Crear nuevo evento]
    CAL3 --> CAL4[Título · fecha · hora · descripción\nubicación texto · tipo]
    CAL2 -->|Toca un ítem| CAL5[Detalle del evento\nlista de asistentes]

    %% CONFIGURACIÓN
    T5 --> CFG1[Perfil: nombre · logo]
    T5 --> CFG2[Planes de suscripción para atletas]
    T5 --> CFG3[Configuración de comunidad\nmodo · deportes · permisos atletas]
    T5 --> CFG4[Notificaciones]
    T5 --> CFG5[Idioma]
    T5 --> CFG6[Cuenta: cambiar contraseña · cerrar sesión · eliminar]
```

---

## 3. Flujo Atleta — Navegación Principal

```mermaid
flowchart TD
    ATH_HOME([Atleta Home]) --> NAV{Pestañas}

    NAV --> T1[🏠 Home]
    NAV --> T2[🎽 Coach]
    NAV --> T3[📅 Calendario]
    NAV --> T4[💬 Comunidad]
    NAV --> T5[⚙️ Configuración]

    %% HOME
    T1 --> H1[Estadísticas generales por deporte]
    T1 --> H2[Próximos entrenamientos]
    T1 --> H3[⚠️ Alerta de pago pendiente al coach]
    T1 --> H4[Notificaciones de la comunidad]

    %% COACH TAB
    T2 --> C_INFO[Info del coach: nombre · logo]
    T2 --> C_CHAT[💬 Chat directo con el coach]
    T2 --> C_ROUTINES[📋 Rutinas]
    T2 --> C_PAY[💳 Pagos]

    C_ROUTINES --> CR1{¿Hay rutinas asignadas?}
    CR1 -->|No| CR_EMPTY[Estado vacío:\nTu coach no te asignó rutinas aún]
    CR1 -->|Sí| CR2[Lista de rutinas por fecha]
    CR2 -->|Toca una rutina| ROUTINE[Detalle de Rutina]

    ROUTINE --> R1[Bloques y ejercicios\nseries · reps · carga · notas]
    ROUTINE --> R2[Tildar ejercicios completados]
    ROUTINE --> R3{¿Todos los ejercicios atendidos?}
    R3 -->|Sí| R4[Botón: Terminar Entrenamiento]
    R4 --> RPE[Modal de RPE\nEscala 1–10 + comentario opcional]
    RPE --> RPE_SEND[✓ Feedback enviado\nNotificación push al coach]

    C_PAY --> P1[Estado de pago actual\nmonto del plan · estado]
    C_PAY --> P2[Historial de pagos]
    P1 --> P3[➕ Registrar Pago]
    P3 --> P4[Subir comprobante\ncámara o galería]
    P4 --> P5[Ingresar monto pagado]
    P5 --> P6[Nota opcional]
    P6 --> P7[✓ Enviado al coach\nNotificación push al coach]

    %% Compartir desde app externa
    SHARE_EXT([Compartir desde app del banco]) --> P_MODAL[Se abre modal de pago\ncon imagen pre-cargada]
    P_MODAL --> P5

    %% CALENDARIO
    T3 --> CAL1[Vista mensual / semanal]
    CAL1 -->|Toca un día| CAL2[Lista del día:\nrutinas asignadas · eventos]
    CAL2 -->|Toca rutina| ROUTINE
    CAL2 -->|Toca evento| CAL3[Detalle del evento\nasistentes · sumarse]
    CAL3 --> CAL4[✓ Me anoto\nNotificación si un amigo también se anota]

    %% COMUNIDAD
    T4 --> COM1[Feed del coach\nposts · logros · eventos]
    COM1 --> COM2[Reaccionar a un post 👍]
    COM1 --> COM3[Comentar un post]
    COM1 --> COM4[Ver lista de miembros de la comunidad]
    COM4 -->|Toca un atleta| COM5[Perfil del atleta:\ninfo · últimos eventos · próximos eventos]

    %% CONFIGURACIÓN
    T5 --> CFG1[Perfil: nombre · foto]
    T5 --> CFG2[Privacidad:\nno ser destacado en el feed\nno compartir logros]
    T5 --> CFG3[Notificaciones]
    T5 --> CFG4[Idioma]
    T5 --> CFG6[Cuenta: contraseña · cerrar sesión · eliminar]
```

---

## 4. Flujo de Pago — Completo (Coach + Atleta)

```mermaid
flowchart TD
    A([Coach configura plan]) --> B[Configuración → Suscripciones\ncrear plan: nombre · precio · período]
    B --> C[Asignar plan al atleta]

    C --> D([Atleta debe pagar])
    D --> E{¿Cómo paga?}

    E -->|Desde Athletica| F[Pestaña Coach → Pagos\ntocar Registrar Pago]
    E -->|Desde app del banco| G[Transferencia en app bancaria\ncompartir comprobante → Athletica]

    G --> H[Se abre Athletica con\ncomprobante pre-cargado]
    F --> I[Subir comprobante\ncámara o galería]
    H --> J[Ingresar monto + nota opcional]
    I --> J

    J --> K[✓ Pago registrado\nestado: PENDIENTE DE REVISIÓN]
    K --> L[🔔 Notificación push al coach]

    L --> M([Coach recibe notificación])
    M --> N[Pestaña Atletas → card con badge de pago]
    N --> O[Abrir perfil del atleta → Pagos]
    O --> P[Ver comprobante a pantalla completa]

    P --> Q{¿Qué decide el coach?}

    Q -->|Aprobar| R[✓ Estado: APROBADO]
    Q -->|Rechazar| S[Escribir nota de rechazo\n→ Estado: RECHAZADO]

    R --> T[🔔 Notificación al atleta: Pago confirmado ✓]
    S --> U[🔔 Notificación al atleta: Tu pago necesita revisión]
    U --> V[Atleta puede volver a registrar un nuevo pago]
```

---

## 5. Estados Vacíos — Día 1 Post-Onboarding

Este es el estado de la app cuando el coach y el atleta se acaban de unir y no hay datos aún.

```mermaid
flowchart TD
    subgraph COACH [Coach — Día 1]
        CH[Home] --> CH1[Stats en cero\n0 atletas activos · sin facturación]
        CH --> CH2[Sin próximos entrenamientos]
        CA[Atletas] --> CA1[Card del atleta recién unido\nsin RPE · sin rutinas · sin pagos]
        CA1 --> CA2[Perfil del atleta]
        CA2 --> CA3[Actividad: vacío\nTodavía no hay entrenamientos]
        CA2 --> CA4[Chat: vacío · puede escribirle]
        CA2 --> CA5[Rutinas: vacío\n➕ Crear primera rutina]
        CA2 --> CA6[Pagos: sin historial\nAsignar plan]
    end

    subgraph ATLETA [Atleta — Día 1]
        AH[Home] --> AH1[Stats vacías]
        AH --> AH2[Sin próximos entrenamientos]
        AC[Coach] --> AC1[Info del coach: nombre + logo]
        AC --> AC2[Chat: vacío · puede escribirle]
        AC --> AC3[Rutinas: vacío\nTu coach no te asignó rutinas aún]
        AC --> AC4[Pagos: muestra el plan asignado\nsin historial de pagos]
    end
```
