# Práctica 8: Pantalla OLED con LOGO

Este repositorio contiene la octava práctica de la materia de Sistemas Embebidos Aplicados a Móviles, enfocada en la configuración y uso de una pantalla OLED utilizando el protocolo I2C con la Raspberry Pi.

## 🎯 Objetivo General
Desarrollar un programa modular en Python para Raspberry Pi que permita configurar y controlar una pantalla OLED (SSD1306). El proyecto tiene como fin visualizar texto, símbolos y datos en tiempo real aplicando buenas prácticas de programación.

## 📦 Materiales

| Cantidad | Componente | Descripción |
| :--- | :--- | :--- |
| 1 | Raspberry Pi (3, 4 o Zero W) | Con internet y Raspbian instalado |
| 1 | Display OLED 0.96" | Resolución 128x64, I2C, SSD1306 |
| 1 | Protoboard y cables jumper | Para realizar las conexiones físicas |
| 1 | Fuente de alimentación | Cargador USB según el modelo de la placa |

## 🔌 Esquema de Conexión

| Pin de la pantalla OLED | Conexión a la Raspberry Pi |
| :--- | :--- |
| **VCC** | 3.3V (Pin físico 1) |
| **GND** | GND (Pin físico 6) |
| **SCL** | GPIO 3 - SCL1 (Pin físico 5) |
| **SDA** | GPIO 2 - SDA1 (Pin físico 3) |

## ⚙️ Configuración del Sistema

Antes de ejecutar el código, es necesario preparar el entorno:

1. **Actualizar el sistema:**
   ```bash
   sudo apt update && sudo apt upgrade -y
Garantiza que el sistema tenga las versiones más recientes y evita errores al instalar los programas.

Habilitar la interfaz I2C:
Ingresa al menú de configuración mediante sudo raspi-config y navega a Interfacing Options → I2C → Enable. Este paso enciende la conexión física para enviar información a la pantalla.

Instalar bibliotecas necesarias:

Bash
sudo apt install python3-pip -y
pip3 install adafruit-circuitpython-ssd1306 adafruit-blinka
Instala el gestor de descargas y las bibliotecas principales que le enseñan a Python cómo comunicarse con los pines de la placa y prender los puntos de luz en la pantalla.

Verificar la conexión I2C:

Bash
sudo apt install i2c-tools -y
i2cdetect -y 1
Realiza un escaneo de los cables; si el hardware está bien conectado, debe aparecer la dirección 3c.

📂 Estructura del Proyecto
Para mantener el orden, el código se divide en diferentes archivos:

main.py: Es el controlador central del proyecto. Arranca el programa, muestra el logo opcional de inicio, y entra en un bucle infinito para imprimir la hora en tiempo real.

display_manager.py: Controla la comunicación gráfica. Define instrucciones exactas para limpiar el display, mostrar textos o proyectar la imagen convirtiéndolos en píxeles.

utils.py: Guarda funciones de ayuda, encargándose de capturar la fecha y hora del sistema operativo para enviarla a la pantalla.

assets/logo.pbm: Archivo de imagen opcional en blanco y negro (mapa de bits) utilizado para proyectar un icono inicial.

▶️ Ejecución y Uso
Una vez armados los componentes y preparadas las librerías, asegúrate de dar permisos al archivo principal y ejecútalo mediante:

Bash
python3 main.py
Para detener la ejecución de forma segura, limpiar la pantalla y no dejar los puertos bloqueados, utiliza la combinación de teclas Ctrl + C en tu terminal.
