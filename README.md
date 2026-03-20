---

# Desafio-Telecom-X-Latam-Parte-2 (Predicción de Cancelación de Clientes – Machine Learning aplicado)
Proyecto de **modelado predictivo y análisis explicativo de churn**, orientado a identificar clientes con alto riesgo de cancelación y transformar los resultados de machine learning en **estrategias concretas de retención**.

---

## Problema de Negocio

Las empresas de telecomunicaciones operan bajo modelos de **suscripción recurrente**, donde la rentabilidad depende principalmente de la **retención de clientes**.

Cuando un cliente cancela el servicio (churn), la empresa enfrenta:

* pérdida directa de ingresos recurrentes
* aumento del costo de adquisición de clientes (CAC)
* disminución del valor de vida del cliente (LTV)

En este contexto, **anticipar qué clientes podrían cancelar su servicio permite intervenir antes de que abandonen la empresa**.

El objetivo de este proyecto es:

* construir modelos predictivos de churn
* identificar los factores que más influyen en la cancelación
* traducir los resultados en **estrategias de retención basadas en datos**

---

## Enfoque Analítico

El proyecto sigue un enfoque completo de **ciencia de datos aplicada**:

1. Limpieza y preparación de datos
2. Análisis exploratorio (EDA)
3. Selección y reducción de variables
4. Entrenamiento de múltiples modelos de clasificación
5. Evaluación comparativa de desempeño
6. Interpretación de variables con SHAP y Odds Ratio
7. Traducción de resultados en estrategias de negocio

---

## Arquitectura del Pipeline de Ciencia de Datos

El proyecto sigue un pipeline completo de **Machine Learning aplicado**:

```
Datos → Limpieza → EDA → Selección de variables
        ↓
Modelos de Machine Learning
        ↓
Evaluación comparativa
        ↓
Explicabilidad de modelos
        ↓
Insights de negocio
        ↓
Estrategias de retención
```

---

## Modelos de Machine Learning Evaluados

Se entrenaron **7 algoritmos de clasificación**:

| Modelo              | Tipo                          |
| ------------------- | ----------------------------- |
| KNN                 | Basado en distancia           |
| SVM                 | Máquinas de soporte vectorial |
| Regresión Logística | Modelo lineal                 |
| Red Neuronal (MLP)  | Deep learning                 |
| Árbol de Decisión   | Modelo interpretable          |
| Random Forest       | Ensemble de árboles           |
| XGBoost             | Gradient boosting             |

---

## Evaluación de Modelos

Se utilizaron múltiples métricas para comparar desempeño:

* Accuracy
* Precision
* Recall
* F1-score
* ROC-AUC
* Precision–Recall
* Matriz de confusión

### Desempeño en conjunto de prueba

| Modelo              | Accuracy   | Precision  | Recall     | F1         |
| ------------------- | ---------- | ---------- | ---------- | ---------- |
| **XGBoost**         | 76.40%     | 53.80%     | 79.41%     | **64.15%** |
| Regresión Logística | 75.12%     | 52.13%     | 78.61%     | 62.69%     |
| Random Forest       | 76.62%     | 54.53%     | 72.46%     | 62.23%     |
| Árbol de Decisión   | 73.42%     | 50.00%     | **82.09%** | 62.15%     |
| SVM                 | 74.06%     | 50.77%     | 79.14%     | 61.86%     |
| Red Neuronal (MLP)  | **79.39%** | **62.14%** | 57.49%     | 59.72%     |
| KNN                 | 76.83%     | 56.59%     | 55.08%     | 55.83%     |

### Conclusión

**XGBoost presentó el mejor desempeño global**, logrando el mayor equilibrio entre:

* precisión
* recall
* F1-score

---

## Curva de Aprendizaje del Modelo

![Curva de Aprendizaje XGBoost Entrenamiento vs Validación](/images/Curva%20de%20Aprendizaje%20XGBoost%20Entrenamiento%20vs%20Validación.png)

El entrenamiento de XGBoost mostró que la mejor iteración se alcanza alrededor de:

**396 árboles**

Esto indica:

* buen aprendizaje del modelo
* baja probabilidad de sobreajuste
* estabilidad entre entrenamiento y validación

---

## Explicabilidad del Modelo

Se utilizaron tres enfoques para interpretar los modelos:

### 1. Coeficientes de Regresión Logística

Permiten interpretar el efecto de cada variable sobre la probabilidad de churn.

### 2. Odds Ratio

Transforman los coeficientes en **multiplicadores de probabilidad relativa**, facilitando su interpretación de negocio.

### 3. SHAP (Explainable AI)

Se utilizó SHAP para analizar el impacto de cada variable en la predicción del modelo.

Esto permite:

* identificar variables clave
* entender cómo cada variable afecta la predicción
* validar consistencia entre modelos

---

## Hallazgos Clave

* El churn ocurre principalmente en **clientes nuevos**.
* Los **contratos mensuales concentran la mayor fuga**.
* Los clientes de **mayor valor mensual son más sensibles al precio y la calidad**.
* Los servicios adicionales pueden **aumentar o reducir churn dependiendo del valor percibido**.
  
---

## Impacto Económico Potencial

Una reducción del churn tiene un impacto directo en los ingresos recurrentes de la empresa.

Supongamos el siguiente escenario hipotético:

* 10,000 clientes activos
* ingreso promedio mensual por cliente: **$70**
* churn actual: **26.6%**

Si mediante un sistema de predicción se logra reducir el churn en **solo 5%**, el impacto sería:

* **500 clientes retenidos**
* **$35,000 adicionales por mes**
* **$420,000 adicionales por año**

Esto demuestra que incluso mejoras moderadas en la retención pueden generar **impactos económicos significativos**.

---

## Sistema de Predicción de Churn en Producción

El modelo XGBoost desarrollado en este proyecto podría implementarse como un **sistema de alerta temprana de cancelación**.

Flujo de uso en producción:

```text
Datos de clientes actuales
        ↓
Modelo de predicción de churn
        ↓
Probabilidad de cancelación
        ↓
Clasificación de riesgo
        ↓
Activación de campañas de retención
```

Ejemplo de segmentación operativa:

| Probabilidad de churn | Nivel de riesgo | Acción recomendada                       |
| --------------------- | --------------- | ---------------------------------------- |
| > 0.80                | Alto            | Contacto inmediato / oferta de retención |
| 0.60 – 0.80           | Medio           | Incentivos y beneficios                  |
| < 0.60                | Bajo            | Seguimiento estándar                     |

Esto permite **priorizar recursos de retención en clientes con mayor probabilidad de abandonar el servicio.**

---

## Estrategias de Retención Propuestas

### 1. Incentivar contratos de mayor duración

Migrar clientes mensuales hacia contratos anuales o bienales.

### 2. Intervención en los primeros meses

Los primeros **6–12 meses son la ventana crítica de abandono**.

### 3. Programas de fidelización para clientes premium

Clientes con mayor gasto requieren **mejor experiencia y soporte**.

### 4. Mejora del servicio en clientes con fibra óptica

Este segmento presenta **mayor sensibilidad a calidad y precio**.

### 5. Sistema predictivo de riesgo de churn

Implementar un modelo como **XGBoost** para detectar clientes en riesgo y activar campañas de retención.

---

## Conclusión Final
El análisis demuestra que el churn en telecomunicaciones está principalmente determinado por:

* duración del contrato
* antigüedad del cliente
* tipo de servicio contratado
* valor mensual del plan

El modelo **XGBoost** presentó el mejor desempeño predictivo, mientras que la **Regresión Logística permitió interpretar con claridad los factores que explican la cancelación**.

El principal hallazgo estratégico es que:

**el churn no depende únicamente del precio, sino del valor percibido del servicio durante los primeros meses de relación con el cliente.**

**Reducir la cancelación requiere intervenir temprano, fortalecer la experiencia del cliente y promover contratos de mayor duración.**

---

## Posibles Mejoras Futuras

El proyecto podría extenderse mediante:

* **Ingeniería avanzada de variables**
* Modelos de **Deep Learning más complejos**
* **Modelos de supervivencia (Customer Lifetime Analysis)**
* Sistemas de **detección temprana de churn**
* integración con **dashboards de monitoreo en tiempo real**

---

## Tecnologías utilizadas

- **Python 3**
- **Pandas**: manipulación y análisis de datos.
- **NumPy**: operaciones numéricas.
- **Matplotlib**: visualización de datos estática.
- **Plotly**: visualización de datos interactiva y dinámica.
- **Scikit-learn** – modelos de machine learning
- **XGBoost** – gradient boosting
- **SHAP** – explicabilidad de modelo
- **Google Colab**: entorno de ejecución y colaboración.

---

## Datos

Los datos fueron obtenidos del tratamiento previo realizado en el [Desafío_Telecom_X_Latam](https://github.com/fsoaresg/Desafio_Telecom_X_Latam)

Fuente:[CSV](https://raw.githubusercontent.com/fsoaresg/Desafio-Telecom-X-Latam-Parte-2/refs/heads/main/Datos%20Telecom%20X%20Latam%20Parte%202/datos_procesados.csv)

---

## Visualizaciones

![Matriz de Correlación (Variables Numéricas)](/images/Matriz%20de%20Correlación%20(Variables%20Numéricas).png)

![Distribución de Variables Numéricas por Churn](images/Distribución%20de%20Variables%20Numéricas%20por%20Churn.png)

![Optimización de Hiperparámetros KNN](images/Optimización%20de%20Hiperparámetros%20KNN.png)

![Curvas ROC por Modelo (Evaluación en Test)](images/Curvas%20ROC%20por%20Modelo%20(Evaluación%20en%20Test).png)

![Curvas Precision-Recall por Modelo (Evaluación en Test)](images/Curvas%20Precision-Recall%20por%20Modelo%20(Evaluación%20en%20Test).png)

![Comparativa de Matrices de Confusión](images/Comparativa%20de%20Matrices%20de%20Confusión.png)

![Consistencia de los Factores de Riesgo entre Modelos Líderes](images/Consistencia%20de%20los%20Factores%20de%20Riesgo%20entre%20Modelos%20Líderes.png)

![Impacto de Variables en Churn (Odds Ratio - Regresión Logística)](images/Impacto%20de%20Variables%20en%20Churn%20(Odds%20Ratio%20-%20Regresión%20Logística).png)

![Importancia Simple de Variables (SHAP - Regresión Logística)](images/Importancia%20Simple%20de%20Variables%20(SHAP%20-%20Regresión%20Logística).png)

![Impacto Global de las variables en la predicción de abandono (SHAP)](images/Impacto%20Global%20de%20las%20variables%20en%20la%20predicción%20de%20abandono%20(SHAP).png)

[![Explorar Visualizaciones Interactivas](https://img.shields.io/badge/Explorar-Visualizaciones%20Interactivas-2563eb?style=for-the-badge&logo=plotly&logoColor=white)](https://tranquil-longma-fc6a1f.netlify.app/)

**Vista Previa:**
![Captura de visualizaciones interactivas](images/Visualizaciones%20interactivas.png)

---

## Contenido del proyecto

1. **Preparación de los Datos**
   - Extracción del Archivo Tratado
   - Eliminación de Columnas Irrelevantes
   - Verificación de la Proporción de Cancelación (Churn)

2. **Correlación y Selección de Variables**
   - Análisis de Correlación
   - Análisis Dirigido
   - Encoding

3. **Modelado Predictivo**
    - Separación de Datos
    - Balanceo de Clases
    - Normalización o Estandarización
    - Creación de Modelos
    - Evaluación de los Modelos
  
4. **Interpretación y Conclusiones**
   - Análisis de la Importancia de las Variables
  
4. **Informe Final**
   - Objetivo del análisis
   - Preparación de los datos y selección de variables
   - Hallazgos del análisis exploratorio
   - Rendimiento comparativo de los modelos
   - Evaluación con curvas ROC y Precision-Recall
   - Estabilidad de los modelos
   - Factores que más influyen en la cancelación
   - Integración de resultados entre modelos
   - Perfil de cliente con mayor riesgo de cancelación
   - Estrategias de retención propuestas
   - Conclusión final

---

## Cómo usar este proyecto

1. Abrir el cuaderno en **[Google Colab](https://colab.research.google.com/github/fsoaresg/Desafio-Telecom-X-Latam-Parte-2/blob/main/Telecom_X_Parte_2_Latam.ipynb)**.
2. Ejecutar las celdas paso a paso para:
    - Importar los datos desde la API.
    - Realizar limpieza y transformación.
    - Generar análisis estadístico y visualizaciones.
3. Explorar los gráficos interactivos.
4. Analizar los insights y evaluar recomendaciones estratégicas.

---

## Estructura del repositorio

├── Telecom X_Latam.ipynb # Cuaderno de Colab con análisis completo

├── README.md

├── 📂 Datos-Telecom-X-Latam-Parte-2/

├── 📂 images/

---

## Competencias Demostradas y Posicionamiento Profesional

Este proyecto evidencia habilidades en:

### Ciencia de Datos

* análisis exploratorio de datos
* modelado predictivo
* evaluación comparativa de modelos
* validación cruzada
* selección de variables

### Machine Learning

* clasificación supervisada
* ensemble learning
* gradient boosting
* evaluación de modelos

### Explainable AI

* SHAP
* coeficientes logísticos
* odds ratio

### Data Storytelling

* traducción de resultados técnicos en insights de negocio
* generación de recomendaciones estratégicas
* comunicación de resultados para toma de decisiones

---

## Autor

**Fátima Soares**  
Data Analyst | Enfoque en análisis estratégico y toma de decisiones basada en datos.
Especializada en transformar métricas operativas en insights ejecutivos accionables.
[GitHub](https://github.com/fsoaresg)

---

## Licencia

Este proyecto es de **uso educativo y demostrativo**, con base en un desafío de Alura Latam.

---
