# Bot de Supervivencia 🌤️🎒

## Descripción del Proyecto

El **Bot de Supervivencia** es un sistema automatizado desarrollado con n8n que integra servicios meteorológicos y un modelo de Inteligencia Artificial local (Ollama) para ofrecer recomendaciones útiles a estudiantes universitarios en Colombia. 

A través de Telegram, los usuarios envían el nombre de su ciudad y reciben al instante información del clima, alertas especiales (como calor extremo o lluvia) y un consejo práctico con un tono cercano y natural para afrontar su día de clases.

---

## Enlaces Importantes

* 🎥 **Demo del proyecto:** [Ver video de demostración](https://drive.google.com/file/d/1UgXjqOkFy8sIstvzJ8T1qmSUR2e1MNS_/view?usp=sharing)
* 📊 **Historial de consultas:** [Ver base de datos en Google Sheets](https://docs.google.com/spreadsheets/d/1zjFzcc1DAUmfcxQ9pKrqHeiixanEvpoEpY7wjS57MDg/edit#gid=0)

---

## Tecnologías Utilizadas

| Tecnología | Propósito en el proyecto |
| :--- | :--- |
| **n8n** | Orquestación y automatización de todo el flujo de trabajo. |
| **Telegram API** | Interfaz principal de interacción con el usuario. |
| **Open-Meteo Geocoding** | Conversión del nombre de la ciudad a coordenadas (Lat/Lon). |
| **Open-Meteo Weather** | Obtención de datos climáticos en tiempo real. |
| **Ollama (Gemma 3)** | Ejecución local del modelo de IA para generar consejos personalizados. |
| **Google Sheets API** | Almacenamiento y registro histórico de las consultas realizadas. |
| **JavaScript / Node.js** | Procesamiento de texto, validación de intenciones y lógica de recomendaciones. |

---

## Cómo Funciona (Flujo del Sistema)

1. **Recepción:** El usuario envía un mensaje al bot de Telegram (ej. "Medellín").
2. **Clasificación de Intención:** Un script de JavaScript analiza el texto para saber si es un saludo, una ciudad válida, un número o un agradecimiento.
3. **Geolocalización:** Si es una ciudad colombiana, se consulta la API de Open-Meteo para obtener sus coordenadas exactas.
4. **Consulta Climática:** Se extraen los datos de temperatura, lluvia y viento.
5. **Lógica de Supervivencia:** El sistema determina qué objetos son necesarios (sombrilla, bloqueador, chaqueta) según el clima actual.
6. **Generación con IA:** Ollama recibe los datos y redacta un consejo corto y amigable, adaptado al contexto de un estudiante universitario colombiano.
7. **Respuesta:** El bot envía el reporte formateado al usuario en Telegram.
8. **Registro:** Se guarda la consulta (ciudad, clima y consejo) en una hoja de cálculo de Google Sheets.

---

## Guía de Instalación y Ejecución

Para replicar y hacer funcionar este proyecto en tu entorno local, sigue estos pasos:

### 1. Requisitos Previos

* Tener **n8n** instalado (ya sea de forma local usando npm/Docker o en la nube).
* Tener **Ollama** instalado en tu computadora para correr la IA localmente.
* Una cuenta de Telegram y un bot creado a través de **BotFather** (para obtener el Token).
* Credenciales de **Google Cloud Console** habilitadas para la API de Google Sheets.

### 2. Configurar el Modelo de IA (Ollama)

Abre tu terminal de comandos y descarga el modelo utilizado en este proyecto ejecutando:

`ollama run gemma3`

Asegúrate de que Ollama se esté ejecutando en el puerto por defecto (`http://127.0.0.1:11434`) para que n8n pueda comunicarse con él.

### 3. Importar el Flujo en n8n

* Abre tu interfaz de n8n.
* Ve a la sección **Workflows** y haz clic en **Add Workflow**.
* Selecciona la opción **Import from File** y carga el archivo JSON de este proyecto (`sobrevivir (1).json`).

### 4. Configurar las Credenciales en n8n

Una vez importado el flujo, verás algunos nodos con advertencias. Debes configurar tus propias credenciales:

* **Telegram Trigger y Nodos de Telegram:** Haz doble clic, selecciona "Create New Credential" y pega el Token que te dio BotFather.
* **Google Sheets:** Configura la autenticación OAuth2 con tu cuenta de Google para dar permisos de escritura al documento del historial.

### 5. Activar y Probar el Bot

* Asegúrate de que el documento de Google Sheets tenga las columnas correctas (`ciudad`, `clima`, `consejo`).
* Activa el interruptor de **Active** en la esquina superior derecha de n8n para encender el flujo.
* ¡Ve a Telegram, busca tu bot y escríbele el nombre de una ciudad como "Bucaramanga" o "Bogotá" para ver la magia en acción!

---

## Posibles Mejoras Futuras

* Soporte para ciudades internacionales.
* Predicción del clima para fechas o días futuros.
* Recomendaciones de lugares para estudiar o visitar según el clima.
* Generación de alertas climáticas automáticas por la mañana.