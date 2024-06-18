# Clase practica de RAG
Esta es una guía paso a paso para crear una aplicación RAG sencilla (Retrieval-Augmented Generation) utilizando chromadb y/o PostgreSQL, la API de OpenAI y modelos locales con ollama. 
También se explica como hacer preguntas sobre cualquier vídeo de YouTube.

## Configuración inicial e instalación de software necesario

### 1. Crear un entorno virtual e instalar los paquetes necesarios.
**Se recomienda utilizar python 3.10 o superior.**

```bash
$ python3 -m venv .venv
$ source .venv/bin/activate
$ pip install -r requirements.txt
```

### 2. Si se cuenta con una KEY de OPENAI:  
crear un archivo `.env` con la siguiente variable:

```bash
OPENAI_API_KEY = [ENTER YOUR OPENAI API KEY HERE]
```
Se puede cargar créditos en OPEN AI aquí: https://platform.openai.com/storage/files (es pago)

### 3. Instalar Ollama:

**Mac:**
```bash
https://ollama.ai/download/mac
```
**Linux:**
```bash
 curl https://ollama.ai/install.sh | sh
```
**Windows**

Todavía no es posible de forma nativa pero sí que lo podrías instalar utilizando WSL2
PD: Quizá puedas revisar ollama.ai a ver si ha habido novedades y si ya está disponible esta versión. 

**Información adicional**
```bash
https://lunaticoin.blog/ollama
```

### 4. Instalar modelos locales en ollama:

Ejecutar en la consola: 
```bash
 ollama list
```
para ver los modelos instalados. Si no hay ninguno bajar alguno de los existentes, esta lista: https://ollama.com/library
Se recomienda bajar alguno de estos 3: 
* gemma:latest
* llama3:latest
* llama3-chatqa:8b

```bash
 ollama pull gemma:latest
```
Cuando este descargado. Se puede probar en la consola con el siguiente comando:
```bash
 ollama run gemma:latest
```
Más información aqui: https://lunaticoin.blog/ollama

### 5. Instalar PostgreSQL (opcional)

1. para instalar PostgreSQL (version 12 o superior) revisar esta pagina: https://www.postgresql.org/download/

2. Verificar que el servicio esta corriendo:
```bash
service postgresql status
```
Sino lo esta, inicializarlo:

***Linux***
```bash
service postgresql start
```
***Mac***
```bash
brew services start postgresql
```

3. Crear una base de datos llamada: postgres
```bash
psql postgres
```

### 5.1 Instalar PGVector (complemento para PostgreSQL, opcional)

Para instalar el complemento que nos permitirá
guardar datos vectoriales:

**Linux and Mac**
```bash
cd /tmp
git clone --branch v0.7.2 https://github.com/pgvector/pgvector.git
cd pgvector
make
make install # may need sudo
```
**Windows**

Asegurarse que que esta corriendo el soporte para C++ en Visual Studio y ejecutar:

```bash
call "C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Auxiliary\Build\vcvars64.bat"
```
**Nota**: La ruta exacta variará según la versión y edición de Visual Studio.

Luego usa nmake para construir:
```bash
set "PGROOT=C:\Program Files\PostgreSQL\16"
cd %TEMP%
git clone --branch v0.7.2 https://github.com/pgvector/pgvector.git
cd pgvector
nmake /F Makefile.win
nmake /F Makefile.win install
```
**Más información**: https://github.com/pgvector/pgvector


### 6. levantar maquina jupyter local
```bash
python3.11 -m jupyter notebook 
```
