# Práctica 9: Visualización de Texto Desplazable en Pantalla OLED con Raspberry Pi

Este repositorio contiene la novena práctica de la materia de Sistemas Embebidos Aplicados a Móviles.

## 🎯 Objetivo General
Desarrollar un programa modular en Python para Raspberry Pi con el fin de configurar y controlar una pantalla OLED (SSD1306). El proyecto tiene como objetivo desplegar mensajes y texto con efectos de desplazamiento continuo (scrolling), aplicando buenas prácticas de diseño de software embebido.

## 📦 Materiales Requeridos

| Cantidad | Componente | Observaciones |
| :--- | :--- | :--- |
| 1 | Raspberry Pi (con pines GPIO) | Recomendado: Raspberry Pi 3 o 4 |
| 1 | Pantalla OLED 0.96" I2C | Resolución 128x64 (controlador SSD1306) |
| 4 | Cables jumper Dupont (macho-hembra)| Para la comunicación I2C |
| 1 | Protoboard (Opcional) | Para facilitar el montaje físico |
| 1 | Fuente de alimentación | USB-C o MicroUSB según el modelo de la placa |
| 1 | Conexión a Internet | Para la instalación inicial de librerías |

## 🔌 Esquema de Conexión

| Pin OLED SSD1306 | Conexión Raspberry Pi | Observaciones |
| :--- | :--- | :--- |
| **VCC** | 3.3V (Pin físico 1) | Alimentación de energía para encender la pantalla (¡Ojo! No conectar a 5V para evitar daños). |
| **GND** | GND (Pin físico 6) | Conexión a tierra común para cerrar el circuito eléctrico. |
| **SCL** | GPIO 3 - SCL1 (Pin físico 5) | Serial Clock: Línea de reloj encargada de sincronizar la comunicación de los datos. |
| **SDA** | GPIO 2 - SDA1 (Pin físico 3) | Serial Data: Línea principal por donde viaja la información del texto hacia la pantalla. |

> **Dato Importante:** Para que esta conexión física funcione, es indispensable asegurar que el puerto I2C esté encendido en el sistema operativo. Esto se habilita desde la terminal ejecutando `sudo raspi-config` y navegando a la ruta: **Interfacing Options → I2C → Enable**.

## ⚙️ Configuración del Entorno

Antes de ejecutar el código, es necesario preparar las librerías en la Raspberry Pi:

**1. Actualizar el sistema operativo:**
```bash
sudo apt update && sudo apt upgrade -y
Actualiza el listado de paquetes para evitar problemas de compatibilidad al instalar las librerías de Python.

2. Habilitar I2C:

Bash
sudo raspi-config
Navegar a: Interfacing Options > I2C > Habilitar. Este paso enciende la conexión física a nivel de sistema operativo.

3. Instalar librerías y dependencias necesarias:

Bash
sudo apt install python3-pip -y
pip3 install adafruit-circuitpython-ssd1306
pip3 install pillow
Se instala el gestor de descargas (pip), el controlador oficial de la pantalla y la librería de gráficos (pillow) para crear el "lienzo virtual" donde se calculan las coordenadas matemáticas para lograr el efecto de desplazamiento.

4. Verificar dirección I2C:

Bash
sudo apt install i2c-tools
i2cdetect -y 1
Confirma que el hardware fue detectado exitosamente. Si la conexión en la protoboard es correcta, el escaneo arrojará el valor 3C.

📂 Estructura del Proyecto
Para mantener el orden y aplicar buenas prácticas, el código se divide en tres módulos:

config.py (Configuración general): Funciona como el panel de control central. Se encarga de guardar los valores fijos y los ajustes generales (como el mensaje a mostrar, la velocidad del efecto y el tamaño de la pantalla) en un solo documento para no romper el código principal.

oled_display.py (Lógica de pantalla): Es el motor gráfico. Establece la conexión física por I2C con el hardware de la pantalla y contiene toda la lógica matemática necesaria para crear un lienzo virtual del doble de ancho y generar los "recortes" que dan el efecto visual de movimiento fluido.

main.py (Ejecución del programa): Es el punto de entrada y el cerebro del programa. Une la configuración y el control gráfico para ejecutar un bucle infinito (while True) que mantiene el texto moviéndose en la pantalla de forma continua, contando con un bloque de seguridad (try-except) para un cierre limpio.

▶️ Ejecución y Uso
Una vez armados los componentes y preparadas las librerías, asegúrate de estar dentro de la carpeta del proyecto y ejecuta el archivo principal mediante:

Bash
python3 main.py
Para detener el desplazamiento del texto de forma segura y liberar la terminal, utiliza la combinación de teclas Ctrl + C en tu teclado.

📌 Conclusión
En conclusión, el desarrollo de esta práctica nos permitió comprender a fondo cómo establecer una comunicación I2C estable entre la Raspberry Pi y una pantalla OLED. Además de lograr exitosamente el efecto visual de desplazamiento de texto (scrolling) usando lienzos virtuales, comprobamos que dividir el proyecto en módulos separados (configuración, controlador gráfico y programa principal) hace que el código sea mucho más ordenado, fácil de leer y rápido de modificar.