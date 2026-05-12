# 🧬 Módulo: Análisis Comparativo de Variantes Virales

> **Plataforma Web para la Manipulación, Visualización y Análisis de Datos Bioinformáticos con Aplicaciones en la Industria Farmacéutica**  
> Proyecto académico de tesis | Jupyter Notebook | Google Colaboratory

---

## 📋 Descripción

Este módulo implementa un pipeline automatizado en Python 3 para el **análisis comparativo de variantes nucleotídicas entre dos aislados virales**. A partir del nombre de los aislados, el módulo realiza la búsqueda y descarga automática de sus genomas desde la base de datos **GenBank (NCBI)**, ejecuta un alineamiento global y calcula un conjunto de métricas evolutivas y filogenéticas.

El módulo fue desarrollado en **Google Colaboratory** y está diseñado para ser reproducible y accesible sin configuración de entorno local.

---

## ⚙️ Dependencias

Las siguientes librerías son instaladas automáticamente mediante `pip` al inicio del notebook:

| Librería | Versión recomendada | Uso |
|---|---|---|
| `BioPython` | ≥ 1.81 | Acceso a NCBI Entrez, alineamiento, parseo de secuencias |
| `NumPy` | ≥ 1.24 | Cálculos numéricos y matrices |
| `Pandas` | ≥ 2.0 | Construcción y estilización de tablas de resultados |
| `Matplotlib` | ≥ 3.7 | Generación de gráficas de barras |

```python
# Instalación (incluida en el notebook)
!pip install biopython numpy pandas matplotlib
```

---

## 🔬 Metodología

### 1. Entrada de datos
El módulo recibe como entrada los **nombres exactos de dos aislados virales**, tal como aparecen en la sección *Genome* del portal NCBI. Se recomienda seguir el procedimiento descrito en el manual de usuario del repositorio para identificar los nombres correctos.

### 2. Búsqueda y descarga de secuencias
- **Búsqueda:** `Entrez.esearch` sobre la base de datos GenBank
- **Descarga:** `Entrez.efetch` en formato `.fasta`
- Se selecciona automáticamente el **genoma de mayor longitud disponible** para cada aislado

### 3. Alineamiento global
- Algoritmo de **Needleman-Wunsch** (Kellis, 2010)
- Implementado mediante `Bio.Align.PairwiseAligner`

### 4. Métricas calculadas

| Métrica | Método |
|---|---|
| Porcentaje de identidad | Cálculo directo del alineamiento |
| Gaps totales | Conteo en el alineamiento |
| Distancia p | Proporción de sitios diferentes |
| Distancia corregida | Modelo de Jukes-Cantor (Jukes, 1970) |
| Clasificación de SNPs | Transiciones (Ti) y transversiones (Tv) por gen codificante |
| Tasas Ka / Ks | Método de Nei-Gojobori (Nei, 1986) con corrección Jukes-Cantor |

### 5. Visualización de resultados
- **Tablas estilizadas** generadas con `Pandas`
- **Gráficas de barras** (frecuencia de mutaciones por gen y cociente Ka/Ks) con `Matplotlib`

---

## 🦠 Caso de uso: Ebolavirus

Para validar el módulo se compararon dos aislados del **Ebolavirus**:

| Aislado | Brote | Año | Región |
|---|---|---|---|
| `Ebola virus/H. sapiens-tc/COD/1995/Kikwit-9510623` | Kikwit | 1995 | República Democrática del Congo |
| `Ebola virus Makona isolate Frankfurt` | África Occidental | 2013–2016 | África Occidental |

### Resultados obtenidos

**Métricas generales del alineamiento:**

| Métrica | Valor |
|---|---|
| Identidad genómica | 96.83% |
| SNPs totales | 601 |
| Transiciones (Ti) | 499 |
| Transversiones (Tv) | 102 |
| Cociente Ti/Tv | 4.89 |
| SNPs en regiones codificantes | 390 |
| SNPs en regiones intergénicas | 211 |

**Análisis por gen codificante (genes con mayor variabilidad):**

| Gen | Total SNPs | Transiciones | Transversiones | Variantes no sinónimas |
|---|---|---|---|---|
| L | 170 | 145 | 25 | — |
| NP | 65 | — | — | — |
| GP | 64 | — | — | 36 (56.25%) |
| VP30 | 15 | — | — | 0 (100% sinónimas) |

> Los genes `sGP` y `SsGP` fueron excluidos del análisis Ka/Ks por no cumplir con el criterio mínimo de longitud requerido por el método de Nei-Gojobori, aunque sí fueron incluidos en el análisis de variantes nucleotídicas.

**Selección natural (Ka/Ks):**
- Todos los genes presentaron Ka/Ks < 1, indicando **selección purificante**
- Valor más alto: gen `GP` (Ka/Ks = 0.108)
- Valor más bajo: gen `VP30` (Ka/Ks = 0.000)

---

## 📁 Contenido de la carpeta

```
Variantes Virales/
│
├── variantes_virales.ipynb   # Notebook principal del módulo
└── README.md                 # Este archivo
```

> Las tablas detalladas de mutaciones por posición nucleotídica y cambios de aminoácido por gen se generan como salida del notebook durante la ejecución.

---

## 🚀 Cómo usar el módulo

1. Abrir el notebook en **Google Colaboratory**
2. Ejecutar la celda de instalación de dependencias
3. Ingresar el **nombre exacto de los dos aislados virales** cuando el módulo lo solicite (consultar la sección *Genome* del NCBI y el manual de usuario del repositorio)
4. Ejecutar las celdas en orden secuencial
5. Los resultados se presentarán como tablas y gráficas directamente en el notebook

---

## 📚 Referencias

- Kellis, M. (2010). *Computational Biology: Genomes, Networks, Evolution*. MIT OpenCourseWare.
- Jukes, T. H., & Cantor, C. R. (1970). Evolution of protein molecules. *Mammalian Protein Metabolism*, 3, 21–132.
- Nei, M., & Gojobori, T. (1986). Simple methods for estimating the numbers of synonymous and nonsynonymous nucleotide substitutions. *Molecular Biology and Evolution*, 3(5), 418–426.
- NCBI GenBank: https://www.ncbi.nlm.nih.gov/genbank/

---

## 👤 Autor

**J. Manuel R. G.**  
Proyecto de tesis académica  
Repositorio: [Herramientas-NCBI](https://github.com/JManuelRG/Herramientas-NCBI)
