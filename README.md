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
1. Abre el notebook con el badge:  
   [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](URL_DEL_NOTEBOOK)
2. Instala ultralytics: `!pip install ultralytics`
3. Ejecuta el entrenamiento: `model.train(...)`
4. Revisa métricas y resultados en `/results/`.

## 📈 Resultados
- Precision: 65.2%  
- Recall: 39.4%  
- mAP: 41.7%  
- Conclusiones:  
  - Clase X se detecta bien.  
  - Clase Y presenta falsos negativos.  
  - El modelo generaliza en imágenes nuevas.

## ✅ Checklist de reproducibilidad
- Dataset: Roboflow Project `M4T3_TAREA_DORA_VACA`, versión v3 (140 imágenes, split 72/16/12)
- Modelo: yolo8n
- Parámetros: epochs=30, batch=16, imgsz=640
- Métricas: mAP@50=41.7%, Precision=65.2%, Recall=39.4%
- Versión ultralytics: 8.0.196

## 🧪 Prueba de Reproducibilidad
- Última ejecución exitosa: 07/03/2026, 23:30 (hora local)
- Entorno: Google Colab con GPU T4 (NVIDIA)
- Tiempo de ejecución: ~35–40 minutos para 30 épocas

## 🔗 Pesos del modelo
- [Descargar best.pt (GitHub Release)](https://github.com/usuario/repositorio/releases)  
  *(o enlace externo si lo subes a Drive/OneDrive)*
  
## 📑 Open in Colab
- [Open in Colab]([docs/slides.pdf](https://github.com/DoraVaca/M4T3_TAREA_DORA_VACA/blob/main/notebooks/train.ipynb)

## 📑 Paquete PDF
- [Diapositivas](docs/slides.pdf)  
- [Mini-informe](docs/mini_report.pdf)
