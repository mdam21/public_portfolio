---
layout: default
title: "Hands_PIU - Plataforma de Baile Interactiva"
permalink: /projects/hands_piu
---

# Teclado Interactivo de 5 Letras inspirado en tablero Pump It Up

**Hands_PIU** es un proyecto que replica la experiencia de una plataforma de baile **Pump It Up**, pero adaptada para jugar con las manos. Se compone de una matriz de 5 botones físicos que simulan los steps principales del juego, permitiendo que el jugador interactúe a través de un teclado HID personalizado.

Este proyecto integra hardware, firmware y modelado 3D, buscando una alternativa compacta, funcional y accesible a los costosos sistemas comerciales.

---

## 🔩 Componentes del sistema

<div class="content-with-image">
  <div class="text-block">
    <ul>
      <li>🔌 <strong>Microcontrolador:</strong> Arduino Leonardo (emulación de teclado HID)</li>
      <li>💡 <strong>LEDs:</strong> Indicadores visuales de respuesta por step</li>
      <li>🧱 <strong>Diseño 3D:</strong> Caja personalizada para los 5 botones tipo arcade</li>
      <li>🧠 <strong>Firmware:</strong> Escrito en C++ con PlatformIO</li>
      <li>🧪 <strong>Electrónica:</strong> Diseño de circuito de control con resistencias pull-down, transistores y mapeo por pines</li>
    </ul>
  </div>
  <div class="image-block">
    <img src="{{ '/assets/img/teclado/hands_piu.png' | relative_url }}" 
      alt="Caja impresa de Hands_PIU" 
      class='zoomable'>
  </div>
</div>

---

## 🎮 Funcionamiento

Al presionar uno de los 5 botones físicos, el Arduino Leonardo envía un carácter específico como si fuese una tecla del teclado (por ejemplo: `W`, `A`, `S`, `D`, `Q`). Esto permite que el sistema funcione directamente en juegos de PC que aceptan entrada de teclado, sin necesidad de software adicional.

El comportamiento de los LEDs puede personalizarse para indicar paso exitoso, mantener iluminación en espera, o apagarse tras cierta inactividad.

---

## 🧰 Diseño y programación

- 💻 **Firmware** en C++ con PlatformIO, utilizando las funciones `Keyboard.h` para simular escritura.
- 🛠️ **Modelado CAD** de la caja en SolidWorks, diseñada para impresión 3D en PLA, con guía de montaje, separadores para PCB y espacio para LEDs difusores.
- 🔧 **Circuito electrónico** con pulsadores arcade, transistores NPN para controlar LEDs y conexión directa a pines digitales del Leonardo.

---

## 📦 Aplicaciones y futuro

Este proyecto es ideal como plataforma educativa para:

- Introducirse en sistemas HID con microcontroladores
- Aplicaciones de accesibilidad para videojuegos
- Prototipado de interfaces físicas interactivas
- Controladores DIY personalizados

Entre futuras mejoras se incluyen:

- Reemplazo de pulsadores por sensores capacitivos o piezoeléctricos
- Añadir feedback háptico (vibración)
- Sistema de scoring básico con display OLED

---

[🔗 Ver código en GitHub](https://github.com/mdam21/hands_piu) <!-- Cambia la URL si es diferente -->
