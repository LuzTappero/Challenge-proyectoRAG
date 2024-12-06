
# PROYECTO DE RESPUESTAS GENERATIVAS BASADAS EN RECUPERACIÓN (RAG)

## INTRODUCCIÓN

En este proyecto utilicé técnicas de Recuperación y Generación (RAG) para responder preguntas de manera contextualizada. Las respuestas son generadas a partir de un conjunto de historias, extraidas a partir de un documento PDF y almacenadas en una base de datos vectorial utilizando embeddings y modelos de lenguaje. 🚀

El objetivo es ofrecer respuestas consistentes, amigables y personalizadas para cada pregunta del usuario, siguiendo un tono definido.


## TÉCNOLOGIAS Y HERRAMIENTAS

### **1. PyPDF**
- **Uso**: **PyPDF** es una librería en Python que permite trabajar con archivos PDF de manera sencilla. La utilicé para extraer el texto de los documentos en formato PDF, lo cual fue esencial para obtener la información necesaria para generar respuestas contextuales y basadas en documentos.
- **Motivo**: La extracción del texto es eficiente, es simple de usar, es compatible también en casos de uso de textos en diversos idiomas.

### **2. RecursiveCharacterTextSplitter-Langchain**
- **Uso**: Librería **Langchain** junto con la clase **RecursiveCharacterTextSplitter** para dividir los documentos largos en "chunks" o fragmentos más pequeños. Esto es fundamental para manejar documentos extensos y procesarlos de manera eficiente, asegurando que el modelo pueda trabajar con ellos sin sobrecargar la memoria o el tiempo de procesamiento.
- **Motivo**: La división del texto es eficiente, simple de utilizar y configurar. Langchain proporciona una forma sencilla y flexible de integrar este método de partición de texto en el flujo de trabajo de procesamiento de documentos, lo que mejora la eficiencia y la escalabilidad del sistema.

### **3. Cohere**
- **Uso**: Generación de embeddings y respuestas generativas.
- **Motivo**: Utilicé el modelo multilingual-v3.0 para generar embeddings multilingües de alta calidad, optimizados para manejar texto en varios idiomas. Esto permite comprender preguntas y buscar similitudes semánticas de forma precisa, incluso en diferentes lenguajes. Aunque el modelo soporta múltiples idiomas (importante para comprensión de preguntas en diferentes idiomas), las respuestas se especifican siempre en español para garantizar consistencia en la comunicación.

### **4. ChromaDB**
- **Uso**: Base de datos vectorial para almacenar y recuperar embeddings.
- **Motivo**: Permite búsquedas eficientes y rápidas en un espacio vectorial, ideal para encontrar documentos relevantes basados en similitud semántica.

### **5. Python**
- **Uso**: Lenguaje principal para la implementación del flujo RAG.
- **Motivo**: Su amplio ecosistema de bibliotecas y soporte para APIs como Cohere lo hacen ideal para proyectos de IA.

### **6. RAG (Retrieve-Answer-Generate)**
- **Uso**: Arquitectura utilizada para responder preguntas.
- **Motivo**: Combina lo mejor de la recuperación de información (retrieval) y generación de texto (generation) para ofrecer respuestas precisas y contextualizadas.

## ARQUITECTURA DEL PROYECTO

### **1. Flujo del Sistema**
1. **Generación de embeddings**:
   - Se utiliza el modelo `embed-multilingual-v3.0` para convertir el texto del prompt y los chunks de la historia en un embedding vectorial.
2. **Búsqueda en la base de datos**:
   - El embedding generado se compara con los almacenados en ChromaDB(embeddings de chunks) para recuperar el documento más relevante.
3. **Generación de respuesta**:
   - Utilizando el modelo generativo de Cohere, se produce una respuesta personalizada(según las características especificadas en system_prompt) basada en el documento relevante.

### **2. Archivos Principales**
- **`RAG.ipynb`**: Contiene el código estructurado de manera accesible listo para ser ejecutado.
- **`historias.pdf`**: Documento del cual se ha extraido la información para pasarle como contexto al modelo.
- **`embeddings.json`**: Directorio que almacena los datos de historias en formato vectorial (Cada embedding con su chunk correspondiente)
- **`README.md`**: Documentación del proyecto.
- **`requirements.txt`**: Archivo con  librerias necesarias para instalar.

## INSTRUCCIONES DE EJECUCIÓN
### **1. Requisitos**
- Python 3.8 o superior.

### **3. Instalación**
1. Clona este repositorio:
   ```
   git clone https://github.com/LuzTappero/Challenge-proyectoRAG
   cd proyecto-rag

2. Creación de entorno virtual(recomendado):

   - Para crear el entorno: python -m venv venv,
   - Para activar el entorno: .\venv\Scripts\activate

2. Instala las dependencias necesarias en el entorno virtual
   - pip install -r requirements.txt

   - Crear un archivo .env para colocar tu API_KEY de Cohere.

### **3.Ejecución**
    En la raiz del proyecto desde la terminal ejecutar el comando:
       ```
        jupyter lab

   Esto abrirá Jupyter Lab en tu navegador predeterminado accediendo a tu notebook para comenzar la ejecución.

## EJEMPLO DE USO

   #Uso - prueba 1 - Historia Sol y Luna

   #Definición del prompt

   - prompt = "¿Quiénes son Sol y luna?"

   #Llamada a la función RAG_answer

   - response = RAG_answer(prompt, collection, system_prompt)

   #Obtención de la respuesta
   - print(response)

¡Sol y Luna son dos adorables gatitos 🐱! Sol es muy valiente y le encanta explorar, mientras que Luna es más tranquila y suave como una nube 🌙. ¡Son los mejores amigos y siempre se divierten juntos! 😻


