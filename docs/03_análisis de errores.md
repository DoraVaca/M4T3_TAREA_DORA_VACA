# Análisis de errores

## Falsos positivos

1. **Welding mask detectada incorrectamente en otras clases**  
El modelo predice welding_mask en objetos o regiones que corresponden a otras clases como helmet, person o safety_vest. Esto ocurre debido a la similitud visual entre el casco y la careta de soldadura, así como a la baja cantidad de ejemplos de esta clase en el dataset.

2. **Person detectado en regiones de fondo**  
En algunas imágenes el modelo predice la clase person en zonas del fondo o en objetos que no corresponden a trabajadores. Esta clase tiene muchas más instancias que otras categorías.

3. **Safety vest detectado en ropa de trabajo común**  
El modelo a veces identifica chalecos de seguridad en prendas de ropa similares en color o textura. 



## Falsos negativos

1. **Guantes no detectados**  
El modelo no detecta correctamente la clase gloves en varias imágenes. Los guantes suelen ocupar una pequeña región de la imagen y existen pocos ejemplos de esta clase en el conjunto de entrenamiento.

2. **No_safety_vest no detectado**  
En varios casos el modelo no identifica correctamente cuando un trabajador no lleva chaleco. Esto sugiere que el modelo tiene dificultad para aprender clases basadas en la ausencia de un elemento.

3. **Welding mask no detectada o confundida con otras clases**  
La clase welding_mask presenta una alta tasa de error, ya que frecuentemente se confunde con helmet, person o incluso con el fondo. Esto indica problemas de representación en el dataset y posibles inconsistencias en las anotaciones.

---

## Mejoras prioritarias en los datos

1. **Aumentar ejemplos en clases minoritarias**  
Incrementar el número de imágenes para clases con bajo rendimiento como gloves, no_safety_vest y welding_mask para mejorar el equilibrio del dataset.

2. **Revisar y mejorar las anotaciones**  
Verificar las etiquetas de clases visualmente similares como helmet y welding_mask, ya que pueden existir solapamientos o inconsistencias en las anotaciones actuales.

3. **Aplicar data augmentation específico**  
Incorporar técnicas de aumento de datos como rotaciones, recortes y variaciones de iluminación, especialmente para clases minoritarias, con el fin de mejorar la capacidad de generalización del modelo.
