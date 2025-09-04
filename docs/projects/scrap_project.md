---
layout: default
title: Scraping y Análisis con LLM
permalink: /projects/scrap_project.html
---

# 📰 Scraping de Noticias + LLM Analysis – `scrap_project`

Este proyecto busca automatizar la **recolección de noticias desde medios digitales** y aplicar técnicas de procesamiento de lenguaje natural usando modelos de lenguaje (LLMs) para:

- Analizar el contenido noticioso
- Realizar fact-checking automático
- Detectar sesgos o contradicciones entre fuentes

Es un puente entre el **scraping tradicional**, la **minería de información** y el uso avanzado de **LLMs como APIs externas**, en este caso DeepSeek.

---

## ⚙️ Tecnologías usadas

- `Selenium` para scraping dinámico
- `BeautifulSoup` para parsing HTML
- `requests` y `asyncio` para manejo paralelo
- Integración con APIs de LLM (como DeepSeek o GPT)
- Análisis semántico y clasificación por tema / tono

---

## 💡 Casos de uso

- Comparar titulares entre medios
- Detectar inconsistencias en declaraciones políticas
- Resumir múltiples versiones de una misma noticia
- Marcar entidades (personas, lugares, eventos) y analizarlas

---

## 🧠 Arquitectura del sistema

<div class="tree-diagram">
scrap_project/
├── scraper.py # Scraping básico por sitio
├── aggregator.py # Comparación entre fuentes
├── llm_interface.py # Módulo para conexión con APIs LLM
├── prompts/ # Prompts y estrategias de análisis
├── logs/ # Historial de resultados
└── README.md
</div>

---

## 📊 Resultados esperados

- Archivos CSV/JSON con noticias y metadatos
- Resúmenes automáticos por evento
- Análisis de veracidad con etiquetas de riesgo
- Posibilidad de expandirse a un dashboard visual

---

## 🚀 Próximos pasos

- Agregar interfaz visual o CLI para selección de medios
- Entrenamiento o afinamiento con datasets públicos (FactCheck, LIAR)
- Generar gráficas de coincidencia entre fuentes

---

## 🔗 Repositorio

[Ver código en GitHub](https://github.com/mdam21/scrap_project)
