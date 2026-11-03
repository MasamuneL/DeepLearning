# Lab 3: segmentación semántica con U-Net

La entrega principal es `Segmentacion_semantica_UNet.ipynb`. Incluye resultados, gráficas, conclusiones calculadas y bibliografía. Las tablas numéricas se exportan a `resultados/` durante su ejecución.

## Ejecución

Desde la carpeta `Lab3_U2`, abrir el notebook y ejecutar todas las celdas en orden. La primera celda de código comprueba las dependencias del kernel e instala únicamente las que falten. También pueden instalarse previamente:

```bash
python -m pip install -r requirements.txt
python -m jupyter nbconvert --to notebook --execute --inplace Segmentacion_semantica_UNet.ipynb --ExecutePreprocessor.timeout=2400
```

El entrenamiento utiliza CUDA, MPS o CPU según disponibilidad; el experimento 3D usa CUDA o CPU. Los tiempos dependen del equipo. Los datos se descargan en `data/`; las cachés de Pets y Kvasir existentes en `../Actividades/data` se reutilizan sin modificar los notebooks de esa carpeta. La descarga completa de Moving MNIST ocupa aproximadamente 819 MB. Se necesita conexión para las descargas iniciales.

## Experimentos

- Oxford-IIIT Pet: U-Net compacta; CE, Dice, CE + Dice, CE ponderada + Dice y ablación sin información de los saltos. Misma inicialización y orden de lotes. Selección en validación; evaluación en una muestra aleatoria fija de la prueba oficial.
- Kvasir-SEG: segmentación binaria de pólipos, con entrenamiento, validación y prueba separados.
- Moving MNIST: CNN estática y CNN-LSTM; evaluación global y dentro de la oclusión del último cuadro.
- MSD Task04_Hippocampus: NIfTI 3D, U-Net 3D, CE ponderada + Dice, métricas por región y Dice por caso.
- Fraude con TensorFlow/Keras: modelo base, pesos de clase y sobremuestreo; umbrales elegidos en validación y métricas en prueba.
- Revisión crítica de arXiv:2502.06895 y relación con los experimentos.

## Adaptaciones y límites

El enlace SharePoint del tutorial RISE/LISA respondió HTTP 401 durante la preparación. Se usa MSD Task04_Hippocampus, de descarga pública, con regiones **anterior y posterior**, distintas de las etiquetas bilaterales de LISA. Es una adaptación del flujo de segmentación médica, no una reproducción del experimento LISA. La rejilla de evaluación es de 32³; no se informa rendimiento en resolución clínica original. La separación es por archivo/caso; no se reconstruyó la agrupación de recortes bilaterales por paciente.

Carvana requiere acceso autorizado a su competencia Kaggle. La actividad con otro dataset se ejecuta con Kvasir-SEG; no se afirma haber entrenado Carvana. DSB 2018 y Kvasir-SEG son conjuntos diferentes.

Los experimentos usan una semilla y presupuestos breves. No establecen significancia estadística ni utilidad clínica. El notebook distingue las métricas observadas de las hipótesis sobre cada arquitectura.
