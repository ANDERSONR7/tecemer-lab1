## semana04
Proyecto de práctica de la "Semana 4 "del curso "Tecnologías Emergentes (ISO46B)" — UNCP. Implementa un clasificador de precipitación para Huancayo utilizando Redes Neuronales Artificiales (Keras / TensorFlow), pruebas automatizadas y control de versiones.

## Instalación

```bash
python -m venv .venv
.\.venv\Scripts\activate   # Windows
source .venv/bin/activate   # Linux/macOS
pip install -r requirements.txt
```
## Estructura del repositorio

```
tecemer-lab1/
└── semana04/
    ├── tests/
    │   └── test_preparacion.py             
    ├── ampliar_dataset.py                  
    ├── preparar_dataset.py                 
    ├── perceptron_sintetico.py             
    ├── clasificador_lluvia.py              
    ├── predecir.py                         
    ├── pronostico_huancayo.csv             
    ├── dataset_preparado.npz               
    ├── modelo_lluvia.keras                 
    ├── curvas_entrenamiento_sintetico.png  
    ├── curvas_entrenamiento_lluvia.png     
    └── README.md                           
```
## Autor

Curso: Tecnologías Emergentes (ISO46B) — Facultad de Ingeniería de Sistemas, UNCP.

## Clasificador de Lluvia con Redes Neuronales — Semana 4

Esta sección documenta la construcción del pipeline de clasificación binaria de lluvia para Huancayo utilizando un **Perceptrón Multicapa (MLP)** en Keras/TensorFlow.

### Fuente

API pública Open-Meteo (https://api.open-meteo.com/v1/forecast): Consulta histórica del clima de Huancayo guardada en `pronostico_huancayo.csv`.

### Transformación y Modelado

 `preparar_dataset.py`: Limpia los datos, calcula la característica derivada `amplitud_termica`, normaliza las variables climáticas mediante `StandardScaler` y guarda la partición train/test en `dataset_preparado.npz`.
 `perceptron_sintetico.py`: Entrena un MLP sencillo sobre datos sintéticos para validar la configuración y el flujo de trabajo de Keras.
 `clasificador_lluvia.py`: Entrena una red neuronal MLP sobre los datos de Huancayo y evalúa su precisión comparándola contra un modelo baseline de Regresión Logística.
 `predecir.py`: Carga el modelo guardado `modelo_lluvia.keras` y ejecuta inferencias sobre nuevas condiciones métricas.

### Salida

 `modelo_lluvia.keras` — Red neuronal entrenada y lista para producción/inferencia.
 `dataset_preparado.npz` — Datos divididos y escalados para entrenamiento y validación.
 `curvas_entrenamiento_sintetico.png` y `curvas_entrenamiento_lluvia.png` — Visualizaciones del proceso de entrenamiento.

### Resultados Obtenidos

Modelo Baseline (Regresión Logística):** \~73.68% de precisión en test.
Red Neuronal MLP (Keras):** \~84.21% de precisión en test.

La red neuronal superó al modelo baseline, demostrando mejor capacidad para capturar relaciones no lineales entre las variables climáticas.

### Cómo reproducirlo y Pruebas

```
# 1. Ampliar y preparar el dataset
python semana04/ampliar_dataset.py
python semana04/preparar_dataset.py

# 2. Probar modelo sintético
python semana04/perceptron_sintetico.py

# 3. Entrenar y evaluar el clasificador de lluvia
python semana04/clasificador_lluvia.py

# 4. Inferencia con el modelo entrenado
python semana04/predecir.py

# 5. Ejecución de pruebas unitarias
python -m pytest semana04/tests/ -v

```

```

```