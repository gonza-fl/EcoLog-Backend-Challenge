# 📖 Guía de Estructura de Proyecto: EcoLog Backend

Esta guía explica la organización de carpetas del proyecto para que puedan navegar el código de forma profesional. El proyecto utiliza una **Arquitectura de Capas**, lo que significa que cada carpeta tiene una responsabilidad única y específica.

---

## 📂 Estructura General

### 🏠 Raíz del Proyecto
*   **`exports/`**: Aquí se guardarán los archivos PDF y Excel generados por el servidor. 
*   **`.env`**: Archivo para tus "secretos" (API Keys, URL de base de datos). **¡Nunca lo compartas!**
*   **`package.json`**: El mapa de dependencias y comandos de ejecución del proyecto.

---

## 📂 Carpeta `src/` (El Código Fuente)

El código de la lógica está organizado según su función:

### 1. ⚙️ `src/config/`
Contiene la configuración de herramientas externas.
*   **`db.js`**: Lógica para conectar nuestra aplicación con **MongoDB** usando Mongoose.

### 2. 🗃️ `src/models/`
Aquí definimos **qué datos guardamos**.
*   **`ResidueLog.js`**: Define el "Schema" (esquema) de los residuos. Especifica que el tipo es un String, el peso un número, etc.

### 3. 🛣️ `src/routes/`
Define las **URLs** que nuestra API escucha.
*   **`residueLog.routes.js`**: Mapea los endpoints (ej: `GET /api/logs`) con la función que debe ejecutarse.

### 4. 🎮 `src/controllers/`
Es el "director de orquesta".
*   Recibe la petición del usuario, llama al servicio correspondiente y devuelve la respuesta (éxito o error). No debe contener lógica compleja, solo gestionar la comunicación.

### 5. 🧠 `src/services/`
Aquí vive la **Lógica de Negocio**.
*   Es donde ocurre la "magia": cálculos, llamadas a la IA de Gemini, generación de archivos y consultas a la base de datos. Si el proceso de reciclaje cambia, el cambio se hace aquí.

### 6. 🛡️ `src/middlewares/`
Funciones que se ejecutan "en el medio" de una petición.
*   **`errorHandler.js`**: Nuestro salvavidas. Si algo falla en cualquier parte del código, este archivo captura el error y le responde al usuario de forma elegante sin que el servidor se caiga.

### 7. 🚀 Archivos Principales
*   **`app.js`**: Configura Express (instancia, middlewares globales y rutas).
*   **`server.js`**: El punto de arranque. Enciende el servidor y la conexión a la base de datos.

---

## 🔄 El camino de una petición (Flujo de datos)
Cuando un usuario hace una petición, los datos viajan así:
`Petición del Cliente` ➡️ `Routes` ➡️ `Controller` ➡️ `Service` ➡️ `Model/DB`
Y luego la respuesta vuelve por el mismo camino.

---

> **Tip para alumnos:** Mantener esta separación ayuda a que si hay un error en la base de datos, sepan que deben mirar en `models` o `config`, y si el error es en una URL, deben ir directo a `routes`. ¡Éxitos con el desafío! 🌏✨
