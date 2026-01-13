
<img width="960" height="487" alt="stm32" src="https://github.com/user-attachments/assets/d26631be-4611-4d64-9907-a7a9e042c476" />

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

# Variante segura
1. Genera el binario compilado desde Arduino IDE (<b>Ctrl+Alt+S</b>)
2. Ir al directorio del binario (<b>Alt+Ctrl+K</b>)
3. Descargar y abrir <b>mcuisp.exe</b> desde el repositorio.
4. Configurar a <b>Reset@DTR Low (<-3V),ISP@RTS Low</b>
5. Cargar binario (.hex) en la región <b>Code Line For Online ISP</b> y presionar en <b>Start ISP(P)</b>
6. Presionar el botón <b>RST</b> en el módulo STM32 (<b>DX-SMART DX-PJ26-V1.1</b>) y esperar a que termine la grabación.
