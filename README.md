# 🚀 Sprint de Desarrollo: EcoLog Backend
## Gestión de Residuos e Impacto Ambiental Integrado con IA

¡Bienvenidos al desafío final de Mongoose y Express! En este proyecto deberán aplicar todo lo aprendido sobre APIs REST y enfrentar retos del mundo real: **integración con IA y generación de reportes físicos.**

---

### 📜 1. La Temática: EcoLog
La ONG "Planeta Limpio" necesita una API para registrar la recolección de residuos en diferentes puntos. El sistema debe permitir el seguimiento detallado de qué se recolecta, dónde y cuál es el impacto.

### 🛠️ 2. Requisitos de Arquitectura
El proyecto debe estar organizado de forma profesional (Arquitectura de Capas):
*   `/src/models`: Definición de esquemas.
*   `/src/controllers`: Lógica de control de peticiones.
*   `/src/services`: Lógica de negocio e interacción con la DB.
*   `/src/routes`: Definición de endpoints.
*   `/src/middlewares`: Validaciones y manejo de errores.
*   `/src/config`: Conexión a la base de datos.

### 📊 3. Modelo de Datos (`ResidueLog`)
El documento de MongoDB debe tener al menos:
*   `residueType`: (String, obligatorio, Enum: `Plastic`, `Glass`, `Metal`, `Paper`, `Organic`, `Hazardous`).
*   `weight`: (Number, obligatorio, en kilogramos).
*   `location`: (String, obligatorio, ej: "Punto Verde Palermo").
*   `collectorName`: (String, obligatorio).
*   `state`: (String, por defecto `active`).
*   `deletedAt`: (Date, por defecto `null`).

### 🛣️ 4. Endpoints Obligatorios
1.  `GET /api/logs`: Listar todos los registros activos.
2.  `POST /api/logs`: Crear un nuevo registro.
3.  `PATCH /api/logs/:id`: Actualizar datos de un registro.
4.  `DELETE /api/logs/:id?softDelete=true`: Borrado lógico o físico según query.
5.  `PATCH /api/logs/:id/restore`: Restaurar un registro de la papelera.

---

### 🔥 5. EL DESAFÍO TÉCNICO (Bonus de Investigación)
Deberán crear un endpoint avanzado: `POST /api/logs/:id/export`

Este endpoint no guarda nada en la DB, sino que realiza un proceso de "vuelo":
1.  **AI Insight (Gemini)**: Consultar a la IA de Google (Gemini) enviando el tipo de residuo y el peso, y pedirle un "Tip de reciclaje creativo" para ese residuo específico.
2.  **Generación de PDF**: Crear un PDF en la carpeta `/exports` del servidor que contenga:
    *   Título: "Certificado de Impacto Ambiental".
    *   Datos del residuo (Tipo, Peso, Ubicación).
    *   El "Tip creativo" devuelto por la IA.
3.  **Generación de Excel**: Crear un archivo `.xlsx` que liste el historial completo de recolecciones almacenadas.

#### 📚 Librerías Sugeridas para Investigar:
*   **IA**: `@google/generative-ai` (Necesitarán una API Key gratuita de Google AI Studio).
*   **PDF**: `pdfkit`
*   **Excel**: `exceljs` o `xlsx`

---

### ⏱️ Entrega y Metodología
*   **Fase 1 (Análisis)**: 30 minutos sin escribir código. Diseñen su esquema y piensen cómo van a estructurar las carpetas. (No se permite usar IA en esta fase)
*   **Fase 2 (Configuración Entorno)**: Configurar el entorno, la base de datos (MongoDB Atlas) y las dependencias. (No se permite usar IA en esta fase)
*   **Fase 3 (Desarrollo Base)**: Implementar el CRUD y el manejo de errores centralizado. (Se permite usar IA en esta fase solo para buscar librerías y entender conceptos, no para lógica del proyecto)
*   **Fase 4 (Investigación)**: Conectar con Gemini y generar los archivos. (Se permite usar IA en esta fase)

> **Regla de Oro**: Si el código falla, el Error Handler Centralizado debe capturar el error y devolver un JSON prolijo, ¡nunca dejen que el servidor se caiga!

¡Muchos éxitos! 🌏✨
