# deteccion-glaucoma-transferencia-aprendizaje
Clasificación de glaucoma mediante VGG16, transferencia de aprendizaje, evaluación entre bases de datos e interpretabilidad con Grad-CAM.

# Detección de glaucoma mediante transferencia de aprendizaje

Proyecto de aprendizaje profundo centrado en la clasificación de imágenes de fondo de ojo para la detección de glaucoma mediante redes neuronales convolucionales y transferencia de aprendizaje.

El proyecto estudia el uso de **VGG16 preentrenada en ImageNet**, evalúa su rendimiento en diferentes bases de datos y utiliza **Grad-CAM** para explorar las regiones de las imágenes que influyen en las predicciones del modelo.

## Objetivos

- Evaluar el rendimiento de VGG16 preentrenada sin entrenamiento específico para la tarea.
- Aplicar transferencia de aprendizaje mediante una arquitectura VGG16 con capas convolucionales congeladas.
- Analizar el rendimiento del modelo en una base de datos de entrenamiento y prueba y en una base de datos externa.
- Evaluar métricas de clasificación como accuracy, sensibilidad, especificidad, F1 y AUC.
- Explorar la interpretabilidad de las predicciones mediante Grad-CAM.
- Analizar las limitaciones de generalización entre diferentes conjuntos de datos.

## Metodología

### 1. Modelo base

Se evalúa VGG16 con pesos preentrenados en ImageNet sobre imágenes de la base de datos ACRIMA, sin entrenamiento específico para la clasificación de glaucoma.

### 2. Transferencia de aprendizaje

Se mantienen congeladas las capas convolucionales de VGG16 y se añade una cabeza de clasificación personalizada con:

- Global Average Pooling.
- Batch Normalization.
- Capas densas con activación ReLU.
- Dropout para reducir el riesgo de sobreajuste.
- Una capa de salida sigmoide para la clasificación binaria.

El modelo se entrena con imágenes de ACRIMA utilizando TensorFlow y Keras.

### 3. Evaluación

El modelo entrenado se evalúa en ACRIMA y, sin reentrenamiento, en la base de datos externa RIM-ONE-r2 para estudiar su capacidad de generalización.

### 4. Interpretabilidad

Se utiliza Grad-CAM para generar mapas de activación que permiten explorar qué regiones de las imágenes contribuyen a las predicciones del modelo.

## Resultados

### VGG16 preentrenada sin ajuste específico

Evaluación sobre ACRIMA:

| Métrica | Resultado |
|---|---:|
| Accuracy | 55,32 % |
| AUC | 0,582 |
| Loss | 1,7433 |

### VGG16 con transferencia de aprendizaje

Evaluación sobre ACRIMA:

| Métrica | Resultado |
|---|---:|
| Accuracy | 90,78 % |
| AUC | 0,9710 |
| F1-score | 0,9008 |
| Valor predictivo positivo (PPV) | 0,96 |
| Sensibilidad | 0,87 |
| Especificidad | 0,87 |

La matriz de confusión obtenida en ACRIMA fue:

| | Predicción normal | Predicción glaucoma |
|---|---:|---:|
| Real normal | 69 | 10 |
| Real glaucoma | 3 | 59 |

### Evaluación externa en RIM-ONE-r2

El modelo entrenado en ACRIMA se evalúa en RIM-ONE-r2 sin reentrenamiento:

| Métrica | Resultado |
|---|---:|
| Accuracy | 48,35 % |
| AUC | 0,5467 |
| F1-score | 0,2900 |
| Sensibilidad | 0,19 |
| Especificidad | 0,86 |

Estos resultados muestran una caída importante del rendimiento en la base de datos externa, lo que pone de manifiesto las dificultades de generalización entre conjuntos de datos.

## Conclusiones

- La transferencia de aprendizaje mejora sustancialmente los resultados respecto al modelo VGG16 preentrenado sin ajuste específico.
- El rendimiento obtenido en ACRIMA es elevado, pero no se mantiene al evaluar el modelo en RIM-ONE-r2.
- La evaluación externa es fundamental para identificar limitaciones de generalización.
- Grad-CAM ofrece una herramienta visual para explorar las predicciones, aunque los mapas de activación no garantizan que el modelo utilice criterios clínicamente adecuados.

## Tecnologías utilizadas

- Python
- TensorFlow
- Keras
- VGG16
- Redes neuronales convolucionales (CNN)
- Transferencia de aprendizaje
- Grad-CAM
- Evaluación de modelos de clasificación

## Limitaciones

Este proyecto tiene carácter académico y experimental. Los resultados no constituyen una validación clínica ni permiten utilizar el modelo como herramienta de diagnóstico médico. La generalización entre bases de datos, la representatividad de las imágenes y la interpretabilidad de las predicciones requieren análisis adicionales.

## Contexto académico

**Asignatura:** Modelos de Redes Neuronales  
**Programa:** Máster en Metodología 
**Institución:** Universidad Complutense de Madrid  
**Año:** 2025

---

*Proyecto académico de aprendizaje profundo aplicado al análisis de imágenes médicas.*
