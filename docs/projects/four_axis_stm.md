---
layout: default
title: "Sistema de Medición STM"
permalink: /projects/four_axis_stm.html
---

# Evolución inmediata del Dispositivo de Tunelamiento
<div class="content-with-image">
  <div class="text-block">
    <p>
        Este proyecto comprende el diseño y desarrollo de un sistema de medición de corriente de tunelamiento con un control de posicionamiento de 3 grados de libertad para escaneo nanométrico y un eje para el posicionamiento macro. Inspirado en la microscopía de efecto túnel (STM) de grado comercial, el dispositivo prioriza la reducción de costos y la sostenibilidad. Bajo un enfoque alineado con los ODS, se integran mecanismos reutilizados y componentes electrónicos de alta disponibilidad en el mercado ecuatoriano.

        El diseño de hardware se realizó bajo estándares profesionales utilizando KiCad V9. El prototipo se presenta como una plataforma de hardware abierto, permitiendo que investigadores y entusiastas repliquen o modifiquen el sistema, maximizando la precisión mediante el uso estratégico de módulos comerciales accesibles.
    </p>
  </div>
  <div class="image-block">
    <img src="{{ '/assets/img/stm/stm.jpeg' | relative_url }}" alt="Fuente simetrica" class="zoomable">
  </div>
</div>
---

##  Características del Dispositivo

### 🔌 Fuente de poder simétrica bajo ruido.

<div class="content-with-image">
  <div class="text-block">
    <p>
      Esta fuente de poder está diseñada para suministrar voltajes de hasta ±17VDC, garantizando el rango dinámico necesario para los amplificadores operacionales y el actuador piezoeléctrico. Asimismo, proporciona una línea de alimentación de 5VDC regulada y libre de ruido para el ESP32.El diseño emplea reguladores lineales LM317 y LM337 para el ajuste preciso de las tensiones positiva y negativa, respectivamente. Adicionalmente, se integran reguladores LM7812 y LM7805 en una etapa previa para distribuir la disipación de potencia y calor, asegurando la estabilidad térmica y la integridad de los voltajes de salida. Para mitigar ruidos de alta frecuencia, se han incorporado filtros a la salida y un núcleo de ferrita reutilizado, reforzando el compromiso del proyecto con la sostenibilidad.
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
      Esta es la etapa más crítica del dispositivo. Se ha adaptado el diseño del proyecto previo de medición de conductancia, cuya función principal es convertir corrientes en el orden de los nanoamperios a niveles de voltaje procesables. Para minimizar la captura de ruido electromagnético y reducir las capacitancias parásitas, el circuito utiliza componentes de montaje superficial (SMD) y está diseñado para ubicarse físicamente lo más cerca posible de la punta de tunelamiento.
      
      Como optimización, se emplean conexiones blindadas (BNC SMD) desde la punta hasta la entrada inversora del amplificador de transimpedancia (TIA). Dado que el operacional utilizado posee salida rail-to-rail, un estado de saturación podría alcanzar el valor de VCC+ suministrado al OPA124. Por esta razón, la señal se dirige posteriormente a una etapa de atenuación y acondicionamiento descrita en la sección de Lectura.
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
<p>
    La etapa de lectura tiene como objetivo escalar la señal proveniente del TIA al rango dinámico del ADS1115 y el ESP32. Para preservar la integridad de la curva de datos y evitar distorsiones, se descartó el uso de limitadores tipo clipper o divisores resistivos simples, los cuales presentan pérdidas por carga o recortes en los umbrales de señal. En su lugar, se implementó un amplificador operacional en configuración inversora con ganancia menor a la unidad. Este enfoque permite una atenuación lineal y precisa, asegurando la captura de la curva de tunelamiento completa.

    Una vez acondicionada, la señal es procesada mediante una lectura diferencial en el ADC. Esta técnica permite restar el ruido ambiental y las componentes capacitivas del dispositivo, mejorando significativamente la relación señal-ruido (SNR) y permitiendo una medición más limpia de los fenómenos cuánticos observados.
</p>
---

### 🧠 Unidad de control

<p>
    El núcleo del dispositivo está basado en un ESP32 DOWD V3, encargado de gestionar 8 canales DAC (dos para cada una de las cuatro regiones del sistema). Para cada región, se implementó una arquitectura de control dual: un DAC genera una señal de rango amplio (coarse) y un segundo DAC produce una señal de rango corto (fine). Al sumar estas señales en una etapa analógica, se logra una resolución efectiva aproximada de 18 bits, superando significativamente la resolución nativa de 12 bits de los módulos MCP individuales.

    Las señales resultantes se procesan mediante amplificadores operacionales en configuración de suma y amplificación de potencia, permitiendo el control preciso de la carga capacitiva del actuador piezoeléctrico. Este arreglo permite inducir deflexiones mecánicas en el piezoeléctrico similares a la flexión de un lápiz en múltiples direcciones. Gracias a este control diferencial de voltajes, se obtienen 3 ejes de libertad en la punta (X, Y, Z), fundamentales para el escaneo nanométrico y el mantenimiento del túnel de corriente.
</p>

---

### ⚙️ Sistema de acercamiento rudo

<div class="content-with-image">
  <div class="text-block">
    <p>
      Para el posicionamiento inicial de la punta, se emplea un mecanismo de leva deslizante. Este sistema utiliza un motor DC acoplado a una guía lineal con una apertura diagonal que actúa sobre el pivote de giro. Aunque la estructura actual es robusta y funcional, al ser un mecanismo reutilizado, presenta dimensiones que podrán optimizarse en futuras iteraciones. Su función principal es transformar el movimiento rotativo del motor en un desplazamiento lineal horizontal, el cual interactúa con la rampa diagonal para aproximar la muestra a la punta con alta sensibilidad.
      
      El control se realiza mediante modulación por ancho de pulso (PWM) desde el ESP32, utilizando un módulo FC-03 (optoacoplador de herradura) para la retroalimentación de posición. Esto permite calibrar el sistema y establecer un punto de referencia o 'puesta a cero' ante cualquier modificación del hardware. Por seguridad, esta etapa cuenta con una interfaz directa para botones de emergencia y retracción manual, operando de forma independiente al software principal en el computador.
      
      Para garantizar la integridad de las mediciones, este sistema está aislado electromagnéticamente del resto del dispositivo, mitigando el ruido generado por el motor. Es importante notar que, debido a la baja fricción del conjunto, existe un riesgo de backlash (juego mecánico); por ello, se recomienda realizar el acercamiento siempre en una misma dirección para mantener la tensión mecánica constante y asegurar la repetibilidad del proceso.
    </p>
  </div>
  <div class="image-block">
    <img src="{{ '/assets/img/stm/acercamiento.png' | relative_url }}" alt="Acercamiento rudo con tornillo sin fin" class="zoomable">
  </div>
</div>

---

### 🪶 Movimiento Fino con Actuadores Piezoeléctricos
<p>
    El escaneo topológico con resolución atómica se logra mediante la manipulación precisa de un actuador piezoeléctrico segmentado. A diferencia de los motores convencionales, los materiales piezoeléctricos permiten desplazamientos del orden de nanómetros o angstroms en respuesta a variaciones de voltaje, lo que resulta indispensable para mantener el régimen de tunelamiento.

    Control Multieje y Segmentación:
    El dispositivo utiliza un disco piezoeléctrico dividido en cuadrantes, lo que permite un control independiente de cada segmento. Mediante la aplicación de voltajes diferenciales en los electrodos opuestos, se induce una deformación mecánica que inclina o desplaza la punta en los ejes X e Y para el barrido superficial. Simultáneamente, el eje Z se controla ajustando el voltaje común o central, permitiendo mantener una distancia constante entre la punta y la muestra mediante un lazo de retroalimentación.

    Sinergia de Controles (Coarse & Fine):
    La arquitectura del sistema integra los controles "rudos" (mecánicos) y "suaves" (electrónicos) para optimizar el rango de trabajo:

    Posicionamiento Macro: El sistema de leva acerca la muestra hasta entrar en el rango de captura del piezoeléctrico.

    Escaneo Micro: Una vez en el rango de túnel, el control de 18 bits mencionado anteriormente permite realizar el barrido topográfico con una estabilidad excepcional.

    Esta combinación garantiza que el sistema no solo sea preciso para capturar la estructura atómica, sino también lo suficientemente versátil para manejar muestras con diferentes rugosidades sin colisionar la punta.

</p>
---


[🔗 Ver documentación en GitHub](https://github.com/mdam21/stm-control)
