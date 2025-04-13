# 📄

Esta guía describe la configuración de un entorno mínimo usando Docker Compose para trabajar con:

- 🧱 **Hadoop**
- ⚡ **Apache Spark**
- ☕ **Java**
- 🐍 **Python**
- 📓 **Jupyter Notebook**

---

## 🧭 Índice

- [📌 Descripción General](#-descripción-general)
- [🔧 Servicios y Configuración](#-servicios-y-configuración)
  - [🧱 Hadoop](#-hadoop)
  - [⚡ Apache Spark](#-apache-spark)
  - [📓 Jupyter Notebook y PySpark](#-jupyter-notebook-y-pyspark)
- [💾 Volúmenes](#-volúmenes)
- [🚀 Instrucciones de Uso](#-instrucciones-de-uso)

---

## 📌 Descripción General

Este entorno contiene servicios esenciales para ejecutar y experimentar con procesamiento distribuido de datos. Está diseñado para funcionar localmente con el mínimo de configuración extra.

---

## 🔧 Servicios y Configuración

### 🧱 Hadoop

| Servicio        | Imagen                                                                   | Puerto(s)        | Descripción                              |
|----------------|--------------------------------------------------------------------------|------------------|------------------------------------------|
| **namenode**    | `bde2020/hadoop-namenode:2.0.0-hadoop3.2.1-java8`                         | `9870`, `9000`   | UI del HDFS y punto de acceso HDFS       |
| **datanode**    | `bde2020/hadoop-datanode:2.0.0-hadoop3.2.1-java8`                         | —                | Almacén de datos                         |
| **resourcemanager** | `bde2020/hadoop-resourcemanager:2.0.0-hadoop3.2.1-java8`              | `8088`           | UI de YARN ResourceManager               |
| **nodemanager** | `bde2020/hadoop-nodemanager:2.0.0-hadoop3.2.1-java8`                      | —                | Gestión de recursos en los nodos         |

---

### ⚡ Apache Spark

| Servicio        | Imagen                                         | Puerto(s)       | Descripción                       |
|----------------|-----------------------------------------------|-----------------|-----------------------------------|
| **spark-master** | `bde2020/spark-master:3.0.0-hadoop3.2`        | `8080`, `7077`  | Coordinador del clúster de Spark |
| **spark-worker** | `bde2020/spark-worker:3.0.0-hadoop3.2`        | `8081`          | Nodo de ejecución de Spark       |

---

### 📓 Jupyter Notebook y PySpark

| Servicio    | Imagen                               | Puerto(s)         | Volumen                              |
|-------------|--------------------------------------|-------------------|--------------------------------------|
| **jupyter** | `jupyter/pyspark-notebook:latest`    | `8888`, `4040`    | `./notebooks:/home/jovyan/work`     |

- `8888`: Interfaz de Jupyter Lab / Notebook  
- `4040`: UI del Spark Driver (cuando se ejecuta un job)

---

## 💾 Volúmenes

| Nombre            | Usado por     | Ruta interna                        |
|-------------------|---------------|-------------------------------------|
| `hadoop_namenode` | namenode      | `/hadoop/dfs/name`                  |
| `hadoop_datanode` | datanode      | `/hadoop/dfs/data`                  |

---

## 🚀 Instrucciones de Uso

### ✅ Requisitos

- Tener instalado:
  - Docker
  - Docker Compose
- Acceso a internet (para descargar las imágenes)

---

### ▶️ Paso a Paso

1. Abre una terminal en el directorio del archivo `docker-compose.yml`.
2. Inicia el entorno:

   ```bash
   docker-compose up -d
   ```

3. Accede a los servicios en tu navegador:

| Servicio          | URL                                 |
|-------------------|--------------------------------------|
| HDFS (NameNode UI) | [http://localhost:9870](http://localhost:9870) |
| YARN UI           | [http://localhost:8088](http://localhost:8088) |
| Spark Master UI   | [http://localhost:8080](http://localhost:8080) |
| Spark Worker UI   | [http://localhost:8081](http://localhost:8081) |
| Jupyter Notebook  | [http://localhost:8888](http://localhost:8888) |

> 💡 El puerto `4040` se activa automáticamente al ejecutar un trabajo Spark desde Jupyter.

---

### 🛑 Para detener todo

```bash
docker-compose down
```

---

## 📝 Notas Finales

- Las imágenes de Hadoop y Spark ya incluyen **Java**, no necesitas instalar nada adicional.
- El contenedor `jupyter` ya viene con **Python**, **Spark** y **Jupyter Lab** listos para usar.
- Esta configuración está pensada para entornos de desarrollo y pruebas locales.
- Para obtener el **token** de jupyter consulta los logs del servicio de `jupyter notebook`

---

**Documentación generada automáticamente** 🤖
> ⚠️ *Esta documentación fue generada automáticamente. Verifica su contenido antes de usarlo.*
