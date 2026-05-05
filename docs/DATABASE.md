# Base de Datos — Athletica

Esquema de tablas y relaciones dividido por área. Es un modelo conceptual — los tipos exactos se definen cuando se arranque el desarrollo.

---

## 1. Usuarios y Perfiles

```mermaid
erDiagram
    USER {
        uuid id PK
        string name
        string email
        string password_hash
        enum role "COACH | ATHLETE"
        boolean has_completed_onboarding
        timestamp created_at
        timestamp deleted_at
    }

    COACH_PROFILE {
        uuid id PK
        uuid user_id FK
        string display_name
        string logo_url
        string invite_code "único por coach"
        string[] sports
    }

    ATHLETE_PROFILE {
        uuid id PK
        uuid user_id FK
        uuid coach_id FK
        string sport
        string goal
        int age
        string sex
        boolean allow_highlights
        boolean allow_public_achievements
    }

    ATHLETE_FOLLOW {
        uuid follower_id FK
        uuid following_id FK
        timestamp created_at
    }

    USER_DEVICE {
        uuid id PK
        uuid user_id FK
        string push_token
        string platform "ios | android"
    }

    USER ||--|| COACH_PROFILE : "tiene"
    USER ||--|| ATHLETE_PROFILE : "tiene"
    USER ||--o{ USER_DEVICE : "tiene"
    USER ||--o{ ATHLETE_FOLLOW : "sigue a otros"
    ATHLETE_PROFILE }o--|| COACH_PROFILE : "pertenece a"
```

---

## 2. Entrenamiento

```mermaid
erDiagram
    ATHLETE_GROUP {
        uuid id PK
        uuid coach_id FK
        string name
        string description
    }

    ATHLETE_GROUP_MEMBER {
        uuid group_id FK
        uuid athlete_id FK
    }

    EXERCISE {
        uuid id PK
        uuid coach_id FK "null = ejercicio global"
        string name
        string description
        string category
        string sport
        string image_url
    }

    ROUTINE {
        uuid id PK
        uuid coach_id FK
        string name
        date target_date
        string sport
        string file_url
    }

    ROUTINE_BLOCK {
        uuid id PK
        uuid routine_id FK
        string name
        string observation
        int order
    }

    ROUTINE_EXERCISE {
        uuid id PK
        uuid block_id FK
        uuid exercise_id FK
        int sets
        int reps
        int duration_seconds
        int rest_seconds
        string load
        string notes
        int order
    }

    ROUTINE_ASSIGNMENT {
        uuid id PK
        uuid routine_id FK
        uuid athlete_id FK
        timestamp assigned_at
    }

    WORKOUT_LOG {
        uuid id PK
        uuid assignment_id FK
        uuid athlete_id FK
        timestamp started_at
        timestamp completed_at
        enum status "PENDING | IN_PROGRESS | COMPLETED"
        int rpe "1 a 10"
        string rpe_comment
        timestamp feedback_at
    }

    WORKOUT_EXERCISE_LOG {
        uuid id PK
        uuid workout_log_id FK
        uuid routine_exercise_id FK
        int completed_sets
        string notes
        timestamp completed_at
    }

    ATHLETE_GROUP ||--o{ ATHLETE_GROUP_MEMBER : "tiene"
    EXERCISE ||--o{ ROUTINE_EXERCISE : "se usa en"
    ROUTINE ||--o{ ROUTINE_BLOCK : "tiene"
    ROUTINE ||--o{ ROUTINE_ASSIGNMENT : "se asigna via"
    ROUTINE_BLOCK ||--o{ ROUTINE_EXERCISE : "contiene"
    ROUTINE_ASSIGNMENT ||--o{ WORKOUT_LOG : "genera"
    WORKOUT_LOG ||--o{ WORKOUT_EXERCISE_LOG : "tiene"
    ROUTINE_EXERCISE ||--o{ WORKOUT_EXERCISE_LOG : "se registra en"
```

---

## 3. Pagos

```mermaid
erDiagram
    COACH_PLAN {
        uuid id PK
        uuid coach_id FK
        string name
        decimal price
        string currency
        enum billing_period "MONTHLY | WEEKLY | PER_SESSION"
    }

    ATHLETE_SUBSCRIPTION {
        uuid id PK
        uuid athlete_id FK
        uuid coach_id FK
        uuid plan_id FK
        date start_date
        enum status "ACTIVE | PAUSED | CANCELLED"
    }

    PAYMENT_RECORD {
        uuid id PK
        uuid athlete_id FK
        uuid coach_id FK
        decimal amount
        string currency
        string receipt_url
        string note
        enum status "PENDING_APPROVAL | APPROVED | REJECTED"
        string review_note
        timestamp created_at
        timestamp reviewed_at
    }

    COACH_PLAN ||--o{ ATHLETE_SUBSCRIPTION : "se aplica en"
    ATHLETE_SUBSCRIPTION }o--|| COACH_PLAN : "usa"
    PAYMENT_RECORD }o--|| ATHLETE_SUBSCRIPTION : "referencia"
```

---

## 4. Comunidad

```mermaid
erDiagram
    COMMUNITY {
        uuid id PK
        uuid coach_id FK
        enum mode "BROADCAST | CONVERSATION"
        string[] active_sports
        boolean allow_athlete_events
        boolean allow_athlete_ai
    }

    POST {
        uuid id PK
        uuid author_id FK
        uuid community_id FK
        string content
        string[] image_urls
        timestamp created_at
        timestamp deleted_at
    }

    REACTION {
        uuid id PK
        uuid post_id FK
        uuid user_id FK
        enum type "LIKE"
    }

    COMMENT {
        uuid id PK
        uuid post_id FK
        uuid author_id FK
        string content
        timestamp created_at
        timestamp deleted_at
    }

    ACHIEVEMENT {
        uuid id PK
        uuid athlete_id FK
        uuid post_id FK "null si no se publicó"
        enum type "FIRST_WORKOUT | THREE_IN_A_ROW | TEN_COMPLETED | FIVE_THIS_MONTH"
        timestamp earned_at
        boolean is_published
    }

    COMMUNITY ||--o{ POST : "contiene"
    POST ||--o{ REACTION : "recibe"
    POST ||--o{ COMMENT : "tiene"
    ACHIEVEMENT }o--o| POST : "puede generar"
```

---

## 5. Calendario

```mermaid
erDiagram
    CALENDAR_EVENT {
        uuid id PK
        uuid coach_id FK
        string title
        string description
        timestamp start_at
        timestamp end_at
        enum type "TRAINING | EVENT | OTHER"
        string location
        int max_attendees
        boolean is_published
        timestamp cancelled_at
    }

    EVENT_ATTENDEE {
        uuid event_id FK
        uuid user_id FK
        enum status "ATTENDING | MAYBE | NOT_ATTENDING"
        timestamp created_at
    }

    CALENDAR_EVENT ||--o{ EVENT_ATTENDEE : "tiene"
```

---

## Mapa de Relaciones General

Cómo se conectan todas las áreas entre sí:

```mermaid
erDiagram
    USER ||--|| COACH_PROFILE : "es coach"
    USER ||--|| ATHLETE_PROFILE : "es atleta"

    COACH_PROFILE ||--o{ ROUTINE : "crea"
    COACH_PROFILE ||--o{ COACH_PLAN : "define"
    COACH_PROFILE ||--|| COMMUNITY : "tiene una"
    COACH_PROFILE ||--o{ CALENDAR_EVENT : "crea"
    COACH_PROFILE ||--o{ ATHLETE_GROUP : "gestiona"

    ATHLETE_PROFILE }o--|| COACH_PROFILE : "entrena con"
    ATHLETE_PROFILE ||--o{ ROUTINE_ASSIGNMENT : "recibe"
    ATHLETE_PROFILE ||--o{ WORKOUT_LOG : "genera"
    ATHLETE_PROFILE ||--o| ATHLETE_SUBSCRIPTION : "tiene"
    ATHLETE_PROFILE ||--o{ PAYMENT_RECORD : "realiza"
    ATHLETE_PROFILE ||--o{ ACHIEVEMENT : "gana"

    ROUTINE ||--o{ ROUTINE_ASSIGNMENT : "se asigna via"
    ROUTINE_ASSIGNMENT ||--o{ WORKOUT_LOG : "genera"

    COACH_PLAN ||--o{ ATHLETE_SUBSCRIPTION : "aplica a"
    PAYMENT_RECORD }o--|| ATHLETE_SUBSCRIPTION : "referencia"

    COMMUNITY ||--o{ POST : "tiene"
    CALENDAR_EVENT ||--o{ EVENT_ATTENDEE : "tiene"
```
