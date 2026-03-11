<a id="readme-top"></a>

[![Python][python-shield]][python-url]
[![Scikit-learn][sklearn-shield]][sklearn-url]
[![Plotly][plotly-shield]][plotly-url]
[![Jupyter][jupyter-shield]][jupyter-url]

<br />
<div align="center">
  <h1>🔬 TelecomX LATAM — Modelado Predictivo de Churn</h1>
  <p>
    Parte 2 del análisis de abandono de clientes: preparación de datos, balanceo de clases con SMOTE y entrenamiento de modelos de Machine Learning.
  </p>
  <p>
    <a href="#sobre-el-proyecto">Proyecto</a>
    ·
    <a href="#resultados">Resultados</a>
    ·
    <a href="#recomendaciones">Recomendaciones</a>
  </p>
</div>

---

<details>
  <summary>Tabla de Contenidos</summary>
  <ol>
    <li><a href="#sobre-el-proyecto">Sobre el Proyecto</a></li>
    <li><a href="#construido-con">Construido Con</a></li>
    <li><a href="#estructura">Estructura</a></li>
    <li><a href="#cómo-empezar">Cómo Empezar</a></li>
    <li><a href="#pipeline">Pipeline</a></li>
    <li><a href="#resultados">Resultados</a></li>
    <li><a href="#recomendaciones">Recomendaciones</a></li>
    <li><a href="#autor">Autor</a></li>
    <li><a href="#agradecimientos">Agradecimientos</a></li>
  </ol>
</details>

---

## Sobre el Proyecto

Continuación del análisis exploratorio (Parte 1). En esta fase se toman los datos limpios y se construye un pipeline de Machine Learning para predecir qué clientes tienen mayor probabilidad de abandonar el servicio.

El enfoque incluye:
- Encoding de variables categóricas y estandarización.
- Análisis de correlación para selección de variables.
- Balanceo de clases con **SMOTE** para abordar el desbalance (~78% Stayed / ~22% Churned).
- Entrenamiento y evaluación de **Regresión Logística** y **Random Forest**.
- Análisis de importancia de variables y coeficientes.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

---

## Construido Con

| Herramienta | Uso |
|-------------|-----|
| **Python 3.x** | Lenguaje principal |
| **Pandas / NumPy** | Manipulación de datos |
| **Scikit-learn** | Modelos, métricas, estandarización |
| **Imbalanced-learn** | SMOTE para balanceo de clases |
| **Plotly** | Visualizaciones interactivas |
| **Jupyter Notebook** | Entorno de desarrollo |

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

---

## Estructura

```
telecom-x-2/
│
├── Parte_2_TelecomX_LATAM.ipynb   # Notebook con el pipeline completo
├── df_final.csv                    # Dataset limpio (de Parte 1)
└── README.md
```

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

---

## Cómo Empezar

### Prerrequisitos

- Python 3.8+

### Instalación

```sh
git clone https://github.com/psychedelic-art/telecom-x-2.git
cd telecom-x-2
pip install pandas numpy scikit-learn imbalanced-learn plotly jupyter
jupyter notebook Parte_2_TelecomX_LATAM.ipynb
```

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

---

## Pipeline

### 1. Preparación de datos
- Eliminación de `customerID`.
- One-hot encoding de `InternetService`, `Contract`, `PaymentMethod`.
- Mapeo de `gender` a binario.
- Estandarización con `StandardScaler`.

### 2. Correlación y selección
- Análisis de correlación de Pearson contra `Churn`.
- Box plots de las variables más correlacionadas (`tenure`, `Charges_Monthly`, `Charges_Total`).

### 3. Modelado
- Split **70/30** estratificado.
- Balanceo con **SMOTE** (clase minoritaria igualada a la mayoritaria).
- Modelos: Regresión Logística y Random Forest (con `max_depth=10`, `min_samples_leaf=5`).

### 4. Evaluación
- Classification report, matrices de confusión y ROC-AUC.
- Análisis de overfitting/underfitting.
- Feature importance (RF) y coeficientes (LR).

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

---

## Resultados

| Métrica | Regresión Logística | Random Forest |
|---------|:-------------------:|:-------------:|
| Train accuracy | ~72% | ~82% |
| Test accuracy | ~68% | ~68% |
| Recall (Churned) | ~73% | ~73% |
| ROC-AUC | ~0.77 | ~0.76 |

**Modelo seleccionado: Regresión Logística** — rendimiento equivalente al Random Forest en test, pero con mayor interpretabilidad y sin riesgo de sobreajuste.

### Variables más influyentes

| Variable | Efecto |
|----------|--------|
| `Contract_Month-to-month` | Mayor aumento del churn |
| `tenure` | A mayor antigüedad, menor abandono |
| `Contract_Two year` | Mayor reducción del churn |
| `Charges_Monthly` | Cargos altos asociados a más abandono |
| `PaymentMethod_Electronic check` | Aumenta el riesgo |

### Impacto de SMOTE

Sin balanceo el recall para Churned era ~52% (la mitad de los abandonos pasaban desapercibidos). Con SMOTE sube a ~73%, lo cual es más útil para campañas de retención donde el costo de no detectar un abandono supera al de una falsa alarma.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

---

## Recomendaciones

1. **Incentivar contratos a largo plazo** — es la variable con mayor peso en ambos modelos.
2. **Retención temprana** — los primeros meses son los de mayor riesgo.
3. **Revisar tarifas de fibra óptica** — cargos altos se asocian con abandono.
4. **Migrar pagos con cheque electrónico** — incentivar métodos automáticos.
5. **Integrar el modelo en operaciones** — alertas tempranas para intervención proactiva.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

---

## Autor

**Andrés Muñoz** — [GitHub](https://github.com/psychedelic-art)

Proyecto: [https://github.com/psychedelic-art/telecom-x-2](https://github.com/psychedelic-art/telecom-x-2)

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

---

## Agradecimientos

- [Alura LATAM](https://www.aluracursos.com/) — Challenge Data Science
- [Best-README-Template](https://github.com/othneildrew/Best-README-Template)
- [imbalanced-learn](https://imbalanced-learn.org/) — SMOTE
- [Plotly](https://plotly.com/python/)

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

---

[python-shield]: https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white
[python-url]: https://python.org
[sklearn-shield]: https://img.shields.io/badge/Scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white
[sklearn-url]: https://scikit-learn.org
[plotly-shield]: https://img.shields.io/badge/Plotly-3F4F75?style=for-the-badge&logo=plotly&logoColor=white
[plotly-url]: https://plotly.com
[jupyter-shield]: https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white
[jupyter-url]: https://jupyter.org
