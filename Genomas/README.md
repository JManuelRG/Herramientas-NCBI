# 🧬 Comparación de Variantes de Virus en Google Colab

Este repositorio contiene un notebook de Google Colab que permite comparar variantes virales a partir de sus secuencias genómicas completas. Utiliza datos del **NCBI (National Center for Biotechnology Information)** y herramientas de bioinformática para:

- Buscar variantes virales por nombre o identificador.
- Descargar genomas completos en formato FASTA desde NCBI Assembly.
- Comparar secuencias utilizando alineamiento global o local (BLAST).
- Identificar mutaciones entre variantes, incluyendo si son codificantes y si afectan la secuencia proteica.
- (Opcional) Construir árboles filogenéticos.

## 🔗 Acceso rápido

[![Abrir en Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/tu-usuario/tu-repo/blob/main/comparacion_variantes.ipynb)

## 📁 Contenido del repositorio


## ⚙️ Requisitos

El notebook está diseñado para ejecutarse directamente en **Google Colab**, por lo que no necesitas instalar nada localmente. Solo necesitas una cuenta de Google y conexión a internet.

Si deseas ejecutarlo localmente, asegúrate de tener instalado:

- Python ≥ 3.8
- Biopython
- BLAST+ (si deseas usar comparaciones locales)

Puedes instalar las dependencias usando:

```bash
pip install biopython

