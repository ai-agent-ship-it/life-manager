# Life Manager - Análisis de Requisitos

## 1. Requisitos Funcionales (RF)

### RF1: Gestión Financiera Inteligente
- **RF1.1: Registro de Transacciones**: El sistema debe permitir registrar ingresos, gastos y créditos.
- **RF1.2: Inferencia de IA**: El agente debe extraer automáticamente: monto, moneda, categoría, fecha y tipo de movimiento a partir de entradas no estructuradas.
- **RF1.3: Procesamiento Multimodal**:
    - **Texto**: Procesamiento de lenguaje natural (NLP) para mensajes de chat.
    - **Voz**: Transcripción de notas de voz a texto para su procesamiento.
    - **Imágenes**: OCR y análisis de fotos de recibos/facturas.
    - **Documentos**: Extracción de datos de archivos PDF (estados de cuenta, facturas electrónicas).
- **RF1.4: Gestión de Activos y Pasivos**: Registro y seguimiento de bienes (activos) y deudas (pasivos).
- **RF1.5: Reportes**: Generación de visualizaciones de gastos por categoría, balance mensual y evolución patrimonial.
- **RF1.6: Gastos e Ingresos Recurrentes**: El sistema debe permitir programar transacciones automáticas con recurrencia flexible y vincularlas a recordatorios:
    - Diaria.
    - Semanal (uno o varios días específicos de la semana).
    - Quincenal.
    - Mensual (días específicos del mes).
    - Bimestral, trimestral, semestral, anual.
    - Personalizada (cada X días/semanas/meses).
    - **Notificaciones**: El sistema debe generar recordatorios automáticos (push, telegram o email) antes o en el momento de la ejecución de la transacción recurrente.

### RF2: Organización Personal
- **RF2.1: Notas y Diario**: Creación de entradas de texto enriquecido para bitácoras personales.
- **RF2.2: Agenda y Recordatorios**: Programación de eventos y notificaciones automáticas.
- **RF2.3: Clasificación Automática**: El agente debe distinguir si una entrada es financiera, una nota, un recordatorio o una entrada de diario.

## 2. Requisitos No Funcionales (RNF)

- **RNF1: Seguridad**: Cifrado de datos financieros en reposo y en tránsito.
- **RNF2: Disponibilidad**: Despliegue en Kubernetes con estrategias de auto-recuperación.
- **RNF3: Escalabilidad**: Arquitectura de microservicios (Backend en Go) para manejar carga variable.
- **RNF4: Usabilidad**: Interfaz web responsiva (Next.js) optimizada para móviles (para fotos de recibos).

## 3. Stack Tecnológico Confirmado
- **Backend**: Go (Golang).
- **Frontend**: Next.js / React.
- **Base de Datos**: PostgreSQL.
- **Infraestructura**: Kubernetes (K8s).
- **IA/ML**: Integración con modelos multimodales (GPT-4o / Claude 3.5 Sonnet) para visión, audio y texto.

---
*Documento generado el 2026-03-06*
