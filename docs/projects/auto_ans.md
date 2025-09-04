---
layout: default
title: Autocompletador de Formularios (auto_ans_mdam)
permalink: /projects/auto_ans.html
---

# 🧠 Autocompletador de Formularios

Este proyecto nace como una herramienta experimental para **automatizar el llenado de formularios tipo test**, inicialmente desarrollada para realizar pruebas unitarias de una pagina de cursos de inglés. 

Se combina **scraping de contenido**, **detección de patrones de respuesta** y **simulación de entrada humana** para lograr un autollenado eficaz observando el comportamiento de la automatizacion en tiempo real.

---

## ⚙️ Tecnologías usadas

- `Selenium` para navegación y control del navegador
- `PyAutoGUI` para movimientos y simulaciones visuales
<!-- - `pytesseract` y OCR para detección en pantalla *(opcional en algunas versiones)* -->
- Automatización de flujos de click + teclado
- Interfaz visual para seleccionar tipo de test

---

## 💡 Motivación

El proyecto nació de una necesidad informal de simplificar tests repetitivos. Su utilidad se expandió a múltiples páginas web que compartían estructuras similares de formularios con selección múltiple, tiempos límite, y validaciones ocultas.

<!-- Fue una **exploración técnica y ética** sobre la capacidad de los bots para imitar el comportamiento humano en plataformas web educativas. -->

---

## 🧪 Estado actual

- Funciona con el sitio original al cual fue enfocado.
- Permite definir patrones de respuestas
- Tiene detección básica de errores en pantalla
- Modular y fácil de extender a nuevos tipos de test

---

## 📂 Estructura del código

<div class="tree-diagram">
auto_answer/
├── bot.py          # Lógica de navegación y llenado
├── config.json     # Configuración de patrones
├── visual_mode.py  # Control visual y simulación
├── tests/          # Pruebas unitarias
└── README.md
</div>

---

## 🚀 Próximos pasos

- Modularizar completamente en una clase Python
- Agregar un modo headless controlado por CLI
- Incluir logging de resultados y tiempos

---

## 🔗 Repositorio

[Ver código en GitHub](https://github.com/mdam21/auto_ans_mdam)
