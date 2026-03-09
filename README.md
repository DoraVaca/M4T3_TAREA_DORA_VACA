# M4T3_TAREA_DORA_VACA
M4T3_TAREA_DORA_VACA
# Prototipo AECO CV — YOLOv8
- Modelo prototipo para entrega de una tarea, el cual detecta ÚNICAMENTE algunos tipos de equipos de protección personal en obras.
- NO apto para veredictos o certificados oficiales de cumplimiento de uso de equipo de protección.
- IMPORTANTE: Este modelo es una herramienta asistiva solo para screening preliminar.  Produce falsos negativos.  NO debe utilizarse como único verificador en decisiones de seguridad vital.

## 📌 Problema y criterios de éxito
Detectar objetos/clases en imágenes de contexto AECO: equipo de protección personal.  
Éxito = obtener mAP ≥ 0.5 en validación y resultados consistentes en imágenes nuevas.

## 🗂️ Lista de clases y reglas de etiquetado
- Clase 1: gloves
- Clase 2: harness
- Clase 3: helmet
- Clase 4: no_helmet
- Clase 5: no_safety_shoe
- Clase 6: no_safety_vest
- Clase 7: person
- Clase 8: safety_shoe
- Clase 9: safety_vest
- Clase 10: welding_mask
👉 Reglas: se etiqueta solo el objeto completo, no partes sueltas.

## 📊 Dataset
- Fuente: [https://app.roboflow.com/dora-nkhz4/m4t3_tarea_dora_vaca/3]  
- Split: 72% entrenamiento / 16% validación  / 12% validación

## ⚙️ Cómo reproducir en Colab
Este proyecto está dividido en dos notebooks que deben ejecutarse en orden, NO ES NECESARIO ejecutar entrenamiento para obtener inferencia.

### Notebook 1: Entrenamiento
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/DoraVaca/M4T3_TAREA_DORA_VACA/blob/main/notebooks/entrenamiento.ipynb)
1. Abre el notebook con el botón de arriba.
2. En Colab, ve al panel izquierdo → **Secrets** (🔑) → agrega tu `ROBOFLOW_API_KEY`.
3. Ejecuta las celdas en orden:
   - Verifica acceso a GPU.
   - Instala dependencias automáticamente.
   - Descarga el dataset desde Roboflow.
   - Entrena el modelo por 30 épocas.
   - Valida el modelo y genera métricas.
   - Guarda `best.pt` en Google Drive para usarlo en el Notebook 2.

### Notebook 2: Inferencia
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/DoraVaca/M4T3_TAREA_DORA_VACA/blob/main/notebooks/inferencia.ipynb)
1. Abre el notebook con el botón de arriba.
2. En Colab, ve al panel izquierdo → **Secrets** (🔑) → agrega tu `ROBOFLOW_API_KEY`.
3. Ejecuta las celdas en orden:
   - Carga el modelo entrenado directamente desde Roboflow (no requiere Google Drive).
   - Descarga el dataset de prueba desde Roboflow.
   - Corre inferencia sobre imágenes del dataset.
   - Corre inferencia sobre imágenes nuevas desde GitHub.
   - Corre inferencia sobre imágenes propias (subida desde computadora o URL).

> **Nota:** El Notebook 2 no requiere haber corrido el Notebook ENTRENAMIENTO localmente. El modelo ya está desplegado en Roboflow y se carga automáticamente con tu API key.

## 📸 Evaluar imágenes propias
Dentro del notebook 2 (inferencia) se incluye una sección llamada **“Evaluar imágenes propias”**. El usuario puede elegir entre tres opciones:
1. **Subir archivo desde su computadora**  
   - Se abre un cuadro de diálogo para seleccionar imágenes locales.  
2. **Usar imágenes desde Google Drive**  
   - Se monta el Drive y se indica la ruta completa del archivo.  
3. **Usar una URL pública**  
   - Se introduce la dirección web de la imagen.  

## 🔑 Notas importantes
- Necesitas tu **API Key de Roboflow** para ejecutar el notebook.  
- No es necesario instalar nada en tu computadora: todo corre en la nube con Google Colab.  
- Si compartes pesos entrenados, colócalos en la carpeta `models/` y documenta cómo cargarlos en el notebook.
  
## ✅ Resultados esperados
- Descarga automática del dataset desde Roboflow.  
- Entrenamiento del modelo (ejemplo: YOLO26).  
- Métricas de desempeño (precisión, recall, mAP).  
- Ejemplos de predicciones sobre imágenes de prueba.

## 📈 Resultados obtenidos
- Precision: 65.2%  
- Recall: 39.4%  
- mAP: 41.7%
- [Matrix de Confusion](M4T3_TAREA_DORA_VACA/results/evidence/01_anotaciones at main · DoraVaca/M4T3_TAREA_DORA_VACA)
- [Curvas](M4T3_TAREA_DORA_VACA/results/evidence/01_anotaciones at main · DoraVaca/M4T3_TAREA_DORA_VACA)      
- Conclusiones:  
  - El modelo detecta bien las clases más comunes (persona, arnés, chaleco).
  - Tiene problemas con clases poco representadas (guantes, sin chaleco, careta de soldadura).
  - A veces confunde objetos con el fondo, perdiendo detecciones reales.
  - La Clase 10 (careta de soldadura) es la más difícil: se mezcla con casco, persona, zapatos y chaleco.
- Recomendaciones:
  - Agregar más datos de las clases débiles (guantes, sin chaleco, sin zapato, careta de soldadura).
  - Revisar etiquetas de casco y careta de soldadura, que se solapan.
  - Balancear el dataset para reducir el sesgo hacia clases dominantes (persona, arnés).
  - Usar data augmentation (recortes, rotaciones, cambios de luz) en clases minoritarias.
  - Diferenciar mejor clases similares (ej. casco vs careta de soldadura).

## ✅ Checklist de reproducibilidad
- Dataset: Roboflow Project `M4T3_TAREA_DORA_VACA`, versión v3 (140 imágenes, split 72/16/12)
- Modelo: yolo26
- Parámetros: epochs=30, batch=16, imgsz=640
- Métricas: mAP@50=41.7%, Precision=65.2%, Recall=39.4%
- Versión ultralytics: 8.0.196

## 🧪 Prueba de Reproducibilidad
- Última ejecución exitosa: 08/03/2026, 4:20 (hora local)
- Entorno: Google Colab con GPU T4 (NVIDIA)
- Tiempo de ejecución: ~10–15 minutos para 30 épocas
- [Evidencia reproductividad otros usuarios](M4T3_TAREA_DORA_VACA/results/evidence/04_prueba_reproductividad at main · DoraVaca/M4T3_TAREA_DORA_VACA)

## 🔗 Pesos del modelo
- [Descargar best.pt (GitHub Release)](https://github.com/usuario/repositorio/releases)  
  *(o enlace externo si lo subes a Drive/OneDrive)*

## Documentos del proyecto
- [Planteamiento del problema](M4T3_TAREA_DORA_VACA/docs/01_planteamiento_del_problema AECO.md at main · DoraVaca/M4T3_TAREA_DORA_VACA)
- [Definicion de clases](M4T3_TAREA_DORA_VACA/docs/02_definiciones de clases.md at main · DoraVaca/M4T3_TAREA_DORA_VACA)
- [Analisis de errores](M4T3_TAREA_DORA_VACA/docs/03_análisis de errores.md at main · DoraVaca/M4T3_TAREA_DORA_VACA)
- [Governance checklist](M4T3_TAREA_DORA_VACA/docs/04_governance_checklist.md at main · DoraVaca/M4T3_TAREA_DORA_VACA)

## 📑 Paquete PDF
- [Diapositivas](docs/slides.pdf)  
- [Mini-informe](docs/mini_report.pdf)

## 📑 Evidencias
- [Resultados Imagenes Anotaciones](M4T3_TAREA_DORA_VACA/results/evidence/01_anotaciones at main · DoraVaca/M4T3_TAREA_DORA_VACA)  
- [Resultados Imagenes Validacion](M4T3_TAREA_DORA_VACA/results/evidence/02_predicciones_validación at main · DoraVaca/M4T3_TAREA_DORA_VACA)
- [Resultados Imagenes Nuevas](M4T3_TAREA_DORA_VACA/results/evidence/03_predicciones_imágenes_nuevas at main · DoraVaca/M4T3_TAREA_DORA_VACA) 
