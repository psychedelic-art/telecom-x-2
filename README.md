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
- Balanceo de clases con **SMOTE** para abordar el desbalance (~74% Stayed / ~26% Churned).
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
├── telecomx_clean.csv              # Dataset limpio (exportado de Parte 1)
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
- Correlación de Pearson contra `Churn`.
- Box plots de las variables más correlacionadas (`tenure`, `Charges_Monthly`, `Charges_Total`).

### 3. Modelado
- Split **70/30** estratificado.
- Balanceo con **SMOTE** (clase minoritaria igualada a la mayoritaria).
- Modelos: Regresión Logística y Random Forest (`max_depth=10`, `min_samples_leaf=5`).

### 4. Evaluación
- Classification report, matrices de confusión y ROC-AUC.
- Análisis de overfitting/underfitting.
- Feature importance (RF) y coeficientes (LR).

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

---

## Resultados

| Métrica | Regresión Logística | Random Forest |
|---------|:-------------------:|:-------------:|
| Train accuracy | 78.24% | 87.80% |
| Test accuracy | 74.54% | 76.67% |
| Recall (Churned) | **80%** | 72% |
| ROC-AUC | 0.8399 | 0.8386 |

**Modelo seleccionado: Regresión Logística** — aunque el Random Forest tiene un accuracy ligeramente superior en test, LR alcanza un recall del **80%** para la clase Churned (frente al 72% de RF), lo que permite identificar a **8 de cada 10 clientes en riesgo de abandono**. Además, la brecha train/test de solo ~4% confirma una generalización sólida sin sobreajuste.

### Variables más influyentes

| Variable | Efecto |
|----------|--------|
| `Contract_Month-to-month` | Fuerte aumento del churn — sin compromiso contractual, el riesgo es máximo |
| `tenure` | Fuerte reducción — la antigüedad genera lealtad, los primeros meses son críticos |
| `Contract_Two year` | Fuerte reducción — el compromiso a largo plazo es la mayor barrera de salida |
| `Charges_Monthly` | Aumento — cargos altos correlacionan con mayor rotación |

### Impacto de SMOTE

El balanceo con SMOTE permitió que el modelo dejara de sesgarse hacia la clase mayoritaria. El recall para Churned subió hasta el **80%**, lo que significa que el modelo detecta eficazmente a 8 de cada 10 clientes que van a abandonar — una métrica crítica para el éxito de campañas de retención.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

---

## Recomendaciones

1. **Migración contractual** — Incentivar el paso de contratos mensuales a anuales mediante descuentos.
2. **Onboarding temprano** — Reforzar la atención en los primeros 6 meses de antigüedad.
3. **Optimización de pagos** — Promover el cambio de cheque electrónico a métodos automáticos.
4. **Monitoreo proactivo** — Desplegar el modelo para generar un score de riesgo semanal y contactar preventivamente a los clientes identificados dentro del 80% de acierto en churn.

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
