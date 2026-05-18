# 💊 Módulo: Análisis de Interacciones Fármaco-Proteína

> **Plataforma Web para la Manipulación, Visualización y Análisis de Datos Bioinformáticos con Aplicaciones en la Industria Farmacéutica**  
> Proyecto académico de tesis | Jupyter Notebook | Google Colaboratory

---
## [Código de la Herramienta](https://github.com/JManuelRG/Herramientas-NCBI/blob/main/Interacci%C3%B3n%20F%C3%A1rmaco-Prote%C3%ADna/Interacci%C3%B3n_farmaco_proteina.ipynb)


## 📋 Descripción

Este módulo implementa un pipeline automatizado en Python 3 para el análisis de interacciones moleculares entre un fármaco y su proteína blanco. A partir del nombre de un fármaco, el módulo identifica automáticamente su target molecular, recupera la estructura cristalográfica correspondiente desde la base de datos RCSB PDB, procesa el archivo estructural y caracteriza todas las interacciones moleculares entre el ligando y los residuos del sitio de unión, incluyendo una visualización tridimensional del complejo fármaco-proteína.

El módulo fue desarrollado en Google Colaboratory y está diseñado para ser reproducible sin configuración de entorno local.

---

## ⚙️ Dependencias

Las siguientes librerías son instaladas automáticamente mediante `pip` al inicio del notebook:

| Librería | Uso principal |
|---|---|
| `BioPython` | Parseo de archivos PDB, análisis de estructura proteica |
| `NumPy` | Cálculo de distancias y geometría molecular |
| `Pandas` | Construcción y estilización de tablas de interacciones |
| `Matplotlib` / `py3Dmol` | Visualización tridimensional del complejo fármaco-proteína |

```python
# Instalación (incluida en el notebook)
!pip install biopython numpy pandas matplotlib py3Dmol
```

---

## 🔬 Metodología

### 1. Entrada y recuperación del target molecular
- El módulo recibe como entrada el nombre del fármaco
- Identifica automáticamente su proteína blanco (target) y el mecanismo de acción
- Recupera el código PDB de la estructura cristalográfica del complejo fármaco-proteína y el identificador del ligando en la estructura

### 2. Descarga y procesamiento de la estructura
- Descarga automática del archivo `.pdb` desde los servidores del RCSB Protein Data Bank
- Procesamiento de la estructura para localizar el ligando y los residuos del sitio de unión

### 3. Análisis de interacciones moleculares
El módulo identifica y clasifica los siguientes tipos de interacciones entre el fármaco y la proteína:

| Tipo de interacción | Criterio geométrico |
|---|---|
| Contacto hidrofóbico | Distancia entre átomos de carbono alifático/aromático ≤ umbral definido |
| Puente de hidrógeno | Distancia donor–aceptor ≤ 3.5 Å, ángulo ≥ 120° |
| Apilamiento π-π | Distancia entre anillos aromáticos ≤ 5.5 Å, ángulo paralelo o perpendicular |
| Contacto aromático π | Interacción de sistema π con átomo cargado o polar |
| Interacción iónica | Distancia entre grupos cargados ≤ 4.0 Å |
| Puente de H mediado por agua | Molécula de agua como puente entre fármaco y residuo |

### 4. Visualización
- Tabla detallada de interacciones por residuo y tipo, generada con `Pandas`
- Visualización tridimensional interactiva del complejo fármaco-proteína con el ligando en el sitio de unión

---

## 💉 Caso de uso: Imatinib – BCR-ABL (Leucemia Mieloide Crónica)

Para validar el módulo se analizó el imatinib, inhibidor de tirosina quinasa utilizado en el tratamiento de la leucemia mieloide crónica (Buchdunger, 2002).

### Identificación automática del target

| Parámetro | Valor recuperado |
|---|---|
| Fármaco | Imatinib |
| Target molecular | Proteína tirosina quinasa BCR-ABL |
| Código PDB | `1IEP` |
| Identificador del ligando en PDB | `STI` |
| Mecanismo de acción | Inhibidor tipo II del sitio de ATP de BCR-ABL |

### Resumen de interacciones identificadas

Se identificaron un total de 24 interacciones entre el imatinib y los residuos del sitio de unión:

| Tipo de interacción | Número de residuos |
|---|---|
| Contacto hidrofóbico | 14 |
| Puente de hidrógeno | 4 |
| Apilamiento π-π | 2 |
| Contacto aromático π | 1 |
| Interacción iónica | 1 |
| Puente de H mediado por agua | 1 |
| **Total** | **24** |

### Residuos del sitio de captación de ATP

De las 24 interacciones identificadas, 7 residuos participan directamente en el sitio de unión al ATP de la quinasa:

| Residuo | Relevancia clínica |
|---|---|
| `VAL289` | Sitio de unión al ATP |
| `GLU286` | Sitio de unión al ATP |
| `MET290` | Sitio de unión al ATP |
| `THR315` | Sitio de unión al ATP — mutación T315I: principal mecanismo de resistencia al imatinib |
| `PHE317` | Sitio de unión al ATP |
| `MET318` | Sitio de unión al ATP |
| `ASP381` | Sitio de unión al ATP |

> Las mutaciones sobre estos residuos constituyen el principal mecanismo de resistencia al imatinib en pacientes con leucemia mieloide crónica. La identificación computacional de estos residuos clave permite anticipar posibles sitios de resistencia sin necesidad de ensayos fenotípicos adicionales (Gambacorti-Passerini, 2013).

### Relevancia farmacéutica
El imatinib estabiliza la conformación inactiva de BCR-ABL compitiendo con el ATP por su sitio de unión, lo que bloquea la autofosforilación de la enzima e inhibe la señalización proliferativa característica de la leucemia mieloide crónica. Las 24 interacciones identificadas son consistentes con la red de contactos moleculares descrita por Nagar et al. (2007).

---

## 📁 Contenido de la carpeta

```
Interacción Fármaco-Proteína/
│
├── interaccion_farmaco_proteina.ipynb   # Notebook principal del módulo
└── README.md                            # Este archivo
```

---

## 🚀 Cómo usar el módulo

1. Abrir el notebook en Google Colaboratory
2. Ejecutar la celda de instalación de dependencias
3. Ingresar el nombre del fármaco cuando el módulo lo solicite
4. Ejecutar las celdas en orden secuencial
5. El módulo generará automáticamente:
   - Identificación del target molecular y mecanismo de acción
   - Descarga y procesamiento del archivo PDB
   - Tabla de interacciones clasificadas por tipo y residuo
   - Visualización tridimensional del complejo fármaco-proteína

---

## 📚 Referencias

- Buchdunger, E., et al. (2002). Imatinib (STI571) is a potent and selective inhibitor of the ABL tyrosine kinase. *European Journal of Cancer*, 38(Suppl 5), S28–S36.
- Nagar, B., et al. (2007). Structural basis for the autoinhibition of c-Abl tyrosine kinase. *Cell*, 112(6), 859–871.
- Gambacorti-Passerini, C., et al. (2013). Molecular mechanisms of resistance to imatinib in Philadelphia-chromosome-positive leukaemias. *The Lancet Oncology*, 4(2), 75–85.
- RCSB Protein Data Bank: https://www.rcsb.org/
- Entrada PDB 1IEP: https://www.rcsb.org/structure/1IEP

---

Proyecto Terminal
Repositorio: [Herramientas-NCBI](https://github.com/JManuelRG/Herramientas-NCBI)
