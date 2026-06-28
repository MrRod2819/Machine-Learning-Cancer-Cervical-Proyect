# ML-Cervical-Cancer-Risk-Prediction 

Este repositorio contiene el desarrollo y despliegue de un pipeline de **Machine Learning** diseñado para el triaje predictivo de riesgo de neoplasia cervical, utilizando el conjunto de datos clínicos *Cervical Cancer Risk Factors*. 

El objetivo primordial es maximizar la identificación de pacientes en riesgo (Clase 1) en entornos de salud pública, abordando técnicamente el desbalance crítico de clases mediante balanceo sintético e ingeniería de características.

---

##  Matriz de Rendimiento Comparativo (Tabla 5.1)

Tras evaluar las arquitecturas sobre el subconjunto de prueba `X_test_selected`, se consolidaron los siguientes resultados analíticos:

| Modelo de Machine Learning | Accuracy | Recall (Clase 1) | F1-Score (Clase 1) |
| :--- | :---: | :---: | :---: |
| **Regresión Logística** | **0.8546** | **36.36%** | **0.2424** |
| Red Neuronal (MLP) | 0.7732 | 18.18% | 0.0930 |
| LightGBM | 0.8895 | 9.09% | 0.0952 |

### Justificación de la Arquitectura Óptima
Aunque *LightGBM* registra la mayor exactitud global (88.95%), el proyecto demuestra la presencia de la **Paradoja de la Exactitud (*Accuracy Paradox*)** [12]. En contextos de triaje oncológico, optimizar bajo el *Accuracy* genera un sesgo crítico que invisibiliza los falsos negativos [13]. 

Al ser el único algoritmo capaz de sostener una estabilidad matemática real sobre la clase minoritaria, triplicando el F1-Score de los modelos complejos, la **Regresión Logística Regularizada** se selecciona como la arquitectura óptima para el despliegue.

---

##  Explicabilidad Global mediante Valores SHAP

El modelo integra una capa de interpretabilidad basada en **SHAP** (*SHapley Additive exPlanations*) para garantizar la transparencia clínica:
* **Vectores de Alto Riesgo (SHAP > 0):** Patologías específicas como `STDs:vulvo-perineal condylomatosis`, `STDs:HIV`, `Dx:HPV` y diagnósticos previos (`Dx:CIN`), junto a factores acumulativos como años de tabaquismo.
* **Control de Colinealidad:** El espacio lineal del modelo regulariza adecuadamente variables agregadas (`STDs (number)`) para evitar redundancias biológicas frente a infecciones ya mapeadas independientemente.

---

## Tecnologías Utilizadas
* **Lenguaje:** Python 3
* **Librerías Core:** Scikit-Learn, LightGBM, Imbalanced-Learn (SMOTE)
* **Interpretabilidad:** SHAP (SHapley Additive exPlanations)
* **Visualización:** Matplotlib & Seaborn

---

##  Referencias Bibliográficas
* [12] F. J. Valverde-Albacete and C. Peláez-Moreno, "100% Classification Accuracy Considered Harmful: The Normalized Information Transfer Factor Explains the Accuracy Paradox," *PLOS ONE*, vol. 9, no. 1, 2014.
* [13] D. Chicco and G. Jurman, "The advantages of the Matthews correlation coefficient (MCC) over F1 score and accuracy in binary classification evaluation," *BMC Genomics*, vol. 21, no. 1, 2020.
