Para programar el módulo <img src="https://ae-pic-a1.aliexpress-media.com/kf/S6dc6eefaed6341769de2a81db9876c51h.jpg_960x960q75.jpg_.avif">

# Requisitos
* Arduino IDE (2.3.5) o cualquier versión funciona.
* Instalar SMT32 MCU Based Board "https://github.com/stm32duino/BoardManagerFiles/raw/main/package_stmicroelectronics_index.json"

# Configuración del IDE
- Board: Generic STM32F1 series
- Board part number: Generic F103C8Tx
- Upload method: STM32CubeProgrammer (Serial)  ← recomendado
- Optimize: Smallest (-Os)
- C Runtime Library: Newlib Nano
- USB support: None

# Método de programación

1. Mantén presionado RST
2. Pulsa Upload en Arduino IDE
3. Observa la consola inferior. Cuando aparezca ESTA LÍNEA EXACTA: "<b>Port configuration: parity = even, baudrate = 115200</b>"
4. SUELTA RST inmediatamente (no antes, no después)
   
<b>⏱ Ventana válida: ~200 ms</b>

<b>Si sueltas RST:</b>
- Antes → MCU ya salió del bootloader
- Después → Arduino ya envió 0x7F y se perdió

# Variante de programación “doble reset”
<b>Variante más fiable (mi recomendación)</b>

1. Mantén RST presionado
2. Pulsa Upload
3. Cuando veas: "Serial Port COM3 is successfully opened."
4. Suelta RST
5. Inmediatamente vuelve a presionar RST y suelta

<b>Esto fuerza:</b>

- Entrada limpia a bootloader
- ACK dentro de la ventana de Arduino
- Funciona sorprendentemente bien en placas OEM.
