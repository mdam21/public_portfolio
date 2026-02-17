---
layout: default
title: "Sistema de Medición STM"
permalink: /projects/stm.html
---

# Sistema de Medición de Conductancia de Tunelamiento
<div class="content-with-image">
  <div class="text-block">
    <p>
        Este proyecto consiste en el diseño y desarrollo de un sistema de medición basado en corriente túnel, inspirado en los principios de la Microscopía de Efecto Túnel (STM, *Scanning Tunneling Microscopy*). El enfoque principal es mantener el costo lo más bajo posible utilizando componentes electrónicos de fácil adquisición en el país, sin sacrificar precisión ni modularidad.

        El sistema está pensado como una plataforma abierta, ideal para estudiantes e investigadores que deseen experimentar, modificar o expandir sus capacidades sin enfrentar barreras técnicas ni económicas.
    </p>
  </div>
  <div class="image-block">
    <img src="{{ '/assets/img/stm/stm.jpeg' | relative_url }}" alt="Fuente simetrica" class="zoomable">
  </div>
</div>
---

## 🧩 Características principales

### 🔌 Fuente de poder simétrica bajo ruido.

<div class="content-with-image">
  <div class="text-block">
    <p>
      Basada en reguladores LM317/LM337, la fuente proporciona voltajes ajustables de hasta ±15 V. Se incorporan filtros pasa-bajo y pasa-alto para asegurar la limpieza de la señal entregada al sistema.
    </p>
  </div>
  <div class="image-block">
    <img src="{{ '/assets/img/stm/fuente_simetrica.png' | relative_url }}" alt="Fuente simétrica" class="zoomable">
  </div>
</div>

---

### 🎛️ Preamplificador de transimpedancia

<div class="content-with-image">
  <div class="text-block">
    <p>
      Construido con el OPA124U en formato SMD, este preamplificador convierte corrientes del orden de nanoamperios en señales de voltaje aprovechables, manteniendo bajo ruido en la etapa inicial. Este es el core del dispositivo, se utiliza microelectrónica con una placa acoplada lo más cercana al evento a registrar para reducir pérdidas por ruido.
    </p>
  </div>
  <div class="image-block">
    <img src="{{ '/assets/img/stm/preamplificador.png' | relative_url }}" 
        alt="Preamplificador de transimpedancia"
        class="zoomable">
  </div>
</div>

---

### 🔒 Etapa de lectura

Etapa compuesta por protección tipo clipper, buffer de aislamiento y un ADC de precisión. Esta configuración asegura que la señal pueda ser digitalizada sin distorsiones o interferencias externas.

---

### 🧠 Unidad de control

Controlada por un microcontrolador **ESP32**, se conecta a través de un **multiplexor I²C** que maneja **3 DACs** (uno por eje del trípode piezoeléctrico) y un ADC para lectura. Esta arquitectura permite realizar barridos precisos en X/Y y ajustes finos en Z.

---

### ⚙️ Sistema de acercamiento rudo

<div class="content-with-image">
  <div class="text-block">
    <p>
      Para el posicionamiento inicial de la punta, se emplean tornillos sin fin controlados por motores reciclados (como unidades de CD/DVD). Esta etapa garantiza un acercamiento mecánico seguro antes del control piezoeléctrico.
    </p>
  </div>
  <div class="image-block">
    <img src="{{ '/assets/img/stm/acercamiento.png' | relative_url }}" alt="Acercamiento rudo con tornillo sin fin" class="zoomable">
  </div>
</div>

---

### 🪶 Movimiento fino con piezoeléctricos

Los ajustes y escaneos a nivel atómico se logran mediante piezoeléctricos segmentados tipo buzzer, dispuestos como trípode. Cada segmento es controlado individualmente para generar movimientos suaves y precisos.

---

### 🎚️ Control de ganancia

El sistema incorpora un **multiplexor digital** y **potenciómetros digitales**, permitiendo seleccionar dinámicamente la ganancia del sistema sin necesidad de modificar hardware.

---

[🔗 Ver código en GitHub](https://github.com/mdam21/stm-control)
