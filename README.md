# deteccion-glaucoma-transferencia-aprendizaje
Clasificación de glaucoma mediante VGG16, transferencia de aprendizaje, evaluación entre bases de datos e interpretabilidad con Grad-CAM.
# Detección de glaucoma mediante transferencia de aprendizaje con VGG16

## Descripción del proyecto

Este proyecto estudia la aplicación de redes neuronales convolucionales a la clasificación de retinografías para distinguir entre imágenes asociadas a ojos normales e imágenes asociadas a glaucoma.

Se utiliza VGG16, una arquitectura preentrenada con ImageNet, para explorar el efecto de la transferencia de aprendizaje en una tarea de clasificación de imágenes médicas.

El trabajo incluye la evaluación del modelo original, su adaptación mediante una nueva cabeza de clasificación, la comparación del rendimiento entre dos bases de datos y el análisis de las predicciones mediante Grad-CAM.

> **Nota:** Este proyecto tiene fines académicos y experimentales. Los resultados no constituyen una validación clínica ni permiten utilizar el modelo como herramienta de diagnóstico médico.

## Objetivos

- Evaluar VGG16 con pesos preentrenados en ImageNet sobre la base de datos ACRIMA.
- Adaptar el modelo mediante transferencia de aprendizaje, manteniendo congeladas las capas convolucionales.
- Evaluar el modelo adaptado en ACRIMA y RIM-ONE-r2.
- Comparar el rendimiento mediante el área bajo la curva ROC (AUC) y el F1-score.
- Visualizar regiones relevantes para las predicciones mediante Grad-CAM.
- Analizar las limitaciones de generalización entre bases de datos.

## Metodología

### 1. Evaluación del modelo preentrenado

Se evalúa VGG16 con pesos de ImageNet, sin entrenar sus capas para la tarea específica de glaucoma.

### 2. Transferencia de aprendizaje

Se mantienen congeladas las capas convolucionales de VGG16 y se incorpora una cabeza de clasificación personalizada para distinguir entre las dos clases.

La nueva arquitectura incluye capas densas, normalización por lotes y Dropout.

### 3. Evaluación en una base de datos externa

El modelo adaptado con ACRIMA se evalúa posteriormente en RIM-ONE-r2 sin reentrenamiento adicional, con el objetivo de estudiar su comportamiento ante imágenes procedentes de otra base de datos.

### 4. Interpretabilidad

Se utiliza Grad-CAM para generar mapas de activación que permiten examinar las regiones de las retinografías que contribuyen a las predicciones del modelo.

## Resultados principales

| Métrica | ACRIMA | RIM-ONE-r2 |
|---|---:|---:|
| Accuracy | 90,78 % | 48,35 % |
| AUC-ROC | 0,9710 | 0,5467 |
| F1-score | 0,9008 | 0,2900 |
| Sensibilidad | 87 % | 19 % |

Los resultados corresponden a las evaluaciones descritas en el informe académico.

## Conclusiones

El modelo adaptado mediante transferencia de aprendizaje alcanza un rendimiento elevado en ACRIMA. Sin embargo, al evaluarlo en RIM-ONE-r2 se observa una reducción considerable de las métricas de rendimiento, especialmente de la sensibilidad y del AUC.

Estos resultados ponen de manifiesto la importancia de evaluar los modelos de aprendizaje profundo con conjuntos de datos independientes y de analizar su capacidad de generalización antes de considerar cualquier posible aplicación clínica.

El uso de Grad-CAM aporta una perspectiva adicional sobre las regiones de las imágenes asociadas a las predicciones, aunque estos mapas no demuestran por sí solos que el modelo utilice criterios clínicamente válidos.

## Tecnologías

- Python
- TensorFlow / Keras
- VGG16
- Redes neuronales convolucionales
- Transferencia de aprendizaje
- Scikit-learn
- Grad-CAM
- Evaluación de modelos de clasificación

## Estructura del repositorio

La estructura definitiva se documentará según los notebooks, scripts y resultados que se publiquen.

## Contexto académico

Proyecto desarrollado en el marco de la asignatura Modelos de Redes Neuronales del Máster en Metodología de las Ciencias del Comportamiento y de la Salud, Universidad Complutense de Madrid, 2025.

## Limitaciones

El rendimiento observado en bases de datos concretas no garantiza la generalización a otras poblaciones, dispositivos o entornos clínicos. Este proyecto es un ejercicio académico y no constituye un sistema validado para el diagnóstico de glaucoma.
