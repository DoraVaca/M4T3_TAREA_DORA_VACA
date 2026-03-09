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
Dentro del notebook 2 (inferencia) se incluye una sección llamada **“Evaluar imágenes propias”** con un menú interactivo. El usuario puede elegir entre tres opciones:
1. **Subir archivo desde su computadora**  
   - Se abre un cuadro de diálogo para seleccionar imágenes locales.  
2. **Usar imágenes desde Google Drive**  
   - Se monta el Drive y se indica la ruta completa del archivo.  
3. **Usar una URL pública**  
   - Se introduce la dirección web de la imagen.  

Ejemplo de flujo en Colab:
- Ejecuta la celda del menú.  
- Escribe `1`, `2` o `3` según la opción deseada.  
- La imagen se mostrará en pantalla y será evaluada automáticamente por el modelo.  

## 🔑 Notas importantes
- Necesitas tu **API Key de Roboflow** para ejecutar el notebook.  
- No es necesario instalar nada en tu computadora: todo corre en la nube con Google Colab.  
- Si compartes pesos entrenados, colócalos en la carpeta `models/` y documenta cómo cargarlos en el notebook.
