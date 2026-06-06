# prediccion_sentimientos

Proyecto de aprendizaje automático orientado a la **predicción de la emoción dominante** a partir de características faciales. El trabajo se desarrolló en distintas fases, comenzando con un planteamiento inicial basado en diferencias entre puntos faciales y evolucionando posteriormente hacia un enfoque final basado en **proporciones faciales**, que resultó más adecuado para representar la información emocional.

## Descripción del problema

El objetivo de este proyecto es construir un modelo capaz de predecir la emoción dominante de cada observación a partir de variables derivadas de puntos faciales. Se trata de un problema de **clasificación multiclase**, ya que cada fila del dataset debe asociarse a una emoción concreta entre varias posibles [web:596][web:648].

La motivación principal del proyecto es analizar si ciertas relaciones geométricas entre puntos del rostro contienen información suficiente para discriminar emociones. Para ello, se compararon distintos enfoques de representación de los datos y varios modelos de clasificación supervisada [web:602][web:648].

## Planteamiento inicial

En una primera fase, el problema se abordó utilizando un dataset construido a partir de la **diferencia en centímetros entre distintos puntos faciales** para cada emoción. Este planteamiento permitió organizar una primera versión del problema y comenzar el análisis exploratorio, la limpieza de datos y las primeras pruebas de modelado.

Sin embargo, conforme avanzó el trabajo, se observó que este enfoque no representaba de la forma más clara la emoción dominante de cada observación. Aunque servía como punto de partida, las diferencias absolutas entre puntos no ofrecían una base suficientemente consistente para capturar mejor la estructura emocional presente en los datos.

## Planteamiento final

A partir de esa limitación inicial, se redefinió el problema utilizando un nuevo dataset basado en **proporciones entre puntos faciales**. Este cambio fue importante porque permitió trabajar con una representación más estable y comparativa de las relaciones faciales, reduciendo la dependencia de medidas absolutas y ofreciendo una formulación más coherente del problema.

Sobre este nuevo planteamiento, se construyó la versión final del proyecto. Además, se definió una nueva variable objetivo llamada `emocion_dominante`, entendida como la emoción con mayor proporción en cada fila, lo que permitió convertir el problema en una tarea de clasificación multiclase más clara y directamente interpretable.

## Flujo de trabajo

El flujo de trabajo seguido en el proyecto fue el siguiente:

1. **Carga y revisión del dataset**  
   Se importó el conjunto de datos y se realizó una inspección inicial para comprender su estructura, tipos de variables y posibles problemas de calidad de datos [web:596][web:648].

2. **Limpieza y preparación de datos**  
   Se llevó a cabo la conversión de columnas numéricas, el tratamiento de valores nulos y la selección de las variables relevantes para el modelado. Esta fase fue clave para asegurar que la entrada a los modelos fuera consistente y utilizable [web:596][web:648].

3. **Definición de la variable objetivo**  
   Se generó la variable `emocion_dominante`, que resume en una sola etiqueta la emoción predominante en cada observación. Esta variable fue la base para entrenar los clasificadores.

4. **Selección de variables predictoras**  
   El modelo final trabajó con variables como `GENERO`, `EDAD`, `punto_base` y `punto_comparado`, que se utilizaron como entrada para predecir la emoción dominante.

5. **Preprocesamiento**  
   Las variables categóricas se transformaron mediante **One Hot Encoding**, mientras que las variables numéricas se mantuvieron sin transformación. Para ello, se utilizó un `ColumnTransformer`, integrado posteriormente dentro de un pipeline, que permite aplicar el mismo flujo de preprocesado y predicción de forma reproducible [web:647][web:603].

6. **División del dataset**  
   El conjunto de datos se dividió en entrenamiento y prueba mediante `train_test_split`, conservando la proporción de clases entre ambos subconjuntos para poder evaluar los modelos de forma realista [web:648].

7. **Entrenamiento y comparación de modelos**  
   Se entrenaron y compararon cuatro modelos de clasificación:
   - Regresión Logística  
   - Árbol de Decisión  
   - Random Forest  
   - Gradient Boosting  

   La comparación se realizó a partir de las métricas **Accuracy** y **F1 macro**, ya que no solo interesaba el porcentaje global de aciertos, sino también el equilibrio del rendimiento entre todas las clases [web:596][web:602].

8. **Interpretación de resultados**  
   Además de las métricas numéricas, se incorporaron recursos visuales para interpretar mejor el comportamiento de los modelos, como la **matriz de confusión**, la visualización del **árbol de decisión** y la gráfica de **importancia de variables** del Random Forest.

9. **Exportación del modelo**  
   Una vez entrenado el modelo final, se exportó para su reutilización posterior. Esto permite volver a cargar el modelo sin necesidad de repetir todo el proceso de entrenamiento, algo especialmente útil en proyectos de machine learning reproducibles [web:648][web:650].

## Modelos evaluados

Durante el proyecto se compararon cuatro algoritmos de clasificación supervisada:

- **Logistic Regression**  
  Modelo base útil como referencia inicial en problemas de clasificación.

- **Decision Tree**  
  Modelo interpretable que permite visualizar reglas de decisión de manera directa.

- **Random Forest**  
  Conjunto de árboles que suele ofrecer mejor estabilidad que un único árbol de decisión.

- **Gradient Boosting**  
  Modelo basado en el aprendizaje secuencial de árboles débiles, orientado a corregir errores progresivamente.

Esta comparación permitió identificar qué enfoque se adaptaba mejor a la representación final del problema.

## Resultados

Los resultados obtenidos mostraron que el modelo con mejor comportamiento fue **Gradient Boosting**, alcanzando un `accuracy` de **0.5625** y un `F1 macro` de **0.514966**. Estos valores indican que el modelo logra un rendimiento moderado, pero suficiente para demostrar que las proporciones faciales contienen información útil para la clasificación emocional.

Aunque los resultados todavía son mejorables, el proyecto permitió establecer una base sólida para continuar explorando el problema desde una perspectiva más robusta y mejor estructurada.

## Estructura del proyecto

La organización del repositorio puede incluir archivos como los siguientes:

```bash
prediccion_sentimientos/
│
├── README.md
├── notebook.ipynb
├── modelo_emociones.pkl
├── dataset_sentimientos.csv
└── imagenes_resultados/
```

La idea es mantener juntos el notebook principal, el modelo exportado, el dataset utilizado en el análisis y las visualizaciones generadas durante el proyecto, siguiendo una estructura clara y fácil de entender en repositorios de machine learning [web:646][web:650].

## Cómo ejecutar el proyecto

1. Clonar o descargar este repositorio.
2. Abrir el notebook en Google Colab o Jupyter Notebook.
3. Instalar las dependencias necesarias.
4. Ejecutar las celdas en orden, desde la carga de datos hasta la evaluación final del modelo.
5. Si se desea reutilizar el modelo ya entrenado, cargar el archivo `.pkl` correspondiente.

## Librerías principales

Este proyecto utiliza principalmente:

- `pandas`
- `numpy`
- `matplotlib`
- `scikit-learn`
- `pickle`

## Conclusión

En este proyecto se ha trabajado con características faciales con el objetivo de predecir la emoción dominante de cada observación. En una primera fase, se intentó abordar el problema utilizando un dataset basado en la diferencia en centímetros entre distintos puntos faciales para cada emoción. Ese planteamiento permitió estructurar el problema de forma inicial, pero no ofreció una representación suficientemente clara de la emoción dominante en cada caso.

Por ello, en una segunda fase se optó por trabajar con un nuevo dataset basado en proporciones entre puntos faciales, que ofrecía una representación más consistente de la información emocional. A partir de este nuevo conjunto de datos, se realizó la limpieza de variables, la conversión de columnas numéricas, la imputación de valores nulos y la creación de una nueva variable objetivo llamada `emocion_dominante`, definida como la emoción con mayor proporción en cada fila.

Después se compararon cuatro modelos de clasificación multiclase: Regresión Logística, Árbol de Decisión, Random Forest y Gradient Boosting. La evaluación se llevó a cabo mediante las métricas Accuracy y F1 macro, lo que permitió comparar tanto el porcentaje global de aciertos como el equilibrio del rendimiento entre todas las emociones.

Los resultados mostraron que el modelo con mejor comportamiento fue **Gradient Boosting**, con un accuracy de 0.5625 y un F1 macro de 0.514966. Además, se utilizaron herramientas visuales como la matriz de confusión, la representación del árbol de decisión y la gráfica de importancias de variables del Random Forest para interpretar mejor el comportamiento de los modelos.

En conjunto, el proyecto demuestra que las proporciones entre puntos faciales contienen información útil para la clasificación emocional. Aunque los resultados aún pueden mejorarse, el trabajo realizado permite establecer una base sólida para seguir avanzando.

## Líneas futuras

Como posibles mejoras futuras del proyecto, se plantean las siguientes:

- ampliar el tamaño del dataset,
- ajustar hiperparámetros de los modelos,
- aplicar técnicas de validación más robustas,
- explorar nuevas variables derivadas de relaciones faciales,
- estudiar otros algoritmos de clasificación que puedan mejorar el rendimiento final.

## Autor

Proyecto desarrollado como práctica de análisis de datos y clasificación supervisada en Python.
