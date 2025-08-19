# Análisis Predictivo de Cancelación de Clientes (Churn)

Este proyecto tiene como objetivo predecir la cancelación de clientes (Churn) de una empresa de telecomunicaciones utilizando técnicas de machine learning. Se realiza un análisis exploratorio de los datos, preprocesamiento, y se entrenan y evalúan modelos de clasificación para identificar los factores más relevantes asociados al churn.

## 📊 Datos

El conjunto de datos utilizado (`df_limpo.csv`) contiene información sobre clientes de una empresa de telecomunicaciones, incluyendo datos demográficos, servicios contratados, información de la cuenta y estado de churn.

## 🛠️ Metodología

El proceso de análisis y modelado siguió las siguientes etapas:

1.  **Extracción y Carga:** Carga inicial de los datos desde el archivo CSV.
2.  **Preparación de Datos:**
    *   Limpieza de datos (manejo de valores nulos).
    *   Transformación de variables categóricas (One-Hot Encoding).
    *   Manejo de la multicolinealidad (análisis VIF y eliminación de variables redundantes).
    *   Normalización/Estandarización de variables numéricas.
    *   Balanceo de clases (SMOTE) para abordar el desbalance en la variable objetivo.
3.  **Análisis de Correlación:** Exploración de las relaciones entre variables y la variable objetivo.
4.  **Modelado Predictivo:**
    *   División de los datos en conjuntos de entrenamiento y prueba.
    *   Entrenamiento de dos modelos de clasificación:
        *   Regresión Logística
        *   Random Forest
    *   Evaluación del rendimiento de los modelos utilizando métricas como Exactitud, ROC AUC, Matriz de Confusión y Reporte de Clasificación.
    *   Análisis de la importancia de las variables para cada modelo.

## 🤖 Modelos y Resultados

Se entrenaron dos modelos predictivos:

### Regresión Logística

*   **Métricas Clave:**
    *   Exactitud: 0.7502
    *   ROC AUC: 0.8454
    *   Recall (Churn): 0.81
*   **Variables más influyentes (basado en coeficientes):**
    *   Aumentan Churn: `internet.InternetService_Fiber optic`, `account.Charges.Total`, `internet.StreamingTV_Yes`, `internet.StreamingMovies_Yes`, `account.PaperlessBilling_Yes`, `account.PaymentMethod_Electronic check`, `customer.SeniorCitizen`.
    *   Disminuyen Churn: `customer.tenure`, `account.Contract_Two year`, `internet.InternetService_No`, `account.Charges.Monthly`, `internet.TechSupport_Yes`, `account.Contract_One year`, `internet.OnlineSecurity_Yes`, `customer.Dependents_Yes`, `customer.Partner_Yes`.
*   **Hallazgo Clave:** El modelo de Regresión Logística es particularmente bueno para identificar a la mayoría de los clientes propensos a cancelar (alto Recall para la clase Churn).

### Random Forest

*   **Métricas Clave:**
    *   Exactitud: 0.7787
    *   ROC AUC: 0.8242
    *   Precisión (Churn): 0.58
*   **Variables más influyentes (basado en importancia de la variable):**
    *   `customer.tenure`
    *   `account.Charges.Total`
    *   `account.Charges.Monthly`
    *   `Total.Day`
    *   `account.Contract_Two year`
    *   `account.PaymentMethod_Electronic check`
    *   `internet.InternetService_Fiber optic`
*   **Hallazgo Clave:** Random Forest mostró una exactitud ligeramente superior y mayor precisión en la predicción de Churn, pero con un Recall menor que la Regresión Logística.

## ✅ Conclusiones

Ambos modelos identificaron consistentemente la **antigüedad del cliente (`customer.tenure`)** como el factor más importante para predecir la cancelación (cuanto mayor la antigüedad, menor el churn). Las **variables relacionadas con los cargos (`account.Charges.Monthly`, `account.Charges.Total`, `Total.Day`)**, el **tipo de contrato** y el **servicio de internet (especialmente fibra óptica)** también fueron identificados como predictores clave por ambos modelos.

La elección del "mejor" modelo depende del objetivo de negocio: si se prioriza la identificación de la mayor cantidad posible de clientes en riesgo (para acciones de retención), la Regresión Logística podría ser más adecuada debido a su alto Recall. Si se prioriza la precisión de las predicciones de churn, Random Forest podría ser preferible.
