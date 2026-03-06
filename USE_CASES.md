# Life Manager - Casos de Uso y Diagramas UML

## 1. Identificación de Actores
- **Usuario**: Persona que interactúa con el sistema para gestionar sus finanzas y vida personal.
- **Agente IA**: Entidad interna que procesa entradas multimodales (OCR, Transcripción, NLP).
- **Sistema de Almacenamiento**: Base de datos PostgreSQL y almacenamiento de archivos (S3/Local).
- **API de IA Externa**: Proveedor de modelos (OpenAI/Anthropic) para procesamiento avanzado.

## 2. Diagrama de Casos de Uso (Mermaid)

```mermaid
graph TD
    %% Actores
    U((Usuario))
    AI[Agente IA]
    S[(Sistema)]

    subgraph Gestion_Financiera [Gestión Financiera]
        UC1([Registrar Gasto/Ingreso])
        UC2([Subir Recibo/Factura])
        UC3([Consultar Reportes])
        UC4([Gestionar Activos])
        UC9([Programar Transacción Recurrente])
    end

    subgraph Organizacion_Personal [Organización Personal]
        UC5([Crear Nota/Diario])
        UC6([Programar Recordatorio])
    end

    subgraph Procesamiento [Procesamiento Inteligente]
        UC7([Categorización])
        UC8([Extracción OCR])
    end

    U --> UC1
    U --> UC2
    U --> UC3
    U --> UC4
    U --> UC5
    U --> UC6
    U --> UC9

    UC1 -.-> UC7
    UC2 -.-> UC8
    UC8 -.-> UC7
    UC9 -.-> UC7
    UC9 -.-> UC6 : include
    
    UC7 --- AI
    UC8 --- AI
    UC3 --- S
    UC4 --> S
    UC9 --> S
```

## 3. Diagrama de Secuencia: Registro Multimodal

```mermaid
sequenceDiagram
    participant U as Usuario
    participant B as Backend (Go)
    participant AI as Agente IA
    participant DB as PostgreSQL
    participant S3 as Almacenamiento

    U->>B: Envía Foto de Recibo
    B->>S3: Guarda archivo
    B->>AI: Procesa Imagen
    AI-->>B: JSON con datos
    B->>DB: Inserta Transacción
    DB-->>B: Confirmación
    B-->>U: Notificación de éxito
```

## 4. Diagrama de Clases (Estructura de Datos)

```mermaid
classDiagram
    class User {
        +UUID id
        +String email
    }

    class Transaction {
        +UUID id
        +Float amount
        +String currency
        +String category
        +DateTime date
        +UUID recurring_id
    }

    class RecurringTransaction {
        +UUID id
        +Float amount
        +String currency
        +String category
        +String frequency
        +JSONB rules
        +DateTime start_date
        +DateTime end_date
        +DateTime last_run
        +DateTime next_run
    }

    class Entry {
        +UUID id
        +String content
        +String type
    }

    class Attachment {
        +UUID id
        +String file_path
    }

    class Reminder {
        +UUID id
        +String title
        +String message
        +DateTime scheduled_at
        +String channel
        +String status
    }

    User "1" -- "*" Transaction : manages
    User "1" -- "*" RecurringTransaction : schedules
    User "1" -- "*" Entry : creates
    User "1" -- "*" Reminder : receives
    Transaction "0..1" -- "1" Attachment : has
    Entry "0..1" -- "1" Attachment : has
    RecurringTransaction "1" -- "*" Transaction : generates
    RecurringTransaction "1" -- "*" Reminder : triggers
```

---
*Documento actualizado el 2026-03-06*
