# Herramienta de Comparación Genómica de Cepas Virales

Este proyecto en Python permite la búsqueda, descarga y comparación de genomas completos de cepas virales desde NCBI. Está diseñado para identificar diferencias entre variantes, mutaciones, y regiones conservadas, facilitando el análisis bioinformático en investigación y vigilancia genómica.

## Funcionalidades

- Búsqueda automática de cepas por nombre en NCBI Assembly.
- Descarga de genomas completos en formato FASTA.
- Comparación de secuencias genómicas mediante similitud de nucleótidos.
- Identificación y anotación básica de mutaciones (codificantes, sinónimas/no sinónimas).
- Salida visual de diferencias entre cepas.

---

## Ejemplo de uso

A continuación se muestra un ejemplo paso a paso de cómo utilizar la herramienta:

### Paso 1: Selección del organismo y acceso a la base de datos Genome en NCBI

Busca el organismo en NCBI Genome. En este ejemplo, se selecciona el virus del Ébola.

![Paso 1](ejem.PNG)

---

### Paso 2: Selección de cepa mediante el campo "Isolate"

Dentro del perfil del virus, copia el valor del aislado ("isolate") que será utilizado para la búsqueda y descarga.

![Paso 2](ejem1.PNG)

---

### Paso 3: Comparación de secuencias y análisis de diferencias

El código compara los genomas descargados, resalta diferencias nucleotídicas y posibles efectos sobre proteínas codificadas.

![Paso 3](ejem2.PNG)

---

## Requisitos

- Python 3.8 o superior
- Biopython
- requests
- pandas
- matplotlib

Instalación:

```bash
pip install biopython requests pandas matplotlib


```bash
pip install biopython

