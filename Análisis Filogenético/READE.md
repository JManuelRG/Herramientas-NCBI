# 🌿 Módulo: Análisis Filogenético con MLSA

> **Plataforma Web para la Manipulación, Visualización y Análisis de Datos Bioinformáticos con Aplicaciones en la Industria Farmacéutica**  
> Proyecto Terminal | Jupyter Notebook | Google Colaboratory

---

## 📋 Descripción

Este módulo implementa un pipeline automatizado en Python 3 para la **reconstrucción filogenética de especies bacterianas** mediante el enfoque de *Multilocus Sequence Analysis* (MLSA). A partir del nombre de una especie bacteriana, el módulo valida su clasificación taxonómica, identifica automáticamente su esquema MLSA en **PubMLST**, descarga las secuencias de los genes *housekeeping* desde **GenBank (NCBI)**, y genera un árbol filogenético por el método **Neighbor-Joining**, junto con una **matriz de presencia y conservación génica** que incluye genes de resistencia a antibióticos.

El módulo fue desarrollado en **Google Colaboratory** y está diseñado para ser reproducible sin configuración de entorno local.

---

## ⚙️ Dependencias

Las siguientes librerías son instaladas automáticamente mediante `pip` al inicio del notebook:

| Librería | Uso principal |
|---|---|
| `BioPython` | Acceso a NCBI Entrez, alineamiento, parseo de secuencias, construcción de árboles |
| `NumPy` | Cálculo de matrices de distancias genéticas |
| `Pandas` | Construcción y estilización de la matriz de conservación génica |
| `Matplotlib` | Visualización del árbol filogenético y matriz de presencia |

```python
# Instalación (incluida en el notebook)
!pip install biopython numpy pandas matplotlib
```

---

## 🔬 Metodología

### 1. Entrada y validación taxonómica
- El módulo recibe como entrada el **nombre de una especie bacteriana**
- Valida automáticamente su clasificación taxonómica (dominio, filo, clase, orden, familia, género) mediante consulta a NCBI Taxonomy

### 2. Identificación del esquema MLSA
- Consulta automática a **PubMLST** para obtener el panel de genes *housekeeping* definido para la especie
- Los genes con **cobertura menor al 50%** entre las especies analizadas son descartados automáticamente del análisis

### 3. Descarga de secuencias
- Búsqueda y descarga de secuencias de cada gen desde **GenBank** mediante `Entrez.esearch` y `Entrez.efetch`
- Las secuencias son concatenadas para cada organismo, generando un **supergen MLSA**

### 4. Selección del modelo de sustitución
El módulo selecciona automáticamente el modelo de distancias genéticas según la distancia media del ingroup:

| Distancia media | Modelo seleccionado |
|---|---|
| ≤ 0.15 sustituciones/sitio | Jukes-Cantor (JC) |
| > 0.15 sustituciones/sitio | Kimura de dos parámetros (K2P) |

### 5. Reconstrucción filogenética
- Algoritmo **Neighbor-Joining** sobre la matriz de distancias K2P/JC
- Selección automática del **outgroup**: género distinto dentro de la misma familia taxonómica
- Árbol visualizado con `Matplotlib`

### 6. Matriz de presencia y conservación génica
- Incluye los genes MLSA del panel y **genes de resistencia a antibióticos** identificados en el genoma de referencia
- Los porcentajes de identidad se calculan respecto a la especie de referencia ingresada

---

## 🦠 Caso de uso: *Acinetobacter baumannii*

Para validar el módulo se utilizó *Acinetobacter baumannii*, patógeno nosocomial clasificado por la OMS como **prioridad crítica** por su amplio espectro de resistencia antimicrobiana.

### Validación taxonómica automática

| Nivel | Clasificación |
|---|---|
| Dominio | Bacteria |
| Filo | Pseudomonadota |
| Clase | Gammaproteobacteria |
| Orden | Moraxellales |
| Familia | Moraxellaceae |
| Género | *Acinetobacter* |

### Esquema MLSA identificado (Oxford)
Panel de 7 genes *housekeeping* (Bartual, 2005):

| Gen | Proteína codificada | Estado en el análisis |
|---|---|---|
| `gltA` | Citrato sintasa | ✅ Incluido |
| `gyrB` | Subunidad B de ADN girasa | ✅ Incluido |
| `recA` | Factor de recombinación homóloga | ✅ Incluido |
| `cpn60` | Chaperonina 60 kDa | ✅ Incluido |
| `rpoD` | Factor sigma de ARN polimerasa | ✅ Incluido |
| `gdhB` | Glucosa deshidrogenasa B | ❌ Descartado (presente en 2/10 especies) |
| `gpi` | Glucosa-6-fosfato isomerasa | ❌ Descartado (presente en 1/10 especies) |

> `gdhB` fue descartado por la presencia de un gen duplicado (`gdhB2`) que genera recuperación de secuencias no confiables en GenBank (Gaiarsa, 2019).  
> `gpi` fue descartado por transferencia horizontal de genes frecuente en regiones relacionadas con la cápsula bacteriana (Gaiarsa, 2019).

**Secuencia concatenada final:** 2,775 pb por organismo (5 genes)

### Selección del modelo y outgroup

| Parámetro | Valor |
|---|---|
| Distancia media ingroup | 0.2928 sustituciones/sitio |
| Modelo seleccionado | Kimura dos parámetros (K2P) |
| Outgroup | *Psychrobacter nivimaris* (dist. media: 0.3119) |
| Total de especies en el árbol | 10 |

### Genes de resistencia identificados en la matriz

| Gen | Función | Resistencia conferida |
|---|---|---|
| `cxpE` | Permeasa de membrana interna | Cloranfenicol (resistencia intrínseca) |
| `mrdA` | Proteína PBP2 (síntesis de peptidoglicano) | Blanco de betalactámicos |
| `adeK` | Canal externo de bomba de eflujo AdeIJK | Betalactámicos, tetraciclinas, fluoroquinolonas, cloranfenicol, eritromicina, rifampicina |
| `baeS` | Sensor de sistema regulador de dos componentes | Regulación de bombas de eflujo |
| `mdtD` | Proteína transportadora MFS | Resistencia a múltiples fármacos |

---

## 📁 Contenido de la carpeta

```
Análisis Filogenético/
│
├── analisis_filogenetico.ipynb   # Notebook principal del módulo
└── README.md                     # Este archivo
```

---

## 🚀 Cómo usar el módulo

1. Abrir el notebook en **Google Colaboratory**
2. Ejecutar la celda de instalación de dependencias
3. Ingresar el **nombre de la especie bacteriana** cuando el módulo lo solicite
4. Ejecutar las celdas en orden secuencial
5. El módulo generará automáticamente:
   - Validación taxonómica
   - Panel MLSA con filtro de cobertura
   - Árbol filogenético Neighbor-Joining
   - Matriz de presencia y conservación génica con genes de resistencia

---

## 📚 Referencias

- Bartual, S. G., et al. (2005). Development of a multilocus sequence typing scheme for characterization of clinical isolates of *Acinetobacter baumannii*. *Journal of Clinical Microbiology*, 43(9), 4382–4390.
- Gaiarsa, S., et al. (2019). Genomic epidemiology of *Acinetobacter baumannii* and the dissemination of antimicrobial resistance globally. *BMC Genomics*.
- Kimura, M. (1980). A simple method for estimating evolutionary rates of base substitutions through comparative studies of nucleotide sequences. *Journal of Molecular Evolution*, 16(2), 111–120.
- Damier-Piolle, L., et al. (2007). AdeIJK, a resistance-nodulation-cell division pump effluxing multiple antibiotics in *Acinetobacter baumannii*. *Antimicrobial Agents and Chemotherapy*, 52(2), 557–562.
- Nemec, A., et al. (2001). *Acinetobacter ursingii* sp. nov. and *Acinetobacter schindleri* sp. nov. *International Journal of Systematic and Evolutionary Microbiology*.
- Rossau, R., et al. (1991). Taxonomy of Moraxellaceae fam. nov. *International Journal of Systematic Bacteriology*, 41(2), 310–319.
- Yamamoto, S., & Harayama, S. (1996). Phylogenetic analysis of *Acinetobacter* strains based on the nucleotide sequences of gyrB genes. *International Journal of Systematic Bacteriology*, 46(2), 506–511.
- Vázquez-López, R., et al. (2020). The resistome of *Acinetobacter baumannii*. *Microorganisms*, 8(6), 935.
- PubMLST: https://pubmlst.org/
- NCBI GenBank: https://www.ncbi.nlm.nih.gov/genbank/

---

## 👤 Autor

**J. Manuel R. G.**  
Proyecto de tesis académica  
Repositorio: [Herramientas-NCBI](https://github.com/JManuelRG/Herramientas-NCBI)
