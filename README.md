# UBA-NLP2-TP3
# RAG Multi-Agente para Análisis de CVs 🤖📄

Un sistema inteligente de Retrieval-Augmented Generation (RAG) que utiliza múltiples agentes para analizar y comparar currículums vitae de manera automática.

## 🌟 Características Principales

- **Sistema Multi-Agente**: Router inteligente que selecciona automáticamente los CVs más relevantes para cada consulta
- **Indexación Vectorial**: Un índice Pinecone independiente por cada CV para búsquedas precisas
- **Interfaz Web Interactiva**: UI desarrollada con Gradio para facilidad de uso
- **Procesamiento Robusto**: Soporte para archivos PDF y TXT con limpieza automática de texto
- **Parámetros Configurables**: Control total sobre la generación y recuperación de información

## 🏗️ Arquitectura del Sistema

```
📁 Documentos CVs (.pdf/.txt)
    ↓
🔄 Procesamiento y Chunking
    ↓
🧠 Embeddings (SentenceTransformers)
    ↓
🗄️ Pinecone Vector Database (1 índice por CV)
    ↓
🤖 Router Agent (Groq LLM)
    ↓
🔍 Retrieval from Selected Indices
    ↓
💬 Response Generation (Groq LLM)
    ↓
🖥️ Gradio Interface
```

## 🛠️ Tecnologías Utilizadas

- **LLM**: Groq (llama3-8b-8192)
- **Vector Database**: Pinecone
- **Embeddings**: SentenceTransformers (all-MiniLM-L6-v2)
- **Text Processing**: LangChain, PyPDF
- **Interface**: Gradio
- **Chunking**: RecursiveCharacterTextSplitter

## 📋 Requisitos

### Dependencias Python
```bash
pip install gradio groq pinecone-client sentence-transformers langchain-text-splitters pypdf
```

### APIs Keys Necesarias
- **Groq API Key**: Obtén una en [Groq Console](https://console.groq.com/)
- **Pinecone API Key**: Regístrate en [Pinecone](https://www.pinecone.io/)

## 🚀 Instalación y Configuración

1. **Clonar el repositorio**
```bash
git clone [tu-repositorio]
cd rag-multiagent-cv
```

2. **Instalar dependencias**
```bash
pip install -r requirements.txt
```

3. **Configurar las API Keys**

En Google Colab:
- Ir a "Secrets" en el panel lateral
- Agregar `GROQ_API_KEY` y `PINECONE_API_KEY`

O configurar como variables de entorno:
```bash
export GROQ_API_KEY="tu_groq_api_key"
export PINECONE_API_KEY="tu_pinecone_api_key"
```

4. **Preparar documentos**
```bash
mkdir /content/cv
# Copiar archivos .pdf o .txt de CVs en esta carpeta
```

## 💻 Uso

### 1. Ejecutar la Notebook

Abrir `TP3_CSalinas_Chat_Bot_Multiagente.ipynb` en Google Colab y ejecutar todas las celdas.

### 2. Interfaz Web

La aplicación Gradio se ejecutará automáticamente y proporcionará una URL pública.

### 3. Flujo de Trabajo

1. **Subir CVs**: Colocar archivos PDF o TXT en la carpeta `/content/cv`
2. **Indexar**: Hacer clic en "Reindexar (/content/cv)"
3. **Consultar**: Hacer preguntas sobre los CVs en el chat
4. **Analizar**: El sistema seleccionará automáticamente los CVs relevantes y proporcionará respuestas contextualizadas

## 🔧 Configuración Avanzada

### Parámetros Ajustables

- **Top-K Retrieve**: Número de pasajes a recuperar (1-10)
- **Temperature**: Creatividad en las respuestas (0.0-1.5)
- **Top-p**: Control de diversidad (0.1-1.0)
- **Max Tokens**: Longitud máxima de respuesta (64-2048)

### Configuración del Sistema

```python
# Configuración de embeddings
EMB_MODEL_NAME = "sentence-transformers/all-MiniLM-L6-v2"
EMB_DIM = 384
CHUNK_SIZE = 200
CHUNK_OVERLAP = 25

# Configuración de Pinecone
PINECONE_CLOUD = CloudProvider.AWS
PINECONE_REGION = AwsRegion.US_EAST_1
INDEX_PREFIX = "cv--"
```

## 📝 Ejemplos de Consultas

- "¿En qué proyectos de ciencia de datos participó Ricardo?"
- "¿Qué experiencia tienen Sofía y Ricardo con sklearn, XGBoost o LightGBM?"
- "¿Cuál de los candidatos tiene un perfil más académico?"
- "¿Quién tiene experiencia en proyectos internacionales y manejo de AWS o GCP?"
- "Estoy buscando alguien con conocimientos en ML, datos y experiencia minera. ¿A quién considero?"

## 🎯 Funcionalidades Principales

### 🤖 Router Multi-Agente
- Analiza automáticamente la consulta del usuario
- Selecciona los CVs más relevantes
- Soporta tanto modo single-agent como multi-agent

### 🔍 Búsqueda Vectorial Inteligente
- Embeddings semánticos para búsquedas precisas
- Recuperación contextual con scoring de relevancia
- Metadatos detallados para trazabilidad

### 🧹 Procesamiento de Texto Robusto
- Limpieza automática de caracteres especiales
- Normalización de acentos y caracteres no ASCII
- Chunking inteligente con solapamiento

### 📊 Interfaz Completa
- Chat interactivo con historial
- Configuración de parámetros en tiempo real
- Herramientas de debugging y verificación
- Ejemplos predefinidos

## 🗂️ Estructura del Proyecto

```
📁 Proyecto/
├── 📓 TP3_CSalinas_Chat_Bot_Multiagente.ipynb
├── 📁 cv/                    # Carpeta de documentos CVs
│   ├── 📄 cv1.txt
│   └── 📄 cv2.txt
├── 📄 README.md
└── 📄 requirements.txt
```

## 🔍 Debugging y Verificación

El sistema incluye herramientas para:
- Verificar chunks generados por documento
- Monitorear el estado de índices en Pinecone
- Inspeccionar embeddings y vectores
- Limpiar y resetear el sistema completo

## ⚠️ Limitaciones y Consideraciones

- **Contexto del Modelo**: llama3-8b-8192 tiene límite de 8192 tokens
- **Memoria del Chat**: El historial se mantiene en memoria durante la sesión
- **Costos**: Las APIs de Groq y Pinecone tienen costos asociados
- **Idioma**: Optimizado para textos en español con limpieza de acentos



## 📧 Contacto

- **Autor**: C. Salinas
- **Proyecto**: TP3 - Chat Bot Multi-Agente
- **Universidad**: UBA - NLP2

## 🙏 Agradecimientos

- Groq por proporcionar acceso a modelos LLM eficientes
- Pinecone por la infraestructura de vectores
- HuggingFace por los modelos de embeddings
- Gradio por la interfaz de usuario intuitiva

---
