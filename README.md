# Análisis de Big Data con Apache Hadoop y MapReduce

## 1. Descripción

Este proyecto implementa un ejercicio de procesamiento distribuido de datos utilizando Apache Hadoop, Java y el modelo de programación MapReduce.

Se desarrolla el algoritmo WordCount, cuyo propósito es identificar las palabras presentes en un archivo de texto y calcular su frecuencia de aparición.

## 2. Tecnologías utilizadas

- Apache Hadoop 3.5.0
- Java OpenJDK 17
- HDFS (Hadoop Distributed File System)
- YARN (Yet Another Resource Negotiator)
- MapReduce

## 3. Estructura del proyecto

```text
hadoop-wordcount/
├── src/
│   └── WordCount.java
├── input.txt
├── wordcount.jar
├── .gitignore
└── README.md
```

## 4. Funcionamiento

La implementación contempla las siguientes etapas:

1. **Mapper:** divide cada línea de texto en palabras y genera pares clave-valor `(palabra, 1)`.
2. **Shuffle and Sort:** agrupa los valores asociados a cada palabra.
3. **Combiner:** realiza una agregación parcial para reducir los registros que deben transferirse.
4. **Reducer:** suma las ocurrencias y genera la frecuencia final de cada palabra.

## 5. Ejecución

Compilación del programa:

```bash
javac -classpath "$(hadoop classpath --glob)" -d build src/WordCount.java
```

Empaquetamiento:

```bash
jar -cvf wordcount.jar -C build .
```

Carga de datos en HDFS:

```bash
hdfs dfs -mkdir -p /user/david/wordcount/input
hdfs dfs -put input.txt /user/david/wordcount/input/
```

Ejecución de MapReduce:

```bash
hadoop jar wordcount.jar WordCount /user/david/wordcount/input /user/david/wordcount/output
```

Consulta de resultados:

```bash
hdfs dfs -cat /user/david/wordcount/output/part-r-00000
```

## 6. Resultados

El procesamiento identificó siete palabras diferentes, con un total de trece ocurrencias:

| Palabra | Frecuencia |
|---|---:|
| big | 3 |
| con | 1 |
| data | 3 |
| datos | 1 |
| hadoop | 2 |
| mapreduce | 1 |
| procesa | 2 |

## 7. Evidencia de ejecución

- Trabajo MapReduce: `job_1794160592440_0001`.
- Aplicación YARN: `application_1794160592440_0001`.
- Estado final: `SUCCEEDED`.
- Tareas ejecutadas: 1 Mapper y 1 Reducer.
- Registros procesados: 4 líneas de entrada y 13 registros generados por el Mapper.

## 8. Conclusión

El ejercicio permitió implementar y ejecutar un proceso MapReduce utilizando Java y el ecosistema Apache Hadoop. Se comprobó la interacción entre HDFS, encargado del almacenamiento, YARN, responsable de la administración de recursos, y MapReduce, utilizado para el procesamiento de los datos.

La experiencia permitió comprender cómo se distribuyen las operaciones de transformación, agrupación y agregación de información dentro de una arquitectura Hadoop. La ejecución se realizó en un entorno pseudo-distribuido de un solo equipo.

