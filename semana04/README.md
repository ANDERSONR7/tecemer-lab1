Semana 04: Clasificador de Lluvia con Redes Neuronales (Keras / TensorFlow)

Este módulo implementa un clasificador binario de precipitación para la ciudad de Huancayo utilizando un **Perceptrón Multicapa (MLP) construido con Keras/TensorFlow [1, 5]. Se abarca desde la preparación e ingeniería de datos hasta la comparación contra un modelo baseline, inferencia y pruebas automatizadas con `pytest` [1, 6, 7].

## Estructura de Archivos

* `ampliar_dataset.py`: Consulta la API histórica de Open-Meteo para obtener más registros climáticos [8].
* `pronostico_huancayo.csv`: Dataset histórico de Huancayo con variables climáticas [8, 9].
* `preparar_dataset.py`: Limpieza, ingeniería de características (`amplitud_termica`), escalado y partición train/test [10-13].
* `dataset_preparado.npz`: Datos numéricos escalados y divididos guardados en formato numpy [13, 14].
* `perceptron_sintetico.py`: Entrenamiento de un MLP con datos sintéticos para validar el flujo de Keras [15, 16].
* `curvas_entrenamiento_sintetico.png`: Gráfico de pérdida y precisión del modelo sintético [17].
* `clasificador_lluvia.py`: Entrenamiento del MLP sobre los datos de Huancayo y evaluación contra el baseline [6, 18, 19].
* `curvas_entrenamiento_lluvia.png`: Gráfico de la curva de pérdida durante el entrenamiento [20, 21].
* `modelo_lluvia.keras`: Red neuronal entrenada y guardada para su reutilización [22].
* `predecir.py`: Script de inferencia que realiza predicciones sobre nuevas observaciones climáticas [22-24].
* `tests/test_preparacion.py`: Pruebas unitarias automatizadas con `pytest` [7, 25].

## Resultados del Modelo

* **Modelo Baseline (Regresión Logística): ~73.68% de precisión en el conjunto de prueba [6, 20].
* **Red Neuronal MLP (Keras):** ~84.21% de precisión en el conjunto de prueba [20].

La red neuronal superó al modelo baseline, demostrando mayor capacidad para aprender relaciones no lineales entre las variables climáticas [1, 20, 21].

## Instrucciones de Ejecución

1. **Ampliar y preparar el dataset:**
   bash
   python ampliar_dataset.py
   python preparar_dataset.py

1. **Entrenar el modelo con datos sintéticos:**
python perceptron_sintetico.py

1. **Entrenar y evaluar el clasificador de lluvia:**

python clasificador_lluvia.py

1. **Ejecutar inferencia sobre nuevas observaciones:**

python predecir.py

1. **Ejecutar pruebas unitarias automatizadas:**
```
python -m pytest tests/ -v



## Mejora Futura Identificada

Refactorización de preparar\_dataset.py Al importar funciones desde `preparar_dataset.py dentro de las pruebas unitarias (`pytest`), se ejecuta todo el script debido al código suelto (efecto secundario de lectura de CSV y guardado del archivo `.npz`)[2][5]. Como mejora futura, la lógica de transformación de datos se aislará en un módulo sin efectos secundarios al importarse[2].