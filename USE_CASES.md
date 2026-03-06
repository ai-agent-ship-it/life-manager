# Life Manager - Casos de Uso y Diagramas UML

## 1. Identificación de Actores
- **Usuario**: Persona que interactúa con el sistema para gestionar sus finanzas y vida personal.
- **Agente IA**: Entidad interna que procesa entradas multimodales (OCR, Transcripción, NLP).
- **Sistema de Almacenamiento**: Base de datos PostgreSQL y almacenamiento de archivos (S3/Local).
- **API de IA Externa**: Proveedor de modelos (OpenAI/Anthropic) para procesamiento avanzado.

## 2. Diagrama de Casos de Uso (Mermaid)

```mermaid
useCaseDiagram
    actor "Usuario" as U
    actor "Agente IA" as AI
    actor "Sistema" as S

    package "Gestión Financiera" {
        usecase "Registrar Gasto/Ingreso (Texto/Voz)" as UC1
        usecase "Subir Recibo/Factura (Imagen/PDF)" as UC2
        usecase "Consultar Reportes Financieros" as UC3
        usecase "Gestionar Activos y Pasivos" as UC4
    }

    package "Organización Personal" {
        usecase "Crear Nota o Diario" as UC5
        usecase "Programar Recordatorio" as UC6
    }

    package "Procesamiento Inteligente" {
        usecase "Inferencia de Datos (Categorización)" as UC7
        usecase "Extracción OCR/Transcripción" as UC8
    }

    U --> UC1
    U --> UC2
    U --> UC3
    U --> UC4
    U --> UC5
    U --> UC6

    UC1 ..> UC7 : <<include>>
    UC2 ..> UC8 : <<include>>
    UC8 ..> UC7 : <<include>>
    
    UC7 -- AI
    UC8 -- AI
    UC3 -- S
    UC4 -- S
```

## 3. Diagrama de Secuencia: Registro Multimodal
Este diagrama muestra el flujo desde que el usuario envía una foto de un recibo hasta que se guarda como transacción.

```mermaid
sequenceDiagram
    participant U as Usuario
    participant B as Backend (Go)
    participant AI as Agente IA (LLM/Vision)
    participant DB as PostgreSQL
    participant S3 as Almacenamiento

    U->>B: Envía Foto de Recibo (Multipart)
    B->>S3: Guarda archivo original
    B->>AI: Procesa Imagen (OCR + Inferencia)
    AI-->>B: JSON {monto: 50.0, moneda: "USD", categoria: "Comida", comercio: "Starbucks"}
    B->>DB: Inserta Transacción + Referencia a Imagen
    DB-->>B: Confirmación
    B-->>U: Notificación: "Gasto de $50 en Starbucks registrado"
```

## 4. Diagrama de Clases (Estructura de Datos)

```mermaid
classDiagram
    class User {
        +UUID id
        +String email
        +String timezone
    }

    class Transaction {
        +UUID id
        +Float amount
        +String currency
        +String category
        +DateTime date
        +String type (Income/Expense/Credit)
        +UUID attachment_id
    }

    class Entry {
        +UUID id
        +String content
        +String type (Note/Journal/Reminder)
        +DateTime scheduled_at
    }

    class Attachment {
        +UUID id
        +String file_path
        +String mime_type
        +String raw_ocr_text
    }

    User "1" -- "*" Transaction : manages
    User "1" -- "*" Entry : creates
    Transaction "0..1" -- "1" Attachment : has
    Entry "0..1" -- "1" Attachment : has
```

---
*Documento generado el 2026-03-06*
