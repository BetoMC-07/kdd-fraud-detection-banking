# Detección de Fraude Bancario usando la Metodología KDD

Este proyecto implementa un sistema inteligente y robusto para la detección de fraude en transacciones bancarias, estructurado bajo el proceso clásico de **Knowledge Discovery in Databases (KDD)**.

## 📋 Estructura y Metodología KDD

El desarrollo del proyecto se divide en las siguientes 5 etapas fundamentales de KDD:

1. **Selección**: Filtrado y justificación teórica de variables relevantes. Se excluyeron IDs de clientes/transacciones y el estado final de la transacción para prevenir la fuga de datos (*data leakage*).
2. **Preprocesamiento**: Imputación de valores faltantes en variables demográficas y de canales con mediana y moda. Análisis del Rango Intercuartílico ($IQR$) para el tratamiento de outliers de montos (conservados y suavizados mediante transformación $\ln(x+1)$ por su alto valor predictivo).
3. **Transformación**: Ingeniería de variables con criterio de negocio (`hora_dia`, `es_noche`, `monto_por_edad`). Normalización de datos con `StandardScaler` y codificación de variables categóricas con `OneHotEncoder` encapsulados en un `Pipeline` de Scikit-Learn.
4. **Minería de Datos**:
   * **Enfoque No Supervisado**: Agrupamiento con *K-Means* ($k=3$) analizado mediante coeficientes de silueta y detección de anomalías espaciales mediante *DBSCAN*.
   * **Enfoque Supervisado**: Clasificación predictiva comparando *Regresión Logística* (optimizada mediante pesos balanceados) y *Random Forest*.
5. **Interpretación / Evaluación**: Análisis del trade-off de negocio entre precisión y exhaustividad (*Recall*). Creación de un Dashboard de analítica integrada para la toma de decisiones estratégicas de riesgo bancario.

## 🛠️ Estructura del Repositorio

* `transacciones_bancarias.csv`: Base de datos de transacciones original.
* `transacciones_preprocesadas.csv`: Conjunto intermedio limpio tras el preprocesamiento.
* `X_train_transformado.csv` y `X_test_transformado.csv`: Sets listos para modelado.
* `requirements.txt`: Archivo con el congelamiento exacto de versiones del entorno.
* `README.md`: Este archivo descriptivo del proyecto.

## 🚀 Instrucciones de Instalación y Ejecución

Para replicar y ejecutar el notebook de análisis de este proyecto:

1. **Clonar o descargar** los archivos del proyecto a su entorno local o cargar en Google Colab.
2. **Instalar dependencias** mediante el archivo de requerimientos:
   ```bash
   pip install -r requirements.txt
   ```
3. **Ejecutar el Notebook** garantizando que el archivo de datos `transacciones_bancarias.csv` se encuentre en el mismo directorio de ejecución.

## 🛡️ Aseguramiento de la Reproducción

Para asegurar la consistencia geométrica y predictiva en cada ejecución, todas las particiones del conjunto de datos (*Train-Test Split*), reducciones de dimensionalidad (*PCA*), inicializaciones de clústeres (*K-Means*) y algoritmos de ensamble (*Random Forest*) han sido configurados utilizando estrictamente la **semilla aleatoria 42** (`random_state=42`).
