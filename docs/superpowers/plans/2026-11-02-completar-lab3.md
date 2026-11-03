# Completar Lab 3: plan de implementación

**Objetivo:** completar y ejecutar el notebook de segmentación con experimentos verificables y revisión de las fuentes indicadas.

**Arquitectura:** conservar U-Net PyTorch y material original; agregar funciones comunes de entrenamiento/evaluación, experimentos controlados y conclusiones calculadas. Usar cachés locales sin modificar notebooks ajenos.

**Tecnologías:** PyTorch, torchvision, torchmetrics, nibabel, pandas, matplotlib, nbclient y TensorFlow/Keras para clasificación desbalanceada.

**Especificación:** auditoría y solicitud «completala» de esta conversación.

## Restricciones
- No inventar resultados ni afirmar superioridad antes de evaluar.
- Misma inicialización y secuencia de lotes en comparaciones de pérdidas, pesos y conexiones.
- Separar entrenamiento, validación y prueba; normalización y pesos estimados solo en entrenamiento.
- Hipocampo: enlace LISA responde HTTP 401; usar Task04_Hippocampus público y distinguir etiquetas anterior/posterior de izquierda/derecha.
- Carvana: documentar acceso Kaggle y completar otro dataset con Kvasir-SEG.
- Mantener cambios del usuario en pyproject.toml, uv.lock y otros notebooks.

## Tareas
- [x] Corregir fórmulas, comparación de exactitud, reproducibilidad y métricas por clase; verificar invariantes con aserciones.
- [x] Ejecutar CE, Dice, CE+Dice, CE ponderada+Dice y ablación sin saltos; reportar historia, métricas y parámetros.
- [x] Completar y ejecutar Kvasir-SEG y CNN estática frente a CNN-LSTM; generar conclusiones desde resultados.
- [x] Completar hipocampo 3D con separación por casos y Dice sin fondo; documentar diferencia con LISA.
- [x] Incluir clasificación de fraude: base, pesos y sobremuestreo, selección de umbral en validación y prueba independiente.
- [x] Añadir revisión crítica y bibliografía corregida; ejecutar notebook completo y revisar salidas/errores.

## Verificación
Validar nbformat, sintaxis Python y ausencia de celdas sin ejecutar/errores; comprobar clases válidas, particiones disjuntas, coherencia IoU/Dice/matriz y resultados finitos. Revisor independiente al terminar.

## Registro de ejecución

- Primera ejecución: entrenamientos Pets, Kvasir, Moving MNIST, hipocampo y fraude terminaron. La comprobación final detectó que el dataset TensorFlow de validación sobrescribía `val_ds` de Pets. Se corrigió el origen con `val_ds_fraude`, conservando la aserción.
- Revisión independiente: fórmulas, etiquetas MSD, inicialización y particiones revisadas. Se incorporó selección aleatoria de las 250 imágenes de prueba Pets y la limitación de independencia por paciente no demostrada en MSD. Sin otros bloqueos detectados.
- Entorno: kernel Python 3.11.16, PyTorch 2.14.1, torchvision 0.29.1, torchmetrics 1.9.0. Se agregaron nibabel y scikit-learn al entorno local sin modificar pyproject.toml ni uv.lock.
- Segunda ejecución completa: terminada con código de salida 0. Las 23 celdas de código se ejecutaron en orden, sin errores, con 9 gráficas; no se reutilizaron salidas anteriores.
- Verificación independiente de artefactos: nbformat y sintaxis válidos; 5 experimentos Pets, 6 filas de fraude, relaciones Dice/IoU y precision/recall/matriz de fraude coherentes; resultados finitos y resumen exportado.
- Resultados observados: mIoU de prueba Pets 0.6288 (Dice seleccionado en validación), Kvasir 0.6388; Dice de hipocampo sin fondo 0.7649. La CNN estática tuvo IoU de dígito cero con cinco épocas; se dejó explícito que una base que no aprende limita la atribución causal a memoria temporal.
- Se conservaron los cambios previos de pyproject.toml, uv.lock y los demás notebooks.
