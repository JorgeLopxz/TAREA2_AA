# Práctica 2: Aprendizaje No Supervisado — Determinación de Tipos de Estrellas

**Asignatura:** Aprendizaje Automático  
**Universidad:** Universidad Carlos III de Madrid  
**Puntuación:** 1.5 puntos (incluye 0.5 puntos por commits semanales en GitHub)

---

## Descripción

Este proyecto aplica técnicas de **aprendizaje no supervisado** para clasificar 240 estrellas a partir de sus propiedades físicas (temperatura, luminosidad, radio, magnitud absoluta, color y clase espectral). El objetivo es descubrir agrupaciones naturales mediante tres algoritmos de clustering y comparar los resultados con las clases astronómicas reales del diagrama de Hertzsprung-Russell.

### Pipeline de trabajo

1. **Preprocesamiento**: Codificación ordinal de variables categóricas (`Color`, `Spectral_Class`) respetando el orden energético/temperatura astronómica.
2. **Reducción de dimensionalidad**: PCA a 2 componentes principales.
3. **Clustering**: K-Means, Clustering Jerárquico (Dendrogramas) y DBSCAN.
4. **Evaluación**: Silhouette Score y Davies-Bouldin (K-Means/Jerárquico); DBCV (DBSCAN).
5. **Comparación**: Contraste de los clusters obtenidos con los tipos estelares astronómicos.

---

## Equipo

| Nombre | NIA |
|--------|-----|
| Jorge López Alonso | 100495876 |
| Álvaro Carrasco Fuentes | 100495918 |

---

## Estructura del Repositorio

```
TAREA2_AA/
├── data/
│   └── stars_data.csv          # Dataset con 240 estrellas (6 atributos)
├── notebooks/
│   └── Practica2_AA.ipynb      # Notebook principal con todo el análisis
├── .gitignore
└── README.md
```

---

## Requisitos e Instalación

### Dependencias principales

```bash
pip install numpy pandas matplotlib seaborn scikit-learn scipy
```

### Para DBCV (métrica de DBSCAN, no disponible en scikit-learn)

```bash
pip install hdbscan
```

### Ejecutar el notebook

```bash
cd notebooks
jupyter notebook Practica2_AA.ipynb
```

---

## Plan de Trabajo

> **Requisito**: Al menos **1 commit/push semanal** a este repositorio (0.5 puntos).

### Semana 1: 16–22 de abril
- [x] Inicialización del repositorio y estructura del proyecto
- [x] Análisis exploratorio del dataset (EDA): distribuciones, correlaciones, valores atípicos
- [x] Preprocesamiento: codificación ordinal de `Color` y `Spectral_Class`
- [x] Escalado de features con `StandardScaler`
- [x] Reducción de dimensionalidad: PCA a 2 componentes + visualización
- **Commit obligatorio antes del 22 de abril**

### Semana 2: 23–29 de abril
- [ ] Implementación de **K-Means**: método del codo + Silhouette para seleccionar k
- [ ] Implementación de **Clustering Jerárquico**: prueba de distintas funciones de enlace, análisis de dendrogramas, selección del número de clusters
- [ ] Visualización y métricas de ambos algoritmos (Silhouette, Davies-Bouldin, Calinski-Harabasz)
- [ ] Comparativa preliminar K-Means vs. Jerárquico
- **Commit obligatorio antes del 29 de abril**

### Semana 3: 30 de abril – 5 de mayo
- [ ] Implementación de **DBSCAN**: estimación de eps con heurística k-distancia, búsqueda de hiperparámetros, evaluación con DBCV
- [ ] Comparativa final de los tres algoritmos (tabla de métricas + visualizaciones)
- [ ] Recomendación del pipeline de clustering con justificación
- [ ] Comparación de clusters obtenidos con las 6 clases astronómicas reales
- [ ] Redacción de conclusiones
- [ ] Revisión final y entrega en Aula Global
- **Commit + Entrega final antes del 6 de mayo**

---

## Dataset

**Archivo:** `data/stars_data.csv`  
**Instancias:** 240 estrellas  
**Atributos:**

| Columna | Tipo | Descripción |
|---------|------|-------------|
| `Temperature` | Numérico | Temperatura superficial media (Kelvin) |
| `L` | Numérico | Luminosidad relativa al Sol |
| `R` | Numérico | Radio relativo al Sol |
| `A_M` | Numérico | Magnitud absoluta (brillo a 10 parsec) |
| `Color` | Categórico | Color principal del espectro |
| `Spectral_Class` | Categórico | Clase espectral (O, B, A, F, G, K, M) |

### Clases astronómicas de referencia

| Tipo | T (K) | L/L☉ | R/R☉ | A_M | Color | Clase Espectral |
|------|-------|-------|------|-----|-------|-----------------|
| Enana roja | 3 000 | 7.0×10⁻⁴ | 1.0×10⁻¹ | +17.5 | Rojo | K–M |
| Enana marrón | 3 300 | 5.5×10⁻³ | 3.5×10⁻¹ | +12.5 | Rojo | M |
| Enana blanca | 14 000 | 2.5×10⁻³ | 1.0×10⁻² | +12.6 | Blanco | B–G |
| Secuencia principal | 16 000 | 3.2×10⁴ | 4.4 | −0.4 | Blanco-amarillo | B–M |
| Supergigante | 15 000 | 3.0×10⁵ | 5.0×10¹ | −6.4 | Blanco-amarillo | B–M |
| Hipergigante | 11 000 | 3.0×10⁵ | 1.4×10³ | −9.6 | Amarillo | B–M |

---

## Notas de Reproducibilidad

- **Semilla aleatoria base:** `100495876` (NIA de Jorge López Alonso)
- Todos los algoritmos que requieren aleatoriedad usan `random_state=SEED`
- Los resultados deben ser completamente reproducibles ejecutando el notebook de arriba abajo
