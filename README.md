# 🧬 Herramientas NCBI — Plataforma Bioinformática para la Industria Farmacéutica

> **Proyecto Terminal — Ingeniería Farmacéutica**  
> Diseño de una Plataforma Web para la Manipulación, Visualización y Análisis de Datos Bioinformáticos con Aplicaciones en la Industria Farmacéutica

## 👤 Autores:
>    Presenta: Fernando López Machaén
>
> Asesores: Dr. José Manuel Rivera Garnica, Dra. Ma. Guadalupe Rojas Torres.

---

## 📌 Descripción general

Este repositorio contiene los módulos de análisis bioinformático desarrollados como proyecto terminal de la carrera de Ingeniería Farmacéutica. La plataforma está compuesta por tres módulos independientes programados en Python 3 sobre Google Colaboratory, que integran bases de datos públicas de biología molecular (NCBI GenBank, PubMLST y RCSB PDB) para realizar análisis de relevancia en la investigación farmacéutica y clínica.

Cada módulo recibe datos de entrada mínimos del usuario (nombre de un organismo, un aislado viral o un fármaco) y ejecuta automáticamente pipelines de búsqueda, procesamiento y visualización de datos biológicos, sin requerir instalación de software adicional ni configuración de entorno local.

---

## 🗂️ Estructura del repositorio

```
Herramientas-NCBI/
│
├── 📁 Variantes Virales/
│   ├── variantes_virales.ipynb
│   └── README.md
│
├── 📁 Análisis Filogenético/
│   ├── analisis_filogenetico.ipynb
│   └── README.md
│
├── 📁 Interacción Fármaco-Proteína/
    ├── interaccion_farmaco_proteina.ipynb
    └── README.md

```

---

## 🔬 Módulos

### 🦠 1. Análisis Comparativo de Variantes Virales
[`📂 Ver módulo`](./Variantes%20Virales/)

Pipeline para la comparación genómica de dos aislados virales. A partir de sus nombres, el módulo descarga automáticamente los genomas desde GenBank, realiza un alineamiento global por Needleman-Wunsch y calcula métricas evolutivas completas.

**Funcionalidades principales:**
- Búsqueda y descarga automática de genomas desde NCBI GenBank (`Entrez.esearch` / `Entrez.efetch`)
- Alineamiento global (Needleman-Wunsch) con `Bio.Align.PairwiseAligner`
- Cálculo de identidad, gaps, distancia p y corrección de Jukes-Cantor
- Clasificación de SNPs en transiciones y transversiones por gen codificante
- Estimación de tasas de sustitución sinónima (Ks) y no sinónima (Ka) por el método de Nei-Gojobori
- Tablas estilizadas con `Pandas` y gráficas de barras con `Matplotlib`

**Caso de uso validado:** Comparación de dos aislados del Ebolavirus (brote de Kikwit 1995 vs. brote de África Occidental 2013–2016) — Identidad genómica: 96.83%, 601 SNPs totales, Ka/Ks < 1 en todos los genes (selección purificante).

---

### 🌿 2. Análisis Filogenético con MLSA
[`📂 Ver módulo`](./An%C3%A1lisis%20Filogen%C3%A9tico/)

Pipeline para la reconstrucción filogenética de especies bacterianas mediante *Multilocus Sequence Analysis* (MLSA). Identifica automáticamente el esquema de genes *housekeeping* en PubMLST, descarga las secuencias desde GenBank y construye un árbol filogenético Neighbor-Joining, acompañado de una matriz de presencia y conservación génica con genes de resistencia a antibióticos.

**Funcionalidades principales:**
- Validación taxonómica automática vía NCBI Taxonomy
- Consulta automática a PubMLST para identificación del esquema MLSA
- Filtro de cobertura génica (descarte automático de genes presentes en < 50% de las especies)
- Selección automática del modelo de sustitución (Jukes-Cantor o Kimura dos parámetros según distancia media)
- Selección automática del outgroup por criterio taxonómico
- Reconstrucción filogenética Neighbor-Joining y árbol visualizado con `Matplotlib`
- Matriz de presencia y conservación génica con genes de resistencia a antibióticos

**Caso de uso validado:** Análisis filogenético de *Acinetobacter baumannii* (prioridad crítica OMS) — Árbol de 10 especies, esquema Oxford de 5 genes (2,775 pb concatenados), modelo K2P, identificación de 5 genes de resistencia cromosómica.

---

### 💊 3. Análisis de Interacciones Fármaco-Proteína
[`📂 Ver módulo`](./Interacci%C3%B3n%20F%C3%A1rmaco-Prote%C3%ADna/)

Pipeline para el análisis estructural de interacciones moleculares entre un fármaco y su proteína blanco. A partir del nombre del fármaco, identifica automáticamente el target molecular, descarga la estructura cristalográfica desde el RCSB PDB y caracteriza todas las interacciones moleculares del complejo, con visualización tridimensional.

**Funcionalidades principales:**
- Identificación automática del target molecular y mecanismo de acción
- Descarga automática del archivo PDB desde RCSB
- Clasificación de interacciones: contactos hidrofóbicos, puentes de hidrógeno, apilamiento π-π, interacciones iónicas y puentes de H mediados por agua
- Identificación de residuos en el sitio activo con relevancia clínica
- Tabla detallada de interacciones por residuo y tipo con `Pandas`
- Visualización tridimensional del complejo fármaco-proteína

**Caso de uso validado:** Análisis del imatinib sobre BCR-ABL (leucemia mieloide crónica, PDB: 1IEP) — 24 interacciones identificadas, 7 residuos en el sitio ATP, consistente con los mecanismos de resistencia clínicamente reportados.

---

## ⚙️ Requisitos técnicos

Todos los módulos están desarrollados para ejecutarse en Google Colaboratory sin configuración adicional. Las dependencias se instalan automáticamente al inicio de cada notebook.

| Librería | Uso |
|---|---|
| `BioPython` | Acceso a NCBI Entrez, parseo de secuencias y estructuras, alineamientos |
| `NumPy` | Cálculos numéricos y matrices |
| `Pandas` | Construcción y visualización de tablas de resultados |
| `Matplotlib` | Gráficas de barras y visualización de árboles filogenéticos |
| `py3Dmol` | Visualización tridimensional de estructuras moleculares |

---

## 🚀 Cómo ejecutar los módulos

1. Hacer clic en el notebook `.ipynb` de la carpeta del módulo deseado
2. Abrir en Google Colaboratory (botón _Open in Colab_ o desde el menú de GitHub)
3. Ejecutar la celda de instalación de dependencias
4. Ingresar los datos de entrada solicitados:
   - **Variantes Virales:** nombres exactos de dos aislados virales (obtenidos desde la sección *Genome* del NCBI)
   - **Análisis Filogenético:** nombre de la especie bacteriana
   - **Interacción Fármaco-Proteína:** nombre del fármaco
5. Ejecutar las celdas restantes en orden secuencial

> 💡 Para el módulo de **Variantes Virales**, se recomienda consultar la sección *Genome* del portal NCBI para obtener el nombre exacto de cada aislado antes de ejecutar el análisis.

---

## 🏗️ Bases de datos integradas

| Base de datos | URL | Uso en la plataforma |
|---|---|---|
| NCBI GenBank | https://www.ncbi.nlm.nih.gov/genbank/ | Descarga de genomas y secuencias génicas |
| NCBI Taxonomy | https://www.ncbi.nlm.nih.gov/taxonomy | Validación taxonómica de especies |
| PubMLST | https://pubmlst.org/ | Identificación de esquemas MLSA |
| RCSB PDB | https://www.rcsb.org/ | Descarga de estructuras cristalográficas |

---

## 📚 Referencias generales

- Jukes, T. H., & Cantor, C. R. (1970). Evolution of protein molecules. *Mammalian Protein Metabolism*, 3, 21–132.
- Kimura, M. (1980). A simple method for estimating evolutionary rates of base substitutions. *Journal of Molecular Evolution*, 16(2), 111–120.
- Nei, M., & Gojobori, T. (1986). Simple methods for estimating the numbers of synonymous and nonsynonymous nucleotide substitutions. *Molecular Biology and Evolution*, 3(5), 418–426.
- Bartual, S. G., et al. (2005). Development of a multilocus sequence typing scheme for *Acinetobacter baumannii*. *Journal of Clinical Microbiology*, 43(9), 4382–4390.
- Buchdunger, E., et al. (2002). Imatinib (STI571) is a potent and selective inhibitor of the ABL tyrosine kinase. *European Journal of Cancer*, 38(Suppl 5), S28–S36.
- Nagar, B., et al. (2007). Structural basis for the autoinhibition of c-Abl tyrosine kinase. *Cell*, 112(6), 859–871.
- Vázquez-López, R., et al. (2020). The resistome of *Acinetobacter baumannii*. *Microorganisms*, 8(6), 935.

---

## 📄 Licencia

Este proyecto se distribuye bajo la licencia **MIT**. Consulta el archivo [`LICENSE`](./LICENSE) para más detalles.

---



[![GitHub](https://img.shields.io/badge/GitHub-JManuelRG-181717?logo=github)](https://github.com/JManuelRG)
