Proyecto de Entrenamiento de IA
Este repositorio contiene los archivos necesarios para entrenar, ajustar y probar un modelo de lenguaje utilizando fine-tuning sobre un modelo preentrenado de tipo MiniLM.

Estructura de Carpetas y Archivos
data/
Carpeta que contiene el dataset de entrenamiento en formato .json.
El archivo principal, train.json, es cargado por el script train.py para iniciar el proceso de fine-tuning.

paraphrase-multilingual-MiniLM-L12/
Carpeta que contiene el modelo base preentrenado, incluyendo:

config.json

tokenizer.json

tokenizer_config.json

Archivos binarios del modelo (pytorch_model.bin o similar)

Este modelo sirve como punto de partida para el fine-tuning personalizado.

finetuned-math-model/
Carpeta que contiene el modelo resultante luego del proceso de entrenamiento.
La estructura es similar a la del modelo base (bin, tokenizer, config), pero con los pesos ajustados según el dataset de entrenamiento.

.gitignore
Archivo de configuración para Git que indica qué archivos o carpetas deben ser ignorados al hacer commits (por ejemplo, checkpoints, datasets pesados, archivos temporales, etc.).

chat.py
Script que permite interactuar con el modelo ya entrenado, enviando preguntas o inputs para obtener respuestas generadas.

train.py
Script principal que realiza el entrenamiento (fine-tuning) del modelo.
Este script:

Carga los datos desde data/train.json.

Carga el modelo base desde paraphrase-multilingual-MiniLM-L12/.

Ajusta los parámetros del modelo según el dataset.

Guarda el modelo resultante en finetuned-math-model/.

Requisitos
Python 3.8+

Paquetes recomendados:

transformers

torch

scikit-learn

datasets

Se recomienda instalar las dependencias usando pip:

bash
Copiar
Editar
pip install -r requirements.txt
(El archivo requirements.txt no está incluido por defecto; deberías generarlo si deseas listar dependencias explícitamente.)

Instrucciones básicas
Entrenar el modelo
Ejecutar el script train.py:

bash
Copiar
Editar
python train.py --dataset_path ./data/train.json --bit_precision 4 --batch_size 1 --grad_accum_steps 16 --max_length 256 --save_steps 5 --lora_r 8 --lora_alpha 16
Probar el modelo entrenado
Ejecutar el script chat.py:

bash
Copiar
Editar
python chat.py
Personalización

Para modificar el dataset de entrenamiento, actualizar el archivo data/train.json.

Para cambiar el modelo base, reemplazar el contenido de paraphrase-multilingual-MiniLM-L12/ con otro modelo compatible.

