---
layout: default
title: "Ampliación de Set de Imágenes"
permalink: /projects/amp_set
---

# Ampliación de Set de Imágenes para Entrenamiento de LLM

Este proyecto fue desarrollado con el objetivo de generar un conjunto de imágenes ampliado, con diversidad visual significativa, para entrenar modelos de lenguaje multimodal para la empresa **TALOV**. El codigo consta de tres etapas: (1) conjunto inicial (10 imágenes + CSV), (2) generación de 20 sets (cada uno con 10 imágenes + su CSV), y (3) consolidación final de todas las imágenes en una sola carpeta. Este aplica transformaciones configurables sobre imágenes RGB, siguiendo lineamientos y recomendaciones comunes de plataformas como Roboflow, pero evitando sus errores comunes a través de una implementación personalizada de los filtros a ocupar.

El sistema permite ampliar datasets de forma controlada mediante filtros ajustables, y finaliza con una consolidación automática de imágenes y anotaciones, listas para su uso en entrenamiento.

---

## 🧪 Procesamiento y filtros aplicados

<div class="content-with-image">
  <div class="text-block">
    <p>
      El script principal `run_img_amp.py` aplica un conjunto de filtros como desenfoque, contraste, brillo, recorte, rotación, saturación, ruido, exposición, efectos sepia, escala de grises, flipping, entre otros. También incluye combinaciones de filtros para ampliar rápidamente el dataset. Originalmente se aumentaron sets de 200 imagenes realizando una ampliacion a 4000 imágenes, trabajando bajo mas de 80 sets distintos generando mas de 300 000 imagenes para alimentar la red neuronal.
    </p>
  </div>
  <div class="image-block">
    <img src="{{ '/assets/img/amp/inv_col.png' | relative_url }}" 
      alt="Ejemplo de filtros aplicados" 
      class='zoomable'>
  </div>
</div>

---

<h2 id="resumen-visual">🖼️ Resumen visual del pipeline</h2>

<div class="triptych">
  <figure>
    <img src="{{ '/assets/img/amp/inicial_10imgs_csv.png' | relative_url }}"
         alt="Estado inicial: 10 imágenes y un CSV"
         class='zoomable'>
    <figcaption>Inicial — 10 imágenes + CSV</figcaption>
  </figure>

  <figure>
    <img src="{{ '/assets/img/amp/intermedio_20sets.png' | relative_url }}"
         alt="Intermedio: 20 sets × 10 imágenes y su CSV"
         class='zoomable'>
    <figcaption>Intermedio — 20 sets × 10 imgs + CSV</figcaption>
  </figure>

  <figure>
    <img src="{{ '/assets/img/amp/final_consolidado.png' | relative_url }}"
         alt="Final: todas las imágenes consolidadas"
         class='zoomable'>
    <figcaption>Final — consolidado en una carpeta</figcaption>
  </figure>
</div>

<!-- Lightbox overlay -->
<div id="lightbox" class="lightbox">
  <span class="close-btn" onclick="closeLightbox()">&times;</span>
  <span class="prev" onclick="changeImage(-1)">&#10094;</span>
  <img id="lightbox-img" src="" alt="">
  <span class="next" onclick="changeImage(1)">&#10095;</span>
  <div id="lightbox-caption"></div>
</div>




---

<details>
  <summary> 🔧 Filtros disponibles (20 principales) </summary>
  <pre>
- **Blur Gaussiano** (`blur_sigma`)
- **Detector de bordes Canny** (`thres1`, `thres2`)
- **Ajuste de brillo y contraste**
- **Recorte y cutout (oclusiones)**
- **Desenfoque selectivo por umbral**
- **Transformación elástica**
- **Exposición**
- **Volteo horizontal / vertical**
- **Escala de grises parcial o total**
- **Hue, Saturación y Ruido**
- **Rotación**
- **Filtro Sepia personalizado**
- **Detección de bordes Sobel**
- **Filtros mixtos:**
  - Blur + Escala de grises
  - Contraste + Brillo
  - Saturación + Brillo

  </pre>
</details>

---

<h2 id="estructura">⚙️ Estructura del Proyecto</h2>

<div class="tree-diagram">
amp_img/
├── ampliacion_lib/        # Librerías de filtros personalizados
├── data/
│   ├── input_images/      # Imágenes originales
│   └── processed_images/  # Imágenes ampliadas
│       ├── temp_set/      # Proceso intermedio
|       └── total_set/     # Set consolidado
├── run_img_amp.py         # Script principal
├── mixture.py             # Consolidación de sets
└── README.md
</div>
---

## 📦 Consolidación y anotaciones
Cuando ya se amplian las imagenes tomamos un segundo script **mixture.py** que permite combinar multiples sets con sus respectivas anotaciones en sus respectivos .json en un set ampliado con un solo set.

Este proceso permite generar datasets homogeneos que cumplan con requerimentos de entrada de modelos como YOLO, DETR, o frameworks de RLHF multimodal con enfoque en personas discapacitadas como se busca hacer en TALOV inc.

---

## 💡 Aplicaciones
- Entrenamiento de modelos de visión por computadora
- Aumento de imágenes para alimentar redes de imagenes profundo
- Preparación de datasets robustos ante ruidos, rotación y cambios de iluminación.
- Entrenamiento multimodal en modelos de LLM que incluyen entradas visuales.


---
[🔗 Ver código en GitHub](https://github.com/mdam21/amp_images)
