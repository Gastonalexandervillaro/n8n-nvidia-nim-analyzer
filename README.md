# 🚀 NVIDIA NIM API & n8n: AUTOMATED TEXT STRUCTURING WORKFLOW

![n8n](https://img.shields.io/badge/n8n-Automation-FF6D5A?style=for-the-badge&logo=n8n&logoColor=white)
![NVIDIA](https://img.shields.io/badge/NVIDIA_NIM-Nemotron--3.5-76B900?style=for-the-badge&logo=nvidia&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![JSON](https://img.shields.io/badge/Data-JSON_Structured-000000?style=for-the-badge&logo=json&logoColor=white)

---

> [!IMPORTANT]
> ### 🎯 PROPÓSITO DEL PROYECTO
> Este workflow está diseñado como un **motor de procesamiento e inteligencia de datos** para la gestión administrativa. Su objetivo es automatizar la recepción de información no estructurada (textos planos, correos, solicitudes) y transformarla de manera instantánea en un formato estandarizado listo para ser integrado en procesos operativos y de toma de decisiones.

---

## 📌 CASO DE USO Y SOLUCIÓN DE NEGOCIO

En la operativa diaria de cualquier departamento comercial o administrativo ingresa un flujo constante de comunicaciones informales: correos extensos, peticiones de licitaciones o mensajes sin formato normalizado.

### ⚠️ Problemas Operativos que Resuelve:
* **TIEMPOS DE LECTURA Y FILTRADO:** Elimina la necesidad de revisar manualmente cada texto para identificar de qué trata.
* **DESORGANIZACIÓN DE PRIORIDADES:** Clasifica automáticamente la urgencia para que los casos críticos reciban atención inmediata.
* **EXTRACCIÓN DE TAREAS OPERATIVAS:** Aisla la acción concreta requerida para acelerar los tiempos de ejecución.

### 💡 Funcionamiento del Sistema:
El flujo recibe el texto de entrada, se conecta con la API del modelo de IA **NVIDIA NIM (Nemotron-3.5)** y genera de forma consistente tres variables clave:

1. **`RESUMEN EJECUTIVO`** ➔ Síntesis del motivo central del mensaje en una sola oración.
2. **`NIVEL DE URGENCIA`** ➔ Categorización de prioridad (`ALTA`, `MEDIA`, `BAJA`).
3. **`ACCIÓN REQUERIDA`** ➔ Instrucción operativa concreta para el seguimiento del caso.

---

## 📐 ARQUITECTURA TÉCNICA DEL WORKFLOW

El procesamiento se ejecuta mediante un pipeline optimizado de 3 etapas de extremo a extremo:


[ 1. Disparador Manual ] ──> [ 2. Consulta a IA NVIDIA ] ──> [ 3. Estructurador y Limpiador JSON ]

DESGLOSE ESTRUCTURADO DE NODOS
NODO 01: 1. Disparador Manual

Tipo / Tecnología: n8n Core Trigger

Función Principal: Punto de inicio del flujo para recepción de carga útil (payload) de prueba o activación manual del proceso.

NODO 02: 2. Consulta a IA NVIDIA

Tipo / Tecnología: HTTP Request (API)

Función Principal: Solicitud POST al endpoint de NVIDIA NIM (Nemotron-3.5-Lightning-30b) con autenticación Bearer Token y prompt delimitador para forzar la estructura.

NODO 03: 3. Estructurador JSON

Tipo / Tecnología: Code Node (JavaScript)

Función Principal: Módulo de transformación en JS nativo (JSON.parse). Filtra los metadatos de red, aísla las variables clave e inyecta la marca de tiempo ISO (fecha_procesado).

📄 ESTRUCTURA DE SALIDA (OUTPUT JSON)
Salida limpia y sin ruido técnico, lista para ser enviada a bases de datos, sistemas CRM o notificaciones internas:
{
  "resumen": "Solicitud de confirmación del presupuesto de licitación para la provisión de insumos.",
  "urgencia": "Alta",
  "accion_requerida": "Confirmar y enviar el presupuesto de la licitación antes de las 18:00 hs.",
  "fecha_procesado": "2026-11-09T03:15:00.000Z"
}

INTEGRACIÓN Y ESCALABILIDAD EN PROCESOS DE NEGOCIO
Como arquitectura base, este workflow está preparado para conectarse a múltiples capas del ecosistema tecnológico de una empresa:

Fuentes de Entrada: Integración directa con casillas de email (Gmail/Outlook), formularios web o plataformas de comunicación.

Enrutamiento Operativo: Derivación automática de la salida JSON hacia el área correspondiente (Ventas, Soporte, Legales).

Conexión con Sistemas Core: Inyección de datos procesados en bases de datos (SQL/NoSQL), planillas de gestión o sistemas CRM (HubSpot, Salesforce).

BUENAS PRÁCTICAS Y SEGURIDAD
GESTIÓN DE CREDENCIALES: El código publicado no contiene API Keys ni tokens. La autenticación se maneja desde la sección de credenciales de la instancia de n8n.

SANITIZACIÓN DE DATOS: Control de excepciones en JavaScript para asegurar que la estructura devuelta sea siempre válida.

GUÍA DE DESPLIEGUE E IMPORTACIÓN
Prerrequisitos
Instancia de n8n (Cloud o Self-hosted).

Clave de acceso a NVIDIA NIM API.

Pasos de Instalación:
Clona este repositorio o descarga el archivo NVIDIA NIM - Administrative Text Analyzer.json.

En tu n8n, ve a Workflows > Import from File.

Selecciona el archivo .json importado.

En el nodo 2. Consulta a IA NVIDIA (Modelo Nemotron), asigna tu API Key en la casilla Value del Header Authorization:
Authorization: Bearer Tu_NVIDIA_API_Key

¡Ejecuta el flujo!
Probá pegarlo ahora en el editor de GitHub y vas a ver que queda perfectamente alineado.
