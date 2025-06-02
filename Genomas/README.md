# 🧬 Comparación de Variantes de Virus en Google Colab

Este repositorio contiene un notebook de Google Colab que permite comparar variantes virales a partir de sus secuencias genómicas completas. Utiliza datos del **NCBI (National Center for Biotechnology Information)** y herramientas de bioinformática para:

- Buscar variantes virales por nombre o identificador.
- Descargar genomas completos en formato FASTA desde NCBI Assembly.
- Comparar secuencias utilizando alineamiento global o local (BLAST).
- Identificar mutaciones entre variantes, incluyendo si son codificantes y si afectan la secuencia proteica.

---

## 🔗 Acceso rápido

[![Abrir en Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/tu-usuario/tu-repo/blob/main/comparacion_variantes.ipynb)

---

## 📁 Contenido del repositorio

El notebook está diseñado para ejecutarse directamente en **Google Colab**, por lo que no necesitas instalar nada localmente. Solo necesitas una cuenta de Google y conexión a internet.

Si deseas ejecutarlo localmente, asegúrate de tener instalado:

- Python ≥ 3.8
- Biopython
- Requests
- pandas
- matplotlib
- 
## Instrucciones de Uso

Este script permite acceder a la base de datos Genome del NCBI para buscar genomas de virus específicos y descargar las secuencias de las cepas (isolates) disponibles en la sección *Assembly*. 

A continuación se explica cómo utilizar el código con un ejemplo práctico para el virus **Ebola**.

---

### Paso 1: Acceso a la página Genome del NCBI

El código está configurado para conectarse directamente a la sección *Genome* de NCBI:  
[https://www.ncbi.nlm.nih.gov/genome/](https://www.ncbi.nlm.nih.gov/genome/)

### Paso 2: Búsqueda del virus

Se debe ingresar el nombre del virus a buscar. Por ejemplo, para buscar genomas de **Ebola**, el código realizará la consulta con la palabra clave `"Ebola"`.

### Paso 3: Listado de variantes (isolates) en Assembly

Dentro de los resultados, el script buscará en la sección *Assembly* las diferentes variantes o isolates disponibles para ese virus.

### Paso 4: Descarga de los genomas

Para cada isolate detectado, el código descargará la secuencia del genoma completo en formato FASTA desde el enlace de "View Genbank sequences".





